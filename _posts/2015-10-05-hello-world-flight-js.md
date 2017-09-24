---
id: 701
title: Hello World with FlightJS
date: 2015-10-05T10:00:38+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=701
permalink: /hello-world-flight-js/
categories:
  - JavaScript
---
[<img class="aligncenter size-full wp-image-702" src="https://codeplanet.io/wp-content/uploads/2015/10/flightjs.png" alt="flightjs" width="807" height="384" srcset="https://codeplanet.io/wp-content/uploads/2015/10/flightjs.png 807w, https://codeplanet.io/wp-content/uploads/2015/10/flightjs-300x143.png 300w, https://codeplanet.io/wp-content/uploads/2015/10/flightjs-768x365.png 768w" sizes="(max-width: 807px) 100vw, 807px" />](https://codeplanet.io/wp-content/uploads/2015/10/flightjs.png)

For those of you that don&#8217;t know, Twitter has it&#8217;s own [Open Source JavaScript Framework](https://github.com/flightjs/flight). It&#8217;s called [FlightJS](https://flightjs.github.io/) and it&#8217;s pretty cool (I may be biased).

It&#8217;s pretty easy to get started with and the documentation is great, but here&#8217;s a quick &#8220;Hello World&#8221; so you can hit the ground running.

## Installation

For this example, let&#8217;s use the CDN hosted libraries for Flight and it&#8217;s dependency, jQuery. We&#8217;ll start with a simple HTML page.

<pre class="lang:default decode:true">&lt;!DOCTYPE html&gt;
&lt;head&gt;
    &lt;title&gt;Hello World with FlightJS&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div id="hello"&gt;Click Me!&lt;/div&gt;
    &lt;!-- jQuery --&gt;
    &lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"&gt;&lt;/script&gt;
    &lt;!-- Flight release --&gt;
    &lt;script src="http://flightjs.github.io/release/latest/flight.min.js"&gt;&lt;/script&gt;
    &lt;!-- Your script --&gt;
    &lt;script src="js/script.js"&gt;&lt;/script&gt;
&lt;/body&gt;</pre>

## Your First Component

Inside that script.js file, let&#8217;s do something like this.

<pre class="lang:js decode:true">/* Component definition */

var Hello = flight.component(hello);

function hello() {
  this.sayHello = function() {
    alert('Hello World!');
  },

  // after initializing the component
  this.after('initialize', function() {
    this.on('click', this.sayHello);
  });
}

/* Attach the component to a DOM node */

Hello.attachTo('#hello');</pre>

Now load the page and click on the text!

## Understanding Components

Components are fairly simple. This one only consists of four parts.

### The definition

<pre class="lang:js decode:true">var Hello = flight.component(hello);

function hello() {</pre>

### Some number of methods

<pre class="lang:js decode:true">this.sayHello = function() {
    alert('Hello World!');
}</pre>

### Event Listeners

<pre class="lang:js decode:true">this.after('initialize', function() {
    this.on('click', this.sayHello);
});</pre>

### DOM Attachment

<pre class="lang:js decode:true">Hello.attachTo('#hello');</pre>

## Conclusion

That&#8217;s really all there is to it. We make our sayHello method, wrap it in a Flight component, bind it to a click listener and attach it to the DOM.

Stay tuned for a lot more FlightJS tutorials!