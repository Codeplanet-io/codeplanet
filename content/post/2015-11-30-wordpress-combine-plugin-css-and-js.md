---
title: WordPress combine plugin CSS and JS
author: Jon Kuperman
type: post
date: 2015-11-30T17:00:10+00:00
excerpt: "If you're like me, you probably have at least one WordPress site with at least 5 plugins. Honestly, I have about ten different WordPress sites. Some of them have over 10 plugins. While all this functionality is great, it comes at a cost!"
url: /wordpress-combine-plugin-css-and-js/
categories:
  - WordPress

---
If you&#8217;re like me, you probably have at least one WordPress site with at least 5 plugins. Honestly, I have about ten different WordPress sites. Some of them have over 10 plugins. While all this functionality is great, it comes at a cost!

## The Problem

You see, each plugin typically brings with it at least one CSS file and one JavaScript file. So, if your WordPress site has 10 plugins, that&#8217;s 10 additional CSS and JS files.

The problem here is with the way HTTP works. To over-simplify, the more requests your website needs to load, the slower it&#8217;s going to be. For this reason, custom developed sites typically minify and concatenate all of their CSS and JS files together so they only have one CSS request and one JavaScript request.

The problem is we can&#8217;t really do that with a WordPress site because we can&#8217;t control the CSS and JS that plugins use. They update frequently so it would not be a good idea to copy the contents and paste them into your giant concatenated file.

## The Solution

Fortunately, as is usually the case, there is a [great free plugin][1] available to do just that for us! It&#8217;ll check all your plugins, take the up to date CSS and JS and stick it all in one minified concatenated bundle!

Check out the difference having done nothing but install Better WordPress Minify.

### Before (54 Requests)

[<img class="aligncenter size-full wp-image-793" src="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.29.33-PM.png" alt="Screen Shot 2015-11-28 at 7.29.33 PM" width="615" height="213" srcset="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.29.33-PM.png 615w, https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.29.33-PM-300x104.png 300w" sizes="(max-width: 615px) 100vw, 615px" />][2]

### After (36 Requests)

[<img class="aligncenter size-full wp-image-794" src="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.30.02-PM.png" alt="Screen Shot 2015-11-28 at 7.30.02 PM" width="616" height="212" srcset="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.30.02-PM.png 616w, https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.30.02-PM-300x103.png 300w" sizes="(max-width: 616px) 100vw, 616px" />][3]

I think that&#8217;s a pretty great win for just installing one plugin!

Go out, download [Better WordPress Minify][1] and speed up your site!

 [1]: https://wordpress.org/plugins/bwp-minify/
 [2]: https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.29.33-PM.png
 [3]: https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.30.02-PM.png