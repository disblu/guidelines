# Swift Walkthrough

The main purpose of this guide is to create code that is concise, readable and simple.✌🏻

- [1 Naming](#1-naming)
   - [1.1 Protocols](#11-protocols)
   - [1.2 Enumerations](#12-enumerations)
   - [1.3 Language](#13-language)
- [2 Spacing](#2-spacing)
   - [2.1 Integrity](#21-integrity)
   - [2.2 States](#22-states)
- [3 How to use it](#3-how-to-use-it)
   - [3.1 Identify yourself](#31-identify-yourself)
   - [3.2 Text Editor](#32-text-editor)
   - [3.3 Current configuration](#33-current-configuration)
   - [3.4 Basic commands](#34-basic-commands)
       - [3.4.1 Creating a new repository](#341-creating-a-new-repository)
       - [3.4.2 Tracking files](#342-tracking-files)
       - [3.4.3 Ignoring files](#343-ignoring-files)
       - [3.4.4 Cloning a repository](#344-cloning-a-repository)
       - [3.4.5 Log](#345-log)
       - [3.4.6 Branches](#346-branches)
       - [3.4.7 Merging](#347-merging)
       - [3.4.8 Resolving merge conflicts](#348-resolving-merge-conflicts)
       - [3.4.9 Stash](#349-stash)
- [4 Conventions](#4-conventions)
    - [4.1 Branch naming](#41-branch-naming)
    - [4.2 Commits](#42-commits)
       - [4.2.1 Structure](#421-structure)
       - [4.2.2 Message](#422-message)
    - [4.3 Merging](#43-merging)
- [5 Alternatives](#5-alternatives)
- [Thanks to](#thanks-to)

# 1 Naming
Use descriptive names with camel case for classes, methods, variables, etc. Type names (classes, structures, enumerations and protocols) should be UpperCamelCase, while method names and variables should be lowerCamelCase.

Good:

```Swift
private let maximumBookCount = 100

class BookContainer {
  var bookButton: UIButton
  let bookWidthPercentage = 0.85
}
```

Bad:

```Swift
let MAX_BOOK_COUNT = 100

class app_bookContainer {
  var bBut: UIButton
  let bWidthPct = 0.85
}
```
According to [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/#follow-case-conventions), abbreviations and initialisms that appear in all uppercase should be uniformly uppercase or lowercase.

Good:
```Swift
let urlString: URLString
let userID: UserID
```
Bad:
```Swift
let uRLString: UrlString
let userId: UserId
```

When specifying the type of an identifier, always put the colon immediately after the identifier, followed by a space and then the type name.

```Swift
class Coffee: Drink { ... }

let timeToCoffee: NSTimeInterval = 2

func makeCoffee(type: CoffeeType) -> Coffee { ... }
```

Rationale: The type specifier is saying something about the identifier so it should be positioned with it.

Also, when specifying the type of a dictionary, always put the colon immediately after the key type, followed by a space and then the value type.

```Swift
let capitals: [Country: City] = [ Spain: Madrid ]
```

## 1.1 Protocols
According to Apple's API Design Guidelines, protocols names that describe what something is should be a noun. Examples: ```Collection```, ```BookFactory```. Protocols names that describe an ability should end in -ing, -able, or -ible. Examples: ```Relatable```, ```Resizing```.


## 1.2 Enumerations

You introduce enumerations with the enum keyword and place their entire definition within a pair of braces. Cases are to be written in LowerCamelCase.

```Swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```
or 
```Swift
enum CompassPoint {
    case north, south, east, west
}
```

## 1.3 Language

Everything should be in US English!

Good:
```Swift
let red = CGColor.redColor()
```
Bad:
```Swift
let rojo = CGColor.redColor()
```

# 2 Spacing

Indent using 2 spaces rather than tabs to conserve space and help prevent line wrapping. Be sure to set this preference in Xcode and in the Project settings as shown below:
![alt text](indentation.png "Indent")

## 2.1 Integrity

Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it’s impossible to change the contents of any file or directory without Git knowing about it.

## 2.2 States

Git has three main states that your files can reside in: committed, modified, and staged.

- **Committed** means that the data is safely stored in your local database.
- **Modified** means that you have changed the file but have not committed it to your database yet.
- **Staged** means that you have marked a modified file in its current version to go into your next commit snapshot.

# 3 How to use it

## 3.1 Identify yourself

If you haven't use Git before you need to setup a basic configuration, the first thing you need to do is to tell Git who you are.   The name and email will be used by Git to identify the person who is making the changes.

```bash
$ git config --global user.name "Disblu"
$ git config --global user.email dev@disblu.com
```

## 3.2 Text Editor

You can configure the default text editor, if you don't do so Git is going to use your default text editor. We recommend to use vim.

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

Before to being able to star tracking the changes on your project you need to initialise the Git repository.  Just go to the root of the project and use the next command:

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

The parameters `-m` means that the following text will be the message for that commit (The command `commit` has a numerous amount of parameters,  you can read more about it [here](https://git-scm.com/docs/git-commit)).



If you added some file by error and you want to unstage the file just run the following command:

```bash
$ git reset HEAD [file name]
```

Also if you want discard changes , you can use the checkout command:

```bash
$ git checkout -- [file name]
```

### 3.4.3 Ignoring files

Sometimes there are files you don't want to track (for example: binary files,  secret files, etc. ). You need to create a `.gitignore` file to tell Git what files you want to ignore.

You can specify entire directories in .gitignore or use the * wildcard to ignore files with a particular extension. For example:

```bash
*.bin
*.DS_STORE
/config/config.yml
```

### 3.4.4 Cloning a repository

Sometimes you need to work using an existing repository,  you can use the `clone` commando to do so.

```bash
$ git clone [url]
```

### 3.4.5 Log

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

### 3.4.6 Branches

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

### 3.4.7 Merging

Merging is Git's way of putting a forked history back together again. The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.

Merge the specified branch into the current branch.

```bash
$ git merge [branch name]
```

### 3.4.8 Resolving merge conflicts

Most of the time,  Git is going to be able to merge everything automatically but sometimes Git needs some help. If the two branches you‘re trying to merge both changed the same part of the same file, Git won’t be able to figure out which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually.


### 3.4.9 Stash

Now let’s say we had to make an emergency fix to our project. We don’t want to commit an unfinished feature, and we also don’t want to lose our current work. The solution is to temporarily remove these changes with the git stash command:

```bash
$ git status
$ git stash
$ git status
```

If you want to get your changes back,  the option `pop`  applies the top stashed element and removes it from the stack.

```bash
$ git stash pop
```
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

- Separate subject from body with a blank line

```
Add news feed module

It shows the news feed to the user, the datum is retrieved in batches (10 news each time)
```
-  Limit the subject line to **50 characters**
```ruby
# good
"Add login module with omniauth (Facebook provider)"
# bad
"Add login module with omniauth, the user can only login using his Facebook account"
```

- **Capitalize** the subject line

```ruby
# good
"Add visa and master card payment methods"
# bad
"add visa and master card payment methods"
```
-  Do not end the subject line with a period

```ruby
# good
"Add push notifications p12 certificates "
# bad
"Add push notifications p12 certificates."
```
- Use the **imperative mood** in the subject line

```ruby
# good
"Add user model and spec tests"
# bad
"Added user model and spec test"
```
- Wrap the body at **72 characters**

Git **never** wraps text automatically. When you write the body of a commit message, you must mind its right margin, and wrap text manually.

The recommendation is to do this at 72 characters, so that Git has plenty of room to indent text while still keeping everything under 80 characters overall.

- Use the body to explain what and **why vs. how**
```
commit eb0b56112492ab5c16c745e6da39c53126924ed6
Author: Corgs Yerena <corgs@disblu.com>
Date:   Wed Jul 10 10:57:55 2017 +0200

   Update devise gem to 4.2

   Replace devise deprecated methods, the Facebook login module
   now doesn't require the birthday field to registrar a user.
```
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

Like we said before the main purpose of this guide is promote between developers the use of a version control system.  Besides how much we love Git, we know there are more version control systems.  We cannot say that Git is better or worse than others, every version has advantages and disadvantages.

You can find a full list of version control systems [here](https://en.wikipedia.org/wiki/List_of_version_control_software).

# Thanks to

This guide takes information from differences sources,   without them this guide couldn't exist:

[Git (Software)](https://en.wikipedia.org/wiki/Git_(software))

[Git Guide by Roger  ](http://rogerdudler.github.io/git-guide/)

[Quora](https://www.quora.com/What-is-git-and-why-should-I-use-it)

[Atlassian Git tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-branch)

[Git by Chris](http://chris.beams.io/posts/git-commit/)







