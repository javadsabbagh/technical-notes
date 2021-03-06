# Git Tutorials - Pro Git

## Github REST API
https://developer.github.com/v3/


## Forking Projects
* [All notes about forking others projects](https://guides.github.com/activities/forking/)
* [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)

Keeping a fork up to date:
1. Clone your fork:

```sh
git clone git@github.com:YOUR-USERNAME/YOUR-FORKED-REPO.git
```

2. Add remote from original repository in your forked repository:

```sh
cd into/cloned/fork-repo
git remote add upstream git://github.com/ORIGINAL-DEV-USERNAME/REPO-YOU-FORKED-FROM.git
git fetch upstream
```

3. Updating your fork from original repo to keep up with their changes:

```sh
git pull upstream master
```


## Git Configuration
```sh
git config --global user.name   "your user name"
git config --global user.email  "your_email@example.com"
git config --list
```

----------

## Creating Repository

When creating a new repository in Github:
It shows you a messsage hot to initialize the repo.
1- …or create a new repository on the command line

echo "# technical-notes" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/javadsabbagh/technical-notes.git
git push -u origin master

2- …or push an existing repository from the command line

git remote add origin https://github.com/javadsabbagh/technical-notes.git
git push -u origin master

----------

## Tortoise Git

Tortoise Git is a nice tool to practice comands.


Pulling 

```sh
git.exe pull -v --progress "origin"


POST git-upload-pack (1007 bytes)
remote: Counting objects: 515, done.
remote: Compressing objects: 100% (102/102), done.
Receiving objects: 100% (515/515), 80.53 KiB | 102.00 KiB/s, done.
Resolving deltas: 100% (192/192), completed with 96 local objects.
remote: Total 515 (delta 178), reused 134 (delta 134), pack-reused 201
From https://github.com/RestComm/jss7
3025312..dee1f1e  master     -> origin/master
= [up to date]      1.x        -> origin/1.x
= [up to date]      2.0.x      -> origin/2.0.x
= [up to date]      2.1.x      -> origin/2.1.x
= [up to date]      SCCP_198   -> origin/SCCP_198
= [up to date]      branch29   -> origin/branch29
b4a1e3e..c7064ab  netty-2    -> origin/netty-2
Updating 3025312..dee1f1e
Fast-forward
.../ss7/cap/isup/GenericNumberCapImpl.java         |  28 ++-
.../map/primitives/ArrayListSerializingBase.java   |  13 +-
.../AnyTimeInterrogationResponseImpl.java          |  79 ++++--
.../subscriberInformation/SubscriberInfoImpl.java  | 275 ++++++++++++++-------
.../subscriberManagement/CUGIndexImpl.java         |   6 +
.../org/mobicents/protocols/ss7/sccp/Rule.java     |   2 +
.../ss7/sccp/impl/SccpRoutingControl.java          |   2 +-
.../protocols/ss7/sccp/impl/router/RuleImpl.java   |  88 ++++++-
.../ss7/sccp/impl/oam/SccpExecutorTest.java        |   2 +-
.../protocols/ss7/sccp/impl/router/RouterTest.java |  61 ++++-
10 files changed, 416 insertions(+), 140 deletions(-)
```

Sabbagh:
Just the current branch (master) is  updated, however netty-2 branch is not up to date! How to update netty-2 branch? switch to it and update it?

"--progress" options shows +/- in front of files to show how much they has been altered.

----------

## Pushing
```sh
git.exe push --progress "origin" master:master
```

Pushing all branches to the remote server (use --all option)
```sh
git.exe push --all --progress "origin"
```
----------

## Tagging

Listing Your Tags:
$ git tag
v0.1
v1.3

Search for tags with a particular pattern:
```sh
$ git tag -l "v1.8.5*"
```
v1.8.5
v1.8.5-rc0
v1.8.5-rc1
v1.8.5-rc2
v1.8.5-rc3
v1.8.5.1
v1.8.5.2
v1.8.5.3
v1.8.5.4
v1.8.5.5

Creating Tags
two main types of tags: lightweight and annotated.

A lightweight tag is very much like a branch that doesn’t change – it’s just a
pointer to a specific commit.

Annotated tags, however, are stored as full objects in the Git database.
They’re checksummed; contain the tagger name, email, and date; have a tagging
message; and can be signed and verified with GNU Privacy Guard (GPG).
It’s generally recommended that you create annotated tags so you can have all
this information.

Annotated Tags
```sh
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
```
v0.1
v1.3
v1.4

If you don’t specify a message for an annotated tag, Git launches your editor so you can
type it in.

see the tag data
$ git show v1.4


Lightweight Tags
To create a lightweight tag, don’t supply the -a, -s, or -m option:

```sh
$ git tag v1.4-lw
$ git tag
```
v0.1
v1.3
v1.4
v1.4-lw
v1.5


```sh
$ git show v1.4-lw
```
----------

## Git Aliases
```sh
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```
This technique can also be very useful in creating commands that you think
should exist. e.g.

```sh
$ git config --global alias.unstage 'reset HEAD --'
```

This makes the following two commands equivalent:
```sh
$ git unstage fileA          # a lot easier  to remember
$ git reset HEAD -- fileA    # original command, hard to remember
```


Another example :
```sh
$ git config --global alias.last 'log -1 HEAD'
$ git last
```

----------

Git’s killer feature: its branching model.


