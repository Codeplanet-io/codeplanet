---
title: 'What I learned while publishing an HTML5 Mobile App, Part 3/5: Distribution and Marketplaces'
author: Thomas Hunter II
type: post
date: 2015-09-30T17:00:03+00:00
url: /what-i-learned-while-publishing-an-html5-mobile-app-part-35-distribution-and-marketplaces/
categories:
  - Mobile Development
tags:
  - Cordova

---
The most tedius port when dealing with each marketplace is acquiring screenshots, especially with iOS.

## iOS / App Store

Cost: $100 / year | Release Approval: 8 Days | Update Approval: _>7 Days ???_

If you want to release apps on the iOS App Store, it&#8217;s going to cost you $100 per year. For some people that&#8217;s not a lot of money. If you&#8217;re a small developer that number could be prohibitive. There&#8217;s another one-time-fee that many overlook, and that is the purchase of an Apple computer. If you&#8217;re like me you&#8217;ve already got a MacBook Pro. If you&#8217;re not like me, you can pick up a [Mac Mini for $500][1].

I submitted SGoL to the App Store on August 26th, and it was approved September 3rd (8 days later). I submitted an update on September 12th, but still haven&#8217;t heard back (at least 7 days). Keeping these numbers in mind and knowing that Apple may very well deny your application can be important to big companies with press releases. However if you&#8217;re an indie game developer the scheduling may not be a big deal. I got lucky and was approved on my first try, YMMV.

At one point I had an issue with my account (Apple calls it an iTunes Connect account for some crazy reason) and I had call Apple Developer support. Apparently my account was fused into another developers account, and their customer database had some referential issues. Another phone call and two hours later I was able to log in. I didn&#8217;t have any issues like this with the other marketplaces, however my accounts on the other marketplaces were much newer.

Capturing screenshots for iOS is a pain in the ass. You&#8217;re going to want to set aside some time to do this. Each device &#8220;screen class&#8221; which you want your application to run on will need at least one screenshot. These screenshots need to be the exact dimensions. The device resolutions I was targeting were represented by the iPhone 4s, iPhone 5, iPhone 6, and iPhone 6+. Since I owned an iPhone 5 I took screenshots from the device, but the others required a lot of time in the iPhone Simulator.

