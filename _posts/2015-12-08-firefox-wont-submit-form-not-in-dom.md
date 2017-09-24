---
id: 817
title: 'Firefox won&#8217;t submit form not in DOM'
date: 2015-12-08T10:00:46+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=817
permalink: /firefox-wont-submit-form-not-in-dom/
image: /wp-content/uploads/2015/12/firefox.png
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

This is because Firefox [won&#8217;t submit forms](https://stackoverflow.com/questions/5208224/firefox-wont-submit-a-form-created-by-javascript) that aren&#8217;t in the DOM.

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