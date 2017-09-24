---
title: Managing CSS in JavaScript Applications
author: Jon Kuperman
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=1297
categories:
  - CSS
  - JavaScript

---
With an influx of great new JavaScript frameworks (Angular, React and Ember) writing JavaScript applications has gotten a lot easier but managing CSS has become somewhat of a challenge.

## History

Before we get into the challenges of managing CSS in modern JavaScript applications, it would be good to take a quick look at where we&#8217;ve come from. From simple HTML websites through the jQuery / AJAX revolution and now on to enormously complicated JavaScript applications a lot has changed.

### CSS

In the very beginning we didn&#8217;t have much in the way of choices. We had to compose and serve vanilla CSS files. We really only had a few different questions to answer.

  1. Should we serve a single file (via a build step) or multiple files?
  2. Should each page have a unique stylesheet with only what it needs? Or should we just simplify and serve one stylesheet for our entire site?

### LESS / SASS / Stylus

Then, over the years a lot of great tools emerged to making CSS authoring a lot easier.

<img class="alignnone size-full wp-image-1302" src="https://codeplanet.io/wp-content/uploads/2016/09/less-css.jpg" alt="less-css" width="540" height="180" srcset="https://codeplanet.io/wp-content/uploads/2016/09/less-css.jpg 540w, https://codeplanet.io/wp-content/uploads/2016/09/less-css-300x100.jpg 300w" sizes="(max-width: 540px) 100vw, 540px" />

The first big player on the scene was [Less][1], a CSS pre-processor. This means that you can author Less (which looks like CSS but with some cool features) and run it through a program which will output perfectly valid CSS.

### PostCSS

## JavaScript Components

## Bundled Assets

## Two Viable Approaches

### 1 CSS file for component

### CSS in JS

 [1]: http://lesscss.org/