---
title: Passing Parameters in Javascript onClick Event
author: Jon Kuperman
type: post
date: 2015-11-23T08:08:34+00:00
url: /passing-parameters-in-javascript-onclick-event/
categories:
  - JavaScript

---
I ran into a problem today.

I was trying to generate a bunch of input buttons with JavaScript and have each of them do something unique onClick.

## The Wrong Way

<pre class="lang:js decode:true ">var temp;
var myArr = ["Peter", "Paul", "Tony", "Adam"];

function display(name) {
    alert(name);
}

for(var i = 0; i &lt; 4; i ++) {
    temp = myArr[i];
    document.write('&lt;input type="button" onclick="display(temp)" value="Display"&gt;'); // Will always log "Adam"
}</pre>

## The Problem

The issue is in JavaScript global variable. Since temp is a global variable, the onclick trigger sends the content of temp after the loop is all finished. Since Adam is the last value to be stored in temp, that&#8217;s what all buttons alert. The trick is to use input name as a non-global and then pass the whole input tag to the function like so:

## The Right Way

<pre class="lang:js decode:true ">var myArr = ["Peter", "Paul", "Tony", "Adam"];

function display(name) {
    alert(name);
}

for(var i = 0; i &lt; 4; i ++) {
    document.write('&lt;input type="button" onclick="display(this)" name="'+ myArr[i] + '" value="' + myArr[i] + '"&gt;'); // Will log Peter, Paul..
}</pre>

&nbsp;