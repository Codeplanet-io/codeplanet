---
title: image-set – CSS for retina displays
author: Jon Kuperman
type: post
date: 2016-09-01T22:32:58+00:00
excerpt: |
  There are a few different ways to serve higher quality images to screens with retina displays. A new one I just found out about is the CSS image-set function.
  
  At the time of this writing, image-set only works on Chrome and Safari.
url: /css-image-set-retina-displays/
categories:
  - CSS

---
There are a few different ways to serve higher quality images to screens with retina displays. A new one I just found out about is the CSS image-set function.

At the time of this writing, it [only works on Chrome and Safari][1].

<img class="alignnone wp-image-1284 size-large" src="https://codeplanet.io/wp-content/uploads/2016/09/Screen-Shot-2016-09-01-at-3.21.13-PM-1024x473.png" alt="CSS image-set function caniuse" width="1024" height="473" srcset="https://codeplanet.io/wp-content/uploads/2016/09/Screen-Shot-2016-09-01-at-3.21.13-PM-1024x473.png 1024w, https://codeplanet.io/wp-content/uploads/2016/09/Screen-Shot-2016-09-01-at-3.21.13-PM-300x139.png 300w, https://codeplanet.io/wp-content/uploads/2016/09/Screen-Shot-2016-09-01-at-3.21.13-PM-768x355.png 768w, https://codeplanet.io/wp-content/uploads/2016/09/Screen-Shot-2016-09-01-at-3.21.13-PM-1080x499.png 1080w" sizes="(max-width: 1024px) 100vw, 1024px" />

## Image-set Example

The CSS looks a little something like this:

<pre class="lang:css decode:true ">background-image: -webkit-image-set(url(./img/logo.png) 1x,
                                    url(./img/logo.png) 2x,
                                    url(./img/logo.png) 3x);</pre>

The function can take up to three parameters. According to [the W3 spec][2]:

> This example shows how to use ‘<code class="css">image-set()</code>’ to provide an image in three versions: a &#8220;normal&#8221; version, a &#8220;high-res&#8221; version, and an extra-high resolution version for use in high-quality printing (as printers can have _extremely_ high resolution):

So you get your regular image, a retina display one and lastly a high res one to send for printing!

Pretty cool stuff.

 [1]: http://caniuse.com/#feat=css-image-set
 [2]: https://www.w3.org/TR/css4-images/#image-set-notation