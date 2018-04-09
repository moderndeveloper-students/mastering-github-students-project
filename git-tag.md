# Introduction to Git Tag

What is a tag in Git? Tagging is a way to create identifiers for commits in Git. 

## Tags vs Branches

Tagging must not be confused with branching. Branches in Git are snapshots, think of a picture of 
the current state of your code.

 A branch is generally associated with a base branch, most of the times named `master`. Branches 
can change, in other words, when a commit happens, the `master` branch will be updated to point to 
the newest commit, tags, on the other hand, are created to point to a specific commit, and do not 
change. 

## Why to `tag`
In software development, there is the concept of "versioning", so we say "I am running version 
v8.0.0, but the latest version is v10.3.0" of a given software application.

Git is a VCS (Version Control System) application, and there is guidelines for it, see [Semantic 
Versioning](https://semver.org/). 

Git tags help developers keep track of versions and releases. 

Tagging is used to track changes in code in a very granular way, helping you go to a specific 
commit in your branch history, that is way is so important to use an easily readable tracking 
system for humans to refer to.

## Tags usage with examples
The `git tag` command and its different optional flags help developers with tag management, you can 
create, deleted, list, or verify tags. Like most flags used with the different Git command, some of 
them can be used together, others are mutually exclusive, and some are implied.

Git has two types of tags - annotated and lightweight.

Annotated tags includes information about the author and a time stamp to the tag, this is important 
in case you need to communicate with the the tag's creator.

Lightweight tags should be used locally only, as they don't provide any additional information and 
it may be difficult to find the originator if needed. 

### Examples:

#### Tagging
The most basic form of the command without flags. The command returns a list of tags (if any), 
otherwise it will output an empty list.

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag

```
Now, will create and add/commit a file that we will use for our example:

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ touch attendees.md

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ echo -e "Name: John Doe\nName: Jane Doe" >> attendees.md

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ cat attendees.md
Name: John Doe
Name: Jane Doe

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git add attendees.md
warning: LF will be replaced by CRLF in attendees.md.
The file will have its original line endings in your working directory.

rafael@Lat_E5550 MINGW64 ~/my_repo_test/my_repo_test (tags_branch)
$ git commit attendees.md
warning: LF will be replaced by CRLF in attendees.md.
The file will have its original line endings in your working directory.
[tags_branch 1ac667f] Initial Version of attendees list.
 1 file changed, 2 insertions(+)
 create mode 100644 attendees.md

```
#### Create tags for commits. 
We will call our first our first commit v0 (includes adding the file with its initial content).

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag v0
```
And modify the attendees.md for a second commit.

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ echo "Name: Donald Duck" >> attendees.md

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ cat attendees.md
Name: John Doe
Name: Jane Doe
Name: Donald Duck

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git add attendees.md
warning: LF will be replaced by CRLF in attendees.md.
The file will have its original line endings in your working directory.

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git commit attendees.md
warning: LF will be replaced by CRLF in attendees.md.
The file will have its original line endings in your working directory.
[tags_branch 8804ae5] Added Donald to the list.
 1 file changed, 1 insertion(+)
```

Let's create our second tag, which we call v1.

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag v1
```

#### Listing and showing tag contents

Issuing `git tag` without flags will show the list of existing tags.

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag
v0
v1
```

Now, we can reference specific commits identified by our version names. We can see what the 
difference between one commit and the other is.

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git show v0
commit 1ac667f577ed8ba8ceddf634f41fac2fc73ddc2f (tag: v0)
Author: Rafael Huijon <rhuijonp@gmail.com>
Date:   Sat Apr 7 11:38:49 2018 -0700

    Initial Version of attendees list.

diff --git a/attendees.md b/attendees.md
new file mode 100644
index 0000000..569ee96
--- /dev/null
+++ b/attendees.md
@@ -0,0 +1,2 @@
+Name: John Doe
+Name: Jane Doe

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git show v1
commit 8804ae5bea394ea38e90005fc2c005c51f666dba (HEAD -> tags_branch, tag: v1)
Author: Rafael Huijon <rhuijonp@gmail.com>
Date:   Sat Apr 7 11:54:25 2018 -0700

    Added Donald to the list.

diff --git a/attendees.md b/attendees.md
index 569ee96..ba74ad9 100644
--- a/attendees.md
+++ b/attendees.md
@@ -1,2 +1,3 @@
 Name: John Doe
 Name: Jane Doe
+Name: Donald Duck
```

#### Tagging old commits

You can tag old commits by referencing the commit's id, which you can see using `git log`. 
Here our commit starting with 8dbc6105b3 is tagged as v2 and then it shows in our list of tags

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)

# The log list has been cut for spacing purposes to show only the log entry we are working with

$ git log
commit 8dbc6105b3ec0cab9ddfc337e1f2e43a26914e2f
Author: rhuijonp <35969612+rhuijonp@users.noreply.github.com>
Date:   Mon Apr 2 10:59:20 2018 -0700

    Fixing spelling mistakes

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag v2 8dbc6105b3

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag
v0
v1
v2

```

#### Pushing tags to remote
Pushing tags to remote a repository requires the use  of the --tags flag, like so:
 
```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git push origin --tags
Counting objects: 21, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (21/21), 14.38 KiB | 1.03 MiB/s, done.
Total 21 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:rhuijonp/my_repo_test.git
 * [new tag]         v0 -> v0
 * [new tag]         v1 -> v1
 * [new tag]         v2 -> v2

```

#### Deleteing tags locally
To delete a tag, you need to use the -d flag along with the `git tag` command. 
**Note that locally deleted tags must be manually deleted remotely**

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag -d 'v2'
Deleted tag 'v2' (was 8dbc610)

rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git tag
v0
v1

```

#### Deleting tags remotely
And removing tags from a remote location gets done in similar a locally, but the path to the file 
that keeps track of the tags is used. 
We can see the command output showing a list of the removed tag(s).

```
rafael@Lat_E5550 MINGW64 ~/my_repo_test (tags_branch)
$ git push origin :refs/tags/v2
To github.com:rhuijonp/my_repo_test.git
 - [deleted]         v2
```

### Summary
Git, been a VCS, helps developers manage code project collaboration by way of keeping detailed 
track of changes to code. But GIT makes developers life easier by providing humans a way to easily 
what changes come first. 

Git keeps commit logs so that they can easily find a commit, but tagging makes it possible for 
humans to tell which comes first just by glancing to a tag name. 

Git `git tag` command is a powerful tool for developers, see the [official 
documentation](https://git-scm.com/docs/git-tag) here.You may also find [this 
article](http://nvie.com/posts/a-successful-git-branching-model/) useful, as it graphically shows 
the difference between branching and tagging.   
  
 









 

  



   
