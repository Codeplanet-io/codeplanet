---
title: Introduction to Lodash
author: Jon Kuperman
type: post
date: 2015-11-20T17:00:19+00:00
excerpt: "An easy introduction to Lodash. We'll talk about it's history, usefulness and end with some simple examples!"
url: /introduction-to-lodash/
categories:
  - JavaScript

---
<p dir="ltr" lang="en">
  <blockquote class="twitter-tweet" data-width="550">
    <p lang="en" dir="ltr">
      Excited to release Lo-Dash, a drop-in Underscore.js replacement that's up to 8x faster <a href="http://t.co/7cNwy6rw">http://t.co/7cNwy6rw</a>; screencast <a href="http://t.co/MSkupmxY">http://t.co/MSkupmxY</a>
    </p>
    
    <p>
      &mdash; John-David Dalton (@jdalton) <a href="https://twitter.com/jdalton/status/194515261594943490">April 23, 2012</a>
    </p>
  </blockquote>
  
  <p>
  </p>
  
  <p>
    Originally forked from <a href="http://underscorejs.org/">Underscore</a> in 2012, Lodash has become <strong>the most depended upon NPM package.</strong>
  </p>
  
  <p>
    <a href="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-19-at-4.42.04-PM.png"><img class="aligncenter size-full wp-image-770" src="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-19-at-4.42.04-PM.png" alt="Screen Shot 2015-11-19 at 4.42.04 PM" width="1153" height="386" srcset="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-19-at-4.42.04-PM.png 1153w, https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-19-at-4.42.04-PM-300x100.png 300w, https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-19-at-4.42.04-PM-768x257.png 768w, https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-19-at-4.42.04-PM-1024x343.png 1024w" sizes="(max-width: 1153px) 100vw, 1153px" /></a>
  </p>
  
  <p>
    So, what is Lodash exactly?
  </p>
  
  <p>
    Lodash brands itself as:
  </p>
  
  <blockquote>
    <p class="description">
      A JavaScript utility library delivering consistency, modularity, performance, & extras.
    </p>
  </blockquote>
  
  <p class="description">
    But, what does this really mean?
  </p>
  
  <h2 class="description">
    Lodash, simplified
  </h2>
  
  <p>
    At its core, Lodash is just a JavaScript library that provides a bunch of helper functions that make writing JavaScript applications easier.
  </p>
  
  <p>
    By that, I mean You include the lodash.js script in your project and then you get access to a ton of great helper functions like:
  </p>
  
  <ul>
    <li>
      _.findLast
    </li>
    <li>
      _.curry
    </li>
    <li>
      _.findKey
    </li>
    <li>
      _.sum
    </li>
    <li>
      _.capitalize
    </li>
    <li>
      and so many more
    </li>
  </ul>
  
  <p>
    All of these helper methods have full browser support back to IE6 and are super fast!
  </p>
  
  <h2>
    Lodash, an example
  </h2>
  
  <p>
    Let&#8217;s say we have a very basic website. Create an index.html file and paste in:
  </p>
  
  <pre class="lang:default decode:true">&lt;!DOCTYPE html&gt;
&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;A simple website&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;h1&gt;Hello world!&lt;/h1&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>
  
  <p>
    Then, download Lodash from <a href="https://lodash.com/">their website</a> and source it in your index.html as well as a blank file we&#8217;ll call script.js. You should now have something that looks like:
  </p>
  
  <pre class="lang:default decode:true ">&lt;!DOCTYPE html&gt;
&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;A simple website&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;h1&gt;Hello world!&lt;/h1&gt;
        &lt;script src="lodash.js"&gt;&lt;/script&gt;
        &lt;script src="script.js"&gt;&lt;/script&gt;
    &lt;/body&gt;
&lt;/html&gt;
</pre>
  
  <p>
    Now, in our script.js file we have access to all the great functionality namespaced to the &#8220;_&#8221; object. Here are some cool examples.
  </p>
  
  <pre class="lang:js decode:true">// inside script.js

// Capitalize
var name = "hello, world";

var newName = _.capitalize(name); // "HELLO, WORLD"

// Flatten Deep

var nestedArray = [1, 2, [3, 4, [5, 6], 7]];

var flattenedArray = _.flatten(nestedArray, true); // [1, 2, 3, 4, 5, 6, 7]

// First

var list = [6, 5, 4, 3, 2, 1];

var firstInList = _.first(list);

</pre>
  
  <p>
    There are a ton of great methods you can find on <a href="https://lodash.com/">the website</a>. Let me know in the comments if there&#8217;s anything I missed!<br />
  </p>