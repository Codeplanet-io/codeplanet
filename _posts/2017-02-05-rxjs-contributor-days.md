---
id: 1333
title: RxJS Contributor Days
date: 2017-02-05T22:17:20+00:00
author: Jon Kuperman
layout: post
guid: https://codeplanet.io/?p=1333
permalink: /rxjs-contributor-days/
categories:
  - JavaScript
---
This week I had the privilege of attending [RxJS contributor days](https://www.contributordays.com/contributor-days/rxjs). It was a day long event attended by core contributors as well as companies using [RxJS](https://github.com/ReactiveX/rxjs) like Slack, Google, Facebook and Netflix.

<img class="alignnone size-full wp-image-1335" src="https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.12.32-PM.png" alt="ReactiveX Website" width="1280" height="657" srcset="https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.12.32-PM.png 1280w, https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.12.32-PM-300x154.png 300w, https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.12.32-PM-768x394.png 768w, https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.12.32-PM-1024x526.png 1024w, https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.12.32-PM-1080x554.png 1080w" sizes="(max-width: 1280px) 100vw, 1280px" />

While there is going to be an awesome video detailing all the cool stuff that happened that day I thought I&#8217;d put together a list of cool resources I learned about.

First are the Github pages for [RxJS version 4](https://github.com/Reactive-Extensions/RxJS) and [RxJS version 5](https://github.com/ReactiveX/rxjs). I hadn&#8217;t actually visited the version 5 repo before the contributor days but it&#8217;s where all the new development is happening!

## What are Observables

The first big topic of discussion was around awareness of what RxJS is. Ultimately, this came down to understanding the core data structure that the library provides &#8212; Observables.

It might be easiest to understand them through the [TC39 proposal](https://github.com/tc39/proposal-observable) but essentially they are a JavaScript data type that are great at dealing with asynchronous streams of data. It&#8217;s cool if you think about being able to map/filter/reduce over &#8220;streams&#8221; of data whether they be DOM events or API calls.

We talked a lot about alternative tools and I discovered this [cool documentation site about Promises](https://promise-nuggets.github.io/) and a [great discussion on Github](https://github.com/whatwg/fetch/issues/447) about adding cancellation (abort) to the fetch proposal.

## Documentation

The next thing that was cool was discovering the [documentation site around RxJS](http://reactivex.io/rxjs/manual/overview.html). They have a great intro and are linked to the http://reactivex.io/ sites for all the other brands of Rx (it&#8217;s not just for JavaScript!).

Also I discovered this awesome introductory post [The introduction to Reactive Programming you&#8217;ve been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754) which eventually led me to check out this cool UI framework called [Cycle.js](https://cycle.js.org/) which applies a lot of the same techniques for UI rendering.

## Competition

It was cool to hear about some competing libraries and we spent a good amount of time talking about [Most.js](https://github.com/cujojs/most).

## Random Links

<img class="alignnone size-full wp-image-1337" src="https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.14.48-PM.png" alt="RxJS Marble Diagram" width="882" height="488" srcset="https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.14.48-PM.png 882w, https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.14.48-PM-300x166.png 300w, https://codeplanet.io/wp-content/uploads/2017/02/Screen-Shot-2017-02-05-at-9.14.48-PM-768x425.png 768w" sizes="(max-width: 882px) 100vw, 882px" />

The last things I wanted to share were [this cool project](http://rxmarbles.com/) that shows draggable marble diagrams for all the RxJS operators and this [great list of tutorials](http://reactivex.io/tutorials.html) for all types of Rx libraries!