---
id: 708
title: Introduction to regular expressions
date: 2015-10-08T10:00:36+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=708
permalink: /introduction-to-regular-expressions/
categories:
  - JavaScript
---
Hey all! Today we&#8217;re going to cover a gentle introduction to regular expressions. We&#8217;ll use JavaScript as our example language although almost everything we cover will work in any modern language.

## Regular Expressions with JavaScript

[JavaScript Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) come with a bunch of handy methods but today we are going to be focusing on the [match](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match) method for testing whether a string matches the regex patterns we&#8217;ll be creating.

To play around with regular expressions interactively, we can use the console or a service like [JS Bin](http://jsbin.com/?js,console) and some code like this:

<pre class="lang:js decode:true">var string, pattern;
console.log(string.match(pattern));</pre>

So, using that simple strategy, let&#8217;s get started!

## String Literals

The very first thing we&#8217;ll learn how to do is match for a literal string. This means checking a string like &#8220;hello&#8221; and matching literally just the word &#8220;hello&#8221;. That looks something like this:

<pre class="lang:js decode:true">var string = "hello";
var pattern = /hello/;

console.log(string.match(pattern)); // returns ["hello"]</pre>

Similarly, searching for a string literal that does not exist will return null.

<pre class="lang:js decode:true ">var string = "hello";
var pattern = /goodbye/;

console.log(string.match(pattern)); // returns null</pre>

## Either or

Sticking with string literals, let&#8217;s say we want to match if a string includes either one word or another. We can do this by grouping the string literals together and using a single pipe as an OR operator.

<pre class="lang:js decode:true">var string = "hello";
var pattern = /(goodbye|hello)/;

console.log(string.match(pattern)); // returns ["hello", "hello"]</pre>

Just like before, if the string doesn&#8217;t contain either of our string literals, it returns null.

<pre class="lang:js decode:true">var string = "foo";
var pattern = /(goodbye|hello)/;

console.log(string.match(pattern)); // returns null</pre>

### Multiple results

Some of you may have noticed that while the or operator returned a match like we wanted, it also returned an Array with two entries.

This is because any time you group any literal or patterns together using parenthesis you are also telling the regex engine to &#8220;remember&#8221; the match. Meaning that it will, if matched, add another entry to your array.

In order to tell the regex engine to &#8220;forget&#8221; the match, you can always prepend a group with &#8220;?:&#8221; like so:

<pre class="lang:js decode:true">var string = "hello";
var pattern = /(?:goodbye|hello)/;

console.log(string.match(pattern)); // returns ["hello"]</pre>

## Any Character

More often than not, we don&#8217;t know the exact word we&#8217;re looking for. Frequently we need to match on something less specific, like a letter or number.

### Match a Letter

Let&#8217;s say we want to match on any single letter &#8220;a&#8221; through &#8220;z&#8221;. We can do a little something like this:

<pre class="lang:js decode:true">var string = "r";
var pattern = /[a-z]/;

console.log(string.match(pattern)); // returns ["r"]</pre>

But let&#8217;s see what happens if the letter is capitalized.

<pre class="lang:js decode:true">var string = "R";
var pattern = /[a-z]/;

console.log(string.match(pattern)); // returns null</pre>

Luckily, we have a great option for handling this. Using &#8220;flags&#8221; we gain a lot of flexibility with our regex searches. For this case, we can add an &#8220;i&#8221; flag which makes our search case insensitive.

<pre class="lang:js decode:true">var string = "R";
var pattern = /[a-z]/i;

console.log(string.match(pattern)); // returns ["R"]</pre>

### Match a Number

Sometimes, it&#8217;s a number we need to find instead of a letter. Very similar to the example above we can use a range like [0-9] to match a number instead of [a-z] for a letter.

<pre class="lang:js decode:true">var string = "7";
var pattern = /[0-9]/;

console.log(string.match(pattern)); // returns ["7"]</pre>

### Match a Letter or Number

As you might imagine, sometimes we need to match on a single character whether it&#8217;s a number or a letter. Fortunately, regular expressions provide us with a character for matching any alphanumeric character. It looks like &#8220;w&#8221;.

<pre class="lang:js decode:true">var string1 = "7";
var string2 = "r";
var pattern = /w/;

console.log(string1.match(pattern)); // returns ["7"]
console.log(string2.match(pattern)); // returns ["r"]</pre>

Before we get too much further, don&#8217;t worry about memorizing all of these flags like &#8220;w&#8221; and &#8220;/i&#8221;. They are all nicely documented over at the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions).

## Match a number of characters

### Any number of characters

The following techniques will work with a letter search &#8220;[a-z]&#8221;, a number search &#8220;[0-9]&#8221; or a alphanumeric search &#8220;w&#8221;.

Let&#8217;s say we want to match any number of letters that are next to each other. We can use the &#8220;+&#8221; character to match one or more of the pattern before it. So to match one or more lowercase letters we can do:

<pre class="lang:js decode:true">var string = "baz";
var pattern = /[a-z]+/;

console.log(string.match(pattern)); // returns ["baz"]</pre>

We could apply the same logic to [0-9] or w.

### Specific number of characters

Other times we want to match only if there are a specific number of characters in a row. Let&#8217;s say we were looking for the string &#8220;www&#8221; to identify a web address. We could use a string literal like &#8220;/www/&#8221; but let&#8217;s check out a cleaner way of doing it.

We can match the letter &#8220;w&#8221; 3 times by using curly braces which allow you to pass in two numbers for minimum and maximum length or a single number for the exact number of occurrences. Let&#8217;s check out some examples to better understand.

<pre class="lang:js decode:true">var string1 = "www";
var string2 = "wwww";
var string3 = "wwwwww";

var pattern1 = /w{3}/;
var pattern2 = /w{2, 5}/;


// Matches exactly 3 w's
console.log(string1.match(pattern1)); // returns ["www"]

// Matches the first 3 w's
console.log(string2.match(pattern1)); // returns ["www"]

// Matches between 2 and 5 w's
console.log(string3.match(pattern2)); // returns null
</pre>

### Special Characters

If we search for &#8220;.&#8221; as a string literal, we&#8217;ll get false positives like this:

<pre class="lang:js decode:true">var string1 = "r";
var string2 = ".";

var pattern = /./;


console.log(string1.match(pattern)); // returns ["r"]
console.log(string2.match(pattern)); // returns ["."]
</pre>

This is because there are special characters in regex which we might also want to search for. In this case, &#8220;.&#8221; is a wildcard so if we want the literal character &#8220;.&#8221; we&#8217;ll need to escape it.

<pre class="lang:js decode:true ">var string1 = "r";
var string2 = ".";

var pattern = /./;


console.log(string1.match(pattern)); // returns null
console.log(string2.match(pattern)); // returns ["."]
</pre>

Additionally, it&#8217;s common that we need a pattern which includes a white space. Let&#8217;s say we&#8217;re looking for the words &#8220;web design&#8221;.

<pre class="lang:js decode:true ">var string = "web design";

var pattern = /w+/;


console.log(string.match(pattern)); // returns ["web"]
</pre>

As we can see, our match fails as soon as it hits a space. For these situations we can use &#8220;s&#8221; to account for a white space character.

<pre class="lang:js decode:true ">var string = "web design";

var pattern = /w+sw+/;

// This will match any number of characters
// plus a white space
// followed by any other number of characters
console.log(string.match(pattern)); // returns ["web design"]
</pre>

## Begins With

Frequently we find ourselves only wanting to match a pattern if the string in question begins that way. Let&#8217;s say for example we still want to match &#8220;www&#8221; but only if that&#8217;s the very beginning of the string.

Here we can use regular expression boundaries. There are four total boundaries that you can use but today we&#8217;re only going to focus on the beginning of an input and the end of an input.

To find a &#8220;www&#8221; only if it&#8217;s the beginning of the input we can use the &#8220;^&#8221; boundary for the beginning of an input.

<pre class="lang:js decode:true">var string1 = "www.google.com";
var string2 = "google.com/www";

var pattern = /^w{3}/;


console.log(string1.match(pattern)); // returns ["www"]
console.log(string2.match(pattern)); // returns null
</pre>

## Ends With

Very similarly, sometimes we need to match a pattern only if it&#8217;s at the end of an input string. For this example, let&#8217;s say we want to find strings that end with either &#8220;.com&#8221; or &#8220;.org&#8221;. Let&#8217;s combine the or operator from earlier with the ends with boundary &#8220;$&#8221;.

<pre class="lang:js decode:true">var string1 = "google.com";
var string2 = "google.org";
var string3 = "someorg.edu";

var pattern = /(?:com|org)$/;


console.log(string1.match(pattern)); // returns ["com"]
console.log(string2.match(pattern)); // returns ["org"]
console.log(string3.match(pattern)); // returns null
</pre>

## Single Word

Let&#8217;s say now we want to match a string literal but only if it&#8217;s in a word by itself. We can use the zero-width word boundary &#8220;b&#8221; for this. Let&#8217;s check out some examples.

<pre class="lang:js decode:true">var string1 = "or";
var string2 = "poor";
var string3 = "organism";

var pattern = /borb/;


console.log(string1.match(pattern)); // returns ["or"]
console.log(string2.match(pattern)); // returns null
console.log(string3.match(pattern)); // returns null
</pre>

## Optional

Another frequent occurrence is searching for optional strings. Going back to our &#8220;www&#8221; example, we know that some websites use www. and some don&#8217;t. Let&#8217;s use the optional qualifier &#8220;?&#8221; in addition to the literal &#8220;.&#8221; assertion &#8220;.&#8221; to match websites whether they start with &#8220;www&#8221; or not.

<pre class="lang:js decode:true">var string1 = "www.google.com";
var string2 = "google.com";

// optional www. followed by google.com literal
var pattern = /(?:www.)?(?:google.com)/;


console.log(string1.match(pattern)); // returns ["www.google.com"]
console.log(string2.match(pattern)); // returns ["google.com"]
</pre>

## Global Search

The last thing we&#8217;ll cover today is how to handle a global search. Say we have a list of websites in a multiline string. Let&#8217;s combine a lot of what we&#8217;ve learned so far. We want a pattern that:

  * Appears anywhere in the multiline string
  * Is the beginning of a new line
  * Optionally starts with &#8220;www.&#8221;
  * Followed by any number of alphanumeric characters
  * Ends with a &#8220;.com&#8221;

<pre class="lang:js decode:true ">var string = "www.google.com nwww.facebook.com ntwitter.com";

var pattern = /^(www.)?w+.com/gm;


console.log(string.match(pattern)); // ["www.google.com", "www.facebook.com", "twitter.com"]</pre>