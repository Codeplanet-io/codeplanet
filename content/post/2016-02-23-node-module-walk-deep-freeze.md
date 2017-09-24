---
title: 'Node Module Walk-Through: Deep Freeze'
author: Jon Kuperman
type: post
date: 2016-02-23T08:32:57+00:00
url: /node-module-walk-deep-freeze/
categories:
  - JavaScript
  - Node.js

---
Deep freeze is a great module from the prolific [Substack][1]. Before we get into how it works, let&#8217;s talk about what it is.

According to the readme, deep freeze is used to:

> recursively `Object.freeze()` objects

[Object.freeze][2] is a built in JavaScript method that allows you to &#8220;freeze&#8221; an object. According to the docs that means:

> It prevents new properties from being added to it; prevents existing properties from being removed; and prevents existing properties, or their enumerability, configurability, or writability, from being changed.

Let&#8217;s take a look at what this means.

<pre class="lang:js decode:true ">var obj = {
  foo: 'foo',
  bar: 'bar'
};

obj.baz = 'baz';

console.log(obj);

// Logs
// [object Object] {
//   bar: "bar",
//   baz: "baz",
//   foo: "foo"
// }
</pre>

As most of you probably know, you can set new properties on an object or change the existing properties at any time. This is what Object.freeze() prevents. Check out the following example:

<pre class="lang:js decode:true">var obj = {
  foo: 'foo',
  bar: 'bar'
};

Object.freeze(obj);

obj.baz = 'baz'; // Fails silently

console.log(obj);

// Logs
// [object Object] {
//   bar: "bar",
//   foo: "foo"
// }</pre>

Now we can see that with Object.freeze you can no longer change or add properties. However, Objects that are frozen aren&#8217;t quite immutable. Let&#8217;s see another example:

<pre class="lang:js decode:true ">var obj = {
  foo: 'foo',
  bar: 'bar',
  baz: {
    foo2: 'foo2'
  }
};

Object.freeze(obj);

obj.baz = 'baz'; // Won't work

obj.baz.bar2 = 'bar2'; // Will work

console.log(obj);

// Logs
// [object Object] {
//   bar: "bar",
//   baz: [object Object] {
//     bar2: "bar2", // Oh no!
//     foo2: "foo2"
//   },
//   foo: "foo"
// }</pre>

This is where Deep Freeze comes in! It will freeze your object and any objects declared as properties recursively down the three of your object.

## The Code

<pre class="lang:js decode:true ">module.exports = function deepFreeze (o) {
  Object.freeze(o);

  Object.getOwnPropertyNames(o).forEach(function (prop) {
    if (o.hasOwnProperty(prop)
    && o[prop] !== null
    && (typeof o[prop] === "object" || typeof o[prop] === "function")
    && !Object.isFrozen(o[prop])) {
      deepFreeze(o[prop]);
    }
  });
  
  return o;
};</pre>

Let&#8217;s walk through it line by line!

  1. Module exports for Node.js imports
  2. Take in the first object ( named &#8220;o&#8221; ) and freeze it
  3. A blank line!
  4. Get each property on the object and iterate through them
  5. If the property belongs to the object ( not the prototype )
  6. Also if the property is not null
  7. Also if the property is &#8220;object&#8221; type or &#8220;function&#8221; type
  8. And lastly, if the property isn&#8217;t already frozen
  9. Then, run deep freeze on it and all of its properties

 [1]: https://github.com/substack
 [2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze