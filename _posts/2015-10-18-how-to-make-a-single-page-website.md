---
id: 751
title: How to Make a One Page Website
date: 2015-10-18T19:50:57+00:00
author: Kelly King
layout: post
guid: http://codeplanet.io/?p=751
permalink: /how-to-make-a-single-page-website/
image: /wp-content/uploads/2015/10/coder.jpg
categories:
  - CSS
  - HTML
  - JavaScript
---
This tutorial explains how to create a **vertical-scrolling** one page website in four steps. Check out [the demo](http://www.adventuresinwebdesign.com/samples/anchors/blog/)!

## One Page Website Design

There are at least 3 kinds of One Page websites. The basic idea is that all content is placed on one page, but only a portion of it is centered on your computer screen at a given time. Then you can watch the old content slide away when you click a link, instead of loading a whole new page. Often, the scroll bar is still visible on the side, so you could actually drag it up and down and see the whole page at once.

The picture below is a screen shot I took of another designer’s website, Eshbeata.com. His first page starts at the top, the second starts at the image gallery, the third page starts where the dirt begins, and the last page is centered around the ocean:

[<img class="aligncenter wp-image-752 size-full" src="https://codeplanet.io/wp-content/uploads/2015/10/coder.jpg" alt="TheCoder's One Page Website" width="600" height="738" srcset="https://codeplanet.io/wp-content/uploads/2015/10/coder.jpg 600w, https://codeplanet.io/wp-content/uploads/2015/10/coder-244x300.jpg 244w" sizes="(max-width: 600px) 100vw, 600px" />](https://codeplanet.io/wp-content/uploads/2015/10/coder.jpg)

I classified the types of one page websites by the direction/s that the page scrolls. Here is my breakdown, with examples:

**Vertical Scroll** (Most Common)

[Barrel + Barc](http://www.barrelny.com/24/ "Barrel + Barc"), [Beaver Lab](http://www.beaverlab.com/#chi_siamo_a "Beaver Lab"), [Little White Umbrella](http://www.leahjuaymah.com/index.php "Little White Umbrella"), [Eshbeata](http://eshbeata.com/ "Eshbeata")

**Horizontal Scroll**

[Vanity Claire](http://www.vanityclaire.com/ "Vanity Claire"), [Hotel Oxford](http://www.hotel-oxford.ro/en "Hotel Oxford"), [Lomotek](http://www.lomotek.com/article/home "Lomotek")

**2D Scroll**

[Steve & Jacqs](http://steveandjacqs.com/ "Steve & Jacqs")

Once again, this post explains the **vertical** method.

When designing your single page website,  you need to decide the following things:

  1. Will my page start at the top and scroll down <a title="Eshbeata.com" href="http://www.eshbeata.com/" target="_blank">(like this)</a>, start at the bottom and scroll up <a title="Adventures in web design" href="http://www.adventuresinwebdesign.com/samples/anchors/#about" target="_blank">(like this)</a>, or start in the middle, and move all over [(like this)](http://www.beaverlab.com/ "Beaver Lab")?
  2. How will you differentiate each page?
  3. Will the page be a journey, as with Eshbeata&#8217;s site, where you travel from above ground to underwater?
  4. Will each &#8220;page&#8221; have a separate background color?
  5. Will you put a piece of art that defines the border?
  6. No separation at all?
  7. Will there be overlap between the pages?
  8. If you don&#8217;t care about overlap, you don&#8217;t have much to worry about, but if you want each &#8220;page&#8221; to fill everyone&#8217;s screen, you need to add extra margin to the bottom of each &#8220;page&#8221;  to account for different screen sizes.  A netbook might only display 500 pixels, while a 27-inch monitor might display 1200 pixels (depending on the user&#8217;s resolution settings).. I tend to give 1200 pixels if I want to be completely sure only one page will display at a time.

## The HTML

One page website html is actually pretty simple. You’ve seen the FAQ pages that have a list of questions at the top, and then you click one and it takes you to the middle of the page (like <a title="University of Michigan FAQ" href="http://www.law.umich.edu/prospectivestudents/admissions/pages/faq.aspx" target="_blank">this</a>)? That’s the technique we’re going to use.

Basically, you’re going to create a navigation just like normal, except where you normally do an href=&#8221;Link Address&#8221;, instead of a link address, you will put a pound sign followed by the unique id of each &#8220;page&#8221;:

<pre class="lang:default decode:true ">&lt;div id="nav"&gt;
     &lt;ul&gt;
         &lt;li&gt;&lt;a href="#about"&gt;About&lt;/a&gt;&lt;/li&gt;
         &lt;li&gt;&lt;a href="#portfolio"&gt;Portfolio&lt;/a&gt;&lt;/li&gt;
         &lt;li&gt;&lt;a href="#contact"&gt;Contact&lt;/a&gt;&lt;/li&gt;
     &lt;/ul&gt;
&lt;/div&gt;</pre>

This lets the browser know that the link is within the page. (Just think about when you use href=”#” causing the page to refresh – it’s the same idea. The “#” is still telling the browser to load the same page, except when you include text after the # sign, it’s further telling the browser to look for link of that name on the same page, and scroll to that location).

So then if you wanted “three” pages in one, you just create an id for each page in the html. Then, the first thing you do within that div is insert the “id” you specified in the navigation within an anchor tag, like this:

<pre class="lang:default decode:true">&lt;div id="page1"&gt;
  &lt;a id="about" class="smooth"&gt;&lt;/a&gt;
    About page content goes here.
&lt;/div&gt;

&lt;div id="page2"&gt;
  &lt;a id="portfolio" class="smooth"&gt;&lt;/a&gt;
    Portfolio page content goes here.
&lt;/div&gt;

&lt;div id="page3"&gt;
  &lt;a id="contact" class="smooth"&gt;&lt;/a&gt;
    Contact page content goes here.
&lt;/div&gt;</pre>

So that’s it for your html – just add the rest of the html content as you normally would, except it will all go in the same file (likely index.html), and each “page’s” content will go within the appropriate id (#page1, #page2, or #page3).

## The CSS

There is a lot I could tell you about the style sheet for a one page website, but the only crucial thing you need to do is give each page id (#page1, #page2 and #page3 from the HTML example) a height of ~1000 pixels (tall enough to take up a user’s computer screen, unless you want overlap – it’s up to you!). This will cause your total page to be several thousand pixels tall, depending on how many internal pages you have.

The other main consideration is the navigation bar. I tend to make a thin navigation bar (say 70px) that is fixed to the top of the screen, so the user can click between &#8220;pages&#8221; instead of having to use the scrollbar to find their way around (which ruins the fun of a 1-page website for me).

## JQuery Smooth Scroll

In order to make your one page website scroll up and down smoothly using jquery, just paste the following code into your html file, right before the “”. Seriously, that’s it. You don’t need anything in the header, and you don’t need to host a jquery file anywhere on your site. When you click a link in your site that takes you somewhere else **within the same page** it will slide smoothly.

<pre class="lang:default decode:true ">&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"&gt;&lt;/script&gt;
&lt;script src="https://github.com/kswedberg/jquery-smooth-scroll/blob/master/jquery.smooth-scroll.min.js"&gt;&lt;/script&gt;
&lt;script&gt;
$('.smooth').on('click', function() {
    $.smoothScroll({
        scrollElement: $('body'),
        scrollTarget: '#' + this.id
    });
    
    return false;
});
&lt;/script&gt;</pre>

(Thanks to [Karl Swedberg](https://github.com/kswedberg/jquery-smooth-scroll/) for this code!)

## Call To Action

If you appreciated this article, I would be very grateful if you would share it with your friends or leave me a comment. I&#8217;m just getting my start as a blogger and would love to hear what I could be doing better.