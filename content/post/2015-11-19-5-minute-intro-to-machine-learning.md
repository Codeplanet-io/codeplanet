---
title: 5-Minute Intro to Machine Learning
author: Kelly King
type: post
date: 2015-11-19T17:00:29+00:00
draft: true
url: /?p=738
categories:
  - Uncategorized

---
<p class="graf--p">
  I’ve been curious about Machine Learning for a long time, but always felt too intimidated to learn it. At Twitter, we have an entire Machine Learning staff that works on complex features like Trends and Follow Recommendations; things that you can’t just pull out of a database and display on a webpage. We have PHD students from Stanford intern with us to study our data; they comb through terabytes of information to find usage patterns, help us understand our users, and make Twitter a better product.
</p>

<p class="graf--p">
  When I was in college, my assignments were things like fake shopping carts and Assembly interpreters —  contrived projects with right and wrong solutions. Machine Learning is nothing like that: it uses concepts like models and training; instead of right and wrong answers, it gives probabilities and predictions. Machine Learning sounds math-y, smart, and mysterious —  and totally out of my league.
</p>

<p class="graf--p">
  <a href="https://codeplanet.io/wp-content/uploads/2015/10/blackboard3.jpg"><img class="alignnone size-full wp-image-741" src="https://codeplanet.io/wp-content/uploads/2015/10/blackboard3.jpg" alt="math on a chalkboard" width="1920" height="813" srcset="https://codeplanet.io/wp-content/uploads/2015/10/blackboard3.jpg 1920w, https://codeplanet.io/wp-content/uploads/2015/10/blackboard3-300x127.jpg 300w, https://codeplanet.io/wp-content/uploads/2015/10/blackboard3-768x325.jpg 768w, https://codeplanet.io/wp-content/uploads/2015/10/blackboard3-1024x434.jpg 1024w, https://codeplanet.io/wp-content/uploads/2015/10/blackboard3-1200x508.jpg 1200w" sizes="(max-width: 1920px) 100vw, 1920px" /></a>
</p>

<p class="graf--p">
  When I joined Twitter almost a year and a half ago, I felt like I didn’t belong. I would come home from work exhausted from trying to figure things out on my own instead of asking co-workers for help (lest they find out what a fraud I am!). Over time, thankfully, I started to understand our codebase, and I made some friends at work. A few months after that, I stopped feeling so tired all the time. Eventually, finally, I started coding on the weekends again.
</p>

<p class="graf--p">
  When my friend Priya — a Business Analyst making the transition into Data Science — said she wanted to take <a class="markup--anchor markup--p-anchor" href="https://www.coursera.org/learn/machine-learning/" data-href="https://www.coursera.org/learn/machine-learning/">Coursera’s Machine Learning class</a> two weeks ago, I felt excited. Priya is so fun and down-to-earth; if she could understand Machine Learning, so could I! Better yet, we could learn ML together!
</p>

<p class="graf--p">
  Okay. Yes. That was a lot of preamble — especially if I’m trying to demystify Machine Learning in five minutes. I just wanted to share how intimidated I was (and still am) by ML to set the stage for this super lightweight introduction to Machine Learning. So now that you’ve spent two of your five minutes reading about me, let’s get into it! I plan to blog throughout this 11-week class, but today I present a high-level glimpse into what Machine Learning is.
</p>

### Intro to Machine Learning {.graf--h3}

#### Two (or three) Definitions {.graf--h4}

<ol class="postList">
  <li class="graf--li">
    Machine learning is the field of study that gives computers the ability to learn without being explicitly programmed.
  </li>
  <li class="graf--li">
    Machine learning is programming a computer so that its performance (P) at a specific task (T) improves with experience (E).
  </li>
</ol>

<p class="graf--p">
  Crystal clear, right?
</p>

<p class="graf--p">
  Okay, maybe not. Maybe my own down-to-earth, completely-non-scientific definition will help:
</p>

<p class="graf--p">
  Machine learning is using <strong class="markup--strong markup--p-strong">programming</strong>, <strong class="markup--strong markup--p-strong">data</strong> and <strong class="markup--strong markup--p-strong">math</strong> to figure out a problem that we can’t solve by hand. ML can be used for such a variety of tasks that maybe it’s easiest to just talk about those things directly.
