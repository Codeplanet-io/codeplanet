---
title: Speeding up Vagrant
author: Jon Kuperman
type: post
date: 2014-09-28T06:25:52+00:00
url: /speeding-vagrant/
categories:
  - Tools

---
Many teams are moving their development environment over to [Vagrant][1] lately. It can have profound effects on reducing developer onboard time,  environment specific errors and even help non technical teammates get up and running with a local environment.

The only real issue with Vagrant is that out of the box it is **slow**. While it will never be as fast as a native environment, there are things you can do to speed up performance considerably.

## 1. Move to NFS

The biggest gain you can get is switching file systems over from the default Virtualbox shared folders to NFS. The best part is that switching couldn&#8217;t really be easier.

by default, Vagrant mounts drives like this:

<pre class="toolbar:2 lang:ruby decode:true">config.vm.synced_folder "../data", "/vagrant_data"</pre>

all you have to do is add type: &#8220;nfs&#8221; like so:

<pre class="toolbar:2 lang:ruby decode:true">config.vm.synced_folder "../data", "/vagrant_data", type: "nfs"</pre>

and you&#8217;re done!

The only issue you might run into is that unlike with Virtualbox shared folders, NFS uses whatever file permissions are already on your files. Where before you could do something like:

<pre class="toolbar:2 lang:ruby decode:true">:mount_options =&gt; ['dmode=775', 'fmode=775']</pre>

now you&#8217;ll have to configure permissions on your laptop / desktop before initializing Vagrant.

The other caveat, which really isn&#8217;t a problem but can seem strange is that if you look at the files owner on the VM you&#8217;ll most likely see something like:

<pre class="toolbar:2 lang:ruby decode:true  ">501:games</pre>

or something like that. Don&#8217;t be alarmed! This is a default user ID that comes on all systems. You&#8217;re user ( vagrant or whatever you set it to ) can still read / write on all of your files, it just looks weird.

## 2. Use more cores and memory

The next thing you can do is allocate more resources to the VM. Personally, I always use 100% of available cores and at least 2GB of memory if I can spare it. You can just add these lines to your Vagrantfile:

<pre class="lang:ruby decode:true ">config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 4
end</pre>

This won&#8217;t help as much as the NFS fix but it should speed things up nicely for you.

 [1]: http://www.vagrantup.com/