---
id: 849
title: Node.js v5.4 vs luvit v2.8 Benchmark
date: 2016-02-08T12:00:35+00:00
author: Thomas Hunter II
layout: post
guid: http://codeplanet.io/?p=849
permalink: /node-js-v54-vs-luvit-v28-benchmark/
categories:
  - Node.js
---
I ran a simple HTTP benchmark against Node.js v5.4.1 and luvit v2.8.0. Benchmarks were performed using a slightly modified version of the example &#8220;Hello World&#8221; script provided by both projects and used **siege** for performing requests. The scripts were modified to send the exact same headers and body content over the wire.

### server.lua

<pre><code class="lua">local http = require('http')

http.createServer(function (req, res)
  local body = "Hello Worldn"
  res:setHeader("Content-Type", "text/plain")
  res:setHeader("Content-Length", #body)
  res:finish(body)
end):listen(5000, '127.0.0.1')

print('Server running at http://127.0.0.1:5000/')</code></pre>

### server.js

<pre><code class="javascript">const http = require('http');

const hostname = '127.0.0.1';
const port = 5001;

http.createServer((req, res) => {
  var body = 'Hello Worldn';
  res.writeHead(200, { 'Content-Type': 'text/plain', 'Content-Length': body.length });
  res.end(body);
}).listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});</code></pre>

### Results

For each test I would run the server, make several hundred ignored requests, then run a siege for 2 minutes:

  * **Node: 29.79** Requests per Second (3549/119.15 sec)
  * **luvit: 30.79** Requests per Second (3687/119.74 sec)

I was a bit surprised, having assumed luvit would have maybe double the throughput as compared to Node, but as you can see the two are nearly tied. Both internally use libuv@1.8.0 which is likely the determining factor for performance.