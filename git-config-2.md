# ```git config```

## **Overview:**
>Git repositories are repositories for version control system. For any user wishing to make a new repository or to use a existing repository, they can either clone the repository or initialize a new repository. For any repository it would need some information about it *(meta data)* , which is stored and referred as configurations. 

>Configurations of a Git repository are stored in a file called as **config** inside **.git** folder. which can be found as a hidden folder when a repository is cloned or initialized using git.

>Configuration of git which is **config** file holds various information about the repository like remote locations for push and pull , etc.

>We could manually edit the config file as per our needs following a specific format, but that could be tedious. To help us out ```git config``` is a command which helps us alter and do changes in the config file as per needed. We will learn more about this command so that we can master and understand everything about git configurations and how to use git config command to play around with it.


## Basics
We will learn its usage starting with basics first. Let us first initialize a repository and check the contents of the config file. Below is and example of what a git configuration file looks like.
```
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[remote "origin"]
        url = http://apps-abc:5427/git/sample_repo.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master

```



### Setting configuration values

As an basic example, let configure your name and e-mail into a git installation.

```bash

git config --global user.email  "your@mail.com"
git config --global user.name  "Your Name"
```
