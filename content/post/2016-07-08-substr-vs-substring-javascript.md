---
title: substr vs. substring in JavaScript
author: Jon Kuperman
type: post
date: 2016-07-08T21:14:15+00:00
url: /substr-vs-substring-javascript/
categories:
  - JavaScript

---
The difference between substr vs. substring in JavaScript bites me more often than any other API confusion in the language. The **only** difference is in the second parameter. Do you know what each of these will return?

<pre class="lang:js decode:true">var word = "The quick brown fox";
console.log(word.substr(5, 10));
console.log(word.substring(5, 10));</pre>

## substr vs. substring

[String.prototype.substr()][1] and [String.prototype.substring()][2] have identical looking APIs in that they both take two parameters and the first parameter for both methods is the numerical index of the string we&#8217;re going to be doing substitutions on. The second parameter is where they differ.

> Substring&#8217;s second parameter is the numerical index on which you stop the substitution; substr&#8217;s second parameter is the length of the substitution.

So, to review the code from above:

<pre class="lang:js decode:true">var word = "The quick brown fox";

// Cut from the 5th character, 10 characters long
console.log(word.substr(5, 10)); // returns "uick brown"

// Cut from the 5th character to the 10th character
console.log(word.substring(5, 10)); // returns "uick "
</pre>

I hope that helps!

 [1]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substr
 [2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring