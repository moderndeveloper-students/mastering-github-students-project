#### Understanding the `Git branch` command

# When using Git, a `branch` can be thought of as simply a movable pointer.

The pointer itself is referred to as the `HEAD`, and one simple way of thinking about the HEAD is to imagine it as the `current` branch. You can find out which branch the HEAD is pointing at by using the following command:

  ```
  cat .git/HEAD
  ```

Whenever you make a change (commit) using Git within a repository you are provided with a `"master"` branch automatically, which points to the last commit you made. Every time you perform a commit, this master branch moves forward. 

When a new branch is created (and given a suitable title) the user can then move the pointer, i.e. the HEAD, to the newly created branch, and this will provide the user with a new direction in which to take their workflow. This new branch will now move forward automatically with each commit.

The user can at any time switch back to the master branch to make changes, and will then move forward with each new commit from an older version of the repository, as both sets of commits will be isolated in separate branches. 

## How to use the Git Branch command

One reason that a developer may wish to create a new branch would be to test a new feature that may or may not be included in the final project. A good name for this branch could be "testing-branch." This branch can be created using the `git branch` command as follows: 

  ```
  git branch testing-branch
  ```

Simply typing `git branch` into the terminal will now show the presence of two branches within Git: "master", and "testing-branch." An asterisk will appear next to the current branch.

  ```
  git branch
  ```

which should give a result that looks like this:

  ```
  * master
    testing-branch
  ```

Adding the flag `-a` to the command will also list the branches that exist on your local device, but this time include remote-tracking branches as well. Remote-tracking branches can be thought of as bookmarks to remind you where the branches in your remote repositories were the last time you connected to them. 

  ```
  git branch -a
  ```

If for any reason you need to change the name of a branch, lets say from "testing-branch" to "john-testing-branch" (to make your identity clear to fellow contributors), this can be done by using the `-m` option as follows:

  ```
  git branch -m testing-branch john-testing-branch
  ```

## When and how to delete a branch

As mentioned previously, it is common for branches to be created and utilized for developing a new feature. If the new feature code found on the branch is fully developed and ready to become a permanent fixture within the master branch code, the programmer will perform a process called merging, i.e. to "pull" and "merge" commits present on the new feature branch, with those found on the master. 

When such a merge occurs it is good practice to then delete the branch from which the commits were pulled to help maintain a workspace free from un-necessary clutter. Deleting a `local` branch is done using the `-d` option with the git branch command:

  ```
  git branch -d john-testing-branch
  ```

Deleting a `remote` branch uses the following command:

  ```
  git push origin --delete <branch_name>
  ```

In the event that code from your new feature branch is not to be merged with the master branch, and you wish to delete the branch (or others) irrespective of its merged status you can do so by capitalizing the previous flag and using `-D` instead:

  ```
  git branch -D john-testing-branch
  ```

## A note on Git Branch tracking

A 'tracking branch' in Git is a local branch that is connected to a remote branch (referred to as the upstream branch). When you push and pull commits on your local branch, it automatically pushes and pulls to the remote branch that it is tracking. Sometimes a developer will find that they need to amend the upstream branch they are tracking, and this can be done with the help of the `-u` option. Lets take the branch example of "john-testing-branch" once again, and lets set it to track the origin. Note the position of the flag this time around:

  ```
  git branch john-testing-branch -u origin
  ```

The `-vv` option can then be used to provide a list of your local branches, outlining what each branch is tracking and if your local branch is ahead, behind or both. 

  ```
  git branch -vv
  ```

See below that "john-testing-branch" and the "master" branches are now both tracking the remote origin, with "john-testing-branch" ahead of the origin by 6 commits. Both local branches can now push (send) and fetch (receive) commits to and from the origin repository- often located on Github.

  ```
* john-testing-branch                  97cc9a8 [origin/john-testing-branch: ahead 6] updated john-testing-branch
  master                               3bad51f [origin/master] Initial commit
  ```

## The real power of `git branch`

Understanding and mastering the `git branch` command will give any developer a dynamic and unique tool with which to bring about the `parallel evolution` of a project. 

John Gribbin
07/27/2017
Career Path 5: Fullstack Engineer