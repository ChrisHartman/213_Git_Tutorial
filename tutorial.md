# Git and Github Workshop - EECS 213

## Before we start

### Making sure `git` is installed
Run the command `git` in the command line to ensure that you have git installed, if not, use a lab machine for the tutorial, and follow the instructions below to install git later.
#### Mac
* To install git, you should just need to install Xcode.

#### Windows
* There is a Windows version of the `git` command line, which you can get from [Git for Windows](https://git-for-windows.github.io/).

#### Linux
* You can use your package manager to download it.

### Github accounts
* You can make a github account at the [github website](https://github.com)

## What is `git`, and what is Github?

### What is `git`, and what can I do with it?
_Git is a code versioning and collaboration tool._

#### Code Versioning
How many of you save copies of your files, at different stages in your process? Different drafts of papers, etc? Git is the same idea for code, but more sophisticated. Git lets you make checkpoints in your project, so at any point you can go back and see what was going on, or switch back to an old checkpoint if you go down the wrong path.

#### Collaboration
How many of you use Dropbox or Google Drive to sync files, for group projects? Git covers the same idea, but even more sophisticated. Multiple people can participate in the same code-writing project using `git`. It’s not simultaneous, but gives you good tools for making sure all your code lines up.

In this tutorial, we will focus on the checkpointing and code versioning features of `git`.

### What is Github, and what can I do on it?
_Github is a website that hosts published code, publicly and privately. It lets you:_

* Publish your projects.
* Browse, download, and contribute to open-source projects.
How many of you save copies of your files, at different stages in your process? Different drafts of papers, etc? Git is the same idea for code, but more sophisticated. Git lets you make checkpoints in your project, so at any point you can go back and see what was going on, or switch back to an old checkpoint if you go down the wrong path.

* Host websites, write public documents, and a bunch of other cool stuff.

#### How is code stored?
Code lives in what are referred to as “repositories”, which is basically a fancy name for a directory/folder. Repositories usually have a specific structure to them, depending on the language/type of project you're using.

#### How do I interact with/put code on Github?
Using `git`, of course!

#### Are there alternatives to Github?
Other code hosting sites exist, such as Bitbucket, but Github is by far the most popular.

#### Github Student account
* Github has a bunch of premium features, like having an unlimited number of private repositories (which are handy for classwork, since you can’t publish that publicly).
* You can get a student account by [applying for it on their website](https://education.github.com/pack), with your @u.northwestern email. I highly recommend doing so!
    * It can take between a few minutes and a few days to get approved, so something to check out later.
    * We won't need any premium features today.

#### Making a new repository
* Click the `+` symbol in the top right, and select “New repository”.
* Give it a short, descriptive name - for example, “213_git_workshop”.
* Since you don’t have student accounts yet, you’ll have to leave it public for now.
* Click “Initialize this repository with a README” - all this does is create your new code repository with one file in it that just has the repo name.
* Create the repository!
* Important: if your repository has a file named “README” or “README.md” in it, Github will display it when you enter the folder containing it. README’s are typically used to give people a description of the project, what it does, how to use it, how to install it, etc.
    * READMEs are typically written in a format called Markdown, which is like a quick-and-dirty way of doing nice formatting in a basic text file (vs an MS word or HTML file).

## Local vs. remote, and the `git` workflow.
With `git`, we frequently talk about “local” and “remote” repositories.

* A “local” repository is one that exists on your machine.
* A “remote” repository is one that exists on Github.
* A local repository will be set up to “track” a remote repository, linking the two.
    * There is typically a one-to-one relationship between locals and remotes. However, this is not always true, and if you’re interested in those use cases we can talk offline. For now, think of one remote being paired with one local, so your Github repo you just created online paired with a copy you’ll download to your machine (more on this in a minute).

The `git` workflow is, generally:

1. Download the most recent version of the code from a remote repository on Github, to a local repository.
2. Modify the code and test your modifications in your local.
3. Once you’re done modifying the code, you upload it back to the remote on Github.

This workflow gives you a couple things:

* Your up-to-date code is backed up and safe.
* Your code is only published when it’s ready.
* You can download your up-to-date code, and work on it, anywhere.
* If you have collaborators on the project, they can see, download, and play around with the changes you make, and vice versa.
* If you’re working on a public project, your consumers can stay up-to-date with your most recent features and progress.

### Your first `git` command: `clone`
`git clone` is used to download a remote repository, in its current state, into a local repository on your machine.

* The general form of the command is `git clone <URL of remote>`.
* You can find that URL by clicking the green “Clone or download” button from the main page of a remote.
    * There are two ways to clone a Github repo - HTTPS, and SSH.
    * The default is HTTPS. For the most part, the difference is irrelevent

#### Using `git clone`
1. Copy the HTTPS-prefixed URL from the “Clone or download” button, and paste it into the clone command.
    * For example, for my repo the full command would be: `git clone https://github.com/sashaweiss/211_git_workshop.git`.
2. Run the command. Once it finishes, run `ls`. You’ll see that a new folder has been created, with the name of your repo!
3. `cd` into the local repo, and explore!
    * You’ll see the README.md file.
    * If you run `ls -a`, you’ll see a `.git` folder. That folder contains a bunch of information that `git` uses. Don’t worry about that for now.

## How `git` organizes code: commits and branches
* `git` organizes your code changes into a “tree” (If you've taken 214 it's technically a DAG but don't worry about that).
* This tree is composed of a bunch of “commits”,  each of which represents a checkpoint in your code.
  * Ideally, a commit is a small set of code changes that make an incremental improvement to your code, rather than a giant set of changes. All a git really is, is a series of changes that take your repo from one state to another
  * Small code changes make it easier to track your changes, to “go back” to old checkpoints, and to review changes that you or others have made.
* A set of sequential commits (checkpoints) is referred to as a “branch” of the tree.
  * Commits within a branch build on each other, and are organized in chronological order.
  * Your main branch has the special name “master”, and should generally represent a clean, working version of your code.
* For today we won't cover much about using - we'll be learning how to commit to `master`, which is the "default" behavior.

### Local and remote branches
The same way that that you have a local and remote copy of a repository that are paired and track each other, you have a local and remote copy of each branch in a repository that are paired and track each other. We'll see later how to keep them synced up.

* Local branches are denoted by just their name.
* Remote branches are denoted by the name of their remote, a slash, and then the name of the branch.
    * Your remote is named “origin” by default. Consequently, the branch name “master” refers to your local copy of the master branch, while “origin/master” refers to the copy of master that’s synced to Github (this branch syncs when you run certain commands, don't automatically assume it's a perfect copy of github)

## Make and commit some changes
Now that we’ve cloned our starter repo, let’s make and commit some changes.

### What’s going on in my repo: `git status` and `git diff`
`git status` and `git diff` are used to show you what changes you’ve made in your local repo that aren’t yet synced to your remote.
* `git status` shows you which files have been added, deleted, or modified since the last commit.
* `git diff` shows you the actual lines that have been added, deleted, or modified in those files.
    * By default, `git diff` uses a program called `less` to display the changed lines. You can use `d` and `u` to scroll down and up if the changes are large, and `q` to quit.

#### Using `git status` and `git diff`
* Run `git status` in your local. Since you just cloned it and haven’t made any changes, you’ll see a message saying your local master branch is up-to-date with origin/master.
* Run `git diff` in your local. Since you just cloned it and haven’t made any changes, you’ll see a blank display.

### Make some changes!

#### Modify a file
Use your favorite text editor to make some changes to the readme file. We'll use vim for this demo
1) Run `vim README.md` to open.
2) Type `i` to enter insert mode, then type to add text, use arrow keys to move around.
3) Hit `escape` to exit insert mode, and then `:wq` to save and quit

Let's use `vim` to add a new file.

1) Run `vim <filename>`.
2) Add some text.
3) Exit as above.

