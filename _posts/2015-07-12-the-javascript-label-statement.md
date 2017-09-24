---
id: 422
title: The JavaScript Label Statement
date: 2015-07-12T21:50:05+00:00
author: Jon Kuperman
excerpt: The JavaScript label statement is used in conjunction with continue or break statements. Essentially you can label a for loop or a switch case and then break or continue to it. This is extremely useful if you have nested statements and you want to break or continue to the outer one.
layout: post
guid: http://codeplanet.io/?p=422
permalink: /the-javascript-label-statement/
image: /wp-content/uploads/2015/12/js-logo.jpg
categories:
  - JavaScript
---
The JavaScript label statement is used in conjunction with continue or break statements. Essentially you can label a for loop or a switch case and then break or continue to it.

This is extremely useful if you have nested statements and you want to break or continue to the outer one. For example:

<pre class="lang:js decode:true ">my_label:
for (var i = 0; i &lt; 3; i++) {
   for (var j = 0; j &lt; 10; j++) {
      if (j === 1) {
         continue my_label;
      }
      console.log("i = " + i + ", j = " + j);
   }
}

// Will return
// "i = 0, j = 0"
// "i = 1, j = 0"
// "i = 2, j = 0"</pre>

In the above code, each time that j gets to zero we continue but instead of continuing the inner loop we specify the label of the outer group ( my_label ). This causes the outer loop to start again so the inner loop never gets past zero.

## No Goto in JavaScript

JavaScript does not have a [goto statement](https://en.wikipedia.org/wiki/Goto) so the only way to transfer control of a program is with continue or break. However using continue and break in conjunction with JavaScript labels will get you pretty close to full control over your program execution.

Unfortunately, these labels only work for nested loops or switch statements. You can&#8217;t break from a loop to a completely separate loop by calling it&#8217;s label. For example:

<pre class="lang:js decode:true ">var i, j, k;

foo:
for(i = 0; i &lt; 3; i++) {
  console.log('foo');
}

loop1:
for (j = 0; j &lt; 3; j++) {
   loop2:
   for (k = 0; k &lt; 3; k++) {
      console.log('bar');
   }
}

// This will generate an error
// "SyntaxError: Undefined label 'foo'</pre>

&nbsp;