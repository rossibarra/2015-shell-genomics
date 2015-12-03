=========
The Shell
=========

Updated Dec 2015 by Titus Brown.

Original author: Tracy Teal for Data Carpentry (http://datacarpentry.org).

Original contributors:
Paul Wilson, Milad Fatenejad, Sasha Wood and Radhika Khetani for
Software Carpentry (http://software-carpentry.org/)

Objectives
----------

- What is the shell?
- How do you access it?
- How do you use it and what is it good for?
  * Running commands
  * Storing files in folders
  * Manipulating files
  * Automating actions
- Where are resources where I can learn more?

What is the shell?
------------------

The *shell* is a program that presents a command line interface
which allows you to control your computer using commands entered
with a keyboard instead of controlling graphical user interfaces
(GUIs) with a mouse/keyboard combination.

There are many reasons to learn about the shell.  A few specific ones:

* For most bioinformatics tools, you have to use the shell. There is no
  graphical interface. If you want to work in metagenomics or genomics you're
  going to need to use the shell.

* The shell gives you *power*. The command line gives you the power to
  do your work more efficiently and more quickly.  When you need to do
  things tens to hundreds of times, knowing how to use the shell is
  transformative.

* To use remote computers or cloud computing, you need to use the shell.

Automation
~~~~~~~~~~

The most important reason to learn the shell is to learn about
**automation**.  Any time you find yourself doing roughly the same
computational task more than few times, it may be worth automating it;
the shell is often the best way to automate anything to do with files.

Part of our goal is to make you aware of this dynamic:

.. image:: img/gvng.jpg

And here's a handy chart explaining when it pays to automate a task:

https://xkcd.com/1205/

Today we're going to go through how to access Unix/Linux and some of the basic
shell commands.

Information on the shell
------------------------

The challenge with UNIX is that it's not particularly simple - it's a
power tool, with its own deep internal logic with lots of details.
The joke is that Unix is user-friendly - it's just very selective
about who its friends are!

shell cheat sheets:

* http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/
* https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md

Explain shell - a web site where you can see what the different
components of a shell command are doing.

* http://explainshell.com
* http://www.commandlinefu.com

.. @CTB move these to the bottom?

How to access the shell
-----------------------

The shell is already available on Mac and Linux. For Windows, you'll
have to download a separate program.

Mac
~~~

On Mac the shell is available through Terminal  
Applications -> Utilities -> Terminal  
Go ahead and drag the Terminal application to your Dock for easy access.

Windows
~~~~~~~

For Windows, we're going to be using gitbash.  
Download and install [gitbash](http://msysgit.github.io);
Open up the program.

Linux
~~~~~

You probably already know how to find the shell prompt.

Starting with the shell
=======================

We will spend most of our time learning about the basics of the shell
by manipulating some experimental data.

Now we're going to download the data for the tutorial. For this you'll need
internet access, because you're going to get it off the web.

Open up the shell and type the command::

   pwd

and then hit ENTER.  We want to download the file:

   https://s3-us-west-1.amazonaws.com/dib-training.ucdavis.edu/shell-data.zip

to our computer, copy it to that directory, and then unpack it in that
directory.

Once that's done, type::

   ls

and hit ENTER.  You should see a listing of files, with 'shell-data.zip' and
'data' among them.

Once you see that, put up your green stickies.  If you don't know where to
start, put up your pink sticky.

Running commands
----------------

'pwd' and 'ls' are examples of commands - programs you run at the shell
prompt that do stuff. pwd stands for 'print working directory', while
'ls' stands for 'list files'.

Another command you'll find yourself using a lot is 'cd', which stands
for 'change directory'.  Try typing::

   cd data

and then::

   pwd

You should see that you're now in the data/ subdirectory (or folder).
Type 'ls' to see what files are in here.

What's going on?

The shell has a concept of "working directory", which is basically the
default location for commands to look when you run them.  When you run
'ls', by default it looks in your current working directory; when you
run 'cd', it changes your current working directory.

Now type::

  cd ..

and type 'ls'.  You should see shell-data.zip and data.  Here you're
using shorthand notation to go back up a directory.

Type::

  ls data

to tell ls to look in a different directory than your current working
directory.  This is equivalent to::

  cd data
  ls
  cd ..

Files and directories
~~~~~~~~~~~~~~~~~~~~~

Go back into the 'data' directory and list the files::

   cd data
   ls

In here, all mixed up together are files and directories/folders. If
we want to know which is which, we can type::

    ls -F

Anything with a "/" after it is a directory.  Things with a "*" after
them are programs.  It there's nothing there it's a file.

You can also use the command::

    ls -l

to see whether items in a directory are files or directories. `ls -l`
gives a lot more information too, such as the size of the file.

So, we can see that we have several files, directories and a program. Great!

Command line options
~~~~~~~~~~~~~~~~~~~~

Most programs take additional options (or "arguments") that control
their exact behavior. For example, `-F` and `-l` are arguments to
`ls`.  The `ls` program, like many programs, take a lot of
arguments. But how do we know what the options are to particular
commands?

Most commonly used shell programs have a manual. You can access the
manual using the `man` program. Try entering::

    man ls

This will open the manual page for `ls`. Use the space key to go
forward and b to go backwards. When you are done reading, just hit `q`
to quit.

Programs that are run from the shell can get extremely complicated. To
see an example, open up the manual page for the `find` program.  No
one can possibly learn all of these arguments, of course. So you will
probably find yourself referring back to the manual page frequently.

The Unix directory file structure (a.k.a. where am I?)
------------------------------------------------------

As you've already just seen, you can move around in different directories
or folders at the command line. Why would you want to do this, rather
than just navigating around the normal way.

When you're working with bioinformatics programs, you're working with
your data and it's key to be able to have that data in the right place
and make sure the program has access to the data. Many of the problems
people run in to with command line bioinformatics programs is not having the
data in the place the program expects it to be.

Moving around the file system
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let's practice moving around a bit.

We're going to work in that `data` directory we just downloaded.

First let's navigate there using the regular way by clicking on the
different folders.

First we did something like go to the folder of our username. Then we opened
'data'

This is called a hierarchical file system structure, like an upside down tree
with root (/) at the base that looks like this.

.. image:: img/Slide1.jpg

That (/) at the base is often also called the 'top' level.

When you are working at your computer or log in to a remote computer,
you are on one of the branches of that tree, your home directory
(/home/username)

Now let's go do that same navigation at the command line.

Type::

    cd

This puts you in your home directory. This folder here.

Now using `cd` and `ls`, go in to the 'data' directory and list its
contents.

Let's also check to see where we are. Sometimes when we're wandering
around in the file system, it's easy to lose track of where we are and
get lost.

Again, if you want to know what directory you're currently in, type

    pwd

What if we want to move back up and out of the 'data' directory? Can we just
type `cd home`? Try it and see what happens.

To go 'back up a level' we need to use `..`

Type::

    cd ..

Now do `ls` and `pwd`. See now that we went back up in to the home
directory. `..` means go back up a level.

Looking within folders within folder within...
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Try entering::

    cd data/hidden

and you will jump directly to `hidden` without having to go through
the intermediate directory.  Here, we're telling cd to go into
'data' first, and then 'hidden'.  You could put a file on the end,
too; for example, ::

    ls data/hidden/tmp1/notit.txt

You can do the same thing with any UNIX command that takes a file or
directory name.

### Shortcut: Tab Completion

Navigate to the home directory. Typing out directory names can waste a
lot of time. When you start typing out the name of a directory, then
hit the tab key, the shell will try to fill in the rest of the
directory name. For example, type `cd` to get back to your home directy, then enter::

    cd da<tab>

The shell will fill in the rest of the directory name for
'data'. Now cd to data/MiSeq and try::

    ls F3D<tab><tab>

When you hit the first tab, nothing happens. The reason is that there
are multiple directories in the home directory which start with
`F3D`. Thus, the shell does not know which one to fill in. When you hit
tab again, the shell will list the possible choices.

Tab completion can also fill in the names of programs. For example,
enter `e<tab><tab>`. You will see the name of every program that
starts with an `e`. One of those is `echo`. If you enter `ec<tab>` you
will see that tab completion works.

## Full vs. Relative Paths

The `cd` command takes an argument which is the directory
name. Directories can be specified using either a *relative* path or a
full *path*. The directories on the computer are arranged into a
hierarchy. The full path tells you where a directory is in that
hierarchy. Navigate to the home directory. Now, enter the `pwd`
command and you should see:

    /home/username

which is the full name of your home directory. This tells you that you
are in a directory called `username`, which sits inside a directory called
`home` which sits inside the very top directory in the hierarchy. The
very top of the hierarchy is a directory called `/` which is usually
referred to as the *root directory*. So, to summarize: `username` is a
directory in `home` which is a directory in `/`.

Now enter the following command:

    cd /home/username/data/hidden

This jumps to `hidden`. Now go back to the home directory (cd). We saw
earlier that the command:

    cd data/hidden

had the same effect - it took us to the `hidden` directory. But,
instead of specifying the full path
(`/home/username/data`), we specified a *relative path*. In
other words, we specified the path relative to our current
directory. A full path always starts with a `/`. A relative path does
not.

A relative path is like getting directions from someone on the
street. They tell you to "go right at the Stop sign, and then turn
left on Main Street". That works great if you're standing there
together, but not so well if you're trying to tell someone how to get
there from another country. A full path is like GPS coordinates.  It
tells you exactly where something is no matter where you are right
now.

You can usually use either a full path or a relative path depending on
what is most convenient. If we are in the home directory, it is more
convenient to just enter the relative path since it involves less
typing.

Over time, it will become easier for you to keep a mental note of the
structure of the directories that you are using and how to quickly
navigate amongst them.

Saving time with shortcuts, wild cards, and tab completion
----------------------------------------------------------

Shortcuts
~~~~~~~~~

There are some shortcuts which you should know about. Dealing with the
home directory is very common. So, in the shell the tilde character,
""~"", is a shortcut for your home directory. Navigate to the `edamame`
directory:

    cd
    cd data

Then enter the command:

    ls ~

This prints the contents of your home directory, without you having to
type the full path. The shortcut `..` always refers to the directory
above your current directory. Thus:

    ls ..

prints the contents of the `/home/username. You can chain
these together, so:

    ls ../../

prints the contents of `/home' which is above your home
directory. Finally, the special directory `.` always refers to your
current directory. So, `ls`, `ls .`, and `ls ././././.` all do the
same thing, they print the contents of the current directory. This may
seem like a useless shortcut right now, but we'll see when it is
needed in a little while.

To summarize, while you are in the `shell` directory, the commands
`ls ~`, `ls ~/.`, `ls ../../`, and `ls /home/username` all do exactly the
same thing. These shortcuts are not necessary, they are provided for
your convenience.

A data set: FASTQ files
-----------------------

We did an experiment and want to look at the bacterial communities of
mice in two treatments using 16S sequencing. We have 10 mice in one
treatment and 9 in another.each treatment. We also sequenced a Mock
community, so we can check the quality of our data. So, we have 20
samples all together and we've done paired-end MiSeq sequencing.

We get our data back from the sequencing center as FASTQ files, and we
stick them all in a folder called MiSeq. This data is actually data
generated by Pat Schloss and used in mothur tutorials.

We want to be able to look at these files and do some things with
them.

Wild cards
~~~~~~~~~~

Navigate to the ``data/MiSeq`` directory. This directory contains our
FASTQ files and some other ones we'll need for analyses. If we type
``ls``, we will see that there are a bunch of files with long file
names.  Some of the end with .fastq.

The ``*`` character is a shortcut for "everything". Thus, if you enter
``ls *``, you will see all of the contents of a given directory. Now try
this command::

    ls *fastq

This lists every file that ends with a ``fastq``. This command::

    ls /usr/bin/*.sh

Lists every file in ``/usr/bin`` that ends in the characters ``.sh``.

We have paired end sequencing, so for every sample we have two
files. If we want to just see the list of the files for the forward
direction sequencing we can use::

    ls *R1*fastq

lists every file in the current directory whose name contains the
number ``R1``, and ends with ``fastq``. There are twenty such files which
we would expect because we have 20 samples.

So how does this actually work? Well...when the shell (bash) sees a
word that contains the ``*`` character, it automatically looks for
filenames that match the given pattern. In this case, it identified
four such files. Then, it replaced the ``*R1*fastq`` with the list of
files, separated by spaces.

What happens if you do ``ls R1*fastq``?

Moving and copying files
------------------------

