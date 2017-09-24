---
title: 'What I learned while publishing an HTML5 Mobile App, Part 1/5: Development and Debugging'
author: Thomas Hunter II
type: post
date: 2015-09-28T17:00:17+00:00
url: /what-i-learned-while-publishing-an-html5-mobile-app-part-15-development-and-debugging/
categories:
  - Mobile Development
tags:
  - Cordova

---
This series of posts is based on knowledge I gained after releasing Strategic Game of Life (SGoL) for [iOS][1], [Android][2], and [FirefoxOS][3]. SGoL is built using Apache Cordova, which is the open source component (aka majority) of Adobe&#8217;s Phonegap framework. This framework lets web developers use their years of HTML/JS/CSS experience and release apps for every major mobile platform.

Cordova strips out the browser chrome as well as provides a set of JavaScript APIs which allow your application code to talk to native device components by including their **cordova.js** file in your app. Cordova does provide a way to create a build for the FirefoxOS platform, however one of the philosophical requirements for my project is that the developer shouldn&#8217;t actually need Cordova installed to build for the open web. For this reason I use a separate build task for creating Web/FirefoxOS builds which don&#8217;t require **cordova.js**.

This post will be mostly high level, not providing code examples unless necessary to get the point across. If you would like to read a bunch of code, check out my other article [Tips for Building Mobile Games in HTML5][4] or simply wait until I open source SGoL.

As you may have guessed, developing a web-based application using a laptop to run on a phone isn&#8217;t the same as developing a website using a laptop to run on a laptop.

## Simple Node.js Server

Whenever I&#8217;m doing local development I will spin up a simple Node.js server to read files from the filesystem and spit them back out to the browser. If you try to run the files directly from your filesystem you&#8217;re going to have a bad time. Specifically, issues regarding [CORS][5] as well as needing to set content type headers will get in your way. AJAX requests are just not going to work.

When a useragent requests the manifest.webapp file (required for FirefoxOS), you&#8217;ll need to set the Content-Type header to application/x-web-app-manifest+json. Assuming you&#8217;re using an Express app, you can do something like this:

<pre class="lang:js decode:true">app.get('/manifest.webapp', function(req, res) {
  res.type('application/x-web-app-manifest+json');
  res.sendFile(public_dir + '/manifest.webapp');
});</pre>

When a useragent requests a file using AJAX, you&#8217;re going to want to set some CORS headers:

<pre class="lang:js decode:true ">app.get('/data', function (req, res) {
  res.header("Access-Control-Allow-Origin", "*");
  res.send(content);
});</pre>

And of course, any other request can simply return files from your filesystem, and Express should figure out the proper content type for you:

<pre class="lang:js decode:true ">app.use(express.static(public_dir));</pre>

Of course, this should only be done for building a local development server. Once your content is in your Cordova application it won&#8217;t need to come from a server, except for data that you want to keep live (e.g. from a CMS, more on that later).

Also, if Node.js isn&#8217;t your cup of tea, feel free to serve content from any local webserver of your choosing. Apache or NGINX will work just fine.

## Chrome Developer Console + Mobile Viewport

This is the easiest way to debug your app is to open Chrome, then open the Developer Console (Cmd + Opt + I or Ctrl + Shift + I) and click the little phone icon (shown as blue in my screenshot). The screen will resize and you&#8217;ll want to refresh so everything is up to date.

At the top of the screen you&#8217;ll see a dropdown where you can select a device to &#8220;emulate&#8221;, which just means it&#8217;ll resize the viewport and spoof the user agent. About 95% of my development time on SGoL was spent in this view while pointed at a local web server.

[<img class="aligncenter wp-image-627 size-large" src="https://codeplanet.io/wp-content/uploads/2015/09/chrome-inspector-mobile-1024x263.png" alt="chrome-inspector-mobile" width="660" height="170" srcset="https://codeplanet.io/wp-content/uploads/2015/09/chrome-inspector-mobile-1024x263.png 1024w, https://codeplanet.io/wp-content/uploads/2015/09/chrome-inspector-mobile-300x77.png 300w, https://codeplanet.io/wp-content/uploads/2015/09/chrome-inspector-mobile-768x198.png 768w, https://codeplanet.io/wp-content/uploads/2015/09/chrome-inspector-mobile.png 1108w" sizes="(max-width: 660px) 100vw, 660px" />][6]

