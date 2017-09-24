---
id: 582
title: The list of CSS Selectors
date: 2015-09-01T10:00:39+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=582
permalink: /the-list-of-css-selectors/
categories:
  - CSS
---
There are a ton of different CSS selectors out there. Here are the ones that I find extremely useful.

## Element Selectors

If you ever want to style all elements of a certain type ( only recommended for a base stylesheet ) you should use plain element selectors.

<pre class="lang:css decode:true ">a {
  /* Style all links */
  color: red;
}

img {
  /* Style all images */
  max-width: 100%;
}</pre>

## ID and Class Selectors

Perhaps the most common of all selectors. Let&#8217;s say you have some HTML that looks like this:

<pre class="lang:default decode:true ">&lt;div id="foo"&gt;
  &lt;span class="bar"&gt;Hello World&lt;/span&gt;
&lt;/div&gt;</pre>

If we want to add some styles to it. You can target the ID of foo and the class of bar this way:

<pre class="lang:css decode:true ">#foo {
  width: 100px;
  height: 100px;
  background-color: red;
}

.bar {
  display: block;
  width: 25px;
  height: 25px;
  background-color: blue;
}</pre>

## Pseudo Class Selectors

There are all sorts of great ways to select elements in a certain state or position. Although the browser support isn&#8217;t as great as some of the previously mentioned but pseudo selectors work in all current major browsers. They look like this:

<pre class="lang:css decode:true ">/* Control what links look like when hovered */
a:hover {
  color: pink;
}

/* Control what links look like when active */
a:active {
  color: pink;
}

/* Control what links look like when visited */
a:visited {
  color: pink;
}

/* Alter the first list item in any list */
li:first-child {
  font-weight: bold;
}

/* Alter the last list item in any list */
li:last-child {
  font-weight: bold;
}</pre>

## Relationship Selectors

Last but not least, I often see people use classes and IDs when relationship selectors would suffice. Say you have some HTML that looks like:

<pre class="lang:default decode:true ">&lt;div&gt;
  &lt;p&gt;Foo&lt;/p&gt;
  &lt;p&gt;Bar&lt;/p&gt;
&lt;/div&gt;
&lt;p&gt;Baz&lt;/p&gt;
&lt;p&gt;Whatever comes after Baz&lt;/p&gt;</pre>

Let&#8217;s target those elements!

<pre class="lang:css decode:true ">/* Targets all paragraph descendants of every div */
/* In this case, Foo and Bar */
div p {
  color: red;
}

/* Targets the first paragraph child of every div */
/* In this case, Foo */
div &gt; p {
  color: blue;
}

/* Targets the first paragraph sibling of each div */
/* In this case, Baz */
div + p {
  color: yellow;
}

/* Targets all paragraph tags that are siblings of every div */
/* In this case, Baz and whatever comes after Baz */
div ~ p {
  color: green;
}</pre>

&nbsp;