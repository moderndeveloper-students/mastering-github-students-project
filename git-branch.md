
#### Understanding branch command

# When using Git, a `branch` can be thought of as simply a movable pointer.

what does this mean? 

To really understand the way Git does branching, we need to take a step back and examine how Git stores its data- as a series of snapshots

That’s all what branches are: they are movable pointers. What happens if you create a new branch? Well, doing so creates a new pointer for you to move around. Let’s say you create a new branch called testing. You do this with the git branch command Let’s create a branch called feature.

A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is master. As you start making commits, you’re given a master branch that points to the last commit you made. Every time you commit, it moves forward automatically.

How does Git know what branch you’re currently on? It keeps a special pointer called HEAD. The HEAD is a special pointer that simply points to the currently checked out branch or commit. it’s a simple file inside the .git folder called HEAD which in our case currently contains the string master.

The branch that HEAD points to moves forward with each commit.

At this point our history has diverged. And this is the whole point of branches. They enable us to have parallel evolution of a code base.

It moved the HEAD pointer back to point to the master branch, and it reverted the files in your working directory back to the snapshot that master points to. This also means the changes you make from this point forward will diverge from an older version of the project. It essentially rewinds the work you’ve done in your testing branch temporarily so you can go in a different direction.

You created and switched to a branch, did some work on it, and then switched back to your main branch and did other work. Both of those changes are isolated in separate branches: you can switch back and forth between the branches and merge them together when you’re ready. And you did all that with simple branch and checkout commands.

Because a branch in Git is in actuality a simple file that contains the 40 character SHA-1 checksum of the commit it points to, branches are cheap to create and destroy.

Some people refer to Git’s branching model as its “killer feature,” and it certainly sets Git apart in the VCS community. Why is it so special? The way Git branches is incredibly lightweight, making branching operations nearly instantaneous, and switching back and forth between branches generally just as fast. 

Understanding and mastering this feature gives you a powerful and unique tool and can entirely change the way that you develop.

git branch

git checkout