#### Inspect our changes
Run `git status` again. You'll notice:

* README.md is listed under "Changes not staged for commit".
  * This means `git` knows we care about this file, and that we made changes we haven't confirmed with `git`.
* Your other file is listed under "Untracked files".
  * This means `git` doesn't know if this file is important, and therefore if it should track it.

Run `git diff` again. You'll notice:

* It should you what lines were changes in README.md!
  * Deleted lines are shown in red.
  * Added lines are shown in green.
  * Modified lines are considered a deleted line + an added line.
  * At the top it'll show you the name of the file being `diff`ed, README.md.
* Your new file's changed don't show up, since it's currently untracked.

**PULSE: are there any questions about git status or diff? Please voice any questions - `git` can definitely be confusing, and we're going to keep moving fast from here.**

### Preparing to commit: `git add`
`git add` is used to tell `git` which changes you’re ready to commit.

#### The working tree
`git` has a concept called the “working tree”. The working tree is the set of files that `git` knows are included in your project, and tracks. When you run `git status` and `git diff`, they will only report changes to files that are tracked as part of your working tree. Once a file has been added to the working tree once, `git` remembers it for the future.

#### The index and staging
`git` also has a concept called the “index”. The index is simply the changes to files in the working tree that we’re preparing to commit, e.g. to save/checkpoint. Adding a change to the index is referred to as “staging”, since the index is the "staging ground" for a commit.

