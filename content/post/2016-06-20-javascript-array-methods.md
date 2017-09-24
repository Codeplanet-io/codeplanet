---
title: JavaScript array methods
author: Jon Kuperman
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=1056
categories:
  - JavaScript

---
JavaScript array&#8217;s have a ton of cool methods! I&#8217;ve never seen them all listed out before so I figured I&#8217;d give it a shot.

## Array Methods

These are the methods that can be called directly on the Array object.

### Array.from()

Creates a new Array from either an Array-like* or iterable object.

*Array-like means this method **will work** on the arguments object!

<pre class="lang:js decode:true " title="Array.from()">// Turn the arguments object into an Array
function foo() {
  return Array.from(arguments);
}</pre>

### Array.isArray()

Determines whether or not what you passed in **is an array**.

<pre class="lang:js decode:true " title="Array.isArray()">Array.isArray([1]); // Returns true
Array.isArray({});  // Returns false</pre>

## Array Prototype Methods

### Array.prototype.concat()

Create a new Array comprised of the Array concat is called on plus the Array or values it&#8217;s called with.

<pre class="lang:js decode:true " title="Array.prototype.concat()">var first_array = [1, 2, 3];
var second_array = [4, 5, 6];

// Produces [1, 2, 3, 4, 5, 6]
var new_array = first_array.concat(second_array);</pre>

### Array.prototype.copyWithin()

Allows you to copy part of an Array to another location in **the same Array**.

<pre class="lang:js decode:true ">// Returns [4, 5, 3, 4, 5]
[1, 2, 3, 4, 5].copyWithin(0, 3);</pre>

### Array.prototype.entries()

Returns a new Array Iterator of key/value pairs from the Array.

<pre class="lang:js decode:true ">var myArray = ['foo', 'bar', 'baz'];
var entries = myArray.entries();

console.log(entries.next().value); // [0, 'foo']
console.log(entries.next().value); // [1, 'bar']
console.log(entries.next().value); // [2, 'baz']</pre>

### Array.prototype.every()

Tests whether or not each item in the Array passing a test in the callback function.

<pre class="lang:js decode:true">function isEven(element, index, array) {
  return element % 2 == 0;
}

[2, 4, 5, 8, 16].every(isEven); // false</pre>

### Array.prototype.fill()

### Array.prototype.filter()

### Array.prototype.find()

### Array.prototype.findIndex()

### Array.prototype.forEach()

### Array.prototype.includes()

### Array.prototype.indexOf()

### Array.prototype.join()

### Array.prototype.keys()

### Array.prototype.lastIndexOf()

### Array.prototype.map()

### Array.prototype.pop()

### Array.prototype.push()

### Array.prototype.reduce()

### Array.prototype.reduceRight()

### Array.prototype.reverse()

### Array.prototype.shift()

### Array.prototype.slice()

### Array.prototype.some()

### Array.prototype.sort()

### Array.prototype.splice()

### Array.prototype.toLocaleString()

### Array.prototype.toSource()

### Array.prototype.toString()

### Array.prototype.unshift()

### Array.prototype.values()