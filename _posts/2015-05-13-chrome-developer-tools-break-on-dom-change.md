---
id: 394
title: Chrome Developer Tools Break on DOM Change
date: 2015-05-13T00:08:17+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=394
permalink: /chrome-developer-tools-break-on-dom-change/
categories:
  - Web Development
tags:
  - Developer Tools
  - JavaScript
---
Today, my coworker [Kelly King](https://twitter.com/kng) showed me a really cool thing you can do with the Chrome Developer Tools.

You can set breakpoints on changes to specific parts of the DOM, instead of manually placing them inside your JavaScript.

## Use Case

I find this technique particularly useful when you&#8217;re trying to figure out what JavaScript is responsible for a certain visible change in the DOM. For example, if a table is getting populated with numbers and you want to find the code responsible for it.

## The Approach

First you&#8217;ll want to open up inspect element and make sure you are on the &#8220;Elements&#8221; tab.

Next, find the container element of whatever DOM node you are curious about and right click on it.

Select &#8220;Break on&#8230;&#8221; and then &#8220;Subtree Modifications&#8221; as pictured below.

[<img class="alignnone size-large wp-image-396" src="https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.01.29-PM-1024x640.png" alt="Screen Shot 2015-05-12 at 10.01.29 PM" width="640" height="400" srcset="https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.01.29-PM-1024x640.png 1024w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.01.29-PM-300x188.png 300w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.01.29-PM-768x480.png 768w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.01.29-PM-1200x750.png 1200w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.01.29-PM.png 1280w" sizes="(max-width: 640px) 100vw, 640px" />](https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.01.29-PM.png)

Now refresh the page, or simulate whatever interaction causes that part of the DOM to change and you&#8217;ll be dropped into the JavaScript sources tab with a breakpoint on the appropriate line of code. Pictured below.

[<img class="alignnone size-large wp-image-397" src="https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.02.09-PM-1024x640.png" alt="Screen Shot 2015-05-12 at 10.02.09 PM" width="640" height="400" srcset="https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.02.09-PM-1024x640.png 1024w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.02.09-PM-300x188.png 300w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.02.09-PM-768x480.png 768w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.02.09-PM-1200x750.png 1200w, https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.02.09-PM.png 1280w" sizes="(max-width: 640px) 100vw, 640px" />](https://codeplanet.io/wp-content/uploads/2015/05/Screen-Shot-2015-05-12-at-10.02.09-PM.png)