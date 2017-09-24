---
title: How to create React components
author: Jon Kuperman
type: post
date: 2016-07-11T10:00:15+00:00
url: /create-react-components/
categories:
  - JavaScript
  - React.js

---
There are now three ways to create React components in JavaScript. Let&#8217;s take a quick look at each of them and discuss the pros and cons!

## Create React Components with React.createClass

The first way, and the way Facebook still uses is the createClass method. It looks something like this:

<pre class="lang:js decode:true">var MyComponent = React.createClass({
  render: function() {
    return (
      &lt;div&gt;
        {this.props.name}
      &lt;/div&gt;
    );
  }
});</pre>

This is my favorite way of creating components. As we explore the other options you&#8217;ll see some of the extra boilerplate or limitations with them.

## Creating Components with ES6 Classes

With ES6, we can now create react components with ES6 classes. They look like this:

<pre class="lang:js decode:true">export class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      &lt;div&gt;
        {this.props.name}
      &lt;/div&gt;
    );
  }
}</pre>

While I do like the ES6 class syntax, there are a few things I don&#8217;t love about creating components this way.

  * There is no more `getInitialState` method. All the logic you would put in `getInitialState` now must go in the constructor.
  * `propTypes` and `defaultProps` are defined as properties on the constructor instead of in the class body.
  * No mixin support.
  * No more autobinding. This means that you either have to explicitly bind this or use an arrow function. Example below. <pre class="lang:default decode:true">// You can use bind() to preserve `this`
&lt;div onClick={this.tick.bind(this)}&gt;

// Or you can use arrow functions
&lt;div onClick={() =&gt; this.tick()}&gt;</pre>

## Creating Stateless React Functions

I find these really cool. If your component doesn&#8217;t have its own state, you can just use regular JavaScript functions!

<pre class="lang:js decode:true ">function MyComponent(props) {
  return &lt;div&gt;{props.name}&lt;/div&gt;;
}</pre>

If you want to get really fancy with it, you can use ES6 arrow functions!

<pre class="lang:js decode:true ">const MyComponent = (props) =&gt; &lt;div&gt;{props.name}&lt;/div&gt;;</pre>

## Resources

If you&#8217;re looking to learn more, here are some resources!

  * The [official Component documentation][1].
  * [In depth comparison][2] between createClass and ES6 classes.

Have fun!

 [1]: https://facebook.github.io/react/docs/reusable-components.html
 [2]: https://toddmotto.com/react-create-class-versus-component/