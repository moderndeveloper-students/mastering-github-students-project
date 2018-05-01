# Git Good, with Git Grep

When you're working with collaborators on a big project, one of the most nerve-wracking things about submitting your work is the fear of mistakes showing up in your code. Whether they are big mistakes that will break the project, or simple cosmetics like spelling errors, no one wants to look bad or unprofessional. Luckily for us, even if we have thousands of lines of code to review, Git provides us with a powerful option to solve these types of problems. This is where `git grep` comes in to save the day. This command allows you to print lines matching a specific pattern, in the files you have tracked in your repository. For the full technical definition let's look at `git grep --help`:

> Look for specified patterns in the tracked files in the work tree, blobs registered in the index file, or blobs in given tree objects. Patterns are lists of one or more search expressions separated by newline characters. An empty string as search expression matches all lines.

This command goes deep with options that you can customize for patterns you're trying to find, so lets start with basic usage.

### Basic Usage

When we talk about the basics we mean things like, searching for a simple string in your files. First, make sure you've run `git add` recently so we have some files to search through. You can check by running `git status` to see if you already have some files staged. Then try running for this command `git grep foo`. In this case, `foo` is the search term but you can change the term for something more likely to bring back results. If I search for `git` in my commits here's what I get:
```
$ git grep git

git-add.md:`git status`
git-add.md:`git add <filename>`
git-add.md:`git add *.txt`
git-add.md:`git add .`
git-add.md:`git add [-A-|-all]`
git-add.md:`git add -f <filename>`
git-branch.md:  cat .git/HEAD
git-branch.md:  git branch testing-branch
git-branch.md:  git branch
git-branch.md:  git branch -a
```

This search will reveal all the instances in the files you're tracking with Git. In many cases, a simple string search like this will yield many results and it can be cumbersome to read through the results. I've found that `--break` makes this much easier.

Using `git grep --break foo` when the results come back, you'll see an empty line between the results for each file. This is great for being able to visually parse the results. Here's what it looks like using the example from above:
```
$ git grep --break git

git-add.md:`git status`
git-add.md:`git add <filename>`
git-add.md:`git add *.txt`
git-add.md:`git add .`
git-add.md:`git add [-A-|-all]`
git-add.md:`git add -f <filename>`

git-branch.md:  cat .git/HEAD
git-branch.md:  git branch testing-branch
git-branch.md:  git branch
git-branch.md:  git branch -a
```
As you can see, adding `--break` makes it easier to delineate between the results from different files.

### Advanced Usage

One of the things that gets me excited about `git grep` is being able to use Regular Expressions or Regex to search through our code. For those of you not familiar with Regex, it's a powerful way to search and find patterns. While a full tutorial on Regex is out of the scope of this documentation, we should take a look at a couple of examples. Say for instance, that we'd like an easy way to find some common mistakes that show up in JavaScript using `git grep` and remove them from our code.

Let's look at a the common error of forgetting spaces around operators.

Good:
```
var x = y + z;
var values = ["Volvo", "Saab", "Fiat"];
```
Bad:
```
var x= y + z;
var values =["Volvo", "Saab", "Fiat"];
```
Notice that `x` and `=` aren't separated by any space in the example `x=`. Here's how we find these types of errors with `git grep` and Regex:
```
$ git grep -e var.[a-zA-Z0-9]*=

git-grep.js:var x=y + z;
git-grep.js:var x= y + z;
git-grep.js:var dog=y + z;
git-grep.js:var x= y + z;
git-grep2.md:var x=y + z;
git-grep2.md:var x= y + z;
git-grep2.md:var dog=y + z;
git-grep2.md:var x= y + z;
```

Let's break down the pattern and flags in this example. We're using `-e` which simply tells the command line, whatever follows is a pattern to search for `var.[a-zA-Z0-9]*=`. We're looking for `var` in our code followed by `.` which means any character, then you see `[a-zA-Z0-9]*`. This means that we are looking for any combination of lowercase letters, uppercase letters, or numbers; and the `*=` says at any length followed immediately by `=`. As you can see in the results, we found several places in our directory where this common mistake was committed. But there's one thing missing from our search. You'll notice some of the files in the results are `.md` which puts us at risk of finding a bunch of false positives for our search because this pattern is only a mistake in JavaScript. We should modify our pattern to only search through JavaScript files. We'll use `--` which signals that options are finished and the rest of the instructions are `<pathspec>`. When we add `-- *.js` our `git grep` knows to only search for this pattern in our `.js` files.
```
$ git grep -e var.[a-zA-Z0-9]*= -- *.js

git-grep.js:var x=y + z;
git-grep.js:var x= y + z;
git-grep.js:var dog=y + z;
git-grep.js:var x= y + z;
```
Voila! Now our results tell us exactly what files contain errors for us to correct before we submit our code to the repository! As you can see, if you utilize `git grep` to its full potential, the possibilities are endless.