#### Using `git add`
You can use `git add` both to stage changes into the index and to add files to the working tree.

First, let’s stage our changes to README.

* Run `git add README.md`. Then run `git status`. You’ll see now that README.md appears in green, under the heading “Changes to be committed”. That means your changes to README are staged, or have been added to the index.

Next, let’s add our new file to the working tree and stage those changes.

* Run `git add <path to new file>`. Then run `git status`. You’ll see that the new file shows up right next to README. It also has a little note saying it’s a “new file”.
* It's important that you only commit changes that are important. If you added some print statements to another file just to see what was happening, it's best if you don't commit that, since it could make your life harder down the line, especially if someone else is editing that file.


##### Using `git diff --cached` to view staged changes
* Run `git diff`. You’ll notice that what you get is a blank display - the changes we saw before. That’s because once you added the changes to the index, `git` assumes you’re no longer interested in seeing them - you’ve already concluded that those changes are going in the commit.
* To view changes you’ve already staged, run `git diff --cached`.
    * Notice that while before we couldn’t see the changes to our new file, now we see the changes to both. That’s because we used `git add` to add our new file to the working tree and stage its changes, so `git` now knows to include it.

### Committing: `git commit`
`git commit` is used to finalize your staged changes.

Once you’ve written some code, inspected it with `git status` and `git diff`, and confirmed you want to keep it with `git add`, `git commit` locks it in and checkpoints your work.

#### Commit messages
Whenever you commit code, you’ll write a “commit message” that describes, briefly, what the changes in this commit do.

* Make your commit messages short and to the point - only the first 80 characters are shown in the preview of the commit on Github.
* Try and give a good description of what this chunk of changes does, so when you or others look back at the “commit history” they can see how the project developed.
* Remember that these are public to anyone browsing your project, so be polite in your language! Ending punctuation is not necessary.
* Example of a bad commit message: “tweaks to make it build”
* Example of a better commit message:  “Tweaked language in about-me”

#### Using `git commit`
* To commit your staged changes, run `git commit -m “<your message>”`. For example, `git commit -m “Added author names to the README”`.
  * If you forget the `-m`, it'll open a text-editor called Vim for you write a message. Vim is awesome, and I'm a big fan, but it can also be pretty confusing. If that happens, type `:q!` to exit Vim, and use `-m` instead.
  * Avoid exclamation points in your message, if you use `-m`, since that breaks the command (for weird Bash reasons).
* Once you’ve committed, run `git status`. Now, you’ll see that the files you staged are gone, and you get a message saying “Your branch is ahead of 'origin/master' by 1 commit.”
* Now run `git log`, and you should see your commit at the top of the list. Use `q` to quit out of the log.
    * Before you quit, take a look at the right side of the log, and you'll see weird strings of text, these are "commit hashes," and they are used to name your commits.

## Publishing your commit
At this point, you’ve written some changes, staged them, and committed them. All of that, however, happened in your local repo. Now, we want to sync your local repo up to the remote, and publish your changes!

