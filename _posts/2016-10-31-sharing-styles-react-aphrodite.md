---
id: 1306
title: Sharing Styles with React and Aphrodite
date: 2016-10-31T21:47:10+00:00
author: Jon Kuperman
layout: post
guid: https://codeplanet.io/?p=1306
permalink: /sharing-styles-react-aphrodite/
image: /wp-content/uploads/2016/10/react.png
categories:
  - CSS
  - JavaScript
  - React.js
---
Lately I&#8217;ve been using Khan Academy&#8217;s [Aphrodite](https://github.com/Khan/aphrodite) in a lot of my projects. React and Aphrodite work very well together! (although React is not a requirement) and makes managing CSS a lot easier!

Using React and Aphrodite together makes each component look something like this:

<pre class="lang:js decode:true">import React, { Component } from 'react'
import { StyleSheet, css } from 'aphrodite'
import logo from './logo.svg'

const styles = StyleSheet.create({
  App: {
    textAlign: 'center'
  },

  AppLogo: {
    animation: 'AppLogoSpin infinite 20s linear',
    height: '80px'
  },

  AppHeader: {
    backgroundColor: '#222',
    height: '150px',
    padding: '20px',
    color: 'white'
  },

  AppIntro: {
    fontSize: 'large'
  }
})

class App extends Component {
  render () {
    return (
      &lt;div className={css(styles.App)}&gt;
        &lt;div className={css(styles.AppHeader)}&gt;
          &lt;img src={logo} className={css(styles.AppLogo)} alt='logo' /&gt;
          &lt;h2&gt;Welcome to React&lt;/h2&gt;
        &lt;/div&gt;
        &lt;p className={css(styles.AppIntro)}&gt;
          To get started, edit &lt;code&gt;src/App.js&lt;/code&gt; and save to reload.
          &lt;button&gt;Click Me&lt;/button&gt;
        &lt;/p&gt;
      &lt;/div&gt;
    )
  }
}

export default App</pre>

What I love about these two together is that your styles are colocated with your JavaScript components. In practice, this means that it&#8217;s often trivial to find and fix style issues as once you&#8217;ve found the component, you&#8217;re already in the right file!

Coming from a Sass / LESS background one of the things I missed most was being able to easily share styles via creating and importing specific files like Buttons.less and then including them wherever they are needed!

Aphrodite allows you to pass styles as props, something like this:

<pre class="lang:js decode:true">class App extends Component {
  render() {  
    return &lt;Marker styles={[styles.large, styles.red]} /&gt;;
  }
}

class Marker extends Component {
  render() {
    // css() accepts styles, arrays of styles (including nested arrays),
    // and falsy values including undefined.
    return &lt;div className={css(styles.marker, this.props.styles)} /&gt;;
  }
}

const styles = StyleSheet.create({
  red: {
    backgroundColor: 'red'
  },

  large: {
    height: 20,
    width: 20
  },

  marker: {
    backgroundColor: 'blue'
  }
};</pre>

So therefore Marker gets its styling from App. The only issue here is that you&#8217;ll have to pass your shared styles all the way down through your app if a lower component needs something from its parent.

In order to work around that I had an idea for creating individual .js files that export themselves as an Aphrodite StyleSheet object. That way you can create something like:

<pre class="lang:js decode:true ">import { StyleSheet } from 'aphrodite'

export default StyleSheet.create({
  Button: {
    background: 'red'
  }
})
</pre>

and then later in your app:

<pre class="lang:default decode:true  ">import React, { Component } from 'react'
import { StyleSheet, css } from 'aphrodite'
import ButtonStyles from './styles/Buttons'
import logo from './logo.svg'

const styles = StyleSheet.create({
  App: {
    textAlign: 'center'
  },

  AppLogo: {
    animation: 'AppLogoSpin infinite 20s linear',
    height: '80px'
  },

  AppHeader: {
    backgroundColor: '#222',
    height: '150px',
    padding: '20px',
    color: 'white'
  },

  AppIntro: {
    fontSize: 'large'
  }
})

class App extends Component {
  render () {
    return (
      &lt;div className={css(styles.App)}&gt;
        &lt;div className={css(styles.AppHeader)}&gt;
          &lt;img src={logo} className={css(styles.AppLogo)} alt='logo' /&gt;
          &lt;h2&gt;Welcome to React&lt;/h2&gt;
        &lt;/div&gt;
        &lt;p className={css(styles.AppIntro)}&gt;
          To get started, edit &lt;code&gt;src/App.js&lt;/code&gt; and save to reload.
          &lt;button className={css(ButtonStyles.Button)}&gt;Click Me&lt;/button&gt;
        &lt;/p&gt;
      &lt;/div&gt;
    )
  }
}

export default App
</pre>

It seems to work nicely so far. I&#8217;d love to hear your thoughts!

Check out [this demo project](https://github.com/jkup/aphrodite-react) if you&#8217;d like to see an example!