---
title: 'What I learned while publishing an HTML5 Mobile App, Part 2/5: Performance'
author: Thomas Hunter II
type: post
date: 2015-09-29T17:00:58+00:00
url: /what-i-learned-while-publishing-an-html5-mobile-app-part-25-performance/
categories:
  - Mobile Development
tags:
  - Cordova

---
Running JavaScript and shipping files over a cellular connection for mobile devices is a lot different than running it on your beefy dev machine. Whenever possible you&#8217;ll want to strip down filesize and tweak performance. This is especially true if you plan on releasing your app for Firefox OS (those Flame devices are pretty slow.)

When it comes to minifying and concatenating external CSS and JS resources, consider inlining them inside of your main HTML document if outputting a compiled Cordova app.

## CSS Minifying and Concatenation

CSS Minifying is nice for two reasons, one being that filesize is smaller and another being obfuscation (if you&#8217;re into that sort of thing). The importance of these changes depending on your use cases, particularly if you plan on supporting Firefox OS / Web. Filesize is much less important when you ship a fat compiled Cordova app using an online marketplace (wrapping your web app in Cordova adds a few pounds, err megabytes).

Even though your web app is wrapped up in a compiled package, the contents can still be extracted.

## HTML Minifying and Concatenation

In my project I kept the HTML for each screen stored in a separate file then concatenated each. This kept the codebase clean and reduced conflicts in version control. I also used a templating language so that depending on the platform I was building for I could add or remove different elements.

As an example of elements being removed, the webapp manifest files only need to be included for Web/Firefox OS builds, and would be completely ignored by the Cordova web views. Strip out the meta tags to load the files, and keep the files from making it into the Android/iOS builds.

As for minifying HTML, you can make use of the Tidy project to shrink your document down to size. Personally I didn&#8217;t minify my HTML as I was bit by some rendering issues back in the day, though I&#8217;m sure it&#8217;s not a problem anymore.

## JavaScript Minifying and Concatenation

Chances are you&#8217;re going to end up writing a lot of JavaScript for your project, and that it will likely span a couple dozen files. That makes JS a great candidate for shrinking.

In my project I used a simple Gulp configuration which stripped out comments and whitespace and concatenated files into a single output. That said, using Browserify and Webpack or Closure Compiler would be a lot better. Closure Compiler can do some amazing things with minification and obfuscation.

## No jQuery

Honestly this one won&#8217;t be a big deal for you unless you plan on running your app on weaker hardware, particularly a Firefox OS phone. If you just want to target Android and iOS, feel free to skip this section!

Half way through SGoL, CPU related performance was starting to become an issue. It was very apparent on Firefox OS, noticeable on my two year old Android, and inexistent on my three year old iPhone. Memory usage was a tad bit high as well.

Personally I don&#8217;t rely on 90% of what jQuery has to offer, mostly using it as a DOM selector, which made the switch a breeze. (That said, if you use a LOT of jQuery features, especially jQuery UI, removing jQuery is very likely not an option). There is a badass guide out there called [You Might Not Need jQuery][1] which I have to call out. It made switching item by item a breeze.

I would like to mention though that the guide suggests using document.querySelectorAll(&#8216;selector&#8217;) for selecting elements. That is a blanket statement meant to be the easy replacement for $(&#8216;selector&#8217;). There are several different methods for grabbing different types of elements (e.g. document.getElementById(&#8216;id&#8217;) and document.getElementsByClassName(&#8216;class&#8217;)), each of which will be quicker.

When distributing compiled apps you can&#8217;t simply pull a JS library from a CDN, otherwise there&#8217;s no way your app will work offline. This means shipping libraries such as jQuery with your app, preferably minified and concatenated with everything else. By removing these libraries your application renders that much quicker.

Removing jQuery led to a noticeable performance increase on Firefox OS, and honestly, it just feels good not relying on such a large library.

## Perform All DOM Queries at init

This may or may not seem obvious, and I&#8217;m sure many of you already do this with your web apps. Try to perform all DOM Queries when your application initializes, and don&#8217;t do it any more after that. Assuming you build your application in such a way that you&#8217;re not destroying and recreating similar DOM elements this shouldn&#8217;t be hard to implement.

In SGoL, I have a different object for each screen in the game. The DOM elements for these screens are delivered in the original HTML document and don&#8217;t change too much after that. Here&#8217;s an example constructor from one of my Screen objects:

<pre class="">var CampaignScreen = function() {
  this.screen = document.getElementById('screen-campaign');
  this.levels = this.screen.getElementsByClassName('levels')[0];

  this.buttons = {
    back: this.screen.querySelector('.footer-buttons .back')
  };

  this.buttons.back.onclick = this.onBack.bind(this);
  this.levels.onclick = this.onLevel.bind(this);
};</pre>

There&#8217;s another pattern you&#8217;ll notice here; whenever I query anything in the DOM, if I already have one of its parents cached, I&#8217;ll use that for the query instead of starting from the root. So in this example, I grab a pointer to the entire screen (**this.screen** using an ID selector), then I grab the levels collection (**this.levels** using a class selector from **this.screen**). Each screen has a set of buttons and I group them into a common **this.buttons** object. Finally, event handlers are also added. Since I don&#8217;t destroy screen DOM elements I don&#8217;t have to worry about memory leaks with the handlers.

 [1]: http://youmightnotneedjquery.com/