## Local vs. remote, and the `git` workflow.
### `git push`
Until this point, pretty much everything is reversible, even committing. Once you push, it becomes much harder to undo changes. Instead, you’ll have to make a new commit undoing the changes, and push that on top!

Doing this isn’t the end of the world, but can be a pain. Especially on the master branch, you want to avoid pushing commits you’re unsure of or that are works-in-progress, if possible.

When you're ready, use `git push` to sync your local changes up to the remote, on Github. It will connect to your remote repository, ask for a username and password to ensure you have permission to modify the remote, and then upload your changes!

# Quick topics

## Undoing changes: `git reset`
Let's say you wrote some code that, it turns out, isn't quite what you wanted to write, and now you want to get back to an older commit. The usual way to do this is using something called `git reset`.

You have to be careful with git reset, since it can really truly delete your code. 

The standard form is `git reset <commit-hash>`. This will keep all of your changes in the working tree, unstaged, and reset the branch to the commit you named. 

Let's follow the instructions from before and make a new commit, then let's push it. In reality, it's best not to push commits to the remote master until they're definitely working commits, but avoiding that is a more complicated topic, so for now we're just going to let remote master be our working branch.

Now, if you run git log, you should see the new commit at the top. We want to reset to the commit before it, so we can copy that hash and run the command `git reset <commit-hash>`. (note, we could also use the command `git reset HEAD^`)

If you run git status now, you'll see that all of the changes are in the working tree, but we appear to be one commit behind master, right where we want to be.

We can now ammend these changes, then re-commit them. But let's say they're really bad, and we just want them to go away. This is when we would use `git reset --hard <commit>`. The `--hard` indicates that we don't want those changes in our working tree either (`--soft` means we want those changes staged) *Be extremely careful with this command though! Save a backup of your work first if you aren't sure what you're doing! (Backing up can be done using branches, so google that if you're interested)*

When we try to push, it'll give us an error, because we aren't just trying to put new commits on the remote master. To fix this, we'll have to run `git push -f` to force the remote branch to be the same as the local branch.

## I just want my code to be the code that's on github!

This comes up all the time. You've done a whole bunch of things you don't like, other people have pushed code, and you just want a fresh slate. Here is that command. Be careful, as usual, as this will really just make your local branch into an exact replica of the one on github.

All you need to do is run `git fetch` (this ensures that your local git knows what is in the remote repository). Then run `git reset --hard origin/master`.

## How do I get code I've written into git?
* `cd` into the folder 
* run `git init`
* run `git add .` (this adds everythign in the folder)
* run `git commit -m 'initial commit'` 
* create a new repository on github, and follow the instructions for "…or push an existing repository from the command line" which should be as follows:
    * `git remote add origin <url of remote>` This sets your branch up to track that repository.
    * `git push -u origin master` This pushes your new commits



## Summary and recap
In this tutorial, we covered the basics of how to use `git` and Github to track, back up, and version your code. Specifically, we:

1. Set up Github accounts, and created a repository with just a README in it.
2. Used `git clone` to download a copy of this repository to our local machines.
3. Used `git status` and `git diff` to explore the blank repository.
4. Made changes to some files, and used `status` and `diff` to inspect them.
5. Used `git add` to stage our changes.
6. Used `git commit` to solidify and finalize our changes.
7. Used `git push` to publish those changes for our collaborators, and the world, to see!

### Using `git` and Github for EECS 213 homework
I strongly encourage you to practice these skills on the code you write for your homework! This will be especially useful later, as the projects start to build on each other.

**_HOWEVER._**

The same way we ask you not to post code to Piazza, you should **_not_** publish class materials (including your solutions) publicly without explicit permission from your professor.

If you want to use `git` and Github for this class, apply for the Github Student Pack first and use the free private repositories you get to store your code such that other students can’t look at it.

### Practice it all again, on your own!
Try making some changes to your new file, and going through the process of adding, committing, and pushing them!

The full notes for this tutorial are also available online. You can find them, of course, on my Github!

