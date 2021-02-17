# git mergetool

Merge Conflicts are sometimes unavoidable. No matter how careful the collaborative developers are they will encounter merge conflict a few times.

There are several ways to solve merge conflicts and `mergetool` is one of them.

`mergetool` provides a GUI where you can look at versions from your current branch, remote branch, common ancestor and final merged version, all in one window, which we will see going further into the article.

There a so many different GUI tools available. They are made available in different ways:
- Bash commands (New external commands can be installed)
- Comes with IDEs (Xcode comes with FileMerge/opendiff)
- Comes with the OS

In the below example I use a tool called FileMerge/opendiff that comes installed with MacOS (It is part of Xcode IDE).

Here is a list of mergetool:
- Command line mergetool editors
  - Emacs based diff tools: `emerge` or `Ediff`
  - Vim based diff tool: `vimdiff`
- GUI mergetool editors
  - `gvimdiff` - Similar to vimdiff but uses the Linux GUI for Vim
  - `kdiff3`
  - `meld`
  - `tortoisemerge`
  - `P4merge`
  - `Diffuse `
- IDE based
  - IntelliJ IDEA's default merger tool
  - Xcode's tool (FileMerge aka `opendiff`)

##### Practical Example

1) Create a project locally

        $ mkdir my_favorites
        $ cd my_favorites
        $ git init
        $ touch fav-animals.txt

2) Update the project files so contents of fav_animals.txt would look like this

        # Make some changes fav-animals.txt

        $ cat fav-animals.txt
        elephant
        lion
        zebra
        koala

3) Add and Commit the file (`branch: master`)

        $ git add fav-animals.txt
        $ git commit -m 'Added content'

4) Create a new branch, switch to it and make changes to the file.

        $ git branch fav-animals
        $ git checkout fav-animals

        # Make some changes fav-animals.txt

        $ cat fav-animals.txt
        elephant
        lion
        zebra
        koala
        gorilla
        kangaroo
        cheetah
        bear

5) Add and Commit the file (`branch: fav-animals`)

        $ git add fav-animals.txt
        $ git commit -m "Added four new animals"

6) Switch back to `master` and make changes to file again.

        $ git checkout master

        # Make some changes fav-animals.txt

        $ cat fav-animals.txt
        elephant
        lion
        zebra
        koala
        dog
        horse
        panda
        sloth

7) Add and Commit the file (`branch: master`)

        $ git add fav-animals.txt
        $ git commit -m "Added four more animals"

8) Let's try to merge the two branches.

  **This is the current state of the two branches**

  | master                                          | fav-animals                                             |
  |-------------------------------------------------|---------------------------------------------------------|
  | elephant <br> lion <br> zebra <br> koala <br> dog <br> horse <br> panda <br> sloth | elephant <br> lion <br> zebra <br> koala <br> gorilla <br> kangaroo <br> cheetah <br> bear |

      $ git merge fav-animals

     Auto-merging fav-animals.txt
     🚫 CONFLICT (content): Merge conflict in fav-animals.txt
     🚫 Automatic merge failed; fix conflicts and then commit the result.

9) We can use `mergetool` to fix this.

    $ git mergetool

    This message is displayed because 'merge.tool' is not configured.
    See 'git mergetool --tool-help' or 'git help config' for more details.
    'git mergetool' will now attempt to use one of the following tools:
    opendiff tortoisemerge emerge vimdiff
    Merging:
    fav-animals.txt

    Normal merge conflict for 'fav-animals.txt':
      {local}: modified file
      {remote}: modified file
    Hit return to start merge resolution tool (opendiff):

What is happening above is this: It is suggesting us with a default mergetool as I have not configured a tool to use. I will go ahead and use the default mergetool suggested by the system. In my case it is opendiff (Comes preinstalled with Xcode for MacOS users).

This tool will create 4 temprary files:
- `fav-animals_LOCAL_6780.txt`: Content from the current branch (master)
- `fav-animals_REMOTE_6780.txt`: Content from the fav-animals branch
- `fav-animals_BASE_6780.txt`: the common ancestor(s) of LOCAL and BASE.
- `fav-animals_BACKUP_6780.txt`

![Imgur](https://i.imgur.com/MjcejoY.png)

Depending on how you merge the results can vary:

  | left (`master`) | right (`fav-animals`) | both (left first) | choose neither |
  |-------------------------------------------------|---------------------------------------------------------|
  | elephant <br> lion <br> zebra <br> koala <br> dog <br> horse <br> panda <br> sloth | elephant <br> lion <br> zebra <br> koala <br> gorilla <br> kangaroo <br> cheetah <br> bear | elephant <br> lion <br> zebra <br> koala <br> dog <br> horse <br> panda <br> sloth <br> elephant <br> lion <br> zebra <br> koala <br> gorilla <br> kangaroo <br> cheetah <br> bear | # blank |

  In the above example I used a GUI based tool but you can do all of this in the command line as well. I personally think having a visual representation of the changes make things easier.
