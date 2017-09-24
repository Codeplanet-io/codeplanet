---
title: Building Simon Says with JavaScript
author: Kelly King
type: post
date: 2014-01-02T04:08:26+00:00
url: /building-simon-says-javascript/
categories:
  - JavaScript

---
This is a tutorial that will show you how to make the classic Simon Says game on the web using JavaScript. The project lives on <a href="https://github.com/kellyk/javascript-simon" target="_blank">GitHub</a>, so please check out the source code, star the repo, or do a pull request!

## Demo

<a href="http://www.kellyking.me/projects/simon/" target="_blank"><img class="alignnone size-full wp-image-160 demo" alt="Simon Says game" src="https://codeplanet.io/wp-content/uploads/2014/01/simon.jpg" width="400" height="400" srcset="https://codeplanet.io/wp-content/uploads/2014/01/simon.jpg 400w, https://codeplanet.io/wp-content/uploads/2014/01/simon-150x150.jpg 150w, https://codeplanet.io/wp-content/uploads/2014/01/simon-300x300.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" /></a>

## Mark-up

The HTML used for the Simon &#8220;board&#8221; is just an unsorted list with some fancy CSS.

    
    <div class="simon">
    	<ul>
    		<li class="red" data-tile="1"></li>
    		<li class="blue" data-tile="2"></li>
    		<li class="yellow" data-tile="3"></li>
    		<li class="green" data-tile="4"></li>
    	</ul>
    </div>
    

One thing you may notice is that there are two &#8220;identifiers&#8221; for each list item &#8212; a color class and a data-tile attribute. The classes are used for styles, and data- attributes for [JavaScript selectors][1].

## JavaScript

Simon Says is a really simple game, so the code is short (~100 lines). The more difficult part is controlling the &#8220;Light Up&#8221; animation, so I&#8217;ll cover that first.

### Lighting Up

To simulate the lighting, we can just change the background opacity on the list items. However, controlling the order and timing of the light up/down pattern is more complicated. To solve this, we have an array called sequence, filled with numbers that represent colors. When we need to animate, we send the array to the animate function, like this:

    
    
    function newRound() {
    	var sequence = [1,2,1]; //red, green, red
    	animate(sequence);
    }
    
    function animate(sequence) {
    	var i = 0;
    	var interval = setInterval(function() {
    		lightUp(sequence[i]);
    
            i++;
            if (i >= sequence.length) {
    			clearInterval(interval);
            }
       }, 600);
    }
    

We want to make sure the items light up and then down, one at a time. We can use JavaScript&#8217;s setInterval method to regulate the timing. Then whenever the interval function fires, we can increment an index to track our progress over the sequence array, firing a second function, lightUp(), with the current color in the sequence. When we reach the end of the sequence array, we can just clear the interval.

Finally, we define the lightUp() function, which first adds a class of &#8220;lit&#8221;, brightening the background by lowering its opacity. After a 300ms timeout, we remove the &#8220;lit&#8221; class, thus restoring the tile to its normal color. The CSS includes a transition on the opacity property, which makes the animation appear smooth.

    
    function lightup(tile) {
    	var $tile = $('[data-tile=' + tile + ']').addClass('lit');
    	window.setTimeout(function() {
    		$tile.removeClass('lit');
    	}, 300);
    
    }
    

### Sound

Disclaimer: the method used for playing sounds in this demo is sub-optimal. Currently, sounds are embedded on the fly as the playSound() function is triggered, and since the following HTML audio element is set to autoplay, the sound fires right away:

    
    function playSound(tile) {
    	var audio = $('<audio autoplay></audio>');
    	audio.append('<source src="sounds/' + tile + '.ogg" type="audio/ogg" />');
    	audio.append('<source src="sounds/' + tile + '.mp3" type="audio/mp3" />');
    	$('[data-action=sound]').html(audio);
    }
    

The problem with this approach is that we are retrieving each sound from the server every time a sound is played. Since there are only four tones, we should instead be using JavaScript to fire the play() method on the appropriate audio element in HTML. However, I did not use this approach, because without a sound library, it is difficult to interrupt one sound file in order to play the same sound again. For example, if a user clicks the green tile twice in a row, the sound may not play the second time. However if we re-embed the audio tag, this is not an issue. It&#8217;s a hack, but it works.

### Game Sequence

Finally, the game sequence is controlled something like this:

  1. Wait for player to click start
  2. Start a round, which follows these steps 
      1. Add a random number (1-4) to the sequence
      2. Animate the sequence to the user
      3. Enable user interaction with the board, and register any clicks on the Simon tiles
      4. While the player has not entered an incorrect response, and the number of clicks is less than the length of the sequence, wait for player input
  3. Continue adding rounds until the player loses

To view the full source code, please visit my [GitHub repo][2], and don&#8217;t forget to star it!
  
[<img src="https://codeplanet.io/wp-content/uploads/2014/01/github-cat.jpg" alt="Github Logo" width="200" height="200" class="alignnone size-full wp-image-204" srcset="https://codeplanet.io/wp-content/uploads/2014/01/github-cat.jpg 200w, https://codeplanet.io/wp-content/uploads/2014/01/github-cat-150x150.jpg 150w" sizes="(max-width: 200px) 100vw, 200px" />][2]

 [1]: http://codeplanet.io/better-javascript-selectors/
 [2]: https://github.com/kellyk/javascript-simon