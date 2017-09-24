---
id: 297
title: Targeting IE8 With CSS
date: 2014-06-04T23:02:37+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=297
permalink: /targeting-ie8-css/
categories:
  - CSS
---
If you&#8217;re a front-end developer, and the project you work on needs to support users on Internet Explorer 8, odds are that you&#8217;ve run into situations where you need a bit of CSS that should only be triggered by those users.

## Current Options

The most common thing to do in this situation is to create and serve [IE only stylesheets](http://css-tricks.com/how-to-create-an-ie-only-stylesheet/). In your HTML, you&#8217;ll call a separate stylesheet like this:

<pre class="lang:default decode:true">&lt;!--[if lte IE 8]&gt;
    &lt;link rel="stylesheet" type="text/css" href="ie8-and-down.css" /&gt;
&lt;![endif]--&gt;</pre>

### Drawbacks

Honestly this works really well. The only issue is that you&#8217;re serving an extra file, an extra HTTP request to the user and it can affect performance. That and it&#8217;s just another file to deal with.

The next most common option is to use selectors that [target a specific browser](http://css-tricks.com/snippets/css/browser-specific-hacks/). If you wanted to target IE8, you could write something like these:

<pre class="lang:css decode:true">/* IE6, IE7, IE8 */
#diecinueve { color: blue9; }
 
/* IE7, IE8 */
#veinte { color/***/: blue9; }</pre>

### Drawbacks

This also works well, my only real problem with this technique is that your IE8 specific code ends up all over the place, it&#8217;s also a bit confusing because you&#8217;ll use the same selector multiple times in a row ( one for other browsers, one for IE8, etc ). Also, it&#8217;s really difficult to tell what&#8217;s going on ( I&#8217;ve had many people complain about glitches in my CSS! ).

## A New Solution

I&#8217;ve come up with a new way of dealing with this while sticking to only one file. It plays off IE8 not having support for [media queries](http://css-tricks.com/css-media-queries/).

### The Idea

The basic idea here is you write your IE8 and below code in your style.css and then wrap all of your modern browser code in a media query which will be ignored by older browsers. Something like this:

<pre class="lang:css decode:true ">/* Hide button in IE8 */
.button {
    display: none;
}

/* Change link color in IE8 */
a {
    color: pink;
}

/*
 * Now, the modern browser code
 *
 */
@media all and (min-width: 1px) {
    .button {
        display: inline;
    }

    a {
        color: blue;
    }

    /* The rest of your CSS goes here */
}</pre>

What do you all think? Is this something you&#8217;d use in a production environment?