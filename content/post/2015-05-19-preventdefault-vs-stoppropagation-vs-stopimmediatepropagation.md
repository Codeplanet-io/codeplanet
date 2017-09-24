---
title: preventDefault vs. stopPropagation vs. stopImmediatePropagation
author: Jon Kuperman
type: post
date: 2015-05-20T04:52:56+00:00
url: /preventdefault-vs-stoppropagation-vs-stopimmediatepropagation/
categories:
  - JavaScript

---
Three similar and often confused methods. Let&#8217;s explore the different between:

  * Event.preventDefault()
  * Event.stopPropagation()
  * Event.stopImmediatePropagation()

## Summary

First off, let&#8217;s check out the MDN Summaries.

  * **preventDefault: **Cancels the event if it is cancelable, without stopping further propagation of the event.
  * **stopPropagation: **Prevents further propagation of the current event.
  * **stopImmediatePropagation: **Prevents other listeners of the same event from being called.

## Event.preventDefault

Let&#8217;s look at a code example. We know that clicking the submit button on a form submits it to the form handler. Event.preventDefault is a perfect way to not submit a form when the submit button is clicked.

<pre class="lang:default decode:true">&lt;form id="myForm" action="/my-handling-form-page" method="post"&gt;
    &lt;div&gt;
        &lt;label for="name"&gt;Name:&lt;/label&gt;
        &lt;input type="text" id="name" /&gt;
    &lt;/div&gt;
    &lt;div&gt;
        &lt;label for="mail"&gt;E-mail:&lt;/label&gt;
        &lt;input type="email" id="mail" /&gt;
    &lt;/div&gt;
    &lt;div&gt;
        &lt;label for="msg"&gt;Message:&lt;/label&gt;
        &lt;textarea id="msg"&gt;&lt;/textarea&gt;
    &lt;/div&gt;
    
    &lt;div class="button"&gt;
        &lt;button type="submit"&gt;Send your message&lt;/button&gt;
    &lt;/div&gt;
&lt;/form&gt;</pre>

<pre class="lang:js decode:true">$('#myForm').on('submit', function(e) {
    e.preventDefault(); // Now nothing will happen
});</pre>

Event.preventDefault will ensure that the form is never submitted, but it won&#8217;t control or prevent that submit or click event from bubbling up. That&#8217;s what the other two are for.

## Event.**stopPropagation**

stopPropagation ensures that the event doesn&#8217;t bubble any further. Let&#8217;s look at another code example:

<pre class="lang:default decode:true">&lt;div class="container"&gt;
    &lt;a href="#" class="element"&gt;Click Me!&lt;/a&gt;
&lt;/div&gt;</pre>

<pre class="lang:js decode:true">$('.container').on('click', function(e) {
    console.log('container was clicked');
});

$('.element').on('click', function(e) {
    e.preventDefault(); // Now link won't go anywhere
    console.log('element was clicked');
});</pre>

Now if you were to click the link with the console open, you would see:

<pre class="lang:js decode:true ">"element was clicked"
"container was clicked"</pre>

Now let&#8217;s add Event.stopPropagation:

<pre class="lang:js decode:true">$('.container').on('click', function(e) {
    console.log('container was clicked');
});

$('.element').on('click', function(e) {
    e.preventDefault(); // Now link won't go anywhere
    e.stopPropagation(); // Now the event won't bubble up
    console.log('element was clicked');
});</pre>

And click the link again. This time we see:

<pre class="lang:js decode:true ">"element was clicked"</pre>

## Event.**stopImmediatePropagation**

This gets you 90% of everything you&#8217;ll need as far as manipulating events. But let&#8217;s pose a last use case that can prove difficult.

We&#8217;ll start off with similar markup, except we&#8217;ll give the anchor two classes. A generic one, _item_, that all anchors in this area will get, and a specific one, _element_, that&#8217;s very important for our application to work.

<pre class="lang:default decode:true ">&lt;div class="container"&gt;
    &lt;a href="#" class="item element"&gt;Click Me!&lt;/a&gt;
&lt;/div&gt;</pre>

And we&#8217;ll add our nifty Event.stopPropagation we learned about in the last section!

<pre class="lang:js decode:true">$('.item').on('click', function(e) {
    console.log('an item was clicked');
});

$('.element').on('click', function(e) {
    e.preventDefault(); // Now link won't go anywhere
    e.stopPropagation(); // Now the event won't bubble up
    console.log('element was clicked');
});</pre>

But, when we click on the element we see:

<pre class="lang:js decode:true ">"an item was clicked"
"element was clicked"</pre>

The problem here is that item and element are evenly ranked in the DOM. It&#8217;s not as though it hits element and then bubbles up to container like we saw in the last example. Since the click event fires on both element and item at the same time, you cannot stopPropagation like you&#8217;d expect.

This is where stopImmediatePropagation comes in handy!

<pre class="lang:js decode:true">$('.element').on('click', function(e) {
    e.preventDefault(); // Now link won't go anywhere
    e.stopImmediatePropagation(); // Now item on click won't fire
    console.log('element was clicked');
});

$('.item').on('click', function(e) {
    console.log('an item was clicked');
});</pre>

Now one important thing to note here is: Battles over immediate propagation go to the first one declared in your script ( or series of scripts ). So as you may have noticed, in order to get stopImmediatePropagation working we had to switch the listeners so that element comes before item!

Let&#8217;s run it one last time and we should see:

<pre class="lang:default decode:true">"element was clicked"</pre>