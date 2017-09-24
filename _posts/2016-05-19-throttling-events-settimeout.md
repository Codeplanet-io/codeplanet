---
id: 958
title: Throttling events with setTimeout
date: 2016-05-19T18:01:24+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=958
permalink: /throttling-events-settimeout/
image: /wp-content/uploads/2015/12/js-logo.jpg
categories:
  - JavaScript
---
Time and time again, we need to listen for an event (scroll, keyup) and execute some arbitrary code when that event fires. If you do this enough, you&#8217;ll likely run into a situation where you are just receiving **way** **too many** events. In these cases, it&#8217;s best to set and clear a timeout to make sure your code only fires once in a while.

## Example:

Say you want to run some advertising code on the scroll event, to track and see if any of your ads have scrolled into or out of view. You might have something like this:

<pre class="lang:js decode:true">window.addEventListener('scroll', function() {
  // Check to see what ads are showing!
}, false);</pre>

This will work, but you&#8217;ll likely be executing that code thousands of times as the user scrolls around the screen. Another example would be wanted to do an AJAX call as the user types into a form field to popular some search suggestions. Maybe you have:

<pre class="lang:js decode:true">window.addEventListener('keyup', function() {
  // $.GET some sweet suggestions!
}, false);
</pre>

But again, you end up triggering hundreds of AJAX calls as the user types, deletes, re-types. So what&#8217;s the solution?

## setTimeout and clearTimeout

Most of you have probably used setTimeout before, you can execute some code after a specified delay. Something like this:

<pre class="lang:js decode:true ">window.setTimeout(function() {
  alert("Hello World!");
}, 2000);</pre>

That&#8217;s part of the equation, if inside our event listener we put a timeout, it wouldn&#8217;t ever fire right away. It would, however, still fire just as many times as before. Just now they&#8217;d all be delayed by 200 milliseconds. Here&#8217;s where we can use window.clearTimeout to effectively throttle our event listeners.

<pre class="lang:js decode:true ">var timedEvent;

window.addEventListener('scroll', function() {
  clearTimeout(timedEvent);

  timedEvent = setTimeout(function() {
    // AJAX or Check for ads
  }, 2000);
}, false);</pre>

And there you have it! Change that 2000 value to whatever frequency you&#8217;d like to run your code.