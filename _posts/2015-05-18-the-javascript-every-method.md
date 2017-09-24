---
id: 410
title: The JavaScript every Method
date: 2015-05-18T22:53:44+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=410
permalink: /the-javascript-every-method/
image: /wp-content/uploads/2015/12/js-logo.jpg
categories:
  - JavaScript
tags:
  - JavaScript
---
For those of you not familiar, [Array.prototype.every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) is a method that tests every element in an array against whatever callback function you pass in.

It&#8217;s perhaps most similar to [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) but there are two key differences:

  1. It returns a boolean whereas filter returns a new Array.
  2. The boolean is determined by whether or not **all** items in the array pass the test function.

## A Quick Example

<pre class="lang:js decode:true">function isEven(number, index, array) {
  return number % 2 === 0;
}
console.log([10, 11, 12, 13, 14].every(isEven)); // false
console.log([10, 12, 20, 22, 30].every(isEven)); // true</pre>

As you can see, every returns false if any item in the array is odd.

## Comparing Map and Filter

Where Map and Filter return new arrays, every just returns a boolean. This means that every won&#8217;t work for method chaining and can only be used to make sure every item in your array passes a certain test.