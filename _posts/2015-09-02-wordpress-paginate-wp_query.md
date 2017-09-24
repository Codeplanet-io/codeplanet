---
id: 585
title: WordPress paginate WP_Query
date: 2015-09-02T10:00:55+00:00
author: Jon Kuperman
layout: post
guid: http://codeplanet.io/?p=585
permalink: /wordpress-paginate-wp_query/
categories:
  - Uncategorized
---
For those of you that are making [custom post types](https://codex.wordpress.org/Post_Types) on your WordPress blog and using [WP_Query](https://codex.wordpress.org/Class_Reference/WP_Query) to list posts in those types &#8212; you may have noticed that pagination doesn&#8217;t work.

Here is an example template that will pull all posts with a custom post type &#8220;videos&#8217; and display them, five at a time and paginated.

<pre class="lang:php decode:true ">&lt;?php
/**
 * Template Name: Videos
 *
 * Selectable from a dropdown menu on the edit page screen.
 */

get_header(); ?&gt;

&lt;div id="primary" class="content_area"&gt;
  &lt;main id="main" class="site-main" role="main"&gt;

&lt;?php
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$args = array(
    'post_type' =&gt; array('video'),
    'posts_per_page' =&gt; "5",
    'paged' =&gt; $paged
);

// the query
$the_query = new WP_Query( $args );

// Pagination fix
    $temp_query = $wp_query;
    $wp_query   = NULL;
    $wp_query   = $the_query;
?&gt;

&lt;?php if ( $the_query-&gt;have_posts() ) : ?&gt;

  &lt;!-- the loop --&gt;
    &lt;?php while ( $the_query-&gt;have_posts() ) : $the_query-&gt;the_post(); ?&gt;
    &lt;article class="post type-post status-publish format-standard hentry"&gt;
      &lt;header class="entry-header"&gt;
        &lt;h2 class="entry-title"&gt;
          &lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;
            &lt;?php the_title(); ?&gt;
          &lt;/a&gt;
        &lt;/h2&gt;
        &lt;div class="entry-content"&gt;
          &lt;?php the_content(); ?&gt;
        &lt;/div&gt;
      &lt;/header&gt;
    &lt;/article&gt;
    &lt;?php endwhile; ?&gt;
    &lt;!-- end of the loop --&gt;
    &lt;?php
	the_posts_pagination( array(
		'prev_text'          =&gt; __( 'Previous page', 'twentyfifteen' ),
		'next_text'          =&gt; __( 'Next page', 'twentyfifteen' ),
		'before_page_number' =&gt; '&lt;span class="meta-nav screen-reader-text"&gt;' . __( 'Page', 'twentyfifteen' ) . ' &lt;/span&gt;',
	) );
    ?&gt;

    &lt;?php wp_reset_postdata(); ?&gt;

    &lt;?php else : get_template_part( 'content', 'none' ); endif; ?&gt;

  &lt;/main&gt;&lt;!-- #main --&gt;
&lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_footer(); ?&gt;</pre>

&nbsp;