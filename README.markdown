What is Git ?
=============

Git is a *distributed* **version control** system [1]

[1] <a href="http://git-scm.com/about">http://git-scm.com/about</a>

Getting Git
-----------

Some house-cleaning here. We assume of course you have Git installed,
(hopefully \>= 1.7.0).

If you don't you can install it from downloads on the git homepage or you can
install [Github's git GUI](https://help.github.com/articles/set-up-git/).

Setup
-----

First thing to do is to setup your identity. This identifies you to
other people who download the project.

    $ git config --global user.name "Your Name"
    $ git config --global user.email your.email@example.com

Starting your journey
---------------------

First, clone this repository:

    $ git clone https://github.com/Yassine-Baccari/Git.git

You may want to fork (create your own copy of) the project on github and
clone from your own repo. You can find the fork button at the top right of
the screen on a github repository, or more help about doing that [here](https://help.github.com/articles/fork-a-repo/).

Once you have cloned your repository, you should now see a directory
called `git-workshop`. This is your `working directory`

    $ cd Git
    $ ls

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

For the curious, you should also see the `.git` subdirectory. This is
where all your repository’s data and history is kept.

    $ ls -a .git

You will see :

    branches  config  description  HEAD  hooks  info  objects  refs

The staging area
----------------

Now, let’s try adding some files into the project. Create a couple of
files.

Let’s create two files named `bob.txt` and `alice.txt`.

    $ touch alice.txt bob.txt

Let’s use a mail analogy.

In Git, you first add content to the `staging area` by using `git add`.
This is like putting the stuff you want to send into a cardboard box.
You finalize the process and record it into the git index by using
`git commit`. This is like sealing the box - it’s now ready to send.

Let’s add the files to the staging area

    $ git add alice.txt bob.txt

Committing
----------

You are now ready to commit. The `-m` flag allows you to enter a message
to go with the commit at the same time.

    $ git commit -m "I am adding two new files"

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Let’s see what just happened
----------------------------

We should now have a new commit. To see all the commits so far, use
`git log`

    $ git log

The log should show all commits listed from most recent first to least
recent. You would see various information like the name of the author,
the date it was commited, a commit SHA number, and the message for the
commit.

You should also see your most recent commit, where you added the two new
files in the previous section. However git log does not show the files
involved in each commit. To view more information about a commit, use
`git show`.

    $ git show

You should see something similar to:

    commit 5a1fad96c8584b2c194c229de7e112e4c84e5089
    Author: kuahyeow 
    Date:   Sun Jul 17 19:13:42 2011 +1200

        I am adding two new files

    diff --git a/alice.txt b/alice.txt
    new file mode 100644
    index 0000000..e69de29
    diff --git a/bob.txt b/bob.txt
    new file mode 100644
    index 0000000..e69de29

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

A necessary digression
----------------------

In this section, we are going to add more changes, and try to recover
from mistakes.

Be forewarned, this next step is going to be hard. We will need to add
some content to alice.txt.

Open `alice.txt` and type in your favourite line from a song, or:

e.g. Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit
voluptatem accusantium doloremque laudantium

Then **save** the file

What did we change? A very useful command is `git diff`. This is very
useful to see exactly what changes you have done.

    $ git diff

You should see something like the following:

    diff --git a/alice.txt b/alice.txt
    index e69de29..2aedcab 100644
    --- a/alice.txt
    +++ b/alice.txt
    @@ -0,0 +1 @@
    +Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Staging area again
------------------

Now let’s add our modified file, `alice.txt` to the staging area. Do you
remember how ?

Next, check the `status` of `alice.txt`. Is it in the staging area now?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Undoing
-------

Let’s say we did not like putting Lorem ipsum into `alice.txt`. One
advantage of a staging area is to enable us to back out before we
commit - which is a bit harder to back out of. Remembering the mail
analogy - it’s easier to take mail out of the cardboard box before you
seal it than after.

Here’s how to back out of the staging area :

    $ git reset HEAD alice.txt

    Unstaged changes after reset:
    M   alice.txt

Compare the `git status` now to the git status from the previous
section. How does it differ?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Your staging area should now be empty. What’s happened to the Lorem
Ipsum changes? It’s still there. We are now back to the state just
before we added this file to staging area. Going back to the mail
analogy, we just took our letter out of the box.

Undoing II
----------

Sometimes we did not like what we have done and we wish to go back to
the last *recorded* state. In this case, we wish to go back to the state
just before we added the Lorrem ipsum text to `alice.txt`.

To accomplish this, we use `git checkout`, like so:

    $ git checkout alice.txt

You have now un-done your changes. Your file is now empty.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Branching
---------

Most large code bases have at least two branches - a ‘live’ branch and a
‘development’ branch. The live branch is code which is OK to be deployed
on to a website, or downloaded by customers. The development branch
allows developers to work on features which might not be bug free. Only
once everyone is happy with the development branch would it be merged
with the live branch.

Creating a branch in Git is easy. The `git branch` command, when used by
itself, will list the branches you currently have

    $ git branch

The `*` should indicate the current branch you are on, which is
`master`.

If you wish to start another branch, use
`git checkout -b (new-branch-name)` :

    $ git checkout -b exp1

Try git branch again to check which branch you are currently on:

    $ git branch
      exp1
    * master

The new branch is now created. Now let’s work in that branch. To switch
to the new branch:

    $ git checkout exp1

`git checkout (branch-name)` is used to switch branches.

Let’s perform some commits now,

    $ echo 'some content' > test.txt
    $ git add test.txt
    $ git commit -m "Added experimental txt"

Now, let’s compare them to the master branch. Use `git diff`

    $ git diff master

Basically what the above output says is that `test.txt` is present on
the `exp1` branch, but is absent on the `master` branch.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Now you see me, now you don’t
-----------------------------

Git is good enough to handle your files when you switch between
branches. Switch back to the `master` branch

Try switching back to the master branch (Hint: It’s the same command we
used to switch to the exp1 branch above)

Now, where’s our `test.txt` file ?

    $ ls
    README.textile  alice.txt   bob.txt     gamow.txt

As you can see the new file you created in the other branch has
disappeared. Not to worry, it is safely tucked away, and will re-appear
when you switch back to that branch.

Now, switch back to the exp1 branch, and check that the `test.txt` is
now present.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Merging
-------

We now try out merging. Eventually you will want to merge two branches
together after the conclusion of work.\
`git merge` allows you to do that.

Git merging works by first switching the branch you want to *into*, and
then running the command to merge the other branch in.

We now want to merge our `exp1` branch into `master`. First, switch to
the `master` branch.

    git checkout master

Next, we merge the `exp1` branch into `master` :

    $ git merge exp1

Do you see the following output ?

    Merge made by recursive.
     test.txt |    1 +
     1 files changed, 1 insertions(+), 0 deletions(-)
     create mode 100644 test.txt

You have to be in the branch you want merge *into* and then you always
specify the branch you want to merge.

At this point, you can also try out `gitk` to visualize the changes and
how the two branches have merged

Merge Conflicts
---------------

Git is pretty good at merging automagically, even when the same file is
edited. There are however, some situations where the same line of code
is edited there is no way a computer can figure out how to merge.\
This will trigger a conflict which you will have to fix.

We now practise fixing merge conflicts. Recall that conflicts are caused
by merges which affect the same block of code.

Here’s a branch I prepared earlier. The branch is called `alpher`. Run
the code below to set it up (don’t worry if you can’t understand it)

    $ git checkout alpher

You should now have a new branch called `alpher`. Try merging that
branch into `master` now and fix the ensuing conflict.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Fixing a conflict
-----------------

You should see a `conflict` with the `gamow.txt` file. This means that
the same line of text was edited and committed on both the master branch
and the alpher branch. The output below basically tells you the current
situation :

    Auto-merging gamow.txt
    CONFLICT (content): Merge conflict in gamow.txt
    Automatic merge failed; fix conflicts and then commit the result.

If you open the `gamow.txt` file, you will see something similar as
below:

    $ cat gamow.txt
    <<<<<<< HEAD
    It was eventually recognized that most of the heavy elements observed in the present universe are the result of stellar nucleosynthesis (http://en.wikipedia.org/wiki/Stellar_nucleosynthesis) in stars, a theory largely developed by Bethe.
    =======

    http://en.wikipedia.org/wiki/Stellar_nucleosynthesis
    Stellar nucleosynthesis is the collective term for the nuclear reactions taking place in stars to build the nuclei of the elements heavier than hydrogen. Some small quantity of these reactions also occur on the stellar surface under various circumstances. For the creation of elements during the explosion of a star, the term supernova nucleosynthesis is used.
    >>>>>>> alpher

Git uses pretty much standard conflict resolution markers. The top part
of the block, which is everything between `<<<<<< HEAD` and `======` is
what was in your current branch.\
The bottom half is the version that is present from the `alpher` branch.
To resolve the conflict, you either choose one side or merge them as you
see fit.

For example, I might decide to choose the version from the `alpher`
branch.

Now, try to **fix the merge conflict**. Pick the text that you think is
better (Ask for help if stumped)

Once I have done that, I can then mark the conflict as fixed by using
`git add` and `git commit`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

    $ git add gamow.txt
    $ git commit -m "Fixed conflict"

Congratulations. You have fixed the conflict. All is good in the world.

Fin