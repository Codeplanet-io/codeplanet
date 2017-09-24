---
id: 755
title: Install ImageMagick with PHP on Debian
date: 2015-10-18T20:02:02+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=755
permalink: /install-imagemagick-with-php-on-debian/
categories:
  - Uncategorized
---
I&#8217;ve been working on an app lately that involves some image manipulation. Most of the time I use[GD](http://php.net/manual/en/book.image.php) for image manipulation but there are a lot of things it just can&#8217;t do easily.

When I run into prolems GD can&#8217;t solve, I turn to [ImageMagick](http://www.imagemagick.org/).

ImageMagick is great, it&#8217;s powerful and easy-to-use. Unfortunately, it&#8217;s an enormouse pain to install and set-up.

It was far from easy setting it up on Debian / Ubuntu &#8212; so here&#8217;s how I did it. I hope it helps.

## 1. Install ImageMagick

You can get ImageMagick and its dependencies from the apt-get repository.

<pre class="lang:sh decode:true ">sudo apt-get update
sudo apt-get build-dep imagemagick</pre>

## 2. Get The PHP Dev Package

In order to use PHP to interact with ImageMagick you&#8217;ll need this package.

<pre class="lang:sh decode:true ">sudo apt-get install php5-dev</pre>

## 3. Get the PECL Imagick Package

Now that you have the PHP Dev tools and ImageMagick, you just need the Imagick package to interface between PHP and ImageMagick.

<pre class="lang:sh decode:true ">pecl install imagick</pre>

## 4. Write Some Sweet PHP / ImageMagick Code

Now you can use a ton of great tools, check out [a list](http://php.net/manual/en/book.imagick.php) here!

<pre class="lang:php decode:true">&lt;?php
    $thumb = new Imagick();
    $thumb-&gt;readImage('myimage.gif');
    $thumb-&gt;resizeImage(320,240,Imagick::FILTER_LANCZOS,1);
    $thumb-&gt;writeImage('mythumb.gif');
    $thumb-&gt;clear();
    $thumb-&gt;destroy(); 
?&gt;</pre>

&nbsp;