---
id: 776
title: Installing Node.js 4.2 LTS on Debian Wheezy
date: 2015-11-23T10:00:51+00:00
author: Thomas Hunter II
layout: post
guid: http://codeplanet.io/?p=776
permalink: /installing-node-js-4-2-lts-debian-wheezy/
image: /wp-content/uploads/2015/11/debian-logo-1200x340.gif
categories:
  - Linux
  - Node.js
---
Normally I download, compile, and install Node from source. However the LTS version of Node requires GCC >= 4.8, whereas Debian Wheezy is stuck at 4.7. Instead of jumping through the hoops to upgrade GCC I figured I&#8217;d try installing the binary version. Here&#8217;s the commands you can run to get the binary installed on Debian (you&#8217;ll want to run these commands as root).

<pre class="theme:tomorrow-night lang:sh decode:true">wget https://nodejs.org/dist/v4.2.2/node-v4.2.2-linux-x64.tar.gz
tar -xzvf node-v4.2.2-linux-x64.tar.gz && cd node-v4.2.2-linux-x64
cp ./bin/node /usr/local/bin/node
cp -r ./lib/node_modules /usr/local/lib/node_modules
ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm
cp -r ./include/node /usr/local/include
mkdir -p /usr/local/man/man1 && cp ./share/man/man1/node.1 /usr/local/man/man1/node.1</pre>

Once you&#8217;re done, run `node -v` (v4.2.2) and `npm -v` (2.14.7) to ensure everything went smoothly.

Note: If you&#8217;ve already got an older version of Node installed, be sure to delete all the files you&#8217;re about to write to first, otherwise you&#8217;ll get errors.