---
id: 10
title: Getting Started With Git
date: 2013-07-31T03:08:58+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=10
permalink: /getting-started-with-git/
post_views_count:
  - "126"
image: /wp-content/uploads/2013/07/git-logo.png
categories:
  - Git
  - Tools
---
For those of you that are new to development, maintaining your project with Version Control is the industry standard and Git is the Version Control Standard.

[<img class="alignnone size-full wp-image-19" alt="git-logo" src="https://codeplanet.io/wp-content/uploads/2013/07/git-logo.png" />](https://codeplanet.io/wp-content/uploads/2013/07/git-logo.png)

##  What is Version Control

> Version Control refers to the management of changes to documents, computer programs, large web sites, and other collections of information

Essentially Version Control systems such as git allow you to keep a detailed log of every change to your project including who made it and when it was made. This has endless utility as you can easily:

  * Peel back to a time you knew your project was working
  * Check to see who wrote the code you&#8217;re looking at
  * Allow multiple people to edit the same files without worrying about conflict
  * So many more things!

So, now that you know you need git, let&#8217;s figure out how to get git installed!

## Installing Git

Often times git is already installed on your computer. To check if it is, just fire up your favorite terminal and type:

    git --version

If you get a version number, you&#8217;re all set! If not, keep reading this section!

Git is one of the few open source linux programs with a beautiful and easy to understand website. I highly recommend checking out the [installing git article](http://git-scm.com/book/en/Getting-Started-Installing-Git) on their home page.

Essentially it boils down to git being pre-installed on almost every Mac and Linux distribution. If it&#8217;s not already installed you&#8217;ll be able to be install it with most any package manager.

## Using Git

Now that we have git installed. Let&#8217;s cover some basic usage. There are really only three commands you need to know about when starting to use git.

First, let&#8217;s use that sweet terminal to move into a folder where you currently have some code you&#8217;ve been working on!

    cd /my/sweet/project/

### Command #1 &#8211; git init

The first thing we need to do is initialize this project. This is essentially just telling git that you want to consider the current folder a project that you plan on doing sweet Version Control inside of.

    git init

### Command #2 &#8211; git add

This took a minute for me to understand. Just because you have git initialized in the current folder doesn&#8217;t mean that git is &#8216;tracking&#8217; your files. Tracking is the word within the git community that means actively checking for changes.

The simplest thing to do here is tell git to just track every file in your folder.

    git add .

### Command #3 &#8211; git commit

The last thing you really **need** to know in order to use git is when and how to make a &#8216;snapshot&#8217;. A snapshot is the git term for when you decide a moment in time deserves its own save spot. You should take these snapshots often as the more you have and the better they are labeled the easier time you&#8217;ll have jumping back and forth in your code history.

To take a snapshot and give it a message you can just:

    git commit -m 'A description of what has been done since my last commit'

## Take a deep breath!

You made it through! That wasn&#8217;t so bad was it?

From here you can start keeping a good record of your project. I like to make a commit after every task I do on my code base. For example:

  1. <span style="line-height: 13px;">Added new icons</span>
  2. Fixed the log-in bug
  3. Added new column to database
  4. Changed the sidebar width

## Some other fun commands

Now that you&#8217;re well on your way to becoming an expert, here are some other cool tools git comes with out of the box!

### Show a log of commits

    git log

### Show the specifics of a commit

Grab one of those unique SHA&#8217;s from **git log** and run

    git show SHA

### See what you&#8217;ve changed since the last commit

    git status

## More to Come

Be sure to stay tuned as we&#8217;ll talk a lot more about things like:

  1. <span style="line-height: 13px;">Taking git online</span>
  2. Branching
  3. Merging
  4. Rebasing

See you next time!