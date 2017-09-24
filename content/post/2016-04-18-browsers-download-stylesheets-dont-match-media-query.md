---
title: Do browsers download stylesheets when they don’t match media query
author: Jon Kuperman
type: post
date: 2016-04-19T00:33:41+00:00
url: /browsers-download-stylesheets-dont-match-media-query/
categories:
  - Web Development

---
Sorry for the lengthy title! Earlier today I was wondering this:

<blockquote class="twitter-tweet" data-width="550">
  <p lang="en" dir="ltr">
    An example would be:
  </p>
  
  <p>
    <link rel="stylesheet" media="only screen and (min-width: 1024px)" href="foo.css" />
  </p>
  
  <p>
    &mdash; Jon Kuperman (@jkup) <a href="https://twitter.com/jkup/status/722212496652652544">April 18, 2016</a>
  </p>
</blockquote>



So I created a [Github Repo][1] with a reduced test case and ran it on all the major browsers.

<pre class="lang:default decode:true ">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;title&gt;Media queries in link elements&lt;/title&gt;
    &lt;link rel="stylesheet" href="foo.css" /&gt;
    &lt;link rel="stylesheet" media="only screen and (max-width: 500px)" href="bar.css" /&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;h1&gt;Check the console&lt;/h1&gt;
    &lt;h2&gt;How many stylesheets were downloaded?&lt;/h2&gt;
  &lt;/body&gt;
&lt;/html&gt;</pre>

## Results

All across the board, it looks like browsers will not only download the bar.css file but will block page render just like normal until it&#8217;s downloaded. It seems like it might be dangerous to mess around with the rendering process but it would be a cool perf win if browsers could figure out how to skip unnecessary downloads (or at least download them asynchronously!).

 [1]: https://github.com/jkup/browser-tests/tree/master/css-media-query