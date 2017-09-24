---
title: Getting started with Node.js and bcrypt
author: Jon Kuperman
type: post
date: 2015-11-24T17:00:15+00:00
excerpt: Looking for a safe way to store user passwords in your Node.js application? Check out this bcrypt tutorial!
url: /getting-started-with-node-js-and-bcrypt/
categories:
  - Node.js

---
[<img class="aligncenter size-large wp-image-784" src="https://codeplanet.io/wp-content/uploads/2015/11/encryption-1024x576.jpeg" alt="Stock encryption image" width="660" height="371" srcset="https://codeplanet.io/wp-content/uploads/2015/11/encryption-1024x576.jpeg 1024w, https://codeplanet.io/wp-content/uploads/2015/11/encryption-300x169.jpeg 300w, https://codeplanet.io/wp-content/uploads/2015/11/encryption-768x432.jpeg 768w, https://codeplanet.io/wp-content/uploads/2015/11/encryption-1200x675.jpeg 1200w" sizes="(max-width: 660px) 100vw, 660px" />][1]

For those of you looking for a safe way to store user passwords in your Node.js application, look no further!

Introducing [bcrypt][2].

This Node package uses the [UNIX bcrypt library][3] first invented in 1999. It allows you to hash and encrypt sensitive data like user passwords before storing them in your database.

Let&#8217;s check out an example!

First you&#8217;ll want to install bcrypt and save it to your current project

<pre class="lang:default decode:true ">npm install bcrypt --save</pre>

Then, inside your node app, create a salt and use the hashSync method to turn a plain text password into an encrypted hash.

<pre class="lang:js decode:true ">// Your node app

// Require the bcrypt package
var bcrypt = require('bcrypt');

// Create a password salt
var salt = bcrypt.genSaltSync(10);

// Salt and hash password
var passwordToSave = bcrypt.hashSync(passwordFromUser, salt)

</pre>

Last, whenever you need to pull a password out of your database and check it against one the user entered ( like when they are trying to log back in! ) just do something like this:

<pre class="lang:js decode:true ">// Grab user from your database - this example uses MysQL
connection.query("SELECT * FROM users WHERE username = ?",
    [usernameEnteredByUser],
    function(err, rows) {
        if (err) {
            return done(err);
        }

        if (bcrypt.hashSync(passwordEnteredByUser, salt) === rows[0].password) {
          // Yay, it worked!
        }
});</pre>

This should provide you an easy solution for storing and retrieving passwords in a way that is safe. Even if your databases are compromised, any attackers would only get access to the salted and hashed passwords.

 [1]: https://codeplanet.io/wp-content/uploads/2015/11/encryption.jpeg
 [2]: https://www.npmjs.com/package/bcrypt-nodejs
 [3]: https://en.wikipedia.org/wiki/Bcrypt