---
title: Laravel 4 Eloquent Model Relationships, Part 1.
author: Dan Trenz
type: post
date: 2014-01-21T16:04:20+00:00
url: /laravel-model-relationships-pt-1/
categories:
  - Web Development
tags:
  - laravel
  - mvc
  - mysql
  - oop
  - php

---
## The Benefits of Making Your Models &#8220;Eloquent&#8221;

If you are familiar with MVC and are learning Laravel 4, you may be tempted to simply use models as a place to store your database logic. However, you would be robbing yourself of the many benefits of extending the [Eloquent Object-Relational Mapper][1] in your applications.

Among these benefits are route & form model binding &#8211; both of which are features that can save you loads of time and spare you from having to write the same boring code that is required in just about every web application.

## Enter Laravel Model Relationships

One of the more powerful features of the Eloquent ORM are model relationships. Model relationships, once defined, enable you to fetch & update a model object in your database, as well as any models it is related to, without having to write explicit query logic. Common tasks like fetching blog posts along with all metadata, author data, and comments associated with them become trivial.

As of Laravel 4.0 there were the 3 primary types of relationships:

  * **One-to-One**
  * **One-to-Many**
  * **Many-to-Many**

&nbsp;

Laravel 4.1 (released late 2013) brings with it a couple more relationship types:

  * **Has-Many-Through**
  * **Polymorphic One-to-One/One-to-Many**

&nbsp;

This article will cover the first 3 relationship types available as of Laravel 4.0; **one-to-one**, **one-to-many**, & **many-to-many**.

Look for a future article that will cover Eloquent relationships introduced in Laravel 4.1.

## A Simple Blog Example

For the sake of illustration, we will be looking at how these relationships might be used in a real-world web application, such as a blog.

This demo project is a very simple web development blog that has posts, authors, & content tags (i.e. HTML, CSS, Javascript, PHP, MySQL, MongoDB).

[<img class="aligncenter size-large wp-image-262" src="https://codeplanet.io/wp-content/uploads/2014/01/blog-homepage-1024x738.png" alt="Laravel Eloquent Blog Example" width="640" height="461" />][2]

The project that we will be using can be found here: <a title="https://github.com/dtrenz/laravel-model-demo" href="https://github.com/dtrenz/laravel-model-demo" target="_blank">https://github.com/dtrenz/laravel-model-demo</a>

To setup the project;

  1. clone the repo
  2. run `composer install`
  3. create a new database in MySQL
  4. update the db connecton (i.e. host, database, username, password) in app/config/database.php
  5. run migrations, to setup the DB schema: `php artisan migrate`
  6. seed the DB with sample data: `php artisan db:seed`

## One-to-One

Let&#8217;s start with a one-to-one relationship. For the purposes of this demo, I&#8217;ve chosen a somewhat contrived example of a one-to-one relationship.

Each blog post has a title and body text, but the body text is stored in a separate table, called &#8220;texts.&#8221;

Here is the schema for posts and texts:

posts
:   &#8211; id
:   &#8211; title

texts
:   &#8211; id
:   &#8211; text
:   &#8211; post_id

You can see that the texts table has a foreign key of post_id, since each post &#8220;owns&#8221; one text.

Eloquent needs to know how to map a relationship from a post to text. We define this relationship in each model.

First, we create a model file for each of these models, tell Eloquent which table to find the data for the model, and then define the relationship using a model method:

<pre class="lang:php mark:15-18 whitespace-before:1 whitespace-after:1 decode:true" title="app/models/Post.php">class Post extends Eloquent {

    /**
     * The database table used by the model.
     *
     * @var string
     */
    protected $table = 'posts';

    /**
     * Defines a one-to-one relationship.
     *
     * @see http://laravel.com/docs/eloquent#one-to-one
     */
    public function text()
    {
        return $this-&gt;hasOne('Text');
    }

}
</pre>

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true" title="app/models/Text.php">class Text extends Eloquent {

    /**
     * The database table used by the model.
     *
     * @var string
     */
    protected $table = 'texts';

}
</pre>

That was easy, right?

All we had to do was return a hasOne relationship to the Text model and now, anytime you need to access or display the text for a given post, you can simply reference the text attached to the post as if it were a direct property on the post object:

