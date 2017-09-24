---
title: React onClick handlers with ES6 classes
author: Jon Kuperman
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=1077
categories:
  - JavaScript
  - React.js

---
React onClick handlers are fairly straightforward. Let&#8217;s say you have a Link component:

## Simple React Component

<pre class="lang:js decode:true">var Link = React.createClass({
  render: function() {
    return (
      &lt;a href="https://codeplanet.io"&gt;Awesome Blog!&lt;/a&gt;
    );
  }
});</pre>

And now we want to add an onClick handler so that we can do some single page app magic without refreshing the page. We can do that like so:

## React onClick Handler

<pre class="lang:js decode:true ">var Link = React.createClass({
  render: function() {
    return (
      &lt;a onClick={this.handleOnClick} href="https://codeplanet.io"&gt;Awesome Blog!&lt;/a&gt;
    );
  },
  handleOnClick: function(event) {
    event.stopPropagation();
    // Do some magic single page app fanciness
  }
});</pre>