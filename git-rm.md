## Introduction to the `Git RM` command

The 'git rm' command is useful for removing files from you repository. 
Remember to use with caution!

 - If you are creating many files for your project there will often be 
times when you need to make changes.

- You might be creating a directory such as `mkdir myfolder`

- Or adding a new MarkDown file `echo "Hello World" >> newfile.md` for a 
project.

- You might even creating your own version of an open source project on 
Git Hub to fit your needs.

There will be times when you need to remove files and folders from your 
repository and then git command to do this is `git rm`.
 
## How to use the `git rm` command

![How 
To](https://smhttp-ssl-31623-shero.nexcesscdn.net/wp-content/uploads/2016/01/github-banner.png)

### Removing files
If you want to remove one file simply navigate to your folder
`cd folder name`
and enter the following command
`rm filename.rm`
This will remove the file from your repository. Remember if your working 
on your local machine you will still need to commit these changes to the 
origin repo. You can learn more about `git commit` on [git commit 
introduction](/git-commit.md).

If you want to remove multiple files then simple append the names at the 
end like this:

`git rm fileOne.md fileTwo.md fileThree.md`


Daniel Morgan
12/09/2018