`$post->text`

But&#8230;how?

By returning a hasOne relationship in a method called &#8220;text()&#8221; Eloquent is able to map that method to the row in the texts table with the current post_id. It then returns that row as an instance of the Text model. This enables you to get the text, like so:

`$post->text()->first()`

But that&#8217;s not all! Eloquent gives you a dynamic property for accessing the text directly, w/o having to use query builder methods like &#8220;first().&#8221; This enables you to get the text, like so:

`$post->text`

## One-to-Many

Next, let&#8217;s try a one-to-many relationship &#8211; this is probably the most common relationship type you will use. In our blog we have posts and each post belongs to a single author. In other words, _one_ author can have _many_ posts.

[<img class="aligncenter size-large wp-image-260" src="https://codeplanet.io/wp-content/uploads/2014/01/blog-author-1024x738.png" alt="Laravel Blog Example" width="640" height="461" />][3]

Let&#8217;s take a look at the relevant part of the schema:

users
:   &#8211; id
:   &#8211; name

posts
:   &#8211; id
:   &#8211; title
:   &#8211; author_id (aliased user.id)

There are 2 things you should notice here; (1) we have a users table to store all kinds of users on our website (i.e. authors, commenters, admins), and (2) we have added a new column &#8211; author_id &#8211; to the posts table, which is the foreign key to the users table.

Now, I could have simply named it user\_id, but I felt that was too vague. What kind of post user is this? Is this the author of the post, or a commenter, etc? By naming the column author\_id, it makes the relationship much clearer and, fortunately, Eloquent makes this very easy to manage.

Next, let&#8217;s create a User model and define a one-to-many relationship to the Post model:

<pre class="lang:php mark:15-18 whitespace-before:1 whitespace-after:1 decode:true" title="app/models/User.php">class User extends Eloquent {

    /**
    * The database table used by the model.
    *
    * @var string
    */
    protected $table = 'users';

    /**
     * Defines a one-to-many relationship.
     *
     * @see http://laravel.com/docs/eloquent#one-to-many
     */
    public function posts()
    {
        return $this-&gt;hasMany('Post', 'author_id');
    }

}
</pre>

To define a one-to-many relationship, we simply return a hasMany relationship to the Post model and &#8211; since we are aliasing the foreign key &#8211; we pass the name of the foreign key column we want to use as the second parameter. If you simply wanted to use user_id as the column name, you would not need to pass a second argument.

Now we can access all posts by an author like so:

`$author->posts`

Since this is a one-to-**many** relationship, instead of getting back a single Post instance, we get a collection of multiple Post instances. Then, to access/display each instance, we could simply loop through them:

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true"></pre>

### Posts by {{ $author->name }}

@foreach ($author->posts as $post)</p> 

  * {{ $post->title }}

@endforeach

Pretty great, right?

So, now we can get posts for a given author, but when we display a single post page, we also want to be able to display author attribution. So, how do we get the relationship to go the other way, to get the author for a given post?

[<img class="aligncenter size-large wp-image-263" src="https://codeplanet.io/wp-content/uploads/2014/01/blog-single-post-1024x738.png" alt="blog-single-post" width="640" height="461" />][4]

The answer is simple: For every model relationship you define, there is a way to define the inverse relation. For any one-to-* relationship, you can use the belongsTo method to create an inverse mapping.

So, let&#8217;s add an &#8220;author()&#8221; method to the Post model that returns a belongsTo relationship.

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true" title="app/models/Post.php">public function author()
{
    return $this-&gt;belongsTo('User', 'author_id');
}
</pre>

Now, we can display the author&#8217;s name on a post page like so:

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true"></pre>

# {{{ $post->title }}}
  
<small>By {{{ $post->author->name }}}</small>

## Many-to-Many

The last relationship type we will be covering is many-to-many. In the blog we have content tags for tagging posts based on what topics are discussed (i.e. HTML, PHP, MySQL).

A post can have _many_ tags, and a tag may be attributed to _many_ posts, thus we have a many-to-many relationship between posts and tags.

[<img class="aligncenter size-large wp-image-264" src="https://codeplanet.io/wp-content/uploads/2014/01/blog-tag-1024x738.png" alt="Laravel Blog Example" width="640" height="461" />][5]

