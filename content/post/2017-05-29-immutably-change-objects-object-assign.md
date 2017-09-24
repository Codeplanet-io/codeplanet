---
title: Immutably change Objects with Object.assign
author: Jon Kuperman
type: post
date: 2017-05-29T22:37:20+00:00
url: /immutably-change-objects-object-assign/
categories:
  - JavaScript

---
Recently I&#8217;ve been working a lot with [Redux][1]. The library mandates immutability which means you have to find an immutable way to do every type of operation (remove an item from an array, change a value in an object, etc).

## How to immutably change a value in an object

ES6 offers a cool method called [Object.assign][2] which lets you copy properties from one (or more) source objects to a target object. Let&#8217;s take a look at how it works!

<pre class="lang:js decode:true ">const firstObject = {
  name: 'Object One',
  bar: () =&gt; { console.log('Hello world!')}
}

const secondObject = Object.assign(
  {},
  firstObject,
  {name: 'Object Two'}
)

console.log(secondObject) // Name will be "Object Two"</pre>

So the first parameter is an empty object (which is what will be returned with all the new properties). After that you can append as many object parameters as you want and just know the latest one will override. So for example:

<pre class="lang:default decode:true ">const firstObject = {
  name: 'Object One',
  bar: () =&gt; { console.log('Hello world!')}
}

const secondObject = Object.assign(
  {},
  firstObject,
  {name: 'Object Two'},
  {name: 'Object Three'}
)

console.log(secondObject) // Name will be "Object Three"</pre>

&nbsp;

 [1]: http://redux.js.org/
 [2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign