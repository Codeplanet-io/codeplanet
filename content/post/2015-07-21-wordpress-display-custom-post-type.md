---
title: WordPress Display Custom Post Type
author: Jon Kuperman
type: post
date: 2015-07-21T17:00:40+00:00
excerpt: "Alright! So you've figured out how to add a custom post type or just saved yourself the trouble and installed Custom Post Type UI and now you're looking for a way to display them."
url: /wordpress-display-custom-post-type/
categories:
  - WordPress

---
Alright! So you&#8217;ve figured out [how to add a custom post type][1] or just saved yourself the trouble and installed [Custom Post Type UI][2] and now you&#8217;re looking for a way to display them.

Check out the code below:

<pre class="lang:php decode:true">&lt;?php
/**
 * Template Name: Videos
 *
 * Selectable from a dropdown menu on the edit page screen.
 */

get_header(); ?&gt;

&lt;div class="primary"&gt;
    &lt;main id="main" class="site-main" role="main"&gt;

&lt;?php
    $args = array(
        'post_type' =&gt; array('video')
    );

    // the query
    $the_query = new WP_Query( $args );
?&gt;

&lt;?php if ( $the_query-&gt;have_posts() ) : ?&gt;

    &lt;!-- pagination here --&gt;

    &lt;!-- the loop --&gt;
    &lt;?php while ( $the_query-&gt;have_posts() ) : $the_query-&gt;the_post(); ?&gt;
        &lt;h1 class="entry-title"&gt;
            &lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;
                &lt;?php the_title(); ?&gt;
            &lt;/a&gt;
        &lt;/h1&gt;
    &lt;?php endwhile; ?&gt;
    &lt;!-- end of the loop --&gt;

    &lt;!-- pagination here --&gt;

    &lt;?php wp_reset_postdata(); ?&gt;

    &lt;?php else : ?&gt;
        &lt;p&gt;&lt;?php _e( 'Sorry, no posts matched your criteria.' ); ?&gt;&lt;/p&gt;
    &lt;?php endif; ?&gt;

    &lt;/main&gt;&lt;!-- #main --&gt;
&lt;/div&gt;&lt;!-- #content --&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</pre>

 [1]: https://codex.wordpress.org/Post_Types#Custom_Post_Types
 [2]: https://wordpress.org/plugins/custom-post-type-ui/