Let&#8217;s take a look at the schema for tags:

tags
:   &#8211; id
:   &#8211; name

post_tag (pivot table)
:   &#8211; post_id
:   &#8211; tag_id
:   &#8211; author_id (aliased user.id)

Just as you would expect, we add a table called tags w/ an auto-incrementing &#8220;id&#8221; column. But we are establishing a many-to-many relationship, so we cannot simply add a foreign key to either table, since that would limit us to a single owner.

This is why we also need to add a pivot table that maps post\_ids to tag\_ids. Fortunately, Eloquent expects this in a many-to-many relationship and knows to look for a table named in this format (&#8220;model_model&#8221;) in order to map properly to the other model.

To define the relationship, just like the previous examples, we simply add a mapping method to each model:

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true" title="app/models/Post.php">public function tags()
{
    return $this-&gt;belongsToMany('Tag');
}
</pre>

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true">public function posts()
{
    return $this-&gt;belongsToMany('Post');
}
</pre>

That&#8217;s all! Here we simply use the belongsToMany relationship method on both sides of the relationship to be able to map between the models:

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true">// loop through all tags for a given post
@foreach ($post-&gt;tags as $tag)
  {{ $tag-&gt;name }}
@endforeach

// loop through all posts tagged with a given tag
@foreach ($tag-&gt;posts as $post)
  {{ $post-&gt;title }}
@endforeach
</pre>

It should be noted that &#8211; while this pivot table naming convention is the recommended and default convention for an Eloquent many-to-many pivot table &#8211; you are welcome to name the pivotal table whatever you like (just like we did with author_id) by passing the name as the second argument of the belongsToMany method.

## Working with Laravel Model Relationships

Now that we have defined all of these relationships between our models, what else can we do with them?

We&#8217;ve seen how we can access and read the data through these model relationships, but what happens if we want to write data?

Let&#8217;s say we are creating a new blog post, what will that entail?

[<img class="aligncenter size-large wp-image-261" src="https://codeplanet.io/wp-content/uploads/2014/01/blog-create-post-1024x738.png" alt="Laravel Blog Example" width="640" height="461" />][6]

First, We&#8217;ll need to create a new Post & a new Text that will be attached to that Post.

This can be accomplished very easily by using the query builder save() method:

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true" title="app/controllers/PostController::store()">// create new Post instance w/ title
$post = Post::create(array('title' =&gt; Input::get('title'));

// create Text instance w/ text body
$text = Text::create(array('text' =&gt; Input::get('text'));

// save new Text and associate w/ new post
$post-&gt;text()-&gt;save($text);
</pre>

Second, we&#8217;ll need to associate an existing User to the Post as the author & associate some existing tag(s) to the post:

<pre class="lang:php whitespace-before:1 whitespace-after:1 decode:true" title="app/controllers/PostController::store()">// loop through tag ids submitted from create post form
foreach (Input::get('tags') as $tagId) {
  // look up the existing Tag by ID
  $tag = Tag::find($tagId);

  // save the Tag on the Post
  $post-&gt;tags()-&gt;save($tag);
}

// associate the post with the current user as the author
$post-&gt;author()-&gt;associate(Auth::user())-&gt;save();
</pre>

Pretty cool, right?

I don&#8217;t know about you, but when I think of all of the query logic I **didn&#8217;t** have to write to make all of this happen, I get pretty excited.

## The End&#8230;?

This article introduces the fundamentals of Eloquent ORM model relationships in Laravel, but there are many more aspects that you should look into, such as eager loading.

As I mentioned at the top, more relationships were added in Laravel 4.1 (i.e. Polymorphic Relations & Has-Many-Through), so expect a follow-up to this article that will cover those.

 [1]: http://laravel.com/docs/eloquent "Eloquent ORM documentation"
 [2]: https://codeplanet.io/wp-content/uploads/2014/01/blog-homepage.png
 [3]: https://codeplanet.io/wp-content/uploads/2014/01/blog-author.png
 [4]: https://codeplanet.io/wp-content/uploads/2014/01/blog-single-post.png
 [5]: https://codeplanet.io/wp-content/uploads/2014/01/blog-tag.png
 [6]: https://codeplanet.io/wp-content/uploads/2014/01/blog-create-post.png