# Git Walkthrough

The main purpose of this guide is not just explain git or  how to use it, it has the intention of create a culture and consciousness between developers of the importance of using a version control.

- [1 Introduction](#-1-Introduction)
    - [1.1  What's Git?(and a little bit of history)](#11)
    - [1.2 Why should I use Git?](#)
    - [1.3 Download](#)
- [2 How it works](#)
    - [2.1 Integrity](#)
    - [2.2 States](#)
- [3 How to use it](#)
    - [3.1 Identify yourself](#)
    - [3.2 Text Editor](#)
    - [3.3 Current configuration](#)
    - [3.4 Basic commands](#)
        - [3.4.1 Creating a new repository](#)
        - [3.4.2 Tracking files](#)
        - [3.4.3 Cloning a repository](#)
        - [3.4.4 Log](#)
        - [3.4.5 Branches](#)
- [Thanks to](#)

# 1 Introduction

## 1.1  What's Git?(and a little bit of history)
Git is a version control system commonly used to software development.  Git development began in 2005 by Linus Torvalds, He wanted a distributed system that could be used like [BitKeeper](https://en.wikipedia.org/wiki/BitKeeper) unfortunately to him (lucky to us),  there was no free software with those capabilities.


## 1.2 Why should I use Git?

Version control software allows you to have “versions” of a project, which show the changes that were made to the code over time, and allows you to backtrack if necessary and undo those changes.

The benefits of a system like this is that multiple developers can make changes, and each change can then be attributed to a specific developer.

## 1.3 Download

At this point, you may have asked yourself some questions like: How do I get this awesome tool?, is it free? Well git is completely free and its also open source. And its available for mac, linux and windows users.

If you are a mac or linux user a old version of git is probably already installed on your computer, if you are window user you need to download it.

Links to download git:

 - [Mac](https://git-scm.com/download/mac)
 - [Linux](https://git-scm.com/download/linux)
 - [Windows](https://git-scm.com/download/windows)

# 2 How it works

Instead of thinking of the differences between each file across time,  git uses snapshots, it means git makes a copy of the whole directory (only to the files that changed) This is essentially what Git is.

## 2.1 Integrity

Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it’s impossible to change the contents of any file or directory without Git knowing about it.

## 2.2 States

Git has three main states that your files can reside in: committed, modified, and staged.

- **Committed** means that the data is safely stored in your local database.
- **Modified** means that you have changed the file but have not committed it to your database yet.
- **Staged** means that you have marked a modified file in its current version to go into your next commit snapshot.

# 3 How to use it

## 3.1 Identify yourself

If you haven't use git before you need to setup a basic configuration, the first thing you need to do is to tell git who you are.   The name and email will be used by git to identify the person who is making the changes.

```bash
$ git config --global user.name "Disblu"
$ git config --global user.email dev@disblu.com
```

## 3.2 Text Editor

You can configure the default text editor, if you don't do so git is going to use your default text editor. We recommend to use vim.

```bash
$ git config --global core.editor "vim"
```

## 3.3 Current configuration

You can check your current configuration using the next command:

```bash
$ git config --list
user.name=Disblu
user.email=dev@disblu.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

## 3.4 Basic commands

### 3.4.1 Creating a new repository

Before to being able to star tracking the changes on your project you need to initialise the git repository.  Just go to the root of the project and use the next command:

```bash
$ git init
```

### 3.4.2 Tracking files

Before to start adding files to staging,  maybe you want to use the `status` command to know more about the state of the repository.  It gives you information about the files that changed and about what will be include to the commit.

```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   git/README.md
```

If you made changes to the project, it is probably a good time to keep track of those files.  You can use the `add` command to stage the files you want to include to the commit.

```bash
$ git add [file name or regex]
```

Once you added the files you want to include, it's time to save those changes.  The `commit ` command will do that for us.

```bash
$ git commit -m [a message describing the changes]
```

The parameters `-m` means that the following text will be the message for that commit.

The command `commit` has a numerous amount of parameters,  you can read more about it [here](https://git-scm.com/docs/git-commit).

### 3.4.3 Cloning a repository

Sometimes you need to work using an existing repository,  you can use the `clone` commando to do so.

```bash
$ git clone [url]
```

### 3.4.4 Log

If you started from an existing repository,  maybe you want to look back to see what has happened.  The command `log` is the most appropriate for this situation.

```bash
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Albert <albert@disblu.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Add devise gem

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Julian  <julian@disblu.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    Add git ignore

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Frans <frans@disblu.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    Initial commit
```

The log command has many options you can use to filter and give format to the output. For example you can use the --oneline and it will show you something like this:

```bash
$ git log --oneline
ca82a6d Add devise gem
085bb3b Add git ignore
a11bef0 Initial commit
```


To read more about the `log` command click [here](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History).

### 3.4.5 Branches

Until now we have been working on the same branch ("master").  But What is a branch? A branch represents an independent line of development. New commits are recorded in the history for the current branch, which results in a fork in the history of the project.

# Thanks to

This guide takes information from differences sources,   without them this guide couldn't exist:

[Git (Software)](https://en.wikipedia.org/wiki/Git_(software))

[Git Guide by Roger  ](http://rogerdudler.github.io/git-guide/)

[Quora](https://www.quora.com/What-is-git-and-why-should-I-use-it)

[Atlassian Git tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-branch)
