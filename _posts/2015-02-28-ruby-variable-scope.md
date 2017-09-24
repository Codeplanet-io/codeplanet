---
id: 386
title: Ruby Variable Scope
date: 2015-02-28T00:51:37+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=386
permalink: /ruby-variable-scope/
categories:
  - Ruby
---
Ruby is an interesting language. One cool concept is that all variables mark their own scope via the first character in their name. Here are your options:

### Global Variables

Global variables in Ruby start with the \`$\`sign.

<pre class="lang:ruby decode:true">$foo = 3 # Global 3
$BAR = 10 # Global 10</pre>

### Constants

In Ruby, constants are variables that begin with capital letters.

<pre class="lang:ruby decode:true ">A_CONST = 10 # 10
A_CONST = 20 # warning: already initialized constant A_CONST
FOO = 10 # This also works</pre>

### Instance Variables

Ruby instance variables begin with the \`@\`sign.

<pre class="lang:default decode:true">class Person
  def initialize(name, age)
    @name = name
    @age = age
    birthplace = "San Francisco, CA"
  end
  
  def show
    puts @name
    puts @age
    puts birthplace
  end
end

Person.new("Jon",27).show # undefined local variable or method `birthplace'</pre>

### Class Variables

Class variables in Ruby are very similar to instance variables. Instead of a single \`@\`sign, they begin with two, such as \`@@foo\`. While instance variables are shared by every method of an individual object, class variables **are shared between all instances of a class.**

<pre class="lang:ruby decode:true  ">class Person
  def initialize(name, age)
    @@name = name # Setting name will change it for all instances of Person
    @@age = age
    birthplace = "San Francisco, CA"
  end
  
  def show
    puts @@name
    puts @@age
    puts birthplace
  end
end

Person.new("Jon",27).show # undefined local variable or method `birthplace'</pre>