You can click and drag on the screen to drag the screen content, just like a real device. You&#8217;ll even notice your cursor is now different to emphasize you&#8217;re mouse is a finger. Unfortunately this doesn&#8217;t mimic many of the more complex mobile interactions, such as two finger gestures and other subtle (annoying) mobile browser features.

Chrome is of course best used for debugging Android JS and Rendering.

## Chrome Device Inspector

Chrome has an amazing tool built-in which you can use right now by visiting <chrome://inspect/#devices> from your computer. This tool requires you to have an Android device, the device is plugged into your computer via USB, and you have Android USB debugging enabled. And of course, you&#8217;ll want to launch your app.

This tool is particularly useful because it can debug your web app before it&#8217;s even packaged as a Cordova app. This tool is mostly useful for debugging Android web apps, as it hooks into the Android rendering engine, but it can also be useful for debugging some issues which may affect Cordova on any device.

Once you visit that screen you will see a listing of WebView&#8217;s which can be debugged:

[<img class="aligncenter size-full wp-image-623" src="https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-devices.png" alt="chrome-debug-devices" width="518" height="206" srcset="https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-devices.png 518w, https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-devices-300x119.png 300w" sizes="(max-width: 518px) 100vw, 518px" />][7]

This listing will show you both webpages opened using Chrome (as seen in my screenshot) as well as compiled APK apps with debug mode enabled (more on that later). Once you click the Inspect link below your WebView you will see a mirror of the DOM on the Android screen displayed on your screen:

[<img class="aligncenter size-medium wp-image-622" src="https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-app-300x197.png" alt="chrome-debug-app" width="300" height="197" srcset="https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-app-300x197.png 300w, https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-app-768x504.png 768w, https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-app.png 836w" sizes="(max-width: 300px) 100vw, 300px" />][8]

Now, you do have to take this screen with a grain of salt. It won&#8217;t display native modal&#8217;s such as alert and confirm dialogs, and more importantly, it won&#8217;t display rendered canvas elements. Audio won&#8217;t play either. These shortcomings aside, you get a fully interactive console which will interact with the device, and is by far the easiest way to access device logs.

## Firefox Developer Console + Responsive Layout

Firefox also has a developer console (Press Cmd + Shift + I or Ctrl + Shift + I). I&#8217;m using the Firefox Developer Edition browser so I&#8217;m not positive if vanilla Firefox has this as well.

Once in the developer console, there&#8217;s a button to enable Responsive Design Mode, and another button to enable touch event emulation. Much like Chrome there&#8217;s a button to select a mobile-friendly resolution, though there isn&#8217;t a dropdown of actual device names. Once you enable those refresh the screen and you&#8217;re good to go.

[<img class="aligncenter size-large wp-image-629" src="https://codeplanet.io/wp-content/uploads/2015/09/firefox-responsive-1024x211.png" alt="firefox-responsive" width="660" height="136" />][9]

Firefox of course is best used for debugging JS and rendering for Firefox OS.

## Firefox OS Simulator

If you plan on releasing for Firefox OS, the [Firefox OS Simulator][10] plugin for the desktop Firefox browser may be your friend. That said I was unable to get it working.

## Safari

As far as I can tell, Safari doesn&#8217;t have the same tools for mimicking a mobile devices resolution or other touch emulation niceties. That said, if you notice rendering issues or JS execution problems on an iOS device, you&#8217;ll want to launch Safari to check things out.

## Gulpfile Breakdown

Here&#8217;s a high level overview of the **gulpfile.js** file used by SGoL for its various build steps. Eventually the file will be cleaned up and open sourced, but for now here&#8217;s a taste:

<pre class="text">empty
  `rm -rf ./www/*`
