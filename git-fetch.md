# git fetch

## Overview

The `git fetch` command allows you to download remote branches to checkout and review.

Unlike `git pull`, which automatically merges changes with your local branches, `git fetch` imports the latest commits from remote repositories and stores them locally as remote branches keeping all local branches unaffected.

## Description

A key advantage of Git is allowing multiple developers to work on the same codebase on their own local machines. Of course, when multiple developers are working at the same time, they may add or remove code which conflicts with other code another developer has added or removed.

The `git fetch` command can be used to download branches from remote repositories (e.g. Github or another developer's computer) and store them locally as 'remote branches'. Frome here, you can checkout those changes or merge the changes to a local branch.

### Basic example
The below command will 'fetch' from the remote repository updates to existing and new branches:

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

From the above output we see there is a single local branch 'master', and additional remote branches including 'about-page'. To view the files in this branch we could run the command `git log origin/about-page` or alteernatively we could run `git checkout origin/about-page` which would change the files in the current working branch to this new remote branch.

