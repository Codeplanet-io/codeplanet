---
title: Parameter Hell
author: Jon Kuperman
type: post
date: 2014-01-11T21:33:16+00:00
url: /parameter-hell/
categories:
  - Web Development

---
With the rise of popularity in Asynchronous JavaScript applications, the phrase _callback hell _has become quite popular.

For more check out:
  
[callbackhell.com][1]

All of this talk about Callback Hell got me thinking about anti-patterns that I run into when working with synchronous code.

#### Parameter Hell

If you&#8217;ve worked in enough legacy codebases, or maybe even too many modern ones &#8212; you&#8217;ve probably run into a travesty that looks something like this:

    <?php
    function new_person($species = 'mammal', $race = 'human', $alive = 'yes', $legs = 'two', $name = null);

You get the idea.

If you think that&#8217;s ugly, you should see what happens when you need to call a function like that but you only need, let&#8217;s say, the fifth parameter to be set. Are you ready?

    <?php
    $new_user = new_person(NULL, NULL, NULL, NULL, 'Jon');

That&#8217;s not even the worst of it. It can get way worse if you need, say, exact `true`&#8216;s and `false`&#8216;s in order to get the right defaults. Often times you end up with code like this:

    <?php
    some_function(true, true, false, true, false, false, false, $name);

Here&#8217;s the thing. **None of this is necessary**

## Setting Some Limits

The first thing you can do to cure Parameter Hell is set a hard limit on the maximum number of parameters allowed in your codebase. I think 3 is a sane limit.

## A Simple Solution

The next part, the re-factoring, is really not _that_ bad.

Simply replace all of those individual options with an options array. Something like this:

    <?php
    function newFunction($options) {
        $name = $options['name'];
        $age = $options['age'];
    }

You get the idea. This is just a lot nicer for other programmers to work with later, because they don&#8217;t need to keep track of what position in your list of parameters their item is, just set what they need and pass it in.

    <?php
    $options = array(
        'name'      => 'Jon',
        'age'       => 26,
        'privilege' => 'admin'
    );
    newFunction($options);

That wasn&#8217;t so bad, was it?

 [1]: http://callbackhell.com/