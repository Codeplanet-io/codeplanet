---
id: 611
title: 'React.js &#8211; A step backwards?'
date: 2015-09-14T10:00:53+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=611
permalink: /react-js-a-step-backward/
categories:
  - JavaScript
---
In 1990, code looked like:

<pre class="lang:default decode:true">&lt;div onclick=“doSomething”&gt;Click Me&lt;/div&gt;</pre>

In 2010, code looked like:

<pre class="lang:default decode:true">&lt;div id=“js-doSomething”&gt;Click Me&lt;/div&gt;</pre>

and then

<pre class="lang:js decode:true">$(“#js-doSomething”).on(“click”, function() {
    doSomething();
};</pre>

In 2015, code looks like:

<pre class="lang:js decode:true">render () {
    return (
        &lt;div onClick=“doSomething”&gt;Click Me&lt;/div&gt;
    );
}</pre>

So the question is, are we moving backwards?

**Simple answer, no.**

## Why was onclick a good idea?

  * **Readability** &#8211; You can just look at the div and know exactly what happens when you click on it.

## Why was onclick a bad idea?

  * **Separation of Concerns** &#8211; We’re way past that now.
  * **Polluting the Global Namespace** &#8211; Anything you put in an onclick event is automatically bound to the window object. This is bad for multiple reasons.
  * **Strange Scoping** &#8211; Check out [this answer on StackOverflow](http://stackoverflow.com/a/21975639).

Are we back to these problems?

**Simple answer, no.**

Using React’s onClick event suffers from only one of these problems; the separation of concerns.

Like I said earlier though, if you are using JavaScript to create all of your HTML, we’re way passed that. It doesn’t pollute the global namespace and has JavaScript&#8217;s (mostly) sane scoping.

So, even though it really looks like we’re developing using age-old anti-patterns, we’re really writing readable code &#8211; the way it should have been done originally.