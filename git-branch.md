
#### Understanding the `Git branch` command

# When using Git, a `branch` can be thought of as simply a movable pointer.

The pointer itself is referred to as the `HEAD.` Whenever you make a change (commit) using within a repository you are provided with a "`master`" branch automatically by Git which points to the last commit you made. Every time you perform a commit, this master branch moves forward. 

When a new branch is created (and given a suitable title) the user can then move the pointer, i.e. the HEAD, to the newly created branch, and this will provide the user with a new direction in which to take their workflow. This new branch will now move forward automatically with each commit.

The user can at any time switch back to the master branch to make changes, and will then move forward with each new commit from an older version of the repository, as both sets of commits will be isolated in separate branches. 

## How to use the Git Branch command

One reason that a developer may wish to create a new branch would be to test a new feature that may or may not be included in the final project. A good name for this branch could be "testing-branch." This branch can be created using the `git branch` command as follows: 

  ```
  git branch testing-branch
  ```

Simply typing `git branch` into the terminal will now show the presence of two branches within Git: "master", and "testing-branch." An asterisk will appear next to the branch to outline where the HEAD is currently pointing.

  ```
  git branch
  ```

which should give a result that looks like this:

  ```
  * master
    testing-branch
  ```

Adding the flag `-a` to the command will also show all branches that exist, but this time include those that do not exist in your local workspace. This may be useful if the origin repository contains multiple branches that you wish to be aware of. 

  ```
  git branch -a
  ```

If for any reason you need to change the name of a branch, lets say from "testing-branch" to "john-testing-branch" (to make your identity clear to fellow contributors), this can be done by using the `-m` option as follows:

  ```
  git branch -m testing-branch john-testing-branch
  ```

When it is decided that commits from one branch (lets take "john-testing-branch" as the example) should be merged with those present on the master branch, it is often good practice to delete the branch from which the commits were "pulled" afterwards. This will help to maintain a workspace free from un-necessary clutter. Deleting a branch is done using the `-d` option with the git branch command:

  ```
  git branch -d john-testing-branch
  ```

## A note on Git Branch tracking

Sometimes a developer will find that they need to amend the upstream branch they are tracking for a local branch they are working on, and this can be done with the help of the `-u` option. Lets take the branch example of "john-testing-branch" once again, and lets set it to track the origin:

  ```
  git branch -u origin/john-testing-branch
  ```

The `-vv` option can then be used to provide a list out your local branches, outlining what each branch is tracking and if your local branch is ahead, behind or both. 

  ```
  git branch -vv
  ```

See below that "john-testing-branch" and the "master" branches are now both tracking the origin. This means that both branches can now push and pull commits to and from the origin repository (usually found on Github).

  ```
* john-testing-branch                  97cc9a8 [master/john-testing-branch] 
  master                               3bad51f [origin/master] Initial commit
  ```

## The real power of `git branch`
Understanding and mastering the `git branch` command will give any developer a dynamic and unique tool with which to bring about the `parallel evolution` of a project. 

John Gribbin
07/27/2017
Career Path 5: Fullstack Engineer
