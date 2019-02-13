# Basic Usage

## Fork the repository

If you have not done so already, please fork the repository hosted by ksteimel. Forking essentially creates a copy of the repository under your own username. This is done to prevent the other changes we're about to make from interfering with what everyone else is doing. 

To fork the repository, click the button near the top right of the repository's web page that says "Fork". You should then see a dialogue informing you that the files are being copied. 

## Clone a repository

Cloning a repository creates a local version of the repository on the server. To clone the repository you just forked, visit the repository you just made (you should be able to find a link to the repository under your list of repositories on the left when you log in). On the front page of the repository, you will see a green button that says "Clone or download". Click this button and you will see a dialogue that provides a url. If the url listed does not begin with `https://`, click the link that says "Use HTTPS" in the top right of the dialogue box. Copy the url to your clipboard and then switch to the terminal. 

This url is essential to the clone command since it needs to know where to grab the repository files from. 
In your terminal, run the following command: 

```bash
$ git clone <repository url>
```

```bash
$ git clone https://github.iu.edu/ksteimel/git_tutorial.git
```

This will create a new folder in the folder you're currently in that has the contents of the repository. 
Some additional folders are also created in the project folder that help manage the repository. These are hidden by default. 

## Add a file

In order for git to manage a file, it has to be told which files to manage.
Before adding any file, it is always a good idea to see what changes have been made to the local repo. Run the following command to see the changes:

```bash
$ git status
```
This is actually a super useful command to know. I personally tend to  do `$ git status` super frequently regardless of at which step I am. It is much easier to correct a mistake at an early stage. :)
To add one specific file, run the following command:

```bash
$ git add <file name>
```

A lot of the times people will want to add all their changes. This can be done by running the following command (Don't forget the last dot):

```bash
$ git add .
```

## Commit a file

Now we have everything added. It's time to commit them to the local repository. 

```bash
$ git commit -m"This is the commit message."
```

In most cases you can also do:

```bash
$ git commit
```

This will then open a separate vim text editor so we can edit the commit message.
Commit messages are VERY IMPORTANT. Trust me. Later on when you look back and want to find a specific commit in which you made some changes, commit messages will be your best friend. Do not use simple words like "update" or "some changes" as your commit message (Been there, done that, regreted it). A good commit message will be something like "added contents for Basic_usage.md".

## Pull from the remote repository

What do people always say? Pull before you push.
You are asked to pull before you push, because someone pushed changes to the server, after your last pull, so our local repository and the current remote repository are not in sync. Pulling will merge the remote repository with your local one, which brings them back into sync and allows you to push.
The reason that you are not supposed to push straight away, is that this will need merging and might lead to conflicts which need manual resolving. To avoid merging errors and conflicts, merging is best done on the local side, not on the server.

```bash
$ git pull
```

## Push to the remote repository

Now we have (pretty much) everything in place. We are ready to push. Yay! Pushing has the potential to overwrite changes, caution should be taken when pushing. The following command exports local commits and updates them to the remote repository:

```bash
$ git push
```

## Checkout a previous commit

The `git checkout` command is used to update the state of the repository to a specific point in the projects history. When passed with a branch name, it lets you switch between branches. Since this has the potential to overwrite local changes, Git forces you to commit or stash any changes in the working directory that will be lost during the checkout operation.

```bash
$ git checkout <branch>
```

This command can also let you see a previous commit. In order to know which commit you want to see, do:

```bash
$ git log --oneline
```

The first part of the log are the IDs of each commit. The second part, as we discussed in a previous section, are the commit messages (See, now you really want your commit messages to make sense).

Run the following command to checkout a previous commit:

```bash
$ git checkout <commit ID>
``` 