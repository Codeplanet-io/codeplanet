---
title: Write ALT text like someone’s gonna read it
author: Jon Kuperman
type: post
date: 2014-06-19T03:21:22+00:00
excerpt: "There's a decent chance that you don't even use the alt attribute when creating image tags, even if you do, you're probably not putting a lot of thought into what goes inside."
url: /write-alt-text-like-someones-gonna-read/
categories:
  - HTML

---
## Images

<pre class="toolbar:2 whitespace-before:1 whitespace-after:1 lang:default decode:true">&lt;img src="myImage.png" alt="Alt Text" /&gt;</pre>

If you&#8217;ve ever built a website, there&#8217;s a good chance you&#8217;ve written something like this. A simple image tag using the _alt_ attribute. There&#8217;s a decent chance that you don&#8217;t even use the alt attribute when creating image tags; even if you do, you&#8217;re probably not putting a lot of thought into what goes inside.

## Broken Images

When I first learned about the alt attribute, I was told that if for whatever reason your image should fail to load, the alt text is all your users would see. So, I began creating images like this:

<pre class="toolbar:2 whitespace-before:1 whitespace-after:1 lang:default decode:true">&lt;img src="myImage.png" alt="Tree" /&gt;</pre>

## Search Engines

Later in my career I learned about the mysterious ways in which search engines work. I was told that if you want your images to show up well in Google image searches, you must have good keywords in your alt text. So, I began creating images like this:

<pre class="toolbar:2 whitespace-before:1 whitespace-after:1 lang:default decode:true">&lt;img src="myImage.png" alt="San Francisco web developers tree" /&gt;</pre>

## Accessibility

At this point in my career I have tests in place to make sure my images are always served, and I really just don&#8217;t care about SEO anymore. I have, however, begun to care a lot about web accessibility. I want the websites I create to be accessible to all types of devices. Most importantly, I want my alt text to adequately describe my image if the page is being consumed by some sort of screen reader. For the time being, I create my images like this:

<pre class="toolbar:2 whitespace-before:1 whitespace-after:1 lang:default decode:true">&lt;img src="myImage.png" alt="A large tree" /&gt;</pre>

What about you? Do you add alt text to all of your images? What are your priorities? Leave a comment!