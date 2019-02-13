# Fixing Errors

Here we're going to go over a couple of common errors that may come up while using git. 
We're going to cause the errors, explain why they happen and explain how to resolve them. 

## File overwrite errors

A file overwrite error occurs when changes have been made to a remote file, you've made changes to that file locally, and you haven't committed your changes. Because git will only keep track of changes if the file is committed, pulling would overwrite your local changes. 

### Creating the error 

Let's create an overwrite error!

First, pull and push to make sure that the remote repository and the local repository are syncronised. 

You can run `git status` to check the state of your repository if you're not sure whether any other changes
have been made. 

Now we need to modify a file on the remote server and commit it. To do this, open up `demo_file.py` in the github UI by clicking on the file. Then, click the pencil icon towards the top right. Set `word_index` to `4` instead of `3`, scroll down to the "Commit Changes" box and add a descriptive commit title and click the green "Commit Changes" button. Now we have a modified version of `demo_file.py` on the remote server. 

The next step is to modify `demo_file.py` locally. Open `demo_file.py` in your favorite text editor and set `word_index` to `5` instead of `3`. Now we're in a situation where there is a commit on the remote server that will overwrite our local file. Let's try to pull (e.g. run `git pull origin master`).

You should see a large error message print out. I encourage you to read it. The essence of the message is that your local file will be overwritten by the commit on the remote server. The error message even lists the two methods for resolving this error message: we can stash our changes or we can commit the changes. 

### Viewing the changes made 

If you want to see what specifically was changed you can run `git diff demo_file.py`. This command does a comparison of the local file and the version of that file from your last commit. First the lines for the last commit are displayed, then the lines for the local file are displayed. Lines with a + or - in front of them have been added or deleted. The result printed out can help you determine whether you want to keep those local changes or whether they should just be removed. 

### Committing the changes

If the modifications made to the file locally were important, you can commit the file and then pull. If the changes on the remote commit and the local commit conflict, a merge conflict will be raised. This error will be discussed later on this page. If they do not conflict, then an automerge will be performed. 

Either way, a method is provided for the local changes to be added to the remote server on the next push. 

The other resolution of this error does not allow you to add your change to the remote repository. 

### Stashing the changes 

If you run `git stash demo_file.py` your local changes will be stashed and you can then pull.

The stash is a place off to the side where local changes that you do not want on the server can be sent. 

The changes can be retrieved if you want them later. However, this will not be discussed in this tutorial. For more information, read the [description, discussion and examples sections on this page](https://git-scm.com/docs/git-stash). 

## Merge conflict

A merge conflict occurs when a local commit and a remote commit try to change the same thing. When this happens, don't panic! It can be a little frightening but we can work through it. 


### Setting up the error 

To create this error, we will do almost the exact same thing as the previous example during stashing. However, in this case we will commit `demo_file.py` instead of stashing the changes. 

If that makes sense, you can skip to the next section. If not, here is how to create the error. 

First, pull and push to make sure that the remote repository and the local repository are syncronised. 

Now we need to modify a file on the remote server and commit it. To do this, open up `demo_file.py` in the github UI by clicking on the file. Then, click the pencil icon towards the top right. Set `word_index` to `1`, scroll down to the "Commit Changes" box and add a descriptive commit title and click the green "Commit Changes" button. Now we have a modified version of `demo_file.py` on the remote server. 

The next step is to modify `demo_file.py` locally. Open `demo_file.py` in your favorite text editor and set `word_index` to `2`. Let's commit our local version of `demo_file.py` (e.g. `git commit demo_file.py`). Now we're in a situation where there is a commit on the remote repository that disagrees with a commit in our local repository. When we pull again, we will get the Merge conflict error. 


### The error message 

The error message you get after pulling should look like this. 

```
Auto-merging demo_file.py
CONFLICT (content): Merge conflict in demo_file.py
Automatic merge failed; fix conflicts and then commit the result.
```

Git has now altered the file `demo_file.py`. Let's open it up and see what changed. 
 
It should look something like this. 

```
from __future__ import print_function
#The above line is just for python2 compatibility. 

words = ["hey", "you're","learnin","git","ya","know"]
<<<<<<< HEAD
word_index = 2
===========
word_index = 1
>>>>>>> ffa5e39263a8601ad99281aa
print(words[word_index])
```

Let's talk a bit about what that means. The merge conflict blocks that are added always consist of a bunch of left arrows, a bunch of = and a bunch of right arrows. The row of = act as a dividing line showing the two different versions of that line. 

### Resolving the error

To fix this error, we want to choose the appropriate version at each merge conflict block. The markup produced by git as well as the incorrect version should be deleted from the file. You could also write some code that wasn't in either conflict. Git just wants to make sure that all the rows with `====` `<<<<` or `>>>>>`are removed from your file. Determining whether the changes made reflect what you actually want your code to do is your job. I encourage you to run some tests and make sure that everything is working as expected after resolving the conflicts. 

Then, you need to tell git that you've fixed everything. To do this, you run `git add demo_file.py`. Then run `git commit` with no file specified. The `add` tells git that you've dealt with the conflict and `commit` creates a new commit for the merge. 
