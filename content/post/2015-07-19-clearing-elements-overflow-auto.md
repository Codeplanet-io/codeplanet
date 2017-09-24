---
title: Clearing Elements with Overflow Auto
author: Jon Kuperman
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=329
categories:
  - Uncategorized

---
# The Problem

If you&#8217;ve ever filled an element with nothing but floating elements, you may have noticed you lose your background color. In fact, the entire background element is collapsing in on itself. Notice my blue background not showing up?

<p class="codepen" data-height="268" data-theme-id="0" data-slug-hash="Imjbp" data-default-tab="result">
  See the Pen <a href="http://codepen.io/jkup/pen/Imjbp/">Imjbp</a> by jkup (<a href="http://codepen.io/jkup">@jkup</a>) on <a href="http://codepen.io">CodePen</a>.
</p>

The most common way to fix is this is with what is called a `clearfix`

There are a million different ways to do this. For a pretty good list of them check out CSS-Tricks article on how to [Force Element To Self-Clear its Children][1].

Personally, I&#8217;m a big fan of Nicolas Gallagher&#8217;s [micro clearfix hack][2] It looks something like this:

<p data-height="268" data-theme-id="0" data-slug-hash="Jubsg" data-default-tab="result" data-user="jkup" class='codepen'>
  See the Pen <a href='http://codepen.io/jkup/pen/Jubsg/'>Jubsg</a> by jkup (<a href='http://codepen.io/jkup'>@jkup</a>) on <a href='http://codepen.io'>CodePen</a>.
</p>

 [1]: http://css-tricks.com/snippets/css/clear-fix/
 [2]: http://nicolasgallagher.com/micro-clearfix-hack/