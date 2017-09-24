---
id: 404
title: Apply vs. Call vs. Bind in JavaScript
date: 2015-05-16T02:31:26+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=404
permalink: /javascript-apply-vs-call-vs-bind/
image: /wp-content/uploads/2015/12/js-logo.png
categories:
  - JavaScript
tags:
  - JavaScript
---
One of the trickier bits of the language is learning the differences between JavaScript apply vs. call vs. bind. All three of these JavaScript methods allow you to change the value of \`this\` for a given function.

Those methods are [Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call), [Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) and [Function.prototype.bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

They are slightly different but sometimes it&#8217;s difficult to remember which is which.

## TL;DR

  * C[all](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) invokes the function and allows you to pass in arguments one by one.
  * [Apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) invokes the function and allows you to pass in arguments as an array.
  * [Bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) returns a new function, allowing you to pass in a this array and any number of arguments.

## Apply vs. Call vs. Bind Examples

### Call

<pre class="lang:js decode:true " title="An example of call">var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
var person2 = {firstName: 'Kelly', lastName: 'King'};

function say(greeting) {
    console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
}

say.call(person1, 'Hello'); // Hello Jon Kuperman
say.call(person2, 'Hello'); // Hello Kelly King</pre>

### Apply

<pre class="lang:js decode:true" title="An example of apply">var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
var person2 = {firstName: 'Kelly', lastName: 'King'};

function say(greeting) {
    console.log(greeting + ' ' + this.firstName + ' ' + this.lastName);
}

say.apply(person1, ['Hello']); // Hello Jon Kuperman
say.apply(person2, ['Hello']); // Hello Kelly King</pre>

### Bind

<pre class="lang:js decode:true " title="An example of bind">var person1 = {firstName: 'Jon', lastName: 'Kuperman'};
var person2 = {firstName: 'Kelly', lastName: 'King'};

function say() {
    console.log('Hello ' + this.firstName + ' ' + this.lastName);
}

var sayHelloJon = say.bind(person1);
var sayHelloKelly = say.bind(person2);

sayHelloJon(); // Hello Jon Kuperman
sayHelloKelly(); // Hello Kelly King</pre>

## When To Use Each

Call and apply are pretty interchangeable. Just decide whether it&#8217;s easier to send in an array or a comma separated list of arguments.

I always remember which one is which by remembering that **C**all is for comma (separated list) and **A**pply is for Array.

Bind is a bit different. It returns a new function. Call and Apply execute the current function immediately.

Bind is great for a lot of things. We can use it to curry functions like in the above example. We can take a simple hello function and turn it into a helloJon or helloKelly. We can also use it for events like onClick where we don&#8217;t know when they&#8217;ll be fired but we know what context we want them to have.