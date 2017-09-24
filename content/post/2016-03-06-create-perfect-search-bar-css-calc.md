---
title: Create a perfect search bar with CSS Calc
author: Jon Kuperman
type: post
date: 2016-03-06T17:00:01+00:00
url: /create-perfect-search-bar-css-calc/
categories:
  - CSS

---
This is a neat trick with CSS3&#8217;s [calc function][1]. Let&#8217;s say you&#8217;re trying to build a search form and you want the submit button and the text input to float next to each other.

To start off with, let&#8217;s just create a simple form:

<pre class="lang:default decode:true ">&lt;form&gt;
  &lt;input class="form-control" type="text" placeholder="Search this site.." /&gt;
  &lt;input class="btn btn-primary form-control" type="submit" value="Search" /&gt;
&lt;/form&gt;</pre>

<a href="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-3.02.11-PM.png" rel="attachment wp-att-875"><img class="aligncenter size-full wp-image-875" src="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-3.02.11-PM.png" alt="Screen Shot 2016-03-05 at 3.02.11 PM" width="640" height="78" srcset="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-3.02.11-PM.png 640w, https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-3.02.11-PM-300x37.png 300w" sizes="(max-width: 640px) 100vw, 640px" /></a>

In the past, the way we get them to float nicely is to assign them each a fluid, percent based, width. Something like:

<pre class="lang:css decode:true">input[type="text"] {
  width: 70%;
  float: left;
}

input[type="submit"] {
  width: 30%;
  float: left;
}</pre>

Which looks pretty good!

<a href="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-4.04.51-PM.png" rel="attachment wp-att-876"><img class="aligncenter size-full wp-image-876" src="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-4.04.51-PM.png" alt="Screen Shot 2016-03-05 at 4.04.51 PM" width="641" height="44" srcset="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-4.04.51-PM.png 641w, https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-4.04.51-PM-300x21.png 300w" sizes="(max-width: 641px) 100vw, 641px" /></a>

If you do width 70% and 30% there is not guarantee the text will be readable, especially if the button text is long. 30% could well be less width than the text needs.

## The Solution

With CSS calc you can give the button a fixed width and give the remaining width to the input. Check this out!

<pre class="lang:css decode:true">input[type="text"] {
  width: calc(100% - 100px);
  float: left;
}

input[type="submit"] {
  width: 100px;
  float: left;
}
</pre>

This will keep your button a set width, and grow and shrink the text input as needed!

<a href="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-8.51.45-PM.png" rel="attachment wp-att-882"><img class="aligncenter size-full wp-image-882" src="https://codeplanet.io/wp-content/uploads/2016/03/Screen-Shot-2016-03-05-at-8.51.45-PM.png" alt="Screen Shot 2016-03-05 at 8.51.45 PM" width="265" height="86" /></a>

 [1]: https://developer.mozilla.org/en-US/docs/Web/CSS/calc