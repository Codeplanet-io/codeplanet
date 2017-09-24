---
id: 374
title: File Immutability in Linux
date: 2014-12-02T02:31:34+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=374
permalink: /file-immutability-linux/
categories:
  - Linux
---
I&#8217;ve been working with linux for a very long time and I am ashamed to tell you I never knew about this trick. Let me walk you through what happened to me:

  1. SSH into a production server
  2. sudo vim file\_that\_needs_changing
  3. make changes
  4. try to save and quit
  5. get read-only error

I checked the file permissions, root has read-write privileges. I even sudo chmod 777 on the file and **still couldn&#8217;t edit it!**

## CHATTR

<http://linux.die.net/man/1/chattr>

chattr &#8211; change file attributes on a Linux file system

Apparently, you can use chattr to change file attributes, including a +i flag for **immutability**. This means that the file cannot be changed no matter what the permissions. It goes a little something like this:

<pre class="lang:sh decode:true ">chattr +i file_to_become_immutable
# File can no longed be edited

chattr -i file_to_become_mutable
# File can be written to again</pre>

anyway, check out the [manpage](http://linux.die.net/man/1/chattr) and don&#8217;t get confused if you ever run across something like this in the wild!