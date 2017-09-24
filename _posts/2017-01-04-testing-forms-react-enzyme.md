---
id: 1321
title: Testing forms with React and Enzyme
date: 2017-01-04T19:19:21+00:00
author: Jon Kuperman
layout: post
guid: https://codeplanet.io/?p=1321
permalink: /testing-forms-react-enzyme/
categories:
  - JavaScript
  - React.js
---
Lately at [Brave](https://github.com/brave/browser-laptop) I&#8217;ve been adding unit tests for our React code. For our project we use:

  * [Mocha](https://mochajs.org/) &#8211; our test framework
  * [Sinon](http://sinonjs.org/) &#8211; for spies
  * [Assert](https://www.npmjs.com/package/assert) &#8211; for assertions
  * [Mockery](https://github.com/mfncooper/mockery) &#8211; for mocks
  * We also use [React](https://facebook.github.io/react/) and [ImmutableJS](https://facebook.github.io/immutable-js/) (not related to testing!)

We also use ES6 Classes for our react code. So we&#8217;ll have a bit of code that looks like this:

<pre class="lang:js decode:true ">class PaymentsTab extends ImmutableComponent {
  render () {
    const minDuration = someFunction()
    return &lt;div&gt;
      &lt;select
        data-test-id='durationSelector'
        className='form-control'
        defaultValue={minDuration}
        onChange={changeSetting.bind(null, this.props.onChangeSetting, settings.MINIMUM_VISIT_TIME)}&gt;&gt;
        &lt;option value='5000'&gt;5 seconds&lt;/option&gt;
        &lt;option value='8000'&gt;8 seconds&lt;/option&gt;
        &lt;option value='60000'&gt;1 minute&lt;/option&gt;
      &lt;/select&gt;
    &lt;/div&gt;
  }
}</pre>

Enzyme makes it really easy to test a component like this but I struggled to test the default value of the form. In the end I found a good thread on their Github repo and ended up testing it this way:

<pre class="lang:js decode:true">it('defaults to 5 minimum publisher visits', function () {
  const wrapper = shallow(
    &lt;PaymentsTab /&gt;
  )

  assert.equal(wrapper.find('[data-test-id="visitSelector"]').node.value, 5)
})</pre>

We use data-test-id any time we need a unique identifier for testing purposes. So we can just shallow render the component, call find() on the test id and then use **.node.value** to get the default value!

Hope that helps!

&nbsp;