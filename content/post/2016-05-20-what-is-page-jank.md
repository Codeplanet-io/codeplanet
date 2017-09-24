---
title: What is page jank?
author: Jon Kuperman
type: post
date: 2016-05-20T20:27:22+00:00
url: /what-is-page-jank/
categories:
  - CSS
  - HTML
  - JavaScript

---
What is page jank? According to the [Jank Free][1] website:

> Jank is any stuttering, juddering or just plain halting that users see when a site or app isn&#8217;t keeping up with the refresh rate.

So, essentially, if your users ever notice any awkward movements on your site, that&#8217;s page jank.

## Identifying Page Jank

The [Chrome DevTools][2] can help you identify places where they think jank is occurring. If you run a Timeline recording with Paint selected, you can see little red squares on any frame they think is suffering from page jank.

[<img class="aligncenter wp-image-965 size-full" src="http://codeplanet.io/wp-content/uploads/2016/05/Screen-Shot-2016-05-20-at-12.32.21-PM.png" alt="page jank chrome devtools" width="458" height="247" />][3]

You can also learn how to better identify jank with this fun game by [Jake Archibald][4]!

[Jank Invaders][5]

[<img class="aligncenter wp-image-967 size-full" src="http://codeplanet.io/wp-content/uploads/2016/05/jank.gif" alt="page jank invaders" width="720" height="640" />][6]

&nbsp;

## What Causes Page Jank?

According to the Jank Free quote, page jank is caused _when a site or app isn&#8217;t keeping up with the refresh rate_ &#8211; but what does that really mean?

To understand refresh rate, we need to learn a bit more about browsers and rendering performance. This summary by [Google Developers][7] is the best I&#8217;ve seen.

> Most devices today refresh their screens **60 times a second**. If there’s an animation or transition running, or the user is scrolling the pages, the browser needs to match the device’s refresh rate and put up 1 new picture, or frame, for each of those screen refreshes.
> 
> Each of those frames has a budget of just over 16ms (1 second / 60 = 16.66ms). In reality, however, the browser has housekeeping work to do, so all of your work needs to be completed inside **10ms**. When you fail to meet this budget the frame rate drops, and the content judders on screen. This is often referred to as **jank**, and it negatively impacts the user&#8217;s experience.

The two most common causes of page jank, or not having your work done inside 10ms are [animations][8] and general [layout thrashing][9]. These both boil down to the same thing: Doing DOM reads and writes are expensive, and if we&#8217;re not smart about them we can ask the browser to do too much. Take a look at this example from Wilson Page&#8217;s post on [Preventing Layout Thrashing][9].

<pre class="lang:js decode:true ">// Read
var h1 = element1.clientHeight;

// Write (invalidates layout)
element1.style.height = (h1 * 2) + 'px';

// Read (triggers layout)
var h2 = element2.clientHeight;

// Write (invalidates layout)
element2.style.height = (h2 * 2) + 'px';

// Read (triggers layout)
var h3 = element3.clientHeight;

// Write (invalidates layout)
element3.style.height = (h3 * 2) + 'px';</pre>

In an ideal world, we&#8217;d do all of our reads and writes together to prevent unnecessary layout invalidation. Since that&#8217;s not really a possibility, there are great libraries out there like [fastdom][10] to help us do just that!

## Fixing Page Jank

The basic idea with [fastdom][10] is by making use of [Window.requestAnimationFrame][11]. This method tells the browser you want to do an animation and asks the browser to call your function anytime before the next repaint. Fastdom uses this method to batch all of your reads and writes (referred to as measures and mutates) to ensure we don&#8217;t invalidate the layout more than we need to! Here&#8217;s an example of the fastdom code in action:

<pre class="lang:js decode:true ">fastdom.measure(function() {
  console.log('measure');
});

fastdom.mutate(function() {
  console.log('mutate');
});

fastdom.measure(function() {
  console.log('measure');
});

fastdom.mutate(function() {
  console.log('mutate');
});</pre>

## Resources:

  * <http://www.html5rocks.com/en/tutorials/speed/rendering/>
  * <http://jankfree.org/>
  * <http://www.html5rocks.com/en/tutorials/speed/unnecessary-paints/>
  * <http://www.html5rocks.com/en/tutorials/speed/css-paint-times/>
  * <http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/>
  * <https://github.com/google/skia>
  * <http://wilsonpage.co.uk/preventing-layout-thrashing/>
  * <https://github.com/wilsonpage/fastdom>

 [1]: http://jankfree.org/
 [2]: https://developer.chrome.com/devtools
 [3]: https://codeplanet.io/wp-content/uploads/2016/05/Screen-Shot-2016-05-20-at-12.32.21-PM.png
 [4]: https://twitter.com/jaffathecake
 [5]: https://jakearchibald.github.io/jank-invaders/
 [6]: https://codeplanet.io/wp-content/uploads/2016/05/jank.gif
 [7]: https://developers.google.com/web/fundamentals/performance/rendering/?hl=en
 [8]: http://www.html5rocks.com/en/tutorials/speed/high-performance-animations/
 [9]: http://wilsonpage.co.uk/preventing-layout-thrashing/
 [10]: https://github.com/wilsonpage/fastdom
 [11]: https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame