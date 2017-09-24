---
id: 35
title: Debugging with Log Files
date: 2013-07-31T03:37:44+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=35
permalink: /debugging-with-log-files/
post_views_count:
  - "112"
image: /wp-content/uploads/2013/07/log.png
categories:
  - Tools
  - Web Development
---
I was **WAY** too far into my career as a programmer when I learned about log files.

## What are log files

> A log file is a file that records events to provide an audit trail that can be used to understand the activity of the system and to diagnose problems.

Basically, almost all of the big heavy processes that we use daily ( PHP, Apache, Nginx, Kernels, Mail Client, etc ) all have neat flat files where they keep a log of all the important stuff they do. More importantly, they keep track of every time they error and what was happening when they do.

## Life before log files

For years as a developer when I would start up my web application and get a blank page ( indicative of a PHP error ) I would just turn back to my code and scrutinize over what I could have done wrong.

Similarly if I added a new website to my host and the domain wasn&#8217;t showing up properly, I would wait or continuously scour the configuration files I made looking for some obscure typo.

## Meet Logs

[<img class="alignnone size-medium wp-image-38" alt="log" src="https://codeplanet.io/wp-content/uploads/2013/07/log-300x225.png" srcset="https://codeplanet.io/wp-content/uploads/2013/07/log-300x225.png 300w, https://codeplanet.io/wp-content/uploads/2013/07/log.png 400w" sizes="(max-width: 300px) 100vw, 300px" />](https://codeplanet.io/wp-content/uploads/2013/07/log.png)

To see what logs you have already available on your server or computer, just check out the /var/log directory!

    cd /var/log/

and then

    ls

You should see an impressive list like this!

[<img class="alignnone size-medium wp-image-46" alt="terminal" src="https://codeplanet.io/wp-content/uploads/2013/07/terminal-300x184.png" srcset="https://codeplanet.io/wp-content/uploads/2013/07/terminal-300x184.png 300w, https://codeplanet.io/wp-content/uploads/2013/07/terminal-768x471.png 768w, https://codeplanet.io/wp-content/uploads/2013/07/terminal.png 851w" sizes="(max-width: 300px) 100vw, 300px" />](https://codeplanet.io/wp-content/uploads/2013/07/terminal.png)

Don&#8217;t be intimidated! Remember these files are all there to help you and you can ignore as many as you&#8217;d like!

## Using the logs

Before we can start really getting the most out of these log files. There are a few UNIX tools we&#8217;ll need to know.

  1. less &#8211; turn more than a page of results into a scrollable page
  2. tail &#8211; display just the last few lines of a file

## A simple example

Let&#8217;s say you&#8217;re getting one of those pesky PHP errors I mentioned earlier. This time, instead of combing the code for hours we&#8217;re just going to peek inside one of those wonderful logs!

From /var/log/ we can just type ( your experience may differ slightly, just find the file! )

    tail apache2/error.log

and bam! You should see the last few errors that occurred in PHP.

Maybe that returned a lot of results though. Instead of scrolling through your terminal you can pipe those results easily into less for a better experience!

    tail apache2/error.log | less

## More to come!

As always stay tuned as I&#8217;ll be diving way deeper into the logs from PHP, Apache, the Linux Kernel and a whole lot more!