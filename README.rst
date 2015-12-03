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