With four device screen classes and five images per device that ended up being 20 screenshots. Luckily the Simulator (which otherwise isn&#8217;t running at native resolution on my device) has a convenient button for capturing screenshots. And of course, capturing them from the device is as easy as holding power and Home.

## Android / Google Play Store

Cost: $25 / once | Release Approval: ASAP | Update Approval: ASAP

When launching my application on August 17th it was immediately approved and available in store. Iterating and getting a dozen new versions into the store was also immediate. Of course this meant I spent less time polishing each build before submitting, and submitted a broken build once or twice (hey, it worked on my machine!)

I own an Android device and was able to take the important screenshots for it. However for more exotic devices I had to run an Emulator. I wasn&#8217;t able to find a method for taking screenshots at the native device resolution, which meant I had to take normal screenshots and carefully crop. Google isn&#8217;t checking exact dimensions (how can they with thousands of devices in each screen class?) For other devices I would take screenshots of browser windows and use that instead.

Building an application for Android requires a few steps to get it working. When submitting to Apple, the Xcode IDE does all the heavy lifting instead. Personally I prefer issuing commands (it means I get to automate everything in a shell script!)

Here&#8217;s a breakdown of my android build script:

<pre class="">#!/bin/sh

# keytool -genkey -v -keystore thomashunter-mobile.keystore -alias thomashuntermobile -keyalg RSA -keysize 2048 -validity 10000
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore thomashunter-mobile.keystore ./platforms/android/build/outputs/apk/android-release-unsigned.apk thomashuntermobile
rm ./platforms/android/build/outputs/apk/strategic-game-of-life-signed.apk
zipalign -v 4 ./platforms/android/build/outputs/apk/android-release-unsigned.apk ./platforms/android/build/outputs/apk/strategic-game-of-life-signed.apk</pre>

Well isn&#8217;t that one complex shell script?! The first, commented out **keytool** command only needs to be executed once. It generates a **.keystore** file which you&#8217;ll need to keep for signing purposes. The **jarsigner** command will apply your key against the APK file (which contains compiled java jar&#8217;s, hence the name). After that I remove the old signed APK (otherwise the next step fails) and finally we run **zipalign**, which as far as I can tell moves a bunch of stuff around inside the APK (one would think that would need to happen _after_ signing).

Building and submitting an Android application can be done from any computer, whether it&#8217;s Apple with OS X, Windows, or Linux.

## Firefox OS / Firefox Marketplace

Cost: $0 | Release Approval: 12 Days | Update Approval: ASAP

The approval period required for the Firefox Marketplace was surprisingly long, being submitted on July 15th and approved on July 27th (12 days later). My guess is that they&#8217;re understaffed. Once an application is approved, and assuming you&#8217;re hosting it on your own servers (which I am; there&#8217;s an option to upload a zip but rumor has it that is going away), updates don&#8217;t require a submission. You can literally update your application by changing files on your server.

Firefox OS requires that you setup a manifest.webapp file at the root of your application which describes some meta information required by the OS. This includes permissions, name, version, etc. Here&#8217;s a copy the [SGoL manifest.webapp file][2]:

<pre class="">{
  "name": "Strategic GoL",
  "version": "0.8.1",
  "description": "Strategic Game of Life: Blah blah blah...",
  "launch_path": "/apps/sgol/index.html",
  "icons": {
    "128": "/apps/sgol/images/meta/app-128.png"
  },
  "developer": {
    "name": "Thomas Hunter II (@tlhunter)",
    "url": "https://thomashunter.name"
  },
  "default_locale": "en",
  "type": "web",
  "chrome": { "navigation": false },
  "fullscreen": "true"
}</pre>

I have a friend who works at Mozilla, and after visiting the office one day and promising to develop apps for it, he hooked me up with a free Flame phone. These are rather hard to come by though. In fact, buying a Firefox OS phone in the United States is all but impossible. This will have massive negative effects on developer adoption, and I hope Mozilla figures this out soon.

<div id="attachment_662" style="width: 670px" class="wp-caption aligncenter">
  <a href="https://codeplanet.io/wp-content/uploads/2015/09/flame-sgol.jpg"><img class="size-large wp-image-662" src="https://codeplanet.io/wp-content/uploads/2015/09/flame-sgol-1024x576.jpg" alt="The Elusive Flame running Strategic Game of Life" width="660" height="371" srcset="https://codeplanet.io/wp-content/uploads/2015/09/flame-sgol-1024x576.jpg 1024w, https://codeplanet.io/wp-content/uploads/2015/09/flame-sgol-300x169.jpg 300w, https://codeplanet.io/wp-content/uploads/2015/09/flame-sgol-768x432.jpg 768w, https://codeplanet.io/wp-content/uploads/2015/09/flame-sgol-1200x675.jpg 1200w" sizes="(max-width: 660px) 100vw, 660px" /></a>
  
  <p class="wp-caption-text">
    The Elusive Flame running Strategic Game of Life
  </p>
</div>

I was able to take screenshots from the physical device and use those for submission. Luckily I didn&#8217;t have to bother using different devices and resolutions.

Being able to submit an application to the Firefox Marketplace for free is awesome, however if you&#8217;re self hosting that means you will need to pay the price of a server. I already have a server so this isn&#8217;t an issue, but keep it in mind. Also, if your server ever goes down then your users will not be able to use your app. Even if you have been diligent about enabling offline mode / caching, new users won&#8217;t be able to download your app for the first time if your server is down.

## Web

Of course, uploading files and hosting them on your own server will cost whatever you are paying for hosting. Changes are immediate and there&#8217;s no marketplace fees as there&#8217;s no real marketplace. You will be in charge of finding your own users. There are some web game marketplaces out there like [Kongregate][3] and [Clay.io][4] (although they may be dead).

There&#8217;s also a manifest file used by Chrome, which is different than the version used by Firefox OS, even though both are supposed to be based on some sort of standard. Here&#8217;s an example of the [SGoL manifest.json file][5]:

<pre class="">{
  "name": "Strategic Game of Life",
  "short_name": "Strategic GoL",
  "version": "0.8.1",
  "description": "Strategic Game of Life: Blah blah blah...",
  "icons": [
  {
    "src": "./images/meta/app-66.png",
    "sizes": "66x66",
    "type": "image/png"
  },{
    "src": "./images/meta/app-76.png",
    "sizes": "76x76",
    "type": "image/png"
  },{
    "src": "./images/meta/app-120.png",
    "sizes": "120x120",
    "type": "image/png"
  },{
    "src": "./images/meta/app-152.png",
    "sizes": "152x152",
    "type": "image/png"
  }
 ],
 "start_url": "./index.html",
 "display": "fullscreen",
 "author": "Thomas Hunter II (@tlhunter)",
 "default_locale": "en",
 "manifest_version": 2
}</pre>

The content is essentially the same as what is used by Firefox OS, though things have been renamed and munged a bit. The cool thing about the Chrome version is that it doesn&#8217;t require special content type headers, something which will make hosting Chrome apps on shared servers easier than Firefox OS apps.

**Discussion**: [Hacker News][6]

 [1]: http://amzn.to/1FU20MX
 [2]: http://zyu.me/apps/sgol/manifest.webapp
 [3]: http://www.kongregate.com/html5-games
 [4]: http://clay.io/
 [5]: http://zyu.me/apps/sgol/manifest.json
 [6]: https://news.ycombinator.com/item?id=10306398