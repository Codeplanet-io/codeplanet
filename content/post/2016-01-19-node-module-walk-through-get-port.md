---
title: 'Node Module Walk-Through: Get Port'
author: Jon Kuperman
type: post
date: 2016-01-19T17:00:21+00:00
url: /node-module-walk-through-get-port/
categories:
  - JavaScript

---
<a href="https://codeplanet.io/wp-content/uploads/2015/11/node-logo.png" rel="attachment wp-att-809"><img class="aligncenter size-full wp-image-809" src="https://codeplanet.io/wp-content/uploads/2015/11/node-logo.png" alt="Node.js Logo" width="424" height="228" srcset="https://codeplanet.io/wp-content/uploads/2015/11/node-logo.png 424w, https://codeplanet.io/wp-content/uploads/2015/11/node-logo-300x161.png 300w" sizes="(max-width: 424px) 100vw, 424px" /></a>

I had a fun idea for a new blog post series. We&#8217;ll pick an [NPM][1] module and walk through it together! Hopefully learning some cool things along the way.

Today&#8217;s module is [get-port][2] by the awesome [Sindresorhus][3]!

It&#8217;s a very simple module that returns an available port on your network.

## Installation

It&#8217;s very easy to install get-port with NPM!

<pre class="lang:sh decode:true ">npm install --save get-port</pre>

## Usage

Usage is also very simple. To get and use an available port on your network, simply run:

<pre class="lang:js decode:true ">const getPort = require('get-port');
 
getPort().then(port =&gt; {
	console.log(port);
	//=&gt; 51402 
});</pre>

## The Code

Luckily for us, the entire module is only 20 lines long! Let&#8217;s take a look:

<pre class="lang:js decode:true">'use strict';
var net = require('net');
var Promise = require('pinkie-promise');

module.exports = function () {
  return new Promise(function (resolve, reject) {
    var server = net.createServer();

    server.unref();
    server.on('error', reject);

    server.listen(0, function () {
      var port = server.address().port;

      server.close(function () {
        resolve(port);
      });
    });
  });
};</pre>

Let&#8217;s walk through this file one line at a time!

  1. [Strict Mode][4]
  2. Require Node&#8217;s [net package][5]
  3. Require [pinkie-promise][6] ( a polyfill for [JavaScript Promises][7] )
  4. A blank line ?
  5. An anonymous function this file [will export][8] if required
  6. Return a new Promise
  7. Create a [new server][9]
  8. A blank line ?
  9. Exit the program if this is the [only active server][10]
 10. If the server has any errors, reject the Promise
 11. A blank line ?
 12. Start a [new server][11] on port 0 ( **this is where the magic happens **)
 13. Make a new variable named port with the server&#8217;s port as it&#8217;s value
 14. A blank line ?
 15. Stop the server
 16. Resolve the Promise and return the port
 17. That&#8217;s it!

## The Magic

According to the official [Node documentation][11]:

> A port value of zero will assign a random port.

So, honestly, if **all** you wanted was to get a random port you could just use Node&#8217;s net library but this package wraps that functionality in a Promise so you can pull the port number out easily.

Have a package you&#8217;d like to walk-through next week? Leave it in the comments!

&nbsp;

 [1]: https://www.npmjs.com/
 [2]: https://www.npmjs.com/package/get-port
 [3]: https://twitter.com/sindresorhus
 [4]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
 [5]: https://nodejs.org/api/net.html
 [6]: https://www.npmjs.com/package/pinkie-promise
 [7]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
 [8]: https://nodejs.org/api/modules.html
 [9]: https://nodejs.org/api/net.html#net_net_createserver_options_connectionlistener
 [10]: https://nodejs.org/api/net.html#net_server_unref
 [11]: https://nodejs.org/api/net.html#net_server_listen_port_hostname_backlog_callback