# git fetch

## Overview

The `git fetch` command allows you to download remote branches to checkout and review.

Unlike `git pull` which automatically merges changes with your local branches, `git fetch` imports the latest commits from remote repositories and stores them locally as **remote branches** keeping all local branches unaffected.

## Description

A key advantage of Git is allowing multiple developers to work on the same codebase on their own local machines. Of course, when multiple developers are working at the same time, they may add or remove code which conflicts with other code another developer has added or removed.

The `git fetch` command can be used to download branches from remote repositories (e.g. Github or another developer's computer) and store them locally as 'remote branches'. Frome here, you can checkout those changes to review, before merging the changes to a local branch.

Because no changes happen to any of your local branches, `git fetch` is considered a very 'safe' command to use in Git – none of the work you've done locally will be affected.

It is important to note that after running the fetch command, the remote branches are downloaded locally, however they are not automatically synced. This means you'll have access to them without an Internet connection however but you will need to re-run the fetch command to get any new commits that may have been made.

## Using the command

### Basic example
The below command will 'fetch' from the remote repository all updates to existing and new branches:

```
git fetch
```
After this, the following command and flag will show all local and remote branches you have access to:

```
git branch -a
```

An example output of the above command might be:

```
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/about-page
  remotes/origin/master
```

From the above output we see there is a single local branch 'master', and additional remote branches including 'about-page'. To view details of this branch we could run the command `git log origin/about-page` and view the commit history. Alternatively, we could run `git checkout origin/about-page` which would change the files in the current working branch to this new remote branch.

### Merging changes

Merging is similar to merging changes between local branches. Assuming you want to merge fetched changes in `origin/about-page` to your current local branch you would run the following:

```
git merge origin/about-page
```

You might also create a new local branch based on one of your remote branches. This can be done with the following command (it will merge the changes from the remote branch `origin/about-page` into a newly created and checked out local branch called `localaboutpage`):

```
git checkout -b localaboutpage origin/about-page
```

### Fetching specific branches

Often you may want to fetch branches from a specific repository (e.g. `fetch branch origin`) or from a specific branch on a remote repository (e.g. `fetch branch alan mobile-development`). The later example is assuming you've added a remote repository called 'steve' (presumably pointing to a developer's local computer or Github repository).

You can also fetch a branch from a repostiory without having added it as a remote in your local Git repository. For example:

```
git fetch git@github.com:will-schmidt/cuddly-bassoon.git about-page
```

## Additional information

For full documentation on `git fetch` can be found here: [https://git-scm.com/docs/git-fetch](https://git-scm.com/docs/git-fetch)