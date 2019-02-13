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



