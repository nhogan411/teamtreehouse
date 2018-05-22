# PHP for Wordpress


****************************************************************************************************
# Wordpress Theme Development


****************************************************************************************************
# The Wordpress Template Hierarchy


****************************************************************************************************
# Wordpress Hooks - Actions and Filters


****************************************************************************************************
# Customizing the Wordpress Admin Area


****************************************************************************************************
# How to Build a Wordpress Plugin


****************************************************************************************************
# WooCommerce Theme Development


****************************************************************************************************
# SEO for Wordpress

## Course Introduction
SEO - Search Engine Optimization. Process of making your content accessible to search engines.

Search Engines are trying to direct users to content they'd be interested in so SEO is important part of getting your site seen by visitors.


## Content Is King
Most important aspect of SEO is having strong content.

Strong content meets these requirements:
1. Content is unique
2. Well written
3. Strong photos and videos
4. Good metadata and markup
5. Proper use of keywords and terms.


## General Settings for SEO in Wordpress
Adding some keywords into the Site Title and Tagline can help your SEO.

Be wary of logo only in header.


## Search Engine Visibility in Wordpress
When building a develpoment site, probably best to have the Search Engine Visibility box (under Settings > Reading) checked to ensure your half-built site isn't getting indexed by the search engines. 

However, once your site is completed, you want to make sure that box is unchecked so the SEs can find your content.

Robots.txt file acheives the same purpose but Wordpress doesn't create a robots file for you automatically. 


## Permalinks in Wordpress
Essential for SEO to make sure the page/post names are in the parmalinks for your site.

Day and name or Month and name or Post name are all fine. A custom structure that includes the Post name can also work.

If possible, you'll want to try to include a relevant keyword into the URL of every page on your site. 


## Post and Page Titles for Wordpress and SEO
[Moz.com](https://moz.com/) are THE experts on SEO

Recommended that you keep your title tags under 55 characters.


## SEO Headers in Wordpress
Keep your headers in order (H2 after H1) and don't skip header groups (H1, no H2, H3).

Continue using keywords in your headers.


## How to Use Links in Wordpress for SEO
Links are a critical part of SEO. Two types of links:
1. internal links - links to your own content on your sire
2. external links - links to content off site

When you have content related to something in a post or page LINK TO IT.


## Using SEO Friendly Images in Wordpress
Title on an image is typically just used internally.

The Alt Text is necessary to tell the search engines what the image is about.

The image description can be longer than the alt text. Good for big images containing lots of info - like an inforgraphic.

Caption - use the caption to link attribution to the source of the image if it's not your image.


## Using Videos in Wordpress in Improve Your Search Engine Rankings
Generally not a bad idea to host your video content on youtube or another similar service. Don't need to worry about bandwidth or space or accomodating different devices.

Wistia is a solid alternative to youtube. They allow for creating a video sitemap that links back to your site, not youtube.


## Categories and Tags in Wordpress
Important for SEO to include a description with your categories. 

Use your keywords.


## Making Menus in Wordpress SEO Friendly
Use your menus to alter the anchor text and title attribute for links in your navigation or menus to both look good AND rank well.


## Using Widgets to Help with SEO
Widgets aren't super helpful for SEO, but you can utilize the widgets/sidebar area to push internal/external links and/or to promote social networks which can be helpful to your site.


## Title Tags in Wordpress
```
add_theme_support( 'title-tag' );
```

Allows you to setup title tags without having to hard code it into the theme itself.

Allows plugin developers to more easily effect the title tag.

Theme developers can alter the title tags in the functions.php file using a filter hook.


## Meta Description Tags in Wordpress
Meta descriptions are typically displayed on the search engine results page underneath the link to the site. The search engines refer to this as The Snippet and the snippet is typically populated by the site or pages meta description.


## Headers Best Practices for SEO in Wordpress
A good practice is to setup the blog title as an H1 on the homepage of your site, but to have the page or blog post title serve as the H1 on internal pages.

```
<?php if ( is_front_page() && is_home() ) : ?>
  <h1 class="site-title"><?php bloginfo( 'name' ); ?></h1>
<?php else : ?>
  <p class="site-title"><?php bloginfo( 'name' ); ?></p>
<?php endif; ?>
```

```
<?php if ( is_single() ) :
  the_title( 'h1 class="entry-title">', '</h1>' );
else :
  the_title( sprintf( '<h2 class="entry-title"><a href="%s" rel="bookmark">', esc_url( get_permalink() ) ), '</a></h2>' );
endif; ?>
```


## Introduction to Schema
Schema is a way of marking up data that is agreed upon by the major search engines.

Add the agreed upon attributes to your meta data to make the content more SEO friendly.


## Examples of [Schema.org](http://Schema.org) in Wordpress Themes and Plugins
Some themes already have schema already applied. Some plugins do as well.


## Adding Schema Manually to Themes
[schema-creator.org](http://schema-creator.org/) is a good way to get schema created for you.

This gets you a template for things you need to add to your theme templates to generate good schema. Once you have the base code you can use wordpress and php to dynamically fill these fields.


## Wordpress SEO Plugins
Top SEO plugins for wordpress
1. Wordpress SEO by Yoast
2. All in One SEO Pack
3. Broken Link Checker - looks for broken links on your website
4. Safe Redirect Manager - best way to make sure the SEs know how/where to find your content after a redesign
5. WP Super Cache - Speeds up your site by moving them dynamic pages to static files. Speed matters in SEO.
6. Jetpack by [Wordpress.com](http://wordpress.com/) - Has great social features


## The Wordpress SEO Plugin from Yoast
Most SEO plugins provide same or similar features. Yoast has a huge number of users, strong community and support, and a lot of features.


## Revisiting Content with the SEO Plugin from Yoast
Allows for SEO Title and Meta Description at the page and post level.


## Broken Link Checker
Great tool to determine if you have any broken links.

Broken links are BAD for your SEO. Keep your content up-to-date to avoid problems.


## Safe Redirect Manager
Great for move from static site to wordpress or a side redesign that shuffles the hierarchy and structure of your pages.


## Using Caching to Speeding Up Your Wordpress Site
PageSpeed is a factor for determining rankings in the Search Results.