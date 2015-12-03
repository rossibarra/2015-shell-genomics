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

Command line options
~~~~~~~~~~~~~~~~~~~~


Absolute vs relative paths
~~~~~~~~~~~~~~~~~~~~~~~~~~


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

