# Git Checkout

### Name
```
- git checkout
```

### Synopsis
```
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout --patch [<tree-ish>] [--] [<paths>...]
```

### Description
Updates files in the working tree to match the version in the index or the specified tree. The `git checkout` command operates upon three distinct entities: files, commits, and branches. If no paths are given, `git checkout` will also update `HEAD` to set the specified branch as the current branch.

**git checkout \<branch\>**
> Switch to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the <branch>

**git checkout -b|-B \<new_branch\> [\<start point\>]**
> Specifying -b causes a new branch to be created as if `git branch` were called and then checked out
> If -B is given, <new_branch> is created if it doesn’t exist; otherwise, it is reset

### Options
`-q`
`--quiet`
- Quiet, suppress feedback messages.

`-f`
`--force`
- When switching branches, proceed even if the index or the working tree differs from HEAD. This is used to throw away local changes
- When checking out paths from the index, do not fail upon unmerged entries; instead, unmerged entries are ignored

`-b <new_branch>`
- Create a new branch named <new_branch> and start it at <start_point>

`-B <new_branch>`
- Creates the branch <new_branch> and start it at <start_point>. If it already exists, then reset it to <start_point>. This is equivalent to running "git branch" with "-f"

`-m`
`--merge`
- When switching branches, if you have local modifications to one or more files that are different between the current branch and the branch to which you are switching, the command refuses to switch branches in order to preserve your modifications in context

`<new_branch>`
- Name for the new branch

`<start_point>`
- The name of a commit at which to start the new branch. Defaults to HEAD

`<tree-ish>`
- Tree to checkout from (when paths are given). If not specified, the index will be used.

### Summary
This page focused on usage of the git checkout command when changing branches. In summation, git checkout, when used on branches, alters the target of the HEAD ref. It can be used to create branches, switch branches, and checkout remote branches. 