---
id: 705
title: Upgrading FlightJS
date: 2015-10-06T10:00:16+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=705
permalink: /upgrading-flightjs/
image: /wp-content/uploads/2015/10/flightjs.png
categories:
  - JavaScript
---
[<img class="aligncenter size-full wp-image-702" src="https://codeplanet.io/wp-content/uploads/2015/10/flightjs.png" alt="flightjs" width="807" height="384" srcset="https://codeplanet.io/wp-content/uploads/2015/10/flightjs.png 807w, https://codeplanet.io/wp-content/uploads/2015/10/flightjs-300x143.png 300w, https://codeplanet.io/wp-content/uploads/2015/10/flightjs-768x365.png 768w" sizes="(max-width: 807px) 100vw, 807px" />](https://codeplanet.io/wp-content/uploads/2015/10/flightjs.png)

Flight 2.x is actively being developed. In the meantime, if you&#8217;re on an old version of Flight 1.x and looking to upgrade to the most recent version, this guide is for you!

## Upgrade Core

First, head over to the \[FlightJS Github\](https://github.com/flightjs/flight) and replace your current core files with the most up to date versions.

## Changes

### this.defaultAttrs

There&#8217;s really only one big change as Flight moves into 2.x. <code>this.defaultAttrs</code> is being replaced with <code>this.attributes</code>.

### The 1.x Way

This is how things work in Flight 1.x

<pre class="lang:js decode:true">/* Component definition */

var Hello = flight.component(hello);

function hello() {

  this.defaultAttrs({
    name: 'Jon Kuperman'
  });

  this.sayHello = function() {
    alert('Hello ' + this.attr.name);
  },

  // after initializing the component
  this.after('initialize', function() {
    this.on('click', this.sayHello);
  });
}

/* Attach the component to a DOM node */

Hello.attachTo('#hello');</pre>

### The 2.x Way

The Flight 2.x version isn&#8217;t too different at first glance. You simply change:

<pre class="lang:js decode:true">this.defaultAttrs({
  name: 'Jon Kuperman'
});</pre>

to

<pre class="lang:js decode:true">this.attributes({
  name: 'Jon Kuperman'
});</pre>

## A small gotcha

For the most part, a find and replace will take care of your problems. However there is a small gotcha you should be aware of. In Flight 1.x you can do something like this:

<pre class="lang:js decode:true ">/* Component definition */

var Hello = flight.component(hello);

function hello() {

  this.defaultAttrs({
    firstName: 'Jon'
  });

  this.sayHello = function() {
    alert('Hello ' + this.attr.firstName + ' ' + this.attr.lastName);
  },

  // after initializing the component
  this.after('initialize', function() {
    this.on('click', this.sayHello);
  });
}

/* Attach the component to a DOM node */

Hello.attachTo('#hello', {lastName: 'Kuperman'});</pre>

This is a pretty common pattern for passing in attributes on the component attach but it will throw an error in Flight 2.x. Starting in 2.x, you can&#8217;t pass attributes into a component that aren&#8217;t defined. They don&#8217;t have to have their values set but they need to be defined in the <code>this.attributes</code>.

So you&#8217;ll have to change:

<pre class="lang:js decode:true">this.defaultAttrs({
  firstName: 'Jon'
});</pre>

to

<pre class="lang:js decode:true">this.attributes({
  firstName: 'Jon',
  lastName: null
});</pre>

so it will be happy.

Those are really the only gotcha&#8217;s you need to be mindful of when upgrading your version of FlightJS.

Good luck!