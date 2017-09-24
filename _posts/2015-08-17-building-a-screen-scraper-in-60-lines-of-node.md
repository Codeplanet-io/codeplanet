---
id: 556
title: Building a Screen Scraper in 60 lines of Node
date: 2015-08-17T10:00:40+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=556
permalink: /building-a-screen-scraper-in-60-lines-of-node/
categories:
  - Node.js
---
The other day I [open sourced a Node.js screen scraper](https://github.com/jkup/scrape-this). It&#8217;s under 60 lines of Node but it has quite a few features. It can:

  * Scrape any website at regular intervals ( using [cron](https://www.npmjs.com/package/cron) )
  * Send an email with the updated results ( using [nodemailer](https://www.npmjs.com/package/nodemailer) )
  * Query data from any part of the DOM ( using [cheerio](https://www.npmjs.com/package/cheerio) )

Feel free to checkout the [source code on Github](https://github.com/jkup/scrape-this/blob/master/index.js)! But I&#8217;ll walk through the basics of the code here:

<pre class="lang:js decode:true ">// We use express for HTTP requests
var express    = require('express');

// We use request to crawl our target page
var request    = require('request');

// We use cheerio to get jQuery functionality
// from the HTML that request returns
var cheerio    = require('cheerio');

// We use nodemailer to send periodic emails
var nodemailer = require('nodemailer');

// We use cron to run our scrape at regular intervals
var CronJob    = require('cron').CronJob;

// This just bootstraps an express application
var fs         = require('fs');
var app        = express();

// this sets up our email credentials
// you can replace YOUR_SERVICE with something
// like 'Gmail' and then enter your email address
// and password
var transporter = nodemailer.createTransport({
    service: 'YOUR_SERVICE',
    auth: {
        user: 'YOUR_EMAIL_ACCOUNT',
        pass: 'YOUR_PASSWORD'
    }
});

// This defined a new endpoint that we'll hit
// to kick off the scraping task
app.get('/scrape', function(req, res){

  var $, scraped_data, url;

  // Enter the URL you want to scrape here
  url = "YOUR_URL";

  // Send a request to the URL we want to scrape
  // and return the data
  request(url, function(error, response, html) {
    
    // Assuming there is no error
    if(!error) {

      // jQuery'ify the returned HTML
      $ = cheerio.load(html);

      // Grab the specific data you want
      // you can also perform operations here
      // like checking if a number is lower than
      // it was yesterday
      scraped_data = $('YOUR_SELECTOR').text();

      // Send an email
      // you can wrap this in a conditional if
      // you'd like
      var mailOptions = {
          from: 'YOUR_SENDER',
          to: 'YOUR_RECIPIENT',
          subject: 'YOUR_SUBJECT',
          text: 'YOUR_MESSAGE' + scraped_data
      };

      // send mail with defined transport object 
      transporter.sendMail(mailOptions, function(error, info){
        if(error) {
          return console.log(error);
        }
        console.log('Message sent: ' + info.response);
      }); 
    }
  });
});

// How frequently should the job run
new CronJob('0 0 * * *', function() {

      // here we use request to hit our express endpoint
      request.get('YOUR_HOST/scrape')

}, null, true, "America/Los_Angeles");

// This is what port the app will run on
app.listen('8081')
console.log('Listening on port 8081');

exports = module.exports = app;</pre>

There is still a lot to do! I want to abstract all of the user options ( email address, password, frequency, etc ) into command line arguments so you don&#8217;t have to edit the source code every time you build one of these.

Hope the walkthrough was helpful, and please feel free to open an issue or send a pull request on [Github](https://github.com/jkup/scrape-this/blob/master/index.js)!