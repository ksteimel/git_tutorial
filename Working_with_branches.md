# Working with branches

So far, we've been using git in a linear fashion, everything we've been doing has been on the master branch and we've just been directly changing that branch. However, for larger projects, it becomes advantageous to use other branches as well. Say for example, I'm working on a new feature selection implementation. Instead of storing my files in a separate folder of the repository, I can create a new branch and work there. 

In addition, working on a separate branch can be used to easily keep git's history clean. Best practice is generally to use one commit per feature. In this model, you would create a commit when you finished implementing something and every time you changed your implementation. However, you would not commit any partial implementations. 

Sometimes you need those partial implementations though. You want to be able to revert previous things you tried or save your spot before you switch computers. 

This is something that using branches can help immensely with. 

## Let's look at what branches there are 

If you run `git branch` with no arguments, a list of the repository's branches will be printed out with an indicator next to your current branch. 

## Creating a new branch

Let's create a new branch. `git branch <branch name>` will create a new branch with the name specified for `<branch name>`. For example, if you make a branch called `feature_selection`, you would run `git branch feature_selection`. Now if you type `git branch`, you should see a new branch listed. 

## Switching between branches

However, you should also notice that the indicator is still under the `master` branch. To switch between branches, use the `git checkout` command we learned before. However, in this case, you should specify a branch name rather than a commit hash. For example, 


```
git checkout feature_selection
```

Now if you list the branches via `git branch` you should see that we're now on a new branch! 

## Creating a pull request into master

I'm now going back to the issue of keeping our commit history clean. We can have a messy branch and then integrate a bunch of changes on that branch as a single commit on master. For example, we can have a branch called `feature_selection` where we were working on adding a feature selection component to our pipeline. While this was being made, I created a bunch of incremental changes on the `feature_selection` branch. When merging back into `master` I can clean up all these separate commits into a single commit for the feature. 

Let's make a commit on the `feature_selection` branch.

Checkout the feature_selection branch (e.g. `git checkout feature_selection`). Create a new file called `feature_selection.py` and write some content in it. What you write isn't really important for the purpose of illustrating how to do a merge request. 

Add the file to git by running `git add feature_selection.py` and then commit the new file (`git commit feature_selection.py`). So far this should be familiar. Now we're going to pull and push our changes to the other branch. E.g. `git pull` followed by `git push origin feature_selection`. If you go into the github UI, you should see a new branch was created. If you click the dropdown and select the `feature_selection` branch, you should see your file show up. 

Now, click the button that says "New pull request". This will open a new page that looks like this

![github pull request dialogue](https://github.iu.edu/ksteimel/git_tutorial/raw/master/github_pr.png)

The branch listed on the left in the top bar is the branch you're going to merge into (here that branch is master), the branch on the right is the branch you're merging in. Add some details about what the merge is doing in the description (e.g. the feature being added). Then click "Create Pull Request". This will open a new screen which looks like this: 

![github merge](https://github.iu.edu/ksteimel/git_tutorial/raw/master/merge_and_squash.png)

You can create a merge commit (the default option). This will basically just add all the commits you made on the other branch into the `master` branch. However, we wanted to keep things clean. To combine all your commits on the other branch into a single commit, click the down arrow on the right side of the green "Merge pull request" box and select Squash and merge. This will open a new dialogue box. This box is letting you set what your commit for this feature should look like. Select something that makes sense and then do the merge. Your master branch should now contain a single commit with your change.

