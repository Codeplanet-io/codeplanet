---
id: 838
title: The only bad thing about ES7 async/await
date: 2016-01-18T11:00:43+00:00
author: Thomas Hunter II
layout: post
guid: http://codeplanet.io/?p=838
permalink: /the-only-bad-thing-about-es7-asyncawait/
image: /wp-content/uploads/2015/12/js-logo.jpg
categories:
  - JavaScript
  - Node.js
---
I&#8217;ve been using async/await pretty heavily in a side project of mine. It&#8217;s been pretty awesome to work with and my code has become much more terse while gaining readability! If you read my previous post, [The Long Road to Async/Await in JavaScript](https://thomashunter.name/blog/the-long-road-to-asyncawait-in-javascript/), you would know that I am a huge fan of the language construct. However, it&#8217;s not all rainbows and butterflies.

I noticed [this Async Code Example](https://github.com/strongloop/express/pull/2809) yesterday on GitHub, which I&#8217;ve copied and pasted below:

<pre><code class="javascript">app.get('/', async (req, res, next) =&gt; {
    let user = await User.findById(); // assuming .findById() returns a primise
    let org = await Org.findById();
    res.json({
        user: user,
        org: org,
    });
});
</code></pre>

This presumedly contrived code does two things; first it locates a user (possibly from a database), then locates an organization (also from somewhere &#8220;slow&#8221;), returning the two values in the HTTP response. All that without nested callbacks. Hooray! The code to do this ends up being very short and self explanatory.

Can you spot the shortcoming?

The two await statements both result in the function &#8220;pausing&#8221; while the rest of the application is free to serve requests to other users. However, the `Org.findById()` statement will not run until the `User.findById()` statement has completed entirely. Assuming both operations take **100ms** to execute, your response time is **200ms**!

> By applying the easy-to-use async/await pattern to perform work in serial which could have been parallelized, we&#8217;ve partially given up that which makes Node.js great; its ability to perform I/O in parallel without blocking the event loop!

If the code was written in the following manner, where the second action is dependent on the result of the first, it would make absolute sense:

<pre><code class="javascript">app.get('/', async (req, res, next) =&gt; {
    let user = await User.findById(); // assuming .findById() returns a primise
    let org = await Org.findById(user.orgId);
    res.json({
        user: user,
        org: org,
    });
});
</code></pre>

Notice how we _want_ the second await to occur _after_ the first. This is the **perfect** situation for using async and await.

> The only bad thing about ES7&#8217;s async/await is the ease in which we fall into the anti-pattern of serializing work which should be performed in parallel.

How else could this code have been written to be terse, self-descriptive, and run in parallel? Assuming the `User` and `Org` objects still provide an API written utilizing promises, one way would be to make use of `Promise.all()` (see [Promise.all() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)).

<pre><code class="javascript">app.get('/', async (req, res, next) =&gt; {
    let [user, org] = await Promise.all([
        User.findById(), // assuming .findById() returns a primise
        Org.findById()
    ]);
    res.json({
        user,
        org
    });
});
</code></pre>

Of course the code isn&#8217;t _as_ eloquent as before, but since `Promise.all()` returns a promise, we can still await on it. Still assuming each operation takes **100ms** to complete, the user should get their result back in **100ms**.