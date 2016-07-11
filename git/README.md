# Git Walkthrough

The main purpose of this guide is not just explain git or  how to use it, it has the intention of create a culture and consciousness between developers of the importance of using a version control.

# 1 Introduction

## 1.1  What's Git?(and a little bit of history)
Git is a version control system commonly used to software development.  Git development began in 2005 by Linus Torvalds, He wanted a distributed system that could be used like [BitKeeper](https://en.wikipedia.org/wiki/BitKeeper) unfortunately to him (lucky to us),  there was no free software with those capabilities.


## 1.2 Why should I use Git?

Version control software allows you to have “versions” of a project, which show the changes that were made to the code over time, and allows you to backtrack if necessary and undo those changes.

The benefits of a system like this is that multiple developers can make changes, and each change can then be attributed to a specific developer.

## 1.3 Setup

At this point , you may have asked yourself some questions like: How do I get this awesome tool?, is it free? Well git is completely free and its also open source. And its available for mac, linux and windows users.

If you are a mac or linux user a old version of git is probably already installed on your computer, if you are window user you need to download it.

Links to download git:

 - [Mac](https://git-scm.com/download/mac)
 - [Linux](https://git-scm.com/download/linux)
 - [Windows](https://git-scm.com/download/windows)

# 2 How it works?

Instead of thinking of the differences between each file across time,  git uses snapshots, it means git makes a copy of the whole directory (only to the files that changed) This is essentially what Git is.

## 2.1 Integrity

Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it’s impossible to change the contents of any file or directory without Git knowing about it.

## 2.2 States

Git has three main states that your files can reside in: committed, modified, and staged.

- **Committed** means that the data is safely stored in your local database.
- **Modified** means that you have changed the file but have not committed it to your database yet.
- **Staged** means that you have marked a modified file in its current version to go into your next commit snapshot.

# 3 Terminology

# 4 Alternatives

# Thanks to

This guide takes information from differences sources,   without them this guide couldn't exists:

[Git (Software)](https://en.wikipedia.org/wiki/Git_(software))

[Git Guide by Roger  ](http://rogerdudler.github.io/git-guide/)

[Quora](https://www.quora.com/What-is-git-and-why-should-I-use-it)
