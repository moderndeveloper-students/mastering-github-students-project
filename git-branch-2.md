#Git branch command contribution

Git branching allows developers to open multiple local lines of development on their machine. With branches, you can work during a period of time outside the main stream of your project files system. The [`git branch`][1] command is one of the instructions available to the developers for this purpose. Branching is commonly used to handle in silos both several quick fixes and mid-term lines of development. It can also be part of a long-term development strategy with a system of integrated branches.

#Branching basics

`git branch` and its options can create, delete, list and rename branches. 

The main local branch is the stable branch of your projet. It is commonly called the **master branch**. Working with extra branches allows you to develop in silos a number of different lines of development. Their changes won't interfere with your master branch until you decide to merge one of your side work into the main project line. Compared to centralized VCS, Git is supposed to propose a very fast branching process so that it can be done often.

When you clone and track an hosted project using git on our machine, you are making a copy of the remote master branch. However, it is very common that you will have to track and develop on your machine other branches of the remote project.

Conflicts between branches will occur when you are working on the same content or directories from various different branches, so watch out your self or communicate well with your organization.


##Quick start


- List your repository branches and highlight the branch you are working on (*):

		Git branch

- Create a branch in your repository:

		Git branch <branch_name>
		
Tip: to create a branch and start working in it with a unique instruction, use:

		Git checkout -b <branch_name>

- Delete a clean branch (commit is done):

		Git branch -d <branch_name>
		
- Delete a dirty branch (some changes still waiting for a commit):

		Git branch -D <branch_name>

- Rename a branch:

		git branch -m <old_name> <new_name>


##Repository Branches listing options

Let's see how to list with accuracy all your active branches on your local repository.

- When it comes to list your branches, `git branch` accepts pattern matching to find some accurate filenames:

		Git --list 'branch_*'
		Git --list 'branch_[123]'

- List of branches and their last commits:

		Git branch -v
		
- List already merged branches or not merged yet into the current branch:

		Git branch --merged
		Git branch --no-merged
		
- List branches referring to a specific object (commit, directory tree, content blob):

		Git branch --points-at <object>

##Remote branching options

A cloned team project will contain most of the time other branches than the master branch. The `git branch` command can list and even create upstream branches (remote tracking branches) from your machine.

- List all remote tracking branches:

		Git branch -r 

- List all local and tracking branches together:

		Git branch -a

- Add to the remote upstream repository an existing local branch that will track the new remote branch:

		Git branch -u <remote_name>/<branch_name>

- Delete a tracking branch:

		Git branch -rd <branch_name>
		
- List of local branches with more information, including the number of local commits not pushed up yet to the tracking branches:

		Git branch -vv


##Branching use and strategy

With branching, you can avoid a side development line to be shipped to a remote server while pushing up urgent bug fixes. You can also quickly creating several branches to work on some various type of changes. Each separate line of development can be respectively pushed when there are ready for production. 

Branching is sometimes a development strategy for developers teams. Multiple integrated branches stay opened with a specific bleeding-edge flag until a particular stage is considered stable enough to be merged into the master branch.


##Branches internals

Git is tracking the development of each branch by a reference (called "heads") to every last commits made into these branches. A commit is an object that contains information about your project at a specific state (committer name and email address, directories, file content). A branch is a simple file containing digits pointing to a specific commit made into your project.

Your current working branch reference is stored in the `.git/HEAD` file. The HEAD file is a simple text reference to the branch you are working on. To verify where the HEAD file is pointing to, you can use the folowing instruction: 

			`Git log --oneline --decorate` # The --decorate option is showing the HEAD information
			

[1]: https://git-scm.com/docs/git-branch
