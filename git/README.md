# Git Walkthrough

The main purpose of this guide is not just explain git or  how to use it, it has the intention of create a culture and consciousness between developers of the importance of using a version control.

- [1 Introduction](#1-introduction)
    - [1.1 What is git?](#11-what-is-git)
    - [1.2 Why should I use git?](#12-why-should-i-use-git)
    - [1.3 Download](#13-download)
- [2 How it works](#2-how-it-works)
    - [2.1 Integrity](#21-integrity)
    - [2.2 States](#22-states)
- [3 How to use it](#3-how-to-use-it)
    - [3.1 Identify yourself](#31-identify-yourself)
    - [3.2 Text Editor](#32-text-editor)
    - [3.3 Current configuration](#33-current-configuration)
    - [3.4 Basic commands](#34-basic-commands)
        - [3.4.1 Creating a new repository](#341-creating-a-new-repository)
        - [3.4.2 Tracking files](#342-tracking-files)
        - [3.4.3 Cloning a repository](#343-cloning-a-repository)
        - [3.4.4 Log](#344-log)
        - [3.4.5 Branches](#345-branches)
        - [3.4.6 Merging](#346-merging)
        - [3.4.7 Resolving merge conflicts](#347-resolving-merge-conflicts)
- [4 Conventions](#4-conventions)
- [5 Alternatives](#5-alternatives)
- [Thanks to](#thanks-to)

# 1 Introduction

## 1.1 What is git?
Git is a version control system commonly used to software development.  Git development began in 2005 by Linus Torvalds, He wanted a distributed system that could be used like [BitKeeper](https://en.wikipedia.org/wiki/BitKeeper) unfortunately to him (lucky to us),  there was no free software with those capabilities.


## 1.2 Why should I use git?

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

List all of the branches in your repository.

```bash
$ git branch
```

Create a new branch. This does not check out the new branch.

```bash
$ git branch [branch name]
```

Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.

```bash
$ git branch -d [branch name]
```

Force delete the specified branch, even if it has unmerged changes.

```bash
$ git branch -D [branch name]
```

If you want to move to another branch you can use the `checkout` command

``` bash
$ git checkout [branch name]
```

But in some cases you want to move and create a new branch at same time,  you can use the `-b` option:

```bash
$ git checkout -b [branch name]
```

### 3.4.6 Merging

Merging is Git's way of putting a forked history back together again. The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.

Merge the specified branch into the current branch.

```bash
$ git merge [branch name]
```

### 3.4.7 Resolving merge conflicts

Most of the time,  git is going to be able to merge everything automatically but sometimes git needs some help. If the two branches you‘re trying to merge both changed the same part of the same file, git won’t be able to figure out which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually.

# 4 Conventions

## 4.1 Branch naming

Choose short and descriptive names:

```bash
# good
$ git checkout -b fix_login_module

# bad
$ git checkout -b fix_something
```

If you are working with a group of developers,  the branch name usually starts with the initials of the person. For example:

If your name is Juan Perez

```bash
# good
$ git checkout -b jp_refactor_login_module

# bad - It doesn't tell you who is the owner of the branch
$ git checkout -b refactor_login_module
```

## 4.2 Commits

### 4.2.1 Structure

 - Each commit should be a single logical change.
 - Don't make several logical changes in one commit.
 - Don't split a single logical change into several commits.

### 4.2.2 Message

Always think about the 7 rules of a great commit message.

 1. Separate subject from body with a blank line
 2. Limit the subject line to **50 characters**
 3. **Capitalize** the subject line
 4. Do not end the subject line with a period
 5. Use the **imperative mood** in the subject line
 6. Wrap the body at **72 characters**
 7. Use the body to explain what and **why vs. how**

## 4.3 Merging

**Do not rewrite published history.** (Don't use push --force) The repository's history is valuable in its own right and it is very important to be able to tell what actually happened. Altering published history is a common source of problems for anyone working on the project.

If your branch includes more than one commit, do not merge with a fast-forward:

```bash
# good
$ git merge --no-ff [branch name]
# bad
$ git merge [branch name]
```

# 5 Alternatives

Like we said before the main purpose of this guide is promote between developers the use of a version control system.  Besides how much we love git, we know there are more version control systems.  We cannot say that git is better or worse than others, every version has advantages and disadvantages.

You can find a full list of version control systems [here](https://en.wikipedia.org/wiki/List_of_version_control_software).

# Thanks to

This guide takes information from differences sources,   without them this guide couldn't exist:

[Git (Software)](https://en.wikipedia.org/wiki/Git_(software))

[Git Guide by Roger  ](http://rogerdudler.github.io/git-guide/)

[Quora](https://www.quora.com/What-is-git-and-why-should-I-use-it)

[Atlassian Git tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-branch)

[Git by Chris](http://chris.beams.io/posts/git-commit/)
