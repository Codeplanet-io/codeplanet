---
title: Firefox won’t submit form not in DOM
author: Jon Kuperman
type: post
date: 2015-12-08T17:00:46+00:00
url: /firefox-wont-submit-form-not-in-dom/
categories:
  - JavaScript

---
Ah, differences between browsers. Am I right?

Today I learned that Firefox will not allow you to submit a form that hasn&#8217;t been attached to the DOM. Let&#8217;s take a look at a quick example.

<pre class="lang:js decode:true">(function() {
  var form = document.createElement('form');
  form.method = 'GET';
  form.action = 'https://path/to/download/file.zip';
  form.submit();
})();</pre>

This code will run as expected in Chrome, downloading file.zip as soon as you hit the page but it will not run in Firefox.

This is because Firefox [won&#8217;t submit forms][1] that aren&#8217;t in the DOM.

An easy fix here would be to just attach it to the DOM like so:

<pre class="lang:js decode:true ">(function() {
  var form = document.createElement('form');
  form.method = 'GET';
  form.action = 'https://path/to/download/file.zip';
  document.body.appendChild(form);
  form.submit();
})();</pre>

And voilà!

( Also you could just use an anchor tag and force a click! )

 [1]: https://stackoverflow.com/questions/5208224/firefox-wont-submit-a-form-created-by-javascript