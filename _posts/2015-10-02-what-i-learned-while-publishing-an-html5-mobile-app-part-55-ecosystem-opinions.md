---
id: 674
title: 'What I learned while publishing an HTML5 Mobile App, Part 5/5: Ecosystem Opinions'
date: 2015-10-02T10:00:02+00:00
author: Thomas Hunter II
layout: post
guid: http://codeplanet.io/?p=674
permalink: /what-i-learned-while-publishing-an-html5-mobile-app-part-55-ecosystem-opinions/
categories:
  - Mobile Development
tags:
  - Cordova
---
Building Strategic Game of Life was quite a fun experience. Supplementing the Cordova build system with a custom one to allow the building of a web version without Cordova installed is a route I&#8217;m glad I chose. Discovering the differences between the platforms can be a tedious process, but in the end it pays off.

With SGoL out of the way I plan on building many more mobile games and applications using this technology.

Even after learning the platform differences and building a working application, performance is still no where close to what native can provide. As the web matures and the browser wars wage on we&#8217;ll approach native, but we&#8217;ll never catch it. With this in mind, if you yourself are a seasoned developer or you want to write cross-platform apps using open source technology, consider using WebViews for your next project.

## Cordova (Phonegap)

[Apache Cordova](https://cordova.apache.org/) describes itself as &#8220;Apache Cordova is a platform for building native mobile applications using HTML, CSS and JavaScript&#8221;. It provides a set of build tools, native code, JavaScript hooks, a plugin system allowing you to easily consume third party plugins. Cordova is an open source Apache project, and has a relationship with Adobe Phonegap in a way that I don&#8217;t fully understand (I believe the latter is a paid version with feature parity of the former). Your application will run on the device in a native WebView.

I really love the idea behind Cordova. That said, I don&#8217;t love Cordova. There are a lot of sharp edges. Documentation is a bit lacking and it&#8217;s easy to stumble into outdated documentation.

I&#8217;ve opened a pair of bugs in their bugtracker which I have a feeling may never get closed ([CB-9554](https://issues.apache.org/jira/browse/CB-9554) and [CB-9555](https://issues.apache.org/jira/browse/CB-9555)). Both of these relate to playing audio which ships with the exported app. Apparently the Cordova team only ever thought a developer would want to play audio from a remote address via HTTP.

Some features appear to be downright broken. One example is setting your application to be fullscreen (high-level configuration like this happens in a file in the root of the project called **config.xml** which configures the native projects). Setting fullscreen to true and running the application on an iOS device will result in content overlapping the status bar. To fix this one needs to modify Objective-C code in the iOS platform directory and ensure it&#8217;s modified again whenever the project is checked out.

Other iOS bugs include not being able to play music in iOS (see [CB-7599](https://issues.apache.org/jira/browse/CB-7599) for an Objective-C workaround). There were several &#8220;hacks&#8221; like this required to get SGoL (a very simple game) running.

I really want Cordova to be awesome, but I have a feeling the project isn&#8217;t getting the attention it requires. There are plenty of alternatives out there, too. If you&#8217;re making a game and you want to keep writing JavaScript but you don&#8217;t care about having a DOM, you can always look into [Cocos2d-x](http://www.cocos2d-x.org/wiki/Cocos2d-x).  [Titanium](http://www.appcelerator.org/#titanium) lets you build apps using JavaScript and a GUI abstraction written in XML called Alloy. There are many more alternatives, each one good for different use cases.

## Firefox OS

Firefox OS (FxOS) is an operating system built by Mozilla. It has two halves: the backend (Boot2Gecko, bootloader + Gecko rendering engine) and the frontend (Gaia, a bunch of HTML and CSS and JavaScript). Everything you see in the UI of a FxOS phone is rendered web technology. If you want to change how the WiFi listing screen looks on your phone you can check out the Gaia repo and tweak some CSS and run it on your phone.

FxOS is an amazing concept, however, using friendly high level web languages comes with a cost. The performance of FxOS phones are pretty bad. While developing SGoL I used a Flame device, which is intended for use by developers. I&#8217;m fairly certain this is one of the more performance FxOS devices too. The interface is not what one would call snappy. Scrolling through system menus and clicking buttons is a great example of this.

One of the most annoying things that happened while developing SGoL included upgrading the OS. When a user taps the gamefield in SGoL we need to lookup the coordinate of where they clicked. In the previous version of FxOS (and Chrome and Safari) we simply grab the **offsetX** and **offsetY** attributes from the click event and use those. However after the update those attributes were completely missing! Here&#8217;s an example of the workaround SGoL uses:

<pre class="">if ('offsetX' in event && 'offsetY' in event) {
  // WebKit and Firefox Desktop 42.0a2 do have .offsetXY attributes
  raw_x = event.offsetX;
  raw_y = event.offsetY;
} else if ('clientX' in event && 'clientY' in event) {
  // FirefoxOS 42.0a1 does not have .offsetXY attributes
  var rect = this.gamefield.getBoundingClientRect();
  raw_x = event.clientX - rect.left;
  raw_y = event.clientY - rect.top;
}</pre>

Much like Cordova, I really want Firefox OS to be awesome. The ability to point a browser at a URL, click a button, and have that application now be available on the phone is amazing. Like the web itself, the Firefox OS platform truly is open. I&#8217;m certain that as Mozilla continues to develop the platform it will approach its more popular counterparts.

## Mobile Safari (Add to Homescreen)

A lot of this post has been about Cordova, however keep in mind Cordova is just a wrapper around native WebViews. Assuming you&#8217;ve hosted your application somewhere online, simply browse to it from the Mobile Safari browser. Once the page has loaded, click the sharing icon in the center of the lower toolbar and click **Add to Homescreen**. You&#8217;ll be prompted for a name (defaults to a meta tag) and an icon will be provided (also from a meta tag). Now, click the new icon and you will be met with a seemingly-native web app. Here&#8217;s what you&#8217;ll see&#8230;

Playing [HTML5 audio](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML5_audio_and_video) is completely broken. Apparently this is on purpose, Apple doesn&#8217;t want anyone playing audio from a browser. Interestingly enough if you load OGG music files, Mobile Safari will instantly crash. I was able to reproduce this with 100% accuracy in iOS 8. Simply removing the **<audio>** tags resulted in a normally loading pages.

The 300ms click lag is incredibly annoying. As soon as a user uses a web app pretending to be a native app and they encounter this lag they will immediately thing the app is slow. Uncanny Valley kicks in. To combat this you can load a library called [FastClick](https://github.com/ftlabs/fastclick). This isn&#8217;t needed on Android (assuming you set the viewport meta tags) and can be conditionally loaded.

When scrolling content in a browser on iOS, one is able to scroll the content past the edge of the screen. This can be incredibly annoying if the user wants to drag and drop an item in the UI. Luckily there&#8217;s a workaround which isn&#8217;t too intrusive. In SGoL, every element which users should be able to scroll has the class **scrollable** applied to it. What we can do is prevent scrolling on the body, and enable scrolling on scrollable elements:

<pre class="">document.ontouchmove = function(event) {
  event.preventDefault();
};

var scrollables = document.getElementsByClassName('scrollable');

for (var i = 0; i &lt; scrollables.length; i++) {
  scrollables[i].ontouchmove = function(event) {
    event.stopPropagation();
  };
}</pre>

While Mobile Safari has a lot of shortcomings, more than any other platform, on the bright side it does have the fastest JavaScript and rendering performance I&#8217;ve seen.

## Android Chrome (Add to Homescreen)

Much like Mobile Safari, if you launch Chrome on Android, click the menu button, and select **Add to Homescreen**, it too will prompt you for a title (grabbed from meta tag or page title), as well as an icon (grabbed from a meta tag). This app can be launched from the users homescreen and they will see a screen without a browser chrome.

Android is a little different in this regard, however. The bottom screen navigation bar will be visible. Assuming you don&#8217;t want the bar to be visible, you can request fullscreen access and make it go away. This request needs to be the direct result of a users click, otherwise it won&#8217;t work.

<pre class="">body.requestFullscreen();</pre>

For the most part, the users experience is vastly improved over it&#8217;s iOS counterpart. HTML5 Audio works beautifully. There is however one very annoying feature which needs to be disabled. A user can scroll the body past the viewport much like in iOS, however this will actually cause the entire page to reload! To fix it, one needs to do a bit of a hack:

<pre class="">body {
  overflow: hidden;
}</pre>

Then any element you want to be scrollable you&#8217;ll want to set the overflow property to auto. If you did want the entire page content to be scrollable, you&#8217;d want to have one master element at the root of the document that can scroll and use a bunch of properties to make it &#8220;stick to the viewport&#8221;:

<pre class="">.container {
  overflow: auto;
  top: 0px;
  bottom: 0px;
  left: 0px;
  right: 0px;
  position: absolute;
}</pre>

Unfortunately it&#8217;ll take a bit of tweaking to fully understand how to get your DOM structured and working happily on all major platforms. There is no magic bullet CSS framework one can import to make all systems happy.