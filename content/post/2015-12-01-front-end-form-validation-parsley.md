---
title: Front end form validation with Parsley
author: Jon Kuperman
type: post
date: 2015-12-01T17:00:50+00:00
url: /front-end-form-validation-parsley/
categories:
  - JavaScript

---
[<img class="aligncenter size-full wp-image-796" src="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.33.35-PM.png" alt="Screen Shot 2015-11-28 at 7.33.35 PM" width="401" height="159" srcset="https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.33.35-PM.png 401w, https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.33.35-PM-300x119.png 300w" sizes="(max-width: 401px) 100vw, 401px" />][1]

Front end validation for your forms is a must have these days! It&#8217;s not a good user experience to reload the page after the user hits submit, just to find an error and send them back to the same page! Even worse is if you didn&#8217;t store their original entries, forcing them to re-enter even the fields they did get right!

Fortunately, there are all sorts of great, free and open source libraries to make front end validation a breeze. Today we&#8217;re going to check out [Parsley.js][2].

## Installation

First, we&#8217;ll head over to <http://parsleyjs.org/doc/download.html> and download parsley.min.js. Then we&#8217;ll create a new project that looks something like this:

<pre class="lang:default decode:true ">&lt;html&gt;
  &lt;head&gt;
      &lt;title&gt;Front End Validation&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;form id="myForm" action="your_server" method="post"&gt;
      &lt;input id="name" name="username" type="text" placeholder="Username" /&gt;
      &lt;input id="email" name="email" type="text" placeholder="Email" /&gt;
      &lt;input type="submit" value="Submit" /&gt;
    &lt;/form&gt;
    &lt;script src="js/parsley.min.js"&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;</pre>

Next, we&#8217;ll add <span class="attribute">data-parsley-validate</span>=<span class="value">&#8220;&#8221; to the form and then we&#8217;re ready to validate!</span>

<pre class="lang:default decode:true ">&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Front End Validation&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;form id="myForm" action="your_server" method="post"data-parsley-validate=""&gt;
      &lt;input id="name" name="username" type="text" placeholder="Username" /&gt;
      &lt;input id="email" name="email" type="email" placeholder="Email" /&gt;
      &lt;input type="submit" value="Submit" /&gt;
    &lt;/form&gt;
    &lt;script src="https://code.jquery.com/jquery-2.1.4.min.js"&gt;&lt;/script&gt;
    &lt;script src="js/parsley.min.js"&gt;&lt;/script&gt;
    &lt;script&gt;
      $("#myForm").on('submit', function(e) {
        const $form = $(this);

        e.preventDefault();

        $form.parsley().validate();

        if ($form.parsley().isValid()) {
          $form.get(0).submit();
        }
      });
    &lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;</pre>

&nbsp;

When a user tries to submit the form, it will first handle basic validation, making sure the fields aren&#8217;t empty and also that the field with type set to email validates as an email address.

Then, assuming the validation passes, we force the form to actually submit.

 [1]: https://codeplanet.io/wp-content/uploads/2015/11/Screen-Shot-2015-11-28-at-7.33.35-PM.png
 [2]: http://parsleyjs.org/