</p>

#### Types of Machine Learning {.graf--h4}

<ol class="postList">
  <li class="graf--li">
    Learning from large data sets (Facial recognition in iPhoto — the more you tag, the better iPhoto is at guessing your faces!)
  </li>
  <li class="graf--li">
    Apps that can’t be programmed by hand (autonomous vehicles, handwriting recognition)
  </li>
  <li class="graf--li">
    Self-customizing programs (Amazon and Netflix recommendations — the likelihood you will enjoy something based on your history plus the history of other users)
  </li>
</ol>

[<img class="alignnone size-full wp-image-742" src="https://codeplanet.io/wp-content/uploads/2015/10/Screen-Shot-2015-10-16-at-7.09.52-PM.png" alt="Netflix recommendations" width="1249" height="378" srcset="https://codeplanet.io/wp-content/uploads/2015/10/Screen-Shot-2015-10-16-at-7.09.52-PM.png 1249w, https://codeplanet.io/wp-content/uploads/2015/10/Screen-Shot-2015-10-16-at-7.09.52-PM-300x91.png 300w, https://codeplanet.io/wp-content/uploads/2015/10/Screen-Shot-2015-10-16-at-7.09.52-PM-768x232.png 768w, https://codeplanet.io/wp-content/uploads/2015/10/Screen-Shot-2015-10-16-at-7.09.52-PM-1024x310.png 1024w, https://codeplanet.io/wp-content/uploads/2015/10/Screen-Shot-2015-10-16-at-7.09.52-PM-1200x363.png 1200w" sizes="(max-width: 1249px) 100vw, 1249px" />][1]

<p class="graf--p">
  Let’s keep on this example path. All of the use cases above are pretty complicated and frankly, I haven’t learned how to do anything that complex yet. Let’s solve a more contrived problem to see how we use data and math to make a prediction about something really simple.
</p>

#### Contrived Example: How much is my house worth? {.graf--h4}

<p class="graf--p">
  Imagine a super simple market in which housing prices are based on just one factor: square footage. I have a graph of the housing prices in my neighborhood, like this:
</p><section class=" section--body section--first section--last"> 

