---
title: JavaScript continue vs. break
author: Jon Kuperman
type: post
date: 2015-10-09T17:00:52+00:00
url: /javascript-continue-vs-break/
categories:
  - JavaScript

---
Two very similar statements in JavaScript that should not be confused are _continue__ _and _break_. First let&#8217;s talk about their similarities.

## Similarities

  * Both continue and break only work inside of loop, switch, or label statements.
  * They are both statements so they are called without parenthesis as in &#8220;continue;&#8221; or &#8220;break;&#8221;
  * They both terminate the current execution.

## Differences

Continue only terminates the current iteration whereas break terminates the execution of the entire statement. The difference is easier to see with code examples!

Continue just skips 2 and continues going through the for loop.

<pre class="lang:js decode:true ">for (var i = 0; i &lt; 10; i++) {
  if (i === 2) {
    continue;
  }
  console.log(i);
}

// This returns
// 0
// 1
// 3
// 4
// 5
// 6
// 7
// 8
// 9</pre>

Break stops the entire loop and returns execution control to the program.

<pre class="lang:js decode:true ">for (var i = 0; i &lt; 10; i++) {
  if (i === 2) {
    break;
  }
  console.log(i);
}

// This returns
// 0
// 1</pre>

&nbsp;