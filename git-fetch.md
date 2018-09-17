# `git fetch`
---

## Introduction

Let’s say you’re working on a project and a team member pushes changes to the remote repository. If you want to see what your team members have been working on, you can _fetch_ those changes and download them to your local machine by using the command `git fetch`.  `git fetch` is considered safe because unlike `git pull`, it doesn't merge the changes with your workspace, leaving your current work intact.

## Description
---

To understand what happens when we run `git fetch`, lets recap how Git works:

Git is a distributed, peer-to-peer version control system.  To support this model, Git maintains a workspace, a local repository (i.e. repo), and staging area for your updates.  By keeping a local copy of a remote repo, Git can track the changes when the remote repo is not reachable.  Then later when you push your changes upstream, Git can transfer them from a point in time known to the remote repo.  However, it may be important to keep your local branch synchronized with any updates pushed by your teammates. 

Git creates a `.git/` directory where it stores and manipulates everything. If you simply wanted to clone a repo, copying this directory would give you everything that's needed. A git database is a key-value system - whenever you add a file and track it, Git generates a hash on its contents used to uniquely point to that version of the file, then compresses the file and stores it.  Git stores all commits (i.e. tracked changes to the repository) in the objects directory and uses unique names or _refs_ to reference them.  Branches are simply references to a record of changes. Local and remote refs are kept separate: local branch refs are stored in `.git/refs/heads/` and remote branch refs are stored in `.git/refs/remotes/` directories. Remote branches are just like local branches except remote branches map commits from a remote repository. To see the list of local branches, run command `git branch` and to see the list of remote branches, run command `git branch -r`.  

The `git fetch` command downloads updates from a remote tracking branch to your local machine.  A remote tracking branch is a branch that's setup to push/pull with a remote repo. For example, the _master_ branch may be the remote tracking branch a developer commits to before pushing to the remote copy.   Therefore, before you run the `git fetch` command, you must _checkout_ the local branch that corresponds to the remote branch.

## `git fetch` vs `git pull`
---

Behind the scenes to know what branch you are currently on, Git keeps a moveable pointer called HEAD.  HEAD is a pointer to the branch you're working on and represents your current local _workspace_.  When you `git checkout <branch>`, you determine what version of the project you want to work on.  Git uses the branch ref to locate the desired commit, then pulls that revision's files out of the compressed database and places them into your working directory. 

When you fetch, Git updates FETCH_HEAD file which keeps track of the last fetch from the remote branch.  After checking out the local corresponding branch, running command `git merge <branch>` combines the repo histories between parent and specified merged branches.  This _moves_ the HEAD pointer to the most recent commit, thus wiping out any uncommited work.  In short, `git fetch` downloads changes from a remote tracking branch and `git pull` performs a fetch before merging the changes, affecting your current workspace.

## Syntax
---

`git fetch` # when run without specifying braches, runs `git fetch origin master`

`git fetch <remote>` # specify the remote repo that's the source of a fetch/pull

`git fetch <remote> <branch>` #specify the remote repo and branch that's the source of a fetch/pull

`git fetch --all` # fetch all remotes
