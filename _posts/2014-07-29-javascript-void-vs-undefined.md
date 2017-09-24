---
id: 352
title: JavaScript void vs. undefined
date: 2014-07-29T00:08:56+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=352
permalink: /javascript-void-vs-undefined/
image: /wp-content/uploads/2015/12/js-logo.jpg
categories:
  - JavaScript
---
Did you know that JavaScript has a void operator?

<blockquote class="twitter-tweet" lang="en">
  <p>
    Without looking it up, what does the `void` operator in <a href="https://twitter.com/hashtag/JavaScript?src=hash">#JavaScript</a> do? Did you know such a thing existed?
  </p>
  
  <p>
    — Thomas Hunter II (@tlhunter) <a href="https://twitter.com/tlhunter/statuses/493908517535748096">July 28, 2014</a>
  </p>
</blockquote>



Well, [it does](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/void).

## What is it used for

Mostly, I&#8217;ve seen the void operator used to trigger the catch part of a try-catch. Something like this:

<pre class="lang:js decode:true ">try {
    throw void(0);
} catch (e) {
    console.log('This will always run');
}</pre>

The other, and perhaps more common, way of achieving this is to just throw undefined instead of void(0).

So, what&#8217;s the difference?

## undefined vs. void(0)

Well, it turns out back in the day you could actually change the value of the global undefined. That&#8217;s [been changed in JavaScript 1.8.5](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined#Description).

However, you can still use undefined as a variable name as long as it&#8217;s not in the global scope. So, unfortunately, this could be done which would cause problems with your try-catch:

<pre class="lang:js decode:true ">function myObject() {
    var undefined = 'LOL';

    function coolFunction() {
        try {
            throw undefined;
        } catch (error) {
            console.log(error); // 'LOL'
        }
    }
  
    return coolFunction;
}
    
myObject()();</pre>

Honestly, it&#8217;s probably not a very realistic use-case, but it seems like the most common reason I see people using void(0).

&nbsp;

&nbsp;