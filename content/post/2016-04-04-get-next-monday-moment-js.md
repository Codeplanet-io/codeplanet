---
title: Moment.js, get the next day of the week
author: Jon Kuperman
type: post
date: 2016-04-05T05:00:54+00:00
url: /get-next-monday-moment-js/
categories:
  - JavaScript

---
Moment.js is a [JavaScript library][1] that helps you do pretty much anything you could ever need with dates! Specifically, it helps you parse, validate, manipulate, and display dates in JavaScript.

&nbsp;

Today I was writing a little program and I needed to find the date of the &#8220;next Monday&#8221;. If today is Monday, it should return today.** **If today is Tuesday &#8211; Sunday, it should return the following Monday.

Here&#8217;s how you can do that with Moment.js!

## Install Moment.js

Moment can be installed using all of the popular package managers. I installed it with npm like this:

<pre class="lang:default decode:true ">npm install moment --save</pre>

## Days as numbers

The JavaScript Date object has a [getDay() method][2] which returns a number for which day of the week it currently is. Sunday is 0, Monday is 1 and so on. So we can do something like this:

<pre class="lang:default decode:true ">// Require Moment.js
const moment    = require('moment')
const dayNumber = 1 // 1 for Monday, 2 for Tuesday, use whatever day you need!

// Get a Date object for the next Monday
const nextDay = moment().day(dayNumber) // returns a moment date object

// Format it if you want!
console.log(nextDay.format() // something like 2016-04-05T21:59:19-07:00

</pre>

&nbsp;

 [1]: http://momentjs.com/
 [2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getDay