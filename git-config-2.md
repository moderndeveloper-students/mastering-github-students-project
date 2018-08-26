# ```git config```

## *Overview:*
1. Git is a distributed version control system which has various config files to have the control over your git working. 
1.  These config files are present at various levels in your machine like
    i. Entire machine (Entire Operating system for all users), specified by     ```--system```
    ii.  Specific to logged in user, specified by ```--global```
   iii. Specific to a repository, specified by ```--local```. This is default if one doesn't specify any file option
1. A git config file has sections with key value pair and looks like below 
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
4. We could manually edit the config file as per our needs following a specific format, but that could be tedious. To help us out ```git config``` is a command which helps us alter and do changes in the config file as per needed. We will learn more about this command so that we can master and understand everything about git configurations and how to use git config command to play around with it.

### Synopsis / Syntax / How to use the command
```
git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] name [value [value_regex]]
git config [<file-option>] [--type=<type>] --add name value
git config [<file-option>] [--type=<type>] --replace-all name value [value_regex]
git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] --get name [value_regex]
git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] --get-all name [value_regex]
git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] [--name-only] --get-regexp name_regex [value_regex]
git config [<file-option>] [--type=<type>] [-z|--null] --get-urlmatch name URL
git config [<file-option>] --unset name [value_regex]
git config [<file-option>] --unset-all name [value_regex]
git config [<file-option>] --rename-section old_name new_name
git config [<file-option>] --remove-section name
git config [<file-option>] [--show-origin] [-z|--null] [--name-only] -l | --list
git config [<file-option>] --get-color name [default]
git config [<file-option>] --get-colorbool name [stdout-is-tty]
git config [<file-option>] -e | --edit
```

To understand the syntax you can refer to a [article](https://support.ca.com/cadocs/0/CA%20ARCserve%20%20Backup%2015-ENU/Bookshelf_Files/HTML/CMD_Ref/index.htm?toc.htm?command_line_syntax_characters.htm) which explains about it. After you have understood how to follow the syntax you can use the above combinations as per need to achieve any task related to add or change configurations for a git repository or git installation

To undertand the meaning of all options and flags you can refer to [git-scm article](https://git-scm.com/docs/git-config)

## *Few Examples*
### Setting configuration values

As an basic example, let configure your name and e-mail into a git installation.

```bash
git config --global user.email  "your@mail.com"
git config --global user.name  "Your Name"
```
The above command will target the git config file for the logged in user and target the user section and will add/change values for key 'email' and 'name'

### Get/Retrieve configuration values
To retrieve any configuration value you will need to specify the section with added dot ```.``` and the key value you like to retrieve

```bash
#Let's say you want to know your configured user.name
git config user.name 

#OUTPUT:
# Your Name
```
In the above example , user is the section and name is the key.


### Removing configuration values
Like adding/setting a value for a key, if you want to unset/delete the value for a key , you will have to ```--unset``` directive


```bash
git config --unset user.email
```
### Listing all key value pairs for all sections
You can use ```--list``` to list all the key value pairs available in your config file for all sections
```bash
git config --global --list
#OUTPUT
#user.name=username
#user.email=abc@gmail.com
```

### Configuration levels

As mentioned in overview, git config is used to play around with config files at different level. You can find the files on your machines at below locations(Unix based OS)

* ```/etc/gitconfig``` : Configuration relative to the whole OS (All OS users).
* ```~/.gitconfig``` : Configuration relative to your OS user (Unix based OS)
* ```your_project_directory/.git/config``` : Configuration relative to a specific git repository.

When using ```git config``` command you can specify the ```[file option]``` which is optional and by default ```--local```. Below are the ways you can instruct the config command to target the level as per you choice
```
git config --system
git config --global
git config --local
```

### Editor
You can configure git to use editor of your choice by below command.

```bash
git config --global core.editor vim
```

### Aliases

Aliases are of great use to make you more efficient working with git. It helps you create a custom reference of your choice to a command (simple or complex) of your choice, which can help reduce typing.

#### Simple command alias example

If you want to shorten your ```git status``` command to ```git st```. You can set and alias for it and the use it for further executions

```bash
# git config alias.<alias_name> <command being shortened>
git config --global alias.st status

# Using the alias
git st
```


#### Complex command aliases
Lets look at an complex alias example

 ```git config alias.ignore '!f() { echo \"$1\" >> .gitignore; }; f'```
 
 In above example you can see we are adding ignore key to alias section for a function which accepts a parameter to add it to the .gitignore file. We can now use it as follows
 ```git ignore node_modules\```
 
 The above will append node_modules\ to .gitignore file or create a new .gitignore and append the parameter passed.

# Summary

We just covered the basics of ```git config``` command and how we can use it for our needs. However there is lot more to it which has many sections and properties wich you can modify or add. You can refer to [Official Manual Page](https://git-scm.com/docs/git-config) for further information.

