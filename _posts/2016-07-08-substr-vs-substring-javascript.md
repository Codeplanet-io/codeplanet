---
id: 1221
title: substr vs. substring in JavaScript
date: 2016-07-08T21:14:15+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=1221
permalink: /substr-vs-substring-javascript/
image: /wp-content/uploads/2016/07/Screen-Shot-2016-07-08-at-1.07.03-PM.png
categories:
  - JavaScript
---
The difference between substr vs. substring in JavaScript bites me more often than any other API confusion in the language. The **only** difference is in the second parameter. Do you know what each of these will return?

<pre class="lang:js decode:true">var word = "The quick brown fox";
console.log(word.substr(5, 10));
console.log(word.substring(5, 10));</pre>

## substr vs. substring

[String.prototype.substr()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substr) and [String.prototype.substring()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring) have identical looking APIs in that they both take two parameters and the first parameter for both methods is the numerical index of the string we&#8217;re going to be doing substitutions on. The second parameter is where they differ.

> Substring&#8217;s second parameter is the numerical index on which you stop the substitution; substr&#8217;s second parameter is the length of the substitution.

So, to review the code from above:

<pre class="lang:js decode:true">var word = "The quick brown fox";

// Cut from the 5th character, 10 characters long
console.log(word.substr(5, 10)); // returns "uick brown"

// Cut from the 5th character to the 10th character
console.log(word.substring(5, 10)); // returns "uick "
</pre>

I hope that helps!