---
title: PHP If Checks
author: Jon Kuperman
type: post
date: 2014-07-27T23:11:48+00:00
excerpt: "If you're a PHP developer, there's a good chance you've done this hundreds of times, but do you know what it's really doing?"
url: /php-checks/
categories:
  - Web Development

---
It&#8217;s really common in PHP to check a variables status with some code like this:

<pre class="lang:php decode:true ">&lt;?php

if($myVariable) {
    // run some code
}</pre>

If you&#8217;re a PHP developer, there&#8217;s a good chance you&#8217;ve done this hundreds of times, but do you know what it&#8217;s really doing?

Code inside an if-check like the one above is checking to see if the variable evaluates to _any truthy value_.

Here are some examples to help illustrate what&#8217;s it&#8217;s doing:

<pre class="lang:php decode:true ">&lt;?php

// Things that will FAIL the check

$myVariable = '';
if($myVariable) // false

$myVariable = 0;
if($myVariable) // false

$myVariable = NULL;
if($myVariable) // false

$myVariable = array();
if($myVariable) // false

// Things that will PASS the check

$myVariable = 'false';
if($myVariable) // true

$myVariable = 1;
if($myVariable) // true

$myVariable = 'Hello World';
if($myVariable) // true

$myVariable = array(1);
if($myVariable) // true

if($undefinedVariable) // Error</pre>

## Behind the Scenes

If you&#8217;re ever unsure what something is going to evaluate to, you can just cast it as a boolean in PHP to see.

For example:

<pre class="lang:php decode:true ">var_dump((bool) '');

// or

var_dump((bool) 'Hello World!');</pre>

Hope that helps!