<div class="section-content">
  <div class="section-inner layoutSingleColumn">
    <figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*p4dSHJtxBRalpw4VIAuliw.png" alt="" data-image-id="1*p4dSHJtxBRalpw4VIAuliw.png" data-width="1472" data-height="750" data-delayed-src="https://cdn-images-1.medium.com/max/800/1*p4dSHJtxBRalpw4VIAuliw.png" />
    </div></figure> 
    
    <p class="graf--p graf-after--figure">
      If my house is 750 square feet, we can glance at that graph and pretty easily determine that my house will sell for about $200k. Ok, that’s common sense.
    </p>
    
    <p class="graf--p graf-after--p">
       But how do we deal with less clear cases? At the 600 sqft mark, it looks like there is one house for 150k and another for 220k. Moreover, how can we use this chart without having to “eyeball” it? Wouldn’t it be better to have a formula, where you could plug in any number of square feet and get back a price? Let’s try to find an <strong class="markup--strong markup--p-strong">equation for a line that fits that data as well as possible</strong>.
    </p>
    
    <p class="graf--p graf-after--p">
      Remembering back to algebra, the equation of a line looks something like <em class="markup--em markup--p-em">y = mx + b</em>, which would give us a straight line (see the pink line below). Or, we could use a quadratic function to get a curved line, like <em class="markup--em markup--p-em">y = ax^2 + bx + c </em>(the blue line below).
    </p><figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*1_3HzwzTOa5ewYfqiq1tiw.png" alt="" data-image-id="1*1_3HzwzTOa5ewYfqiq1tiw.png" data-width="1438" data-height="780" data-delayed-src="https://cdn-images-1.medium.com/max/800/1*1_3HzwzTOa5ewYfqiq1tiw.png" />
      </p>
    </div></figure> 
    
    <p class="graf--p graf-after--figure">
      It was pretty easy to draw that by hand — but how would we tell a computer to do this? It turns out that this is a pretty standard task in statistics called a <strong class="markup--strong markup--p-strong">linear regression</strong>. The basic idea is to plot out a bunch of different lines, and then calculate the distance between each line and the actual points in our data set.
    </p><figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*NmuuIGnO0aZB9JDcCb6z6g.png" alt="" width="512" height="363" data-image-id="1*NmuuIGnO0aZB9JDcCb6z6g.png" data-width="608" data-height="444" data-delayed-src="https://cdn-images-1.medium.com/max/800/1*NmuuIGnO0aZB9JDcCb6z6g.png" />
      </p>
    </div></figure> 
    
    <p class="graf--p graf-after--figure">
      In the figure above, I’ve drawn a blue, pink, green, purple and several black lines as guesses, or <strong class="markup--strong markup--p-strong">hypotheses</strong>. Assuming we have some code that can generate an infinite number of hypothesis lines (<strong class="markup--strong markup--p-strong">we do NOT have this code yet)</strong>, then we can use a special formula to pick the best line.
    </p>
    
    <h4 class="graf--h4 graf-after--p">
      Cost Function
    </h4>
    
    <p class="graf--p graf-after--h4">
      This formula is called the <strong class="markup--strong markup--p-strong">cost function</strong>, and it checks the distance between a single hypothesis line and every data point in our data set. The lower the cost function, the more accurate our line is. To find the best hypothesis, we need to apply the cost function to each of our hypothetical lines, and choose the line with the <strong class="markup--strong markup--p-strong">lowest</strong> cost function value.
    </p>
    
    <p class="graf--p graf-after--p">
      Again, we don’t yet have the code for generating an infinite number of hypotheses, but we <strong class="markup--strong markup--p-strong">do</strong> have the formula for checking the accuracy of a single given line. Here it is:
    </p><figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*0ixpaDW2w9JDp_6NAz80vA.png" alt="" data-image-id="1*0ixpaDW2w9JDp_6NAz80vA.png" data-width="572" data-height="91" data-delayed-src="https://cdn-images-1.medium.com/max/800/1*0ixpaDW2w9JDp_6NAz80vA.png" data-pin-nopin="true" />
      </p>
    </div></figure> 
    
    <p class="graf--p graf-after--figure">
      Yes, that looks very math-y, but I promise it’s actually pretty simple!
    </p>
    
    <p class="graf--p graf-after--p">
      J(0,0) is just a mathematical representation of “how far away is our hypothesis line from the actual data?” In plain English, our cost function adds the predicted y minus actual y (squared) at each point in our data set, and then calculates the average.
    </p>
    
    <p class="graf--p graf-after--p">
      In the drawing below, our actual data points are at the red x marks, and our current hypothesis line (h) is the straight black line. To calculate how “off” our prediction is, we can just measure the differences in predicted versus actual y values at each point x.
    </p><figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*Ay8e-pzzD1Q8dE2_UfKWHQ.png" alt="" data-image-id="1*Ay8e-pzzD1Q8dE2_UfKWHQ.png" data-width="324" data-height="266" />
      </p>
    </div></figure> 
    
    <h4 class="graf--h4 graf-after--figure">
      Demo calculation
    </h4>
    
    <p class="graf--p graf-after--h4">
      Let’s calculate the cost function of the graph above. This chart below gets its values from the graph.
    </p><figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/600/1*DKHLNJLupHaW6tKFoaiqNw.png" alt="" data-image-id="1*DKHLNJLupHaW6tKFoaiqNw.png" data-width="293" data-height="100" data-delayed-src="https://cdn-images-1.medium.com/max/800/1*DKHLNJLupHaW6tKFoaiqNw.png" />
      </p>
    </div></figure> 
    
    <p class="graf--p graf-after--figure">
      For example, at x = 1, our predicted value from the black line is y = 0.5, but our actual data (the red x) is y = 1. Let’s plug the values from our chart into the cost function formula, keeping in mind that the complicated-looking <em class="markup--em markup--p-em">h</em> term, <em class="markup--em markup--p-em">h0(x(i)) — y(i))</em>, is just the value from the last column in our table:
    </p><figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*0ixpaDW2w9JDp_6NAz80vA.png" alt="" data-image-id="1*0ixpaDW2w9JDp_6NAz80vA.png" data-width="572" data-height="91" data-pin-nopin="true" />
      </p>
    </div></figure> 
    
    <p class="graf--p graf-after--figure">
      The Greek “E” symbol above means we are finding the <strong class="markup--strong markup--p-strong">sum</strong> of all of our <em class="markup--em markup--p-em">h </em>terms as we go from x = 1 to x = 3. That is to say, we will take the last column of the table above, square each value, and sum those together. Since we have three (x,y) coordinates, we will add three terms. (The <em class="markup--em markup--p-em">1/2m </em>part of the formula just turns this into an average).
    </p>
    
    <p class="graf--p graf-after--p">
      J = 1/2m * -0.5^2 + -1^2 + -1.5^2)<br /> J = 1/2m * (.25 + 1 + 2.25)<br /> J = 1/2m * 3.5
    </p>
    
    <p class="graf--p graf-after--p">
      If <em class="markup--em markup--p-em">m </em>is the number of data points (3), then:<br /> J = 1/(2*3) * 3.5<br /> J = 1/6 * 3.5<br /> J = 0.58
    </p>
    
    <p class="graf--p graf-after--p">
      If we made our line a little more steep (like the pink line below), you can probably imagine a smaller distance between our hypothesis line and the data points, which would result in a lower cost function (ie. a better hypothesis)!
    </p><figure class="graf--figure is-defaultValue graf-after--p" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*1dQt6qMrAsVZf4ZuyXp54w.png" alt="" data-image-id="1*1dQt6qMrAsVZf4ZuyXp54w.png" data-width="324" data-height="266" data-delayed-src="https://cdn-images-1.medium.com/max/800/1*1dQt6qMrAsVZf4ZuyXp54w.png" />
      </p>
    </div></figure> 
    
    <h4 class="graf--h4 graf-after--figure">
      Before you go
    </h4>
    
    <p class="graf--p graf-after--h4">
      That’s the end of week 1. I hope, like me, you were surprised by how intuitive this process was! Before you go, here are a few quick terms I didn’t get a chance to mention above:
    </p>
    
    <ol class="postList">
      <li class="graf--li graf-after--p">
        <strong class="markup--strong markup--li-strong">Supervised Learning</strong>: the housing example above is an example of supervised machine learning. It means we have data which tells us the “right” answer.
      </li>
      <li class="graf--li graf-after--li">
        <strong class="markup--strong markup--li-strong">Unsupervised Learning</strong>: Sometimes we may have a bunch of data, and have no idea what a correct solution looks like. For example, if our data set was a social graph, machine learning may help us find things like clusters of friend groups.
      </li>
      <li class="graf--li graf-after--li">
        <strong class="markup--strong markup--li-strong">Regression</strong>: The solution is a continuous value, such as home price in dollars.
      </li>
      <li class="graf--li graf-after--li">
        <strong class="markup--strong markup--li-strong">Classification</strong>: The solution is a discreet value, such as the likelihood that a tumor is 0: benign or 1: malignant.
      </li>
    </ol><figure class="graf--figure is-defaultValue graf-after--li" tabindex="0" contenteditable="false"> 
    
    <div class="aspectRatioPlaceholder is-locked">
      <div class="aspect-ratio-fill">
      </div>
      
      <p>
        <img class="graf-image" src="https://cdn-images-1.medium.com/max/800/1*PeyXbeJnIHD7qqtmxucQFw.png" alt="" data-image-id="1*PeyXbeJnIHD7qqtmxucQFw.png" data-width="1860" data-height="718" data-delayed-src="https://cdn-images-1.medium.com/max/800/1*PeyXbeJnIHD7qqtmxucQFw.png" />
      </p>
    </div></figure> 
    
    <p class="graf--p graf-after--figure graf--last">
      That’s it! Check back soon for Machine Learning Week 2 notes!
    </p>
  </div>
</div></section> 

<div class="inlineTooltip2 button-scalableGroup">
</div><footer class="postArticle-footer"></footer>

 [1]: https://codeplanet.io/wp-content/uploads/2015/10/Screen-Shot-2015-10-16-at-7.09.52-PM.png