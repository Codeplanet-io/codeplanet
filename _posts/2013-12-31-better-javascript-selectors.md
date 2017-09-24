---
id: 135
title: Better JavaScript Selectors
date: 2013-12-31T11:00:56+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=135
permalink: /better-javascript-selectors/
image: /wp-content/uploads/2015/12/js-logo.png
categories:
  - Web Development
---
The problem with current JavaScript selectors is that they are too reliant on the DOM. Not only do we turn seemingly arbitrary things like classes and id&#8217;s into necessary elements for application logic, but we often rely too heavily in the DOM&#8217;s current tree, making redesigns much more difficult than need be.

Let&#8217;s start with a simple example of something you probably would see in the wild.

    
    document.querySelector('.title').onclick = function() { 
        this.getElementsByTagName('h1')[0].innerHTML = 'clicked!';
    };
    

This is pretty basic, we are looking for the element with a class of &#8216;title&#8217; and when it&#8217;s clicked we alter the text of the header underneath. Although simple this introduces a number of problems.

  1. We absolutely are reliant on the element keeping it&#8217;s class of &#8216;title&#8217;. This might not be obvious to designers but our application&#8217;s functionality now relies on it.
  2. We are also reliant on the appropriate header being the first h1 underneath that title class. If someone added another h1 before it, our application would break.

As you can see, even a very simple bit of JavaScript can introduce multiple problems when using our current practice for selectors.

## A New Solution

HTML5 has introduced &#8216;data attributes&#8217;, a new way of embedding hidden data on HTML elements. They are very easy to use, for example:

    
    <div class="title" data-attribute="title">
        <h1 data-attribute="header">Welcome To The Website</h1>
    </div>
    

    
    document.querySelector('[data-attribute~=title]').onclick = function() { 
        this.querySelector('[data-attribute~=header]').innerHTML = 'clicked!';
    };
    

This easy change solves our DOM reliance problems that we had before. Using data attributes like this are a clear sign to our designers that the element they are looking at has some special application significance. Additionally, if we add a data attribute to the h1 that we need to alter we can entirely skip our DOM reliance.

## Triggering Custom Events

So we can switch our class / id based selection to data attributes, but we can take this a step further and instead of doing our application logic inside the selector we can just trigger a custom event, keeping our DOM reliance to an absolute minimum.

Check this out:

<pre>&lt;/code>


<div class="title" data-attribute="title">
  <h1 data-attribute="header">
    Welcome To The Website
  </h1>
  
</div>
&lt;/code></pre>

    
    document.querySelector('[data-attribute~=title]').onclick = function() { 
        var event = new CustomEvent('header-click', {bubbles: true});
        this.querySelector('[data-attribute~=header]').dispatchEvent(event);
    };
    
    document.body.addEventListener('header-click', function(e) {
      e.target.innerHTML = 'clicked!';
    }, false);