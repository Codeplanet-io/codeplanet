---
title: How to Make a Flot Chart with Letters Instead of Symbols
author: Kelly King
type: post
date: 2013-08-09T03:29:10+00:00
draft: true
url: /?p=91
post_views_count:
  - "129"
categories:
  - Web Design

---
I use Flot.js regularly for building JavaScript charts, and recently was asked to plot letters on a graph instead of symbols. It took me a while to figure out, so I thought I&#8217;d share.

[<img class="alignnone size-full wp-image-100" alt="letter chart with flot js" src="https://codeplanet.io/wp-content/uploads/2013/08/letter-chart.jpg" width="833" height="497" srcset="https://codeplanet.io/wp-content/uploads/2013/08/letter-chart.jpg 833w, https://codeplanet.io/wp-content/uploads/2013/08/letter-chart-300x179.jpg 300w, https://codeplanet.io/wp-content/uploads/2013/08/letter-chart-768x458.jpg 768w" sizes="(max-width: 833px) 100vw, 833px" />][1]

My first thought was to check if FlotJS had any plugins that might work, such as Flot&#8217;s [Symbol Plugin][2], which adds extra shapes to flot graphs, such as triangles and diamonds. The symbol plugin seemed like a good starting point, if I could figure out how to create letters. I assumed at first that I would need to create the shapes using lines or arcs, like the other symbols in the plugin:

<pre>diamond: function (ctx, x, y, radius, shadow) {
    // pi * r^2 = 2s^2  =&gt;  s = r * sqrt(pi/2)
    var size = radius * Math.sqrt(Math.PI / 2);
    ctx.moveTo(x - size, y);
    ctx.lineTo(x, y - size);
    ctx.lineTo(x + size, y);
    ctx.lineTo(x, y + size);
    ctx.lineTo(x - size, y);
}</pre>

However, searching for &#8220;letters on HTML Canvas&#8221;, I found that the HTML canvas element already has methods of fillText and strokeText, which allow you to write text directly onto the canvas. From there, I was able to simply add new &#8220;symbols&#8221; to the plugin by adding objects at the end of the the plugin&#8217;s handler list. Here is a snippet:

<pre>var handlers = {
...
cross: function (ctx, x, y, radius, shadow) {
    // pi * r^2 = (2s)^2  =&gt;  s = r * sqrt(pi)/2
    var size = radius * Math.sqrt(Math.PI) / 2;
    ctx.moveTo(x - size, y - size);
    ctx.lineTo(x + size, y + size);
    ctx.moveTo(x - size, y + size);
    ctx.lineTo(x + size, y - size);
},
A: function (ctx, x, y, radius, shadow) {
    ctx.lineWidth = radius/3;
    ctx.font = '' + radius*3 + 'px Arial';
    ctx.strokeText("A", x-radius, y-radius);
},
B: function (ctx, x, y, radius, shadow) {
    ctx.lineWidth = radius/3;
    ctx.font = '' + radius*3 + 'px Arial';
    ctx.strokeText("B", x-radius, y-radius);
},
C: function (ctx, x, y, radius, shadow) {
    ctx.lineWidth = radius/3;
    ctx.font = '' + radius*3 + 'px Arial';
    ctx.strokeText("C", x-radius, y-radius);
},
D: function (ctx, x, y, radius, shadow) {
    ctx.lineWidth = radius/3;
    ctx.font = '' + radius*3 + 'px Arial';
    ctx.strokeText("D", x-radius, y-radius);
},
E: function (ctx, x, y, radius, shadow) {
    ctx.lineWidth = radius/3;
    ctx.font = '' + radius*3 + 'px Arial';
    ctx.strokeText("E", x-radius, y-radius);
}
...
}</pre>

You&#8217;ll notice that I adjusted the line width and font size to be relative to the radius. This way, when the user adjusts the series&#8217; radii, the letters will get smaller too. So now to use the shapes, you can do so like this:

<pre>var data = [
    { data: [someData], points: { symbol: "A" } },
    { data: [someMoreData], points: { symbol: "B" } }
  ];

  $.plot($("#placeholder"), data, {
    series: { points: { show: true, radius: 3 } }
  });</pre>

And the letters will be rendered in place of circles!

Check out the source code and demo here:

[symple\_button color=&#8221;blue&#8221; url=&#8221;../demos/javascript/flot/letters/&#8221; title=&#8221;Flot Letter Chart Demo&#8221; target=&#8221;blank&#8221; border\_radius=&#8221;&#8221;]Demo[/symple\_button] [symple\_button color=&#8221;blue&#8221; url=&#8221;https://github.com/kellyk/flot-letters&#8221; title=&#8221;Flot Letter Chart Code&#8221; target=&#8221;blank&#8221; border\_radius=&#8221;&#8221;]Source[/symple\_button]

 [1]: ../demos/javascript/flot/letters/
 [2]: https://code.google.com/p/flot/source/browse/trunk/jquery.flot.symbol.js?r=263