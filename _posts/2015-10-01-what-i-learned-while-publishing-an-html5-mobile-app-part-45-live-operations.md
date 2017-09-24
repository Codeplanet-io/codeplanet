---
id: 679
title: 'What I learned while publishing an HTML5 Mobile App, Part 4/5: Live Operations'
date: 2015-10-01T10:00:26+00:00
author: Thomas Hunter II
layout: post
guid: http://codeplanet.io/?p=679
permalink: /what-i-learned-while-publishing-an-html5-mobile-app-part-45-live-operations/
categories:
  - Mobile Development
tags:
  - Cordova
---
Once you&#8217;ve got your app or game released, you&#8217;re probably going to want to keep it updated.

## Content Management System

SGoL uses a Google Spreadsheet backed CMS called [Grille](https://www.npmjs.com/package/grille) for handling content updates. This CMS outputs all data as a large structured JSON document. SGoL ships with an exported version of this JSON document. When SGoL launches while the device is online, it&#8217;ll download the latest version of the CMS data and cache it. When SGoL launches and it is not online it&#8217;ll use the cached version. Overall it&#8217;s a very simple system for allowing offline play and usually up-to-date content.

[<img class="aligncenter size-full wp-image-656" src="https://codeplanet.io/wp-content/uploads/2015/09/grille-cms.png" alt="grille-cms" srcset="https://codeplanet.io/wp-content/uploads/2015/09/grille-cms.png 885w, https://codeplanet.io/wp-content/uploads/2015/09/grille-cms-300x111.png 300w, https://codeplanet.io/wp-content/uploads/2015/09/grille-cms-768x284.png 768w" sizes="(max-width: 885px) 100vw, 885px" />](https://codeplanet.io/wp-content/uploads/2015/09/grille-cms.png)

Here&#8217;s a screenshot of the campaign spreadsheet. Unfortunately there&#8217;s no convenient way to express variably sized and dynamic content using a spreadsheet which is why you see JSON fields in the screenshot.

Keeping a game up-to-date is very important, specifically seeing how users interact with your content, where they have problems, and alleviating those problems. But, how do you know how users interact with your content? Read on&#8230;

## Analytics

SGoL uses Mixpanel for tracking analytics. One might be tempted to use the familiar Google Analytics, however that is really geared more towards users of websites, whereas Mixpanel is more about tracking &#8220;events&#8221;. Even if you&#8217;re building a Single Page Application for a desktop browser, using Mixpanel may be a better tool, depending on what you want to track.

That said, Mixpanel isn&#8217;t good for tracking historical data. If you wanted to know how many users interacted with your content last September vs this September, Mixpanel would fall short. The data it stores is ephemeral.

Screenshots

### Events Overview

Here&#8217;s an overview of the most popular events triggered in SGoL over the past month. Notice the two peaks, probably correlated to when I was doing a lot of development.

[<img class="aligncenter size-full wp-image-653" src="https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-overview.png" alt="mixpanel-overview" width="959" height="571" srcset="https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-overview.png 959w, https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-overview-300x179.png 300w, https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-overview-768x457.png 768w" sizes="(max-width: 959px) 100vw, 959px" />](https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-overview.png)

### Funnel Analytics

This is where things really get useful. When you track events you name them and can set attributes. In the screenshot below I&#8217;ve tracked when each level is started. As you can see there is a massive falloff in traffic between levels 2 and 3. While we can&#8217;t tell for sure what the problem is, it may mean that level 2 is too difficult or too boring. That said one can tweak content and keep an eye on the funnel until it improves.

[<img class="aligncenter size-full wp-image-654" src="https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-funnel.png" alt="mixpanel-funnel" width="950" height="529" srcset="https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-funnel.png 950w, https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-funnel-300x167.png 300w, https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-funnel-768x428.png 768w" sizes="(max-width: 950px) 100vw, 950px" />](https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-funnel.png)

### Individual Sessions

If you &#8220;register&#8221; a user in Mixpanel you can keep track of the different activities they perform over time, allowing you to get inside the head of your users.

[<img class="aligncenter size-full wp-image-655" src="https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-session.png" alt="mixpanel-session" width="576" height="634" srcset="https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-session.png 576w, https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-session-273x300.png 273w" sizes="(max-width: 576px) 100vw, 576px" />](https://codeplanet.io/wp-content/uploads/2015/09/mixpanel-session.png)

SGoL ships a Mixpanel bootloader with the application. If the device is offline, the main script will not be downloaded from the Mixpanel CDN. If the device is online, it will download the script and send events. SGoL could have used a system which queues events and ships them when offline, but this wasn&#8217;t a major requirement.

## Interstitial Advertisements

SGoL uses AdMob for delivering advertisements to users. This wasn&#8217;t done with the intention of making money, but instead to gain knowledge of adding advertisements to a mobile app.

[<img class="aligncenter size-large wp-image-652" src="https://codeplanet.io/wp-content/uploads/2015/09/Screen-Shot-2015-09-19-at-14.14.07-1024x139.png" alt="AdMob" width="660" height="90" srcset="https://codeplanet.io/wp-content/uploads/2015/09/Screen-Shot-2015-09-19-at-14.14.07-1024x139.png 1024w, https://codeplanet.io/wp-content/uploads/2015/09/Screen-Shot-2015-09-19-at-14.14.07-300x41.png 300w, https://codeplanet.io/wp-content/uploads/2015/09/Screen-Shot-2015-09-19-at-14.14.07-768x104.png 768w, https://codeplanet.io/wp-content/uploads/2015/09/Screen-Shot-2015-09-19-at-14.14.07.png 1129w" sizes="(max-width: 660px) 100vw, 660px" />](https://codeplanet.io/wp-content/uploads/2015/09/Screen-Shot-2015-09-19-at-14.14.07.png)

And, as  you can see, no money is being made.

AdMob is interesting, it can _only_ be used for mobile apps. Google has another ad platform too, AdSense, which can _only_ be used for websites. With SGoL being web based, loading AdSense is feasible, but it would violate ToS and could get shut down. Really neither of these platforms is perfect for a web based mobile app. In fact, AdMob integration requires the use of native code and must be installed via a Cordova command:

<pre class="">$ cordova plugin add cordova-plugin-admobpro</pre>

Once installed a globally accessible object is provided, **window.AdMob**. This object has a few methods which you can read about in the [Cordova AdMob Pro](https://github.com/floatinghotpot/cordova-admob-pro) page. There are two important methods, one for preparing an ad (SGoL runs this at the beginning of an ad level), then the code to actually display it (executed when an ad level is completed).