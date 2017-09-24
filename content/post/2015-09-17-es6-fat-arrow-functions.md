---
title: ES6 Fat Arrow Functions
author: Jon Kuperman
type: post
date: 2015-09-17T17:00:40+00:00
url: /es6-fat-arrow-functions/
categories:
  - JavaScript

---
Like it or not, ES6 and it&#8217;s **many** features are coming to a browser near you soon &#8211; if they&#8217;re not [implemented already][1]!

The good news we&#8217;ll cover today? You (basically) never have to type the word &#8220;function&#8221; again! Think of all the time you&#8217;ll save!

## Fat Arrow Functions

Let&#8217;s dive into some examples, comparing the ES5 way of doing things to the ES6 way.

<pre class="lang:js decode:true ">// Mapping over an array
var arr = [1, 2, 3, 4, 5];

// ES5
arr.map(function(number) { return number * 2 });

// ES6
arr.map(number =&gt; number * 2);

// Think of the savings!</pre>

Check out how we can do [IIFE&#8217;s][2] with ES6!

<pre class="lang:default decode:true  ">// ES5
(function () {
  console.log('Immediately-Invoked Function Expression');
})();

// ES6

() =&gt; {
  console.log('Immediately-Invoked Function Expression');
}();

// You're welcome, fingers!</pre>

## Lexical this

One big difference to take note of is that unlike the functions you&#8217;re used to, fat arrow functions have a lexically bound _this_.

Let&#8217;s demonstrate this with an age old JavaScript problem.

<pre class="lang:js decode:true">// Say you have a global variables named foo
var foo = 'I am global';

// Then you have a function named Bar
function Bar() {

 // Bar has it's own variable named foo
 this.foo = 'I am local to bar';

 // Bar has a setTimeout inside of it
 setTimeout(function log() {
 // Current scope is bound to the window, so this will console log
 console.log(this.foo); // I am global
 }, 1000);
}

var baz = new Bar();</pre>

In the past, this giant pain had to be solved by binding Game&#8217;s \`this\` to the setInterval or doing something hacky like _var self = this;_ outside the setInterval. Now with fat arrow functions it works like you&#8217;d thing it would.

<pre class="lang:js decode:true ">// Say you have a global variables named foo
var foo = 'I am global';

// Then you have a function named Bar
function Bar() {

 // Bar has it's own variable named foo
 this.foo = 'I am local to bar';

 // Bar has a setTimeout inside of it
 setTimeout(() =&gt; {
 // Current scope is now set to Bar, so it console logs
 console.log(this.foo); // I am local to bar
 }, 1000);
}

var baz = new Bar();</pre>

While this is great for our particular use case, it&#8217;s important to remember whenever using fat arrow functions.

 [1]: http://kangax.github.io/compat-table/es6/
 [2]: http://benalman.com/news/2010/11/immediately-invoked-function-expression/