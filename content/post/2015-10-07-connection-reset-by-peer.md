---
title: 'ssh_exchange_identification: read: connection reset by peer'
author: Jon Kuperman
type: post
date: 2015-10-07T17:00:28+00:00
url: /connection-reset-by-peer/
categories:
  - Linux

---
This tutorial is meant to help troubleshoot **connection reset by peer** issues you might have while using SSH.

Ever tried to SSH into your server and seen an error like this?

<pre class="lang:default decode:true">ssh_exchange_identification: read: Connection reset by peer</pre>

The first thing you should always do if SSH fails is try again with verbose logging on. Just try something like this:

<pre class="lang:default decode:true">ssh username@address.com -vv</pre>

If the problem is on your client&#8217;s side, some sort of error should show up in that log. If you aren&#8217;t seeing anything useful in there, the problem may be with your server.

## The Tricky Part

So, how do you get on your server if you cant ssh!?

If you&#8217;re lucky, your host will provide you with some sort of shell access via their web UI. If not, they should at least offer some alternative method for access. That part you&#8217;ll need to figure out for yourself.

## After You Get Access

If you want to see everything that SSH is doing on the server side, here&#8217;s what you can try ( assuming Debian or Ubuntu here ):

<pre class="lang:default decode:true">sudo service ssh stop
sudo /usr/sbin/sshd -d</pre>

That will show you a real time log of everything that happens to SSH. If, as I suspect, you are banned from your server ( fail2ban or some other program has put your IP in /etc/hosts.deny ) you should see something like this in the log:

<pre class="lang:default decode:true">debug1: Connection refused by tcp wrapper</pre>

It could mean a number of things, but very likely you&#8217;re being blocked by hosts.deny. The simplest way to test would be to put an allow all in hosts.allow

<pre class="lang:default decode:true">vi /etc/hosts.allow</pre>

and put in something like:

<pre class="lang:default decode:true ">sshd: ALL</pre>

Then try re-connecting. If that was your problem, try re-configuring fail2ban or whatever you have on your server that is sticking IPs into hosts.deny. If not, keep Googling! 😉