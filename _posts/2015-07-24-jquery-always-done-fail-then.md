---
id: 472
title: jQuery always vs. done vs. fail vs. then
date: 2015-07-24T10:00:13+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=472
permalink: /jquery-always-done-fail-then/
categories:
  - JavaScript
---
jQuery&#8217;s [deferred objects](https://api.jquery.com/category/deferred-object/) can be tough to get your head around. Specifically learning the difference between **always**, **done**, **fail**, and **then**. Let&#8217;s go over them really quick and then dive into some examples!

  1. **Always **&#8211; called when the deferred object resolved **or** rejected
  2. **Done** &#8211; called when the deferred object is resolved
  3. **Fail **&#8211; called when the deferred object is rejected
  4. **Then** &#8211; a nice shorthand that allows you to pass in a done and then optionally a fail and a progress

## Some Examples

Let&#8217;s cement this with some easy examples!

### Always

<pre class="lang:js decode:true ">$.get( "www.yoursite.com/api" ).always(function() {
  console.log('this will run whether the $.get fails or succeeds');
});</pre>

### Done

<pre class="lang:default decode:true ">$.get( "www.yoursite.com/api" ).done(function() {
  console.log('this will run if the $.get succeeds');
});</pre>

### Fail

<pre class="lang:default decode:true ">$.get( "www.yoursite.com/api" ).fail(function() {
  console.log('this will run if the $.get fails');
});</pre>

### Then

<pre class="lang:default decode:true ">$.get( "www.yoursite.com/api" ).then(
    function() {
      console.log('this will run if the $.get succeeds');
    }, function() {
        console.log('this will run if the $.get fails');
    }, function() {
        console.log('this will run if the deferred generates a progress update');
    }
);</pre>

Hope that helps! There are a [bunch of other cool methods](https://api.jquery.com/category/deferred-object/) you should check out! Let me know in the comments if you have any questions.