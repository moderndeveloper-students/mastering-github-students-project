# ```git push```

## Pushing to Remote

This git command is at the heart of how distributed software version control like git works. By allowing you to make all your changes on your local machine, and then using ```git push``` to commit and merge those changes over to remote copy of it.

## When to use ```git push```

Use when you have changes made on your local project that you are happy with and you are ready to share those changes.

When you clone a git repository, you will have a git master branch and an origin server created automatically. Then you start working on your local copy and all your modified files are tracked(unless you have specifically ignored those via .gitignore). And from time to time, you add your modifications by ```git add .``` and commit your modifications with ```git commit``` which commits those changes to staging area.

Next you would usually do ```git status``` to check if everything is in order because status will show which files have been modified and weather they are tracked or not and ready for pushing. If satisfied you will simply run ```git push``` and your local version of the modified files will now match with the origin copy.

## What and where ```git push``` pushes changes

In short, this command updates the remote branch with local branch.

You can specify where by providing the *repository* as an argument the the command like ```git push master```

If you do not provide this argument to the command, then your configuration
file for the current branch is looked up for reference and to determine where to push the changes, and if this is missing as well then its pushed to the *origin* server.

As for what to push, you can provide a *tag* as an argument, or use -all which will push all branches, or --mirror which means all *refs/* including */heads/* and */tags/* will be mirrored to the remote repository.

Below, you will find most useful and commonly used command arguments with ```git push``` command.

| Option        | Description |
| ------------- |------------- |
| ---all         | Push all branches (i.e. refs under refs/heads/); cannot be used with other <refspec>. |
| --prune       | Remove remote branches that don’t have a local counterpart. For example a remote branch tmp will be removed if a local branch with the same name doesn’t exist any more. This also respects refspecs, e.g. git push --prune remote refs/heads/*:refs/tmp/* would make sure that remote refs/tmp/foo will be removed if refs/heads/foo doesn’t exist. |
| ---mirror      | Instead of naming each ref to push, specifies that all refs under refs/ (which includes but is not limited to refs/heads/, refs/remotes/, and refs/tags/) be mirrored to the remote repository. Newly created local refs will be pushed to the remote end, locally updated refs will be force updated on the remote end, and deleted refs will be removed from the remote end. This is the default if the configuration option remote.<remote>.mirror is set. |
| ---dry-run      | Do everything except actually send the updates. |
| ---delete        | All listed refs are deleted from the remote repository. This is the same as prefixing all refs with a colon. |
| ---tags         | All refs under refs/tags are pushed, in addition to refspecs explicitly listed on the command line. |
| ---repo=*repository*          | This option is equivalent to the <repository> argument. If both are specified, the command-line argument takes precedence. |