scripts
  uglify + concat » JavaScript
styles
  less + concat + minify » CSS
html-cordova / html-web
  handlebars + concat » HTML
watch
  runs: scripts, styles, html-web
  watches scripts, styles, html » rebuilds
data
  Download CMS Data » tmp/data.json
static-android / static-ios / static-web
  Moves asset files depending on platform
prebuild-ios
  runs: empty, data, static-ios, scripts, styles, html-cordova
prebuild-android
  runs: empty, data, static-android, scripts, styles, html-cordova
prebuild-web
  runs: empty, data, static-web, scripts, styles, html-web
build-android
  runs: prebuild-andoid
  `cordova build android --release`
sign-android
  `./bin/sign-android.sh`
build-ios
  runs: prebuild-ios
  `cordova build ios`
build-web
  runs: prebuild-web</pre>

## Gitignore Breakdown

This breakdown is pretty typical of Cordova projects. All of the binary builds are ignored. A bunch of plugin data which can be easily rebuilt using cordova CLI commands in the platforms/ directory are ignored. APK&#8217;s, Android / Java keystore files, a temp directory and NPM modules are also ignored.

<pre class="">build/android/*
build/ios/*
build/firefoxos/*
build/web/*
platforms/*
www/*
node_modules
tmp/*
google-key
*.keystore
*.apk</pre>

What makes this interesting though is that I ignore the www/ directory, which is where all the editable files of a Cordova project normally sit. Instead, I opted to stick all my important files in a src/ directory. When Cordova does a build it copies everything from the www/ directory and bundles it into each platforms build.

In my case, I wanted to do a bunch of pre-processing steps (LESS -> CSS, JS Concatenation, HTML transforming) so I use gulp tasks to perform the pre-processing, write the output to www/, then perform the Cordova builds. There is probably a way to do all of this using the Cordova hooks system, but with one of my requirements being that I want to build a web version without Cordova installed, I opted not to use them.

## Audio File Formats

Here&#8217;s a frustration that you&#8217;ll get to deal with if you plan on building an app with music. There are two prevailing music file formats, one being the open source OGG format, and the other being the license-restricted MP3 format. Everything out there can play OGG&#8217;s&#8230; Except for iOS. And you guessed it, iOS devices can play MP3&#8217;s. That said, not everything out there can play MP3&#8217;s, such as Firefox OS devices, and Firefox desktop on various platforms.

What you want to do is take your music files and convert them so that you have one of each MP3 and OGG formats, keeping in mind that converting one of these compressed files to another will result in some quality loss (if you have the original, higher quality format, start from that). Then, when building for different platforms, use OGG for Web/Firefox OS and Android and use MP3 for iOS.

When it comes to short sound effects, simply using an uncompressed WAV file should be fine (most audio sound effects that you come across will be distributed as WAV&#8217;s.) These WAV files will play anywhere you try them. They&#8217;re larger than their uncompressed brethren, but if they&#8217;re short there&#8217;s no problem.

**Discussion**: [Hacker News][11] | [Reddit][12]

 [1]: https://itunes.apple.com/us/app/strategic-game-of-life/id1033673016?ls=1&mt=8
 [2]: https://play.google.com/store/apps/details?id=name.thomashunter.strategicgol
 [3]: https://marketplace.firefox.com/app/strategic-gol/
 [4]: https://thomashunter.name/blog/tips-for-building-mobile-games-in-html5/
 [5]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS
 [6]: https://codeplanet.io/wp-content/uploads/2015/09/chrome-inspector-mobile.png
 [7]: https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-devices.png
 [8]: https://codeplanet.io/wp-content/uploads/2015/09/chrome-debug-app.png
 [9]: https://codeplanet.io/wp-content/uploads/2015/09/firefox-responsive.png
 [10]: https://developer.mozilla.org/en-US/docs/Tools/Firefox_OS_Simulator
 [11]: https://news.ycombinator.com/item?id=10291924
 [12]: https://www.reddit.com/r/javascript/comments/3mq40v/what_i_learned_while_publishing_an_html5_mobile/