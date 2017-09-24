---
id: 1330
title: Debugging JavaScript with the debugger statement
date: 2017-01-05T16:06:34+00:00
author: Jon Kuperman
layout: post
guid: https://codeplanet.io/?p=1330
permalink: /debugging-javascript-debugger-statement/
image: /wp-content/uploads/2016/05/chrome_devtools.png
categories:
  - Debugging
  - JavaScript
---
One of the most useful statements in JavaScript is [debugger](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger). It invokes any available debugging functionality from your application and has no effect if there is no functionality available.

So, for example if you have some JavaScript running and you want to pause execution at a certain line you can do something like:

<pre class="lang:js decode:true">function foo() {
  doSomeStuff()
  debugger; // will open devtools if executed in the browser or a node debugger if available
  doSomeMoreStuff()
}</pre>

Most of the time, if you are working with browser JavaScript, adding a debugger; line is equivalent to setting a breakpoint in the sources tab of your developer tools. For example in Chrome you could just:

<img class="alignnone size-full wp-image-1331" src="https://codeplanet.io/wp-content/uploads/2017/01/Screen-Shot-2017-01-05-at-3.02.54-PM.png" alt="" width="1248" height="786" srcset="https://codeplanet.io/wp-content/uploads/2017/01/Screen-Shot-2017-01-05-at-3.02.54-PM.png 1248w, https://codeplanet.io/wp-content/uploads/2017/01/Screen-Shot-2017-01-05-at-3.02.54-PM-300x189.png 300w, https://codeplanet.io/wp-content/uploads/2017/01/Screen-Shot-2017-01-05-at-3.02.54-PM-768x484.png 768w, https://codeplanet.io/wp-content/uploads/2017/01/Screen-Shot-2017-01-05-at-3.02.54-PM-1024x645.png 1024w, https://codeplanet.io/wp-content/uploads/2017/01/Screen-Shot-2017-01-05-at-3.02.54-PM-1080x680.png 1080w" sizes="(max-width: 1248px) 100vw, 1248px" />

Because it can be accessed either way, I find debugger to be most useful in 3 situations.

  1. When you don&#8217;t have control over the browser. For example if you are running automated tests and can&#8217;t click through to add a breakpoint adding a debugger; line in your test will do the trick!
  2. If you are not in a browser environment.
  3. If your code is minified/concatendated making it difficult to find from the browser.