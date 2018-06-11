# Local Wordpress Development

## Installing a Local Web Server on a Mac
* [mamp.info](http://mamp.info/) - click to download MAMP
* Install MAMP
* Applications > MAMP Folder > MAMP
* To get MAMP up and running click Start Servers
  * This starts both Apache and MySQL
  * Should also open MAMP start page in browser
* If we remove MAMP from URL we can get to the root directory of the server
  * This file is actually in the MAMP Folder > htdocs folder


## Customizing Your Local Server Setup on a Mac
1. Remove the :8888 from the URL
   
   To do this, open MAMP > Preferences > Ports > "Set to default Apache and MySQL ports" > OK

    * This sets the local host to default :80, which means you don't have to have the port in the URL at all.

       `localhost/SITENAME` will work

2. Change folder location of where we store files
   
   Common to create a Sites folder in their home directory

   Open MAMP > Preferences > Apache > Select new location


## Installing a Local Web Server on a PC
* XAMPP > XAMPP for Windows > Download the latest version
  * Use Installer version
  * Run Installer
  * Uncheck BitNami
  * After finish XAMPP will open automatically.
    * Start Apache and MySQL services
* `localhost/xampp/splash.php` default 
  * Files are stored in C drive > XAMPP folder > htdocs folder 


## Installing Wordpress Locally
* Go to [wordpress.org](http://wordpress.org/) and download wordpress
* Create a new folder in the Sites folder called [localwp.com](http://localwp.com/)
  * Don't install directly into Sites folder because it becomes difficult to deal with multiple installs
* Copy all the files from the downloaded wordpress install into the localwp.com folder.
* Open MAMP control panel > Open Start Page > PHPMyAdmin
  * Databases > Create new database called localwp
  * Users > Create new user: wpuser
    * Set host: localhost
    * Check All for global access to database
  * `localhost/localwp.com` to proceed to installation script
    * Create a Config file
    * Enter DB info
      * Submit
    * Run Install
      * Enter Site and WP User details
      * Uncheck Privacy
      * Install Wordpress
    * Log In

Important to note that MAMP Servers need to be on to run Wordpress locally


## Migrating Wordpress from Local to Live Server
1. FTP into site and drag ALL items from `localwp.com` folder into the `public_html` folder on the server
2. Log into cpanel and create a new MySQL database.
    1. Use name localwp for DB name
    2. Use wpuser as the username
        1. Use same password as the local install
        2. Make sure user has all privleges
    3. Note the final username and database name because we'll need this for the config file
3. Go back to MAMP and open start page.
    1. Go to PHPMyAdmin > localwp database > Export tab
        1. Custom Export
        2. Everything selected
        3. Save as output file to text
        4. Database is successfully backed up
4. Go back to cpanel and open PHPMyAdmin
    1. Click into new database that we created > Import new file from our local development that we just exported
    2. Database info is now on live server
5. Go back to FTP and find wp_config.php > Open and Edit
    1. Still has all DB info from local site
    2. Update with info from live site
    3. DB_Collate tells WP to find site somewhere else

        ```
        define('WP_HOME', 'http://liveurlthatyoubought.com');
        define('WP_SITEURL', 'http://liveurlthatyoubought.com');
        ```

        Make sure you have the 'http://'

6. All setup but should probably use a plugin to Find & Replace all links that might still be pointing at localhost. This can effect images too.
    1. Install and active Search and Replace plugin
    2. Go to Search and Replace plugin
        1. Enter Search URL from local site
          
            [http://localhost/localwp.com](http://localhost/localwp.com)

        2. Enter Replace URL for new site
          
            [http://liveurlthatyoubought.com](http://liveurlthatyoubought.com/)

7. Good idea to run process in reverse if you're going to start developing locally again.


****************************************************************************************************
# Build a Website with Wordpress

## [WordPress.org](http://wordpress.org/) Theme Repository
See featured and most popular themes

Easier to log into admin area > Appearance > Themes  > Add New

Themes have to be installed AND activated

If not using a theme or plugin it's good practice to delete it from the site.


## Best Wordpress Themes
Google is your friend.

"Free Responsive Wordpress Themes"

Easy to activate and install downloaded theme to the site
  * Log into /wp-admin
  * Appearance > Themes > Add New > Upload > Choose downloaded zip file > Install Now > Activate


## Premium Themes - Paid (Not Free Themes)
[themeforest.net](http://themeforest.net/) - hub from finding/searching/paying for premium themes

[woothemes.com](http://woothemes.com/) - hub from finding/searching/paying for premium 


## Theme Frameworks
Theme framework - Advanced WP theme that comes with extensive ability to customize theme within admin area. Also, tend to come with a lot of extra hooks and functions that theme developers can use to quickly build custom layouts and features.

Largely exist as a starting point for building custom themes.

Flexible enough to build any type of site on top of them.

The more you work with a specific theme framework the faster you develop.
* [ ] Do we use a them framework? Which?


## The Wordpress Theme Customizer
Simplest place to update the theme is at Appearance > Customize

When viewing Customize setting page you'll see options on the left and preview of changes on the right.

The specific options available to us is dependant on the theme itself.

* Switch themes = different options available for customization


## Theme Option Pages
Typically found at Appearance > Theme Options

Again, different options are avaialble based on what the theme allows.

Some themes have recommended plugins


## How to Make Child Themes
Theme developers will occasionally update their themes to fix bugs and stay on top of wordpress updates.

When we edit a theme we lose those edits in an update. To avoid this problem we create child themes.

Child Themes live in a separate folder of the theme we want to customize.

Child themes will use parent them files unless a version exist in the child theme, in which case the child theme is used. 
* Copy and paste files from the parent theme to the child theme and then edit the child theme version to customize.

### Steps
1. In FTP go to public_html folder > wp-content > themes
2. Same name as original theme with "child" appended
    * Ex: twentythirteen –> twentythirteenchild
3. Copy .css file from original file and paste it into child theme folder
    1. Need a variable for Template that notes the parent theme
    2. Also need an `@import` to get the parent theme style sheet.
        
        ```
        @import "../twentythirteen/style.css";
        ```

        * Without this step we would still have child theme but would lack styles of parent theme we want it to inherit
4. Also need the screenshot.png file which shows up in the admin area when selecting themes.
5. Upload child theme to server
6. Go back to admin area - Appearance > Themes and find/activate Child Theme


## Customizing Wordpress Theme Files

### CSS Customization
We want to change the navigation menu to be the same background color as the footer.
1. Find the style that sets the background color of the footer.
2. Open the child theme .css file
3. After the `@import` from the parent theme, paste in the CSS setting the background color of the footer.
4. The background color is all we're keeping.
5. Find out the class of id that is setting the background color of the navigation bar and paste that into child theme .css file, replacing the rule name we pasted in during step 3.
6. Save changes
7. Upload to server
8. Refresh

New styles have been applied but the text color isn't legible so we need to update that style as well. Follow the same process to determine where the navigation color was being set and create a new rule that sets a readable color.

Now we want to edit the PHP file for a page, specifically we want to remove the option for a visitor to comment on the page.
1. Open theme folder locally and find the relevant file (page.php)
2. Copy page.php from parent and paste into child theme.
    * This ensures that the child theme file is seen by wordpress first, instead of the page.php file in the parent theme
3. Open up child page.php and let's find the code that allows for comments:

    ```
    <?php comments_template(); ?>
    ```

    * Instead of deleting the line of code, we're just going to comment out the comments_template() function in case we need it later.

    ```
    <?php //comments_template(); ?>
    ```

4. Save changes and upload to server


## Custom Post Types and Field Plugins
Two types of deault content:
1. Posts
2. Pages

Custom Posts operate like posts but allow for custom fields.

Normally going to deal with two sets of plugins to establish custom posts:
1. Custom Post Type UI - helps set up custom post types
2. Advanced Custom Fields - helps setup custom fields in custom post types

The above mentioned plugins are two of the most popular plugins for this type of work, but some plugins might serve both functions. For instance Types - Custom Fields and Custom Post Types Management

* [ ] Do we use same plugins across the board? What plugin(s)?


## Setting Up Custom Post Types and Fields

### Installing Custom Post Type UI Plugin
1. Plugins > Add New > Search for Plugin > Install
2. Activate it
3. Note new option in admin


### Creating new custom post type, Art, using Custom Post Type UI
1. Post Type Name & Label: "Art"
  1. Singular Label might be different from Label ("Movies" vs "Movie")
2. Note new option in admin

To get Custom Post Type Fields will need new plugin

### Install Custom Post Type Fields plugin
1. Plugins > Add New > Search for Plugin > Install
2. Activate it
3. Note new item in admin

### Adding New Fields
1. Custom Fields > Add New
2. Label them as "Art"
3. Under rules make sure the Post Type is equal to "art"
4. Add "Image"
    1. Required
    2. Return Value: "Image URL"
5. Add "Description"
    1. Text Area
    2. Required
6. Add "Price"
    1. Text
    2. Required
7. Adjust style
8. Adjust what options are displayed on page
9. Publish


## Custom Post Type Templates
First step to getting "Art" posts customized is to get new files into child theme.

### art.php
Almost an exact copy of page.php except for few changes.

Code is setup like a regular page but at the end is a call to pull all of the items with `post_type == 'art'` and display them according to the `content-art.php` file.

### content-art.php
Here we can see that we're setup to display the title, price, the image, and the description.

However, we're using an new piece of code that comes from the advanced custom field plugin:

```
the_field()
```

`the_field()` is a function used to display any custom fields that we're working with.

### single-art.php
Determines what a single entry of "art" posts look like.

Inside is some basic code that ALSO uses the content-art.php code, but only displays a single item of art instead of all the art items.

### Setting up a page on the site to display art
1. Move files to child theme.
2. Go to admin and create a new page.
3. Name the page and add a description
4. Change the template to "Art Page"
5. Publish


## How to Create Widgetized Areas in Wordpress
To create a new widgets area we need the files from the project to get edited and moved to the child theme. 

We'll need the following files:
1. `functions.php`
2. `header.php`
3. `style.css`

### functions.php
Allows for more custom code than the normal page template file.

Child functions.php still reads and has access to all the code in the parent functions.php file

### header.php
Exact same file from parent theme

Only made one edit:

```
<?php if (! dynamic_sidebar( 'uptop' ) ); ?>
```

  * If there's a custom widget, or dynamic sidebar called "uptop" then display it
  * Can see that the "uptop" name is set in the functions.php file

### style.css
See that we've added some styles for the #uptop

### back in admin
Appearance > Widgets > refresh
See that there's a new widget area called "Header" (also set in the `functions.php` file

### To setup new widgets
1. Copy the create_widget function in functions.php and edit to reflect new location:

    ```
    create_widget("Header", "uptop", "Displays in the header of the site, above the title");
    create_widget("Pre-Footer", "prefooter", "Displays above the footer");
    ```

2. Copy the dynamic_sidebar function to whatever page you want your new widget to apply to, and adjust the code to reflect your new widget:

    ```
    <?php if ( ! dynamic_sidebar( 'prefooter' ) ); ?>
    ```


## How to Add Custom Menus to a Wordpress Theme
To create a new custom menu we need to copy the code from the original folder

### functions.php
Now we need some code for creating custom menus.

```
<?php
/// Create a custom menu
function register_my_menus() {
  register_nav_menus[
    array(
      'footer-menu' => __( 'Footer Menu' )

      /// Could add multiple menu items by filling out the array with more values
      'sidebar-menu' => __( 'Sidebar Menu' )
    )
  ];
}
add_action( 'init', 'register_my_menus' );
```

### footer.php
Added one line of code to add:

```
<?php wp_nav_menu( array{'menu' => 'Footer Menu' )); ?>
```

This checks for the "Footer Menu" and displays the menu if it exists.


## Finding, Installing and Updating Wordpress Plugins
Plugins extend the functionality of wordpress.

Most of the time, when you're looking for a new plugin you'll do so from the admin area.
* Plugins > Add New > Search

Premium plugins are not listed in the [wordpress.com](http://wordpress.com/) repository
* Plugins > Upload > Select downloaded zip > Activate


## Common Wordpress Plugins
* BackUpWordPress - Simple and sets automated backups of files and database or done manually
VaultPress another good service
* Akismet - Helps prevent spam on your site. Sign up for an API key and you're good to go.
* Jetpack - popular on wordpress.com
* Wordpress SEO by Yoast - lots of SEO features
* Gravity Forms - most popular plugin fro creating forms on wordpress sites. Premium but worth it.
* WooSlider - premium plugin for sliders
* Lightbox Plus ColorBox - automatically add lightbox where it makes sense.
* Custom Post Types UI
* Advanced Custom Fields
* Types - Custom Fields
* Black Studio TinyMCE Widget - Add TinyMCE to the Text option in Widgets area
* Dispaly Widgets - Let's you set which widgets display on which pages.
* Google Analytics for Wordpress - helps setup GA
* Google Analytics Dashboard for WP - lets you see analytics info in Wordpress dashboard
* Admin Menu Editor - Lets you control what users see when they log in to the backend of their site.

****************************************************************************************************
# PHP for Wordpress

## What is PHP
Wordpress + PHP
* Save content to a database
* Read content from a database
* Write loops and conditional statements
* Pull in Wordpress specific information
* Pull in images, PHP, CSS, and javscripts files


## PHP Files
Wordpress has a few different types of PHP files:
1. Core files - only contain PHP code and not files you should be editing since they might break your wordpress install
2. Theme files - contain a combination of PHP and HTML. Most common type of file you'll find yourself editing.
3. Plugin files - primarily PHP code, although might have HTML, javscript or CSS mixed in. Typically don't edit plugin files unless you're building it.

Typically don't edit files outside of the `wp-content` folder.

Keep in mind not to edit themes directly. You will lose edits when a theme updates if you edit directly in the theme. Use child themes.


## A PHP Block
Writing PHP outside of the PHP block will display as plain text. 

Writing HTML inside of a PHP block will cause errors.


## The Importance of the Semicolon
Semicolon in PHP marks the end of a statement or a line of code.


## Adding HTML Markup with PHP
In wordpress markup is typically left outside the PHP tags, especially in templates.


## Template Tags
Template tags - Wordpress comes with a lot of pre-built functions that easily let you get access to commonly used pieces of information that you may want to use on your site.

Some template tags only generate a single bit of data.

Others can output a number of pieces of data and require that you specify what you're looking for. We specify what we're looking for using parameters.

[https://codex.wordpress.org/Template_Tags](https://codex.wordpress.org/Template_Tags) - a list of ALL the major template tags used in wordpress. Find examples to see what's available, how to use it and what the output is.


## Custom Loops
[WP_Query](https://codex.wordpress.org/Class_Reference/WP_Query)


## Custom Functions
When you create your own themes or plugins you'll often have to create your own functions.


## Wordpress Hooks - Actions and Filters 
Two types of hooks exist in wordpress
1. Actions - insert your own code at different points while wordpress is running.
    * ex. Run my code when a post is saved.
    * ex. Run my code when a menu is loaded
2. Filters - Modify content in wordpress
    * ex. Add a custom footer to the end of the main content of a post
    * ex. Limit the excerpt of a post to a certain number of characters

```
add_action( 'after_setup_theme', 'twentyfifteen_setup' );
```

After wordpress does everything it needs to do to setup a theme, let us hook our special setup function to your code when you're setting up this theme.

```
add_action( ;widgets_init', 'twentyfifteen_widgets_init' );
```

The function we created is getting hooked into the widgest_init action hook.


## PHP Coding Standards for Wordpress
* [PHP Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/php/)
* [HTML Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/html/)
* [CSS Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/css/)
* [Javascript Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/javascript/)


## Learning More PHP


****************************************************************************************************
# Wordpress Theme Development

## Where Wordpress Themes Live
`/wp-content/themes/[YOUR THEME HERE]`


## The Wordpress Template Hierarchy
* [http://codex.wordpress.org/Template_Hierarchy](http://codex.wordpress.org/Template_Hierarchy) - Explains all the different possible files you can use to build a wordpress theme
* [http://codex.wordpress.org/imates/1/18/Template_Hierarchy.png](http://codex.wordpress.org/imates/1/18/Template_Hierarchy.png) - Graphic shows flow of what kind of page you're trying to create and what types of templates or naming conventions you would use for that page or template
* [wphierarchy.com](wphierarchy.com) - interactive/dynamic website that linsk you to spots on the codex to get more about particular terms or templates. Really just an interactive version of the Template_Hierarchy.png image.


## Setting Up a Wordpress Theme Folder
Important to namespace the theme folder so no conflicts with other themes with same name.

* Ex. portfolio style theme so name it "portfolio", but that's a potentially a pretty common name. Better to name it "treehouse-portfolio", less likely that someone is using that name.

Drag the folder into sublime text editor and create three files inside:
1. style.css - important and required to activation. All meta information for theme lives in style.css:
  1. Author
  2. Version
  3. Description
  4. Tags
  5. Image
  6. Supported Features
2. index.php - important and required to activation
3. functions.php - just important, not required to activate

### style.css

```
/*
Theme Name: Treehouse POrtfolio Theme
Author: Treehouse
Author URI: http://teamtreehouse.com/
Description: A post modern, simple, responsive portfolio theme designed in Wordpress Theme...
Version: 1.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Tags: black, white, light, one-column, two-columns, left-siderbar, flexible-width, fluid...

At Treehouse we believe that you should reach for your dreams.
You are welcome to use this theme privately or commercially you want to help accomplish...
*/
```

Still needs a screenshot.png file to show image in admin area.
* 880x660px image as screenshot of theme.


## Porting Over Static Template CSS
In the download sections, are the original files used to create a static HTML site. CSS rules already exist in a .css file, so we're just copying those styles over to our styles.css

The `@import` rule is important, but the best way to link to external or additional CSS files is via the functions.php file.


## Adding CSS to a Theme Via functions.php File
How to link to the `@import` for external fonts as well as the additional CSS files that came with our static site.

We need to move the CSS files from static site into a /css folder inside the theme
* Should be wp-content/treehouse-portfolio/css/foundations.css and wp-content/treehouse-portfolio/css/normalize.css

Open up the functions.php file and start a php block:

```
<?php 

?>
```

Now we're going to create a new function. When we do this we put a unique namespace at the beginning of the function name to avoid conflicts with other functions and plugins

```
function wpt_theme_styles() {

}
```

The `wpt_` stands for "WordPress Treehouse" but could be anything.
 - [ ] Does GH have a naming convention they like to throw up at the beginning of functions to serve as namespace?

Inside of our function we're going to call the `wp_enqueue_style()` function, which let's us link to a style sheet for a particular theme.
* First parameter is a unique name or handle that identifies the particular stylesheet that we're linking to. Probably similar to the name of the file, but not required.

   Ex. 'foundation_css' instead of 'foundation.css'

* Second parameter is a link to the actual file. Best way to do this is to use the `get_template_directory_uri() `function and concatenate it with the path to the file.

```
wp_enqueue_style( 'foundation_css', get_template_directory_uri() . '/css/foundation.css' );
wp_enqueue_style( 'normalize_css', get_template_directory_uri() . '/css/normalize.css' );
```

We're also going to use wp_enqueue_style() to bring in the `@import` rule from the original CSS file. 
* Instead of concatenating the `get_template_directory_uri()` function and the path to the file, just use the string directly

```
wp_enqueue_style( 'googlefont_css', 'http://fonts.googleapis.com/css?family=Asap:400,700,400italic,700italic' );
```

Finally, we need to make sure that our main CSS file is being loaded up. So once again we go back to the `wp_enqueue_style()` function

```
wp_enqueue_style( 'main_css', 'get_template_directory_uri() . 'style.css' );
```

Now that our function is created, we need to use an action hook to make sure the function is called. So after we close the function we're going to add an `add_action()` function with `wp_enqueue_scripts` as one parameter and the name of OUR function as the second.

```
add_action( 'wp_enqueue_scripts', 'wpt_theme_styles' );
```

Final look at our functions.php file should be something like:

```
<?php
  function wpt_theme_styles() {
    wp_enqueue_style( 'foundation_css', get_template_directory_uri() . '/css/foundation.css' );
    wp_enqueue_style( 'normalize_css', get_template_directory_uri() . '/css/normalize.css' );
    wp_enqueue_style( 'googlefont_css', 'http://fonts.googleapis.com/css?family=Asap:400,700,400italic,700italic' );
    wp_enqueue_style( 'main_css', 'get_template_directory_uri() . 'style.css' );
  }
  add_action( 'wp_enqueue_scripts', 'wpt_theme_styles' );
?>
```


## How to Link to JS from functions.php File
There are a handful of javascript files and scripts that are included in the static version of the site we created and we're going to use the same method for add those to our wordpress theme that we used for the CSS files.

Before we can do anything to the functions.php we should copy over all the javascript files from our static site into our theme.
* The path for this would be wp-content/treehouse-portfolio/js/app.js, wp-content/treehouse-portfolio/js/foundation.min.js, and wp-content/treehouse-portfolio/js/modernizr.js

Back in our functions.php we're going to create a new function that queues up our javscript files. Again we're using our "wpt_" namespace.

```
function wpt_theme_js() {

}
```

Similar to the `wp_enqueue_style()` function is a `wp_enqueue_script()` function.
```
wp_enqueue_script( 'modernizr_js', get_template_directory_uri() . '/js/modernizr.js', '', '', false );
```

There are additional parameters to pass in the `wp_enqueue_script`. 
1. An array of dependants. Not needed in this example.
2. Sets a version. Not needed in this example
3. True/False parameter asking if we want to include in the footer of the page

Copy the code again and update for the js file

```
wp_enqueue_script( 'foundation_js', get_template_directory_uri() . '/js/foundation.min.js', array('jquery'), '', true );
```

Foundation.min.js is dependant on jquery, so if we pass an array with jquery filled in it'll make sure jquery is loaded prior to foundation.

Lastly, we're going to load up our main javscript file.

```
wp_enqueue_script( 'main_js', get_template_directory_uri() . '/js/app.js', array('jquery', 'foundation_js'), '', true );
```

This last file is not only dependant on jquery, but ALSO dependant on the foundation javascript so the array of dependants will include BOTH dependencies.

Similar to the CSS we can now call the add_action hook to call the function we just created.

```
add_action( 'wp_enqueue_scripts', 'wpt_theme_js' );
```

So a final look at the functions.php file:

```
<?php 
  function wpt_theme_styles() {
    wp_enqueue_style( 'foundation_css', get_template_directory_uri() . '/css/foundation.css' );
    wp_enqueue_style( 'normalize_css', get_template_directory_uri() . '/css/normalize.css' );
    wp_enqueue_style( 'googlefont_css', 'http://fonts.googleapis.com/css?family=Asap:400,700,400italic,700italic' );
    wp_enqueue_style( 'main_css', 'get_template_directory_uri() . 'style.css' );
  }
  add_action( 'wp_enqueue_scripts', 'wpt_theme_styles' );

  function wpt_theme_js() {
    wp_enqueue_script( 'modernizr_js', get_template_directory_uri() . '/js/modernizr.js', '', '', false );
    wp_enqueue_script( 'foundation_js', get_template_directory_uri() .'js/foundation.min.js', array('jquery'), '', true );
    wp_enqueue_script( 'main_js', get_template_directory_uri() . '/js/app.js', array('jquery', 'foundation_js'), '', true );
  }
  add_action( 'wp_enqueue_scripts', 'wpt_theme_js' );
?>
```

jquery uses the $ sign to denote the start of a jquery function and wordpress allows for multiple javascript frameworks that might also use the $ so we have to adjust our main javascript file to note that anytime it sees the $ it's for jquery.

We do this by wrapping our jquery code inside of a function that is specifically calling jquery.

This:
```
$( ".nav-toggle" ).click(function() {
  $(this).toggleClass("open");
  $("nav").fadeToggle(100);

  return false;
});
```

becomes this:

```
jQuery(document).ready(function($) {
  $( ".nav-toggle" ).click(function() {
    $(this).toggleClass("open");
    $("nav").fadeToggle(100);

    return false;
  });
});
```
Any other scripts used in the actual static pages should also be called here:

```
jQuery(document).ready(function($) {
  $(document).foundation();
  $( ".nav-toggle" ).click(function() {
    $(this).toggleClass("open");
    $("nav").fadeToggle(100);

    return false;
  });
});
```


## The header.php and footer.php Files
First we need to create two new files in our theme:
1. header.php
2. footer.php

All wordpress site have to use the above naming convention

in index.php we'll setup some php codeblocks to pull the header and footer files.

```
<?php get_header()' ?>

<h1>Index file</h1>

<?php get_footer(); ?>
```

* `get_header()` function calls the header.php file
* `get_footer()` function calls the footer.php file

   These functions work similar to the php include function, but for these specific files.


## Porting existing headers and footers into Wordpress
Cut from the top of your static page down to the closing `</header>` tag and paste that into the header.php file.

* This include the full `<head>` section the opening `<body>` tag, the start of the `<header>` tag and all the navigation.

Then we'll do the same thing for the footer.php file. 

* Go into your static page and scroll to the bottom and cut everything from the final .footer-clear div down to the closing `</html>` tag and paste it into footer.php.

Everything will show up as code, but the styles won't work yet.

Now we need to clean things up a bit by removing anything in the header.php or footer.php that'll be replaced by any code in another template or by calls in the functions.php file.

### in header.php
1. Replace the contents of the `<title>` tag with `<?php wp_title(); ?>`
2. Delete the references to the stylesheets and javascripts
  1. In their place, we need to put in `<?php wp_head(); ?>` which tells wordpress we're about to hit the closing `</head>` tag and the plugin or theme should dump that stuff in.
3. Replace the href on the "G" logo. Instead of hard coded, it needs to point to `<?php bloginfo('url'); ?>`. `bloginfo()` function contains a lot of info about a wordpress site we just have to tell it what piece of info to pull, hence the 'url' parameter.
4. Instead of leaving the "G" as the site title, we're also going to replace that with the `bloginfo()` function, but this time pass the 'name' parameter:

   ```
   <?php bloginfo('name'); ?>
   ```

5. Replace the same two items (steps 3 & 4) where they live in the navigation.

### in footer.php
1. We're going to remove the social links
2. Instead of the static copyright date we're replace that year with `<?php echo date('Y'); ?>` in order dynamically output the correct date.
3. We can also pull all the links to javascript files and instead put in the `<?php wp_footer(); ?>` function to tell wordpress to output any code right before the closing body tag.


## An Explanation of the Wordpress Loop
The Loop is a powerful block of code that sits at the heart of wordpress templates.

It checks to see what content is available for a page and then loops through and displays it.

The loop is smart enough to know when multiple pieces of content should be displayed (like on a blog listing page), or if a single piece of content should be displayed (like on a static "About" page).

The loop starts with an If statement to see if content is available and then moves into a while statement that continues operating until there's no longer content to display.

INSIDE of the loop is where you find the code that dynamically generates the markup.

[codex.wordpress.org/The_Loop](codex.wordpress.org/The_Loop)

The loop has two different methods for being displayed. 
1. Uses a shorthand method - essentially one line of code or perhaps starting the loop, closing the php block, filling in some HTML markup and coming back to close the loop later.
2. More longhand method - a full PHP block


## Adding the Loop to index.php File
To start, let's pull the .row `<section>` from our static page and put it into our index.php file.

Copy over the loop from the wordpress codex using the shorthand methods. Bring over both the opening and closing blocks of the loop.

Since we want the `<section>` to exist regardless of the output of the loop, we need to make sure the loop starts inside of the `<section>` as well as inside the .small-12 and .leader `<div>`s

Instead of hardcoded `<h1>` and `<p>` tags let's dyanmically pull the title and the content using two function `the_title()` and `the_content()`.

```
<h1><?php the_title(); ?></h1>
<p><?php the_content(); ?></p>
```


## Common Wordpress Functions Used with the Loop
The difference between a "the_" function and a "get_" function is significant. `the_permalink()` will echo out that permalink into a code. `get_permalink()` will go and get the permalink and allows us to save it to a variable for later use.


## The page.php File
page.php controls the static pages in the wordpress site.

Save the index.php file as page.php as a starting point for page.php. This will work as the baseline for all of our pages on the wordpress site. 

That being said, we can create create files that will handle custom templates (like if we wanted a sidebar, etc.).


## Creating Custom Page Templates in Wordpress
Our static site had a blog.html page that was two columns. A primary column on the right and sidebar column on the left.

Open up the blogs.html static page source code as well as a new page (page-sidebar-left.php). Copy everything from page.php so our base code is there.

Now at the top of the page add a block of php that names the template. This tells wordpress we're using a custom template.

```
<?php
/*
  Template Name: Left Sidebar
*/
?>
```

Now we can take what we need from our blogs.html page and move what's needed into page-sidebar-left.php.
* Grab the opening .two-column `<section>` down to the .primary `<div>` and replace the opening `<section>` tag in page-sidebar-left.php. 
* Do the same with the corresponding closing tags. 

It can be difficult to determine where in a static HTML template you want to split your content up, but ultimately the decision comes down to what needs to be repeated (and therefore palced inside the loop), and what doesn't (and therefore outside of the loop).


## The wp_nav_menu Function
The `wp_nav_menu` function takes a number of parameters that mostly control how the menu is displayed, what comes before or after it re: markup, whether there are `<div>` wrapper containers, and the depth of the menu (display one level or two).

However, in order for it to work there are some things we need to do in the theme as well as in the admin area.
1. We need to call the `add_theme_support()` function and pass it a parameter of 'menus'. by default wordpress won't give you menu options for your theme.
  1. Go to functions.php and add a hook action above all your other functions:

   ```
   add_theme_support( 'menus' );
   ```

   Once this is done, we can now see menus as an option in the admin area.

2. In functions.php we need to tell wordpress that we have a specific menu setup. So we create a new function `register_theme_menus()`

```
function register_theme_menus() {
  register_nav_menus(
    array(
      'primary-menu' => __( 'Primary Menu' )
    )
  );
}
add_action( 'init', 'register_theme_menus' );
```

   The parameters passed in the above array tell wordpress that this theme has specific menu or navigation areas.

At this point we've told wordpress that we have a primary menu area, and it is available in the admin area, but it doesn't exist anywhere in our theme.


## Coding a Basic Navigation in Wordpress
So now we're going to go into our header.php file and prepare it for taking in a navigation menu.

In betwee the .open `<h1>` and the .no-bullet `<ul>` we're going to open up a php block. Then we're going to set the default arguments for working with the wp_nav_menu function. This is done with an array full of parameters.
1. 'container' - by default wordpress will wrap your menu, which is an unordered list, inside of a `<div>` tag. Since our code ges straight from an `<h1>` directly into the `<ul>`, we don't want that extra code outputted. Thus we set 'container' => false
2. 'theme_location' - this tells wordpress where the primary menu lives. In functions.php we setup the 'primary-menu' but we didn't tell wordpress where that is. We do this now.
3. 'menu-class' - this assigns a class to the first element (in this case the <ul>. had we left 'container' => true, then that <div would be the first element and recieve whatever class we assign here).

Once we've done all that we simply need to run the `wp_nav_menu()` function, passing $defaults as the parameter.

```
<?php 
  $defaults = array(
    'container' => false,
    'theme-location' => 'primary-menu',
    'menu_class' => 'no-bullets'
  );

wp_nav_menu( $defaults );
?>
```


## Coding Your Own Custom Post Type Templates
It is possible to create a custom post type in our functions.php file using the `register_post_type()` function. This is not recommended though. If the post type is setup in your theme, and someone switches away from your theme, they lose the ability to manage the information in that custom post type. That custom content will no longer be available.

Instead of building these custom post types in the theme we're going to build them using plugins so they operate regardless of selected theme.

So install the Custom Post Type UI and Advanced Custom Fields plugins, which were discussed ina previous lesson; and setup the Portfolio post type with a Description and Image.

Complete the setup in the admin area.


## The WP_Query Function
The `WP_Query` function is a special function that lets us specify what we want a specific loop to display on a page.

Thus far, we've let the loop decide what to display, but with wp_query we can customize this output. 

Check out the [codex.wordpress.org/wp_query#Parameters](codex.wordpress.org/wp_query#Parameters) to see what parameters are available to us to customize the query to look for specific post types.

These are similar to the normal loop in that there's an IF statement checking if anything is avaialble and then looping through those options until there's no longer anything to loop through.

However, it's written a bit differently. Instead of just if have_posts() we're establishing an object ($the_query) by calling a new `WP_Query()` function with blank arguments.

In the past we've just checked if `have_posts()` or while `have_posts()` or `get_the_post()`, etc. Now we'll have to create a query object on our own and make sure we call that object specifically in our loop.

Make sure, once you're done with your loop, to run wp_reset_postdata(); to avoid affecting one loop with the data from another.


## The Portfolio Homepage
Let's start with the page.php template and use it as the base for our page-portfolio.php. Don't forget the code at the top of the page to set it up as a custom template:

```
<?php
/*
  Template Name: Portfolio Page
*/
?>
```

Now we need to jump back to the portfolio page in our static site and grab the HTML markup to display the portfolio data. This is hand coded in the static page, but when it's n our loop we'll only have to enter the code once with some adjustments.

Let's create a new php block and an array called $args, which will house the parameters we send to WP_Query.

```
<?php
  $args = array(
    'post_type' => 'portfolio'
  );

  $query = new WP_Query( $args );
?>

<section class="row no-max pad">
  <?php if( $query->have_posts() ) : while( $query->have_posts() ) : $query->the_post(); ?>

    <div>
      <a href="<?php the_permalink(); ?>"><img src="<?php the_post_thumbnail('large');" alt""></a>
    </div>

  <?php enwhile; endif; wp_reset_postdata); ?>
</section>
```


## The Portfolio Single Page
Since the page-sidebar-left.php has a similar layout to the portfolio details (or single) page, we're going to use that as the basis for the single-portfolio.php.

Since we followed the normal naming convention we don't actually need the php comment at the top of the page that tells wordpress what the template name is.

Since output from the loop is going to be in both the main area AND the sidebar area of this page we need to move our loop up a bit and close it further down the page.

That allows us to work with the cloop content in both the primary and secondary columns.

In the primar column, we want to display the images. We can do that as follows:

```
<?php the_field('images'); ?>
```

In the sidebar, instead of displaying an `<h2>` tag, we want to use the `<h1>` tag and display `the_title()`.

```
<h1><?php the_title(); ?></h1>
```

Let's also display the description in the sidebar. We'll do this by using `the_field()` function again, but this time we'll pass the 'description' parameter.

```
<p><?php the_field('description'); ?></p>
```

Just a note that `the_field()` function is only used with the Custom Fields plugin. It is not native to wordpress.

Now everything works, but it's a bit janky and we want to add an option in the sidebar, underneath the description to jump back to the portfolio or to the previous/next portfolio item.

We can do this using a function called `previous_post_link();` and `next_post_link();`


## Setting up the Blog Homepage
The blog listings are typically managed from home.php. Since the layout for the blogs home is going to be similar to the left sidebar template, we'll use post-sidebar-left.php as the base for our home.php code.

Remove the code at the top that let's wordpress know what the template name is.


## Coding the Blog Homepage
In the blog.html page from our static site you can see the `<article>` tag and the HTML markup that will be applied to our blog posts as they're listed out.

Move that into the the home.php template INSIDE the loop.

Now that the blog post markup is setup, we need to make sure the content is being filled dynamically.

1. The link to the single blog post. Instead of hard coded, we need the permalink for each post. Not surprisingly, `the_permalink()` function will help us here.

```
<h1><a href="<?php the_permalink(); ?>">The Title</h1>
```

2. Next we can pull the hardcoded title and replace that with the_title() function.

```
<h1><a href="<?php the_permalink(); ?>"><?php the_title(); ?></h1>
```

3. Instead of a hard coded excerpt, we want wordpress to handle that, so we use `the_excerpt()` function.

```
<h2><?php echo strip_tags( get_the_excerpt() ); ?></h2>
```

4. Now we need to display the authors avatar. We can do this using the `get_avater()` function, but remember that "get_" functions get the avatar object and we have to pass some parameters about how the item should be displayed.

```
<?php echo get_avater( get_the_author_meta( 'ID' ), Instead
```

5. Instead of displaying a hardcoded authors name, we'll use a function called `the_athor_posts_link()`. This generates a link to a special author page that we can control via the archives page.

```
</php the_author_posts_link(); ?>
```

6. We can then come down to the category links and replace the whole link with `the_category()` function. This particular function will take in a parameter that determines how the categories are separated, but it's not required.

```
<li class="cat">in <?php the_category( ', ' ); ?></li>
```

7. We should also display the date the post was published so:

```
<li class="date">on <?php the_time('f j, Y'); ?></li>
```

8. Finally, we need to display the featured image of the post. We did this early so we can copy/paste that code here with a minor adjustment.

```
<?php if (get_the_post_thumbnail() ) :
  <div class="img-container">
    <?php the_post_thumbnail('large'); ?>
  </div>
<?php endif; ?>
```

To descrease the length of the excerpt go to functions.php and create a new function called `wpt_excerpt_length()`

```
function wpt_excerpt_length( $length ) {
  return 16;
}
add_filter( 'excerpt_length, 'wpt_excerpt_length', 999 );
```


## The single.php Page
The template for a single blog post looks similar to the blogs listing template so we're going to use that as the base for single.php 

Instead of using `the_excerpt` to display we'll obviously display the full content, so...

```
<h2></php echo strip_tags( get_the_excerpt() ); ?></h2>
```

becomes:

```
<?php the_content(); ?>
```


## Adding Comments to a Template
Adding comments to our template is as simple as adding the `comments_template()` function. 

This function takes a couple of parameters, specifically the file option and whether to sepearate comments by comment type. Both of these are optional.

After the_content() function we want another function that displays the comments.

```
<?php comments_template(); ?>
```


## A Catch All Archives
We're going to use home.php as the model for our archive.php page.

Before we get into the loop though we want to add a header to let people know what page they're on.

So push the loop down and above that add the following:

```
<div class="leader">
  <h1><?php wp_title(''); ?> Blog Posts</h1>
</div>
```


## A Static Homepage Template
We need a front-page.php template. We'll use index.php as the base for this new page.

Instead of a regular homepage, we actually want the portfolio loop on the homepage so we're going to go to that portfolio listing page and bring that code into front-page.php

Good coding practices say that just copy/pasting is a bad idea, so instead we're going to use an include to do it.

Create a new file called content-portfolio.php and let's put that altered query in there.

Then on both the front-page.php and the page-portfolio.php we are going to use the `get_template_part()` function.

```
<?php get_template_part('content', 'portfolio'); ?>
```

This is basically a php include that pulls the "content" "-" "portfolio" .php file.

Say for instance that we didn't want to include as many of the portfolio items on the front page as we do on the portfolio page.

To achieve this we can include the posts_per_page parameter.

To do this we should check out the [Conditional _Tags page in the codex](http://codex.wordpress.org/Conditional_Tags).

Now edit the content-portfolio.php file to check if the page is the front page and if so, only display 4 posts.

```
$num_posts = -1  //sets the default to ALL
if( is_front_page() ) $num_posts = 4;  // overwrites the default if the front page
```

A  simplified version of this same if statement is:

```
$num_posts = ( is_front_page() ) ? 4 : -1;
```

We also have to edit the arguments we pass through to include the number of posts.

```
$args = array(
  'post_type' => 'portfolio'
);
$query = new WP_Query( $args );
```

becomes

```
$args = array(
  'post_type' => 'portfolio',
  'post_per_page' => $num_posts
);
$query = new WP_Query( $args );
```


## Adding Widget Areas to a Wordpress Theme
Site is basically setup, but we want to add in the sidebar widgets.

Open up functions.php and drop in the following code to setup widgets:

```
function wpt_create_widget( $name, $id, $description ) {
  register_sidebar(array(
    'name' => __( $name ),
    'id' => $id,
    'description' => __( $description ),
    'before_widget' => '<div class="widget">',
    'after_widget' => '</div>',
    'before_title' => '<h2 class="module-heading">',
    'after_title' => '</h2>'
  ));
}
wpt_create_widget( 'Page Siderbar', 'page', 'Displays on the side of pages with a sidebar' );
wpt_create_widget( 'Blog Sidebar', 'blog', 'Displays on the side of pages in the blog section' );
```

This is a helper function that allows us to easily create widget areas.

Now we need to get into all the templates that display sidebars.

Setup a new file called sidebar.php to easily include this similar code on multiple pages.

Use the `get_sidebar()` function to call the sidebar.php file.

On page-sidebar-left.php we're going to pass a parameter with the `get_sidebar()` function called 'page'. This calls a different file. instead of sidebar.php it will pull up sidebar-page.php which can be customized a little differently.

On sidebar.php and sidebar-page.php you need the following code to dynamically display widgets:

```
<?php if( !dynamic_sidebar( 'page' ) ): ?>

<?php endif; ?>
```


## Adding Shortcodes to Your Theme
Shortcodes can be used to help content contributors easily style content.


## Testing Your Wordpress Theme
in the wp-config.php file you want to turn on debug mode by finding:

```
define('WP_DEBUG', false);
```

and setting it to:

```
define('WP_DEBUG', true);
```


****************************************************************************************************
# The Wordpress Template Hierarchy


## How Wordpress Templates Work
Template in wordpress is a single php document that determines how a page or set of pages look on the front-end of a site.

They can include HTML, php and special wordpress PHP functions. Template even exist for CSS and javascript files.

Anything you would code in a static site moves over to wordpress template in some way.

Wordpress has a special naming convention associated with these files. That means the names are similarly named, which makes the easier to work with.


## The Template Hierarchy
[codex.wordpress.org/Template_Hierarchy](codex.wordpress.org/Template_Hierarchy)
[codex.wordpress.org/imates/1/18/Template_Hierarchy.png](codex.wordpress.org/imates/1/18/Template_Hierarchy.png)
* Types of pages on the left and then moves through the types of templates that would work for each page.

[wphierarchy.com](wphierarchy.com) is the same as the above image, but an interactive web interface that links you to the specific page of the codex.

Say you had a single page on the site. Wordpress will determine whether it's a post page or a static page. Assume it's a static page, then it will determine if there's a custom template (with a custom name) or if it's the default page template, in which case we could have page-slug.php OR page-ID.php (these actual file names would look like page-about-us.php or page-4.php). If neither of these page options are available, then wordpress will look for the backup, page.php. IF that's not available then it will default to index.php

New hypothetical. Say you've got an Archive page that you want categorized by date. In order to do this, we would create date.php. If date.php doesn't exist then wordpress will look for archive.php. As always, if archive.php doesn't exist then wordpress will fall back to using the index.php template.


## Common Wordpress Template Code
The Loop is the most common piece of code you'll find in a wordpress template.

`WP_Query` is also common. It is a customization that we add to the loop to let it search for different things.
* For example, if we wanted the loop to only pull posts from a specific author, then we would edit the WP_Query and pass it a parameter 'author_name'.

`get_template_part` is the final piece of common wordpress template code. We use this in wordpress to include files.

```
<?php get_template_part( 'slug', 'additional items'); ?>
```

For example, `<?php get_template_part( 'loop', 'index'); ?>` would look for the file loop-index.php and `<?php get_template_part( 'loop', 'blog'); ?>` would look for the file loop-blog.php.


## style.css
This page is required of ALL wordpress themes. It contains both the main styles for the theme as well as the meta data about the theme.


## index.php
The index.php file serves as the backup for ALL other templates. For this reason, you will likely want to keep index.php fairly generic, unless you're also building out all of the other templates you'll need.

The index.php in our example is pretty simple. Contains a `get_header()` and `get_footer()` functions to load up the headers and footers, there's some HTML markup, The Loop, the content that displays for each post or page, clode the loop, pull in the sidebar, close some HTML markup.


## header.php
header.php is the naming we use to make sure wordpress' `get_header()` function calls the proper file. If we named header.php something else, like top-header.php, then the `get_header()` function wouldn't work.

```
<?php wp_header(); ?>
```

This is a critical piece of the wordpress code. It allows wordpress to hook into our code and output any CSS or javascript or code that needed. That function needs to be included BEFORE the closing head tag.

```
<body <?php body_class(); ?>>
```

This is another very helpful function. This outputs special code, as class attributes, to the body tag of the site.

Navigation code is also typically found in the header.php file since it will typically be included on every page. 

The `wp_nav_menu()` function is what builds the navigation.


## footer.php
First thing to do in the footer.php is to make sure you're closing any HTML markup that was opened in the header.php file.

Like the header.php file we have a special function that allows plugins to hook into the footer of the site before the closing `</body>` and `</html>` tags.

This function is `<?php wp_footer(); ?>`


## sidebar.php
sidebar.php gets called by templates using the `get_sidebar()` function.

Typically in a sidebar, you'll display widget information, which is done using the `dynamic_siderbar()` function.

Important to note that you can have multiple sidebar files for your site. On index.php you might call the main sidebar.

That would look like this:

```
get_sidebar();
```

However, on the blogs.php you might want a separate sidebar for the blog, in which case you would use the same function, but pass it a parameter, like this:

```
get_sidebar( 'blog' );
```

This would load the sidebar-blog.php file. If the parameter above had been 'about' the function would look for the sidebar-about.php file to load.


## Homepage Templates in Wordpress
Wordpress offers users the option to set whether the homepage of the site is a static page or the blog listings page. Most sites today use a static page and typically that's being managed by front-page.php and the home.php managed the blog listings.

If you don't use the static homepage option, then home.php gets used for the main site homepage and front-page.php is completely ignored.


## front-page.php
If there is no front-page.php your site will default to page.php as the template for your homepage.


## home.php
home.php is the default for blogs listings on your homepage. If home.php doesn't exist, then index.php will be used.


## Static Page Template Files
By default, page.php controls the static pages on the site.

There are way to step in front of that default though. For example, if you wanted a specific template for your about-us page with a post-id of 100 then we could use page-100.php or page-about-us.php to override the default page.php.

Keep in mind this works ONLY on the page selected. In the above example, the Homepage or the Contact Us page or the Services page would be unaffected by the page-100.php code. These pages would still be using page.php instead of page-100.php.

Another way we could do this would be to create a separate page template. This requires that we have some specific code at the top of the page:

```
<?php
/*
Template Name: PAGE TEMPLATE NAME
*/
?>
```

This would allow users to select this template in the backend of wordpress when they edit pages. 

In this case, you could setup the About Us page AND the Contact Us page to use this template, but not the Homepage or the Services page.

Keep in mind that this final option of setting the page template in Wordpress OVERRIDES whatever defaults might have been setup. Even if we have a custom template like page-about-us.php the About Us page would use whatever is set in the backend of wordpress.


## Single Post and Post Format Templates
Single blog posts are controlled by the single.php page.


## The Comment Template
Important to know, when working with posts, about the comments.php template.

The comments.php template contains all the markup and code needed to display the comment form on blog posts.

This file contains a bunch of accessibility code that make the forms easier to use for screen readers and such. It's recommended that you leave as much of this as possible to avoid issues.

A good idea would be to use one of the default themes comments.php files as a base for creating your own. Go copy their code and then edit/adjust as necessary.


## Post Formats
Post formats in wordpress help describe either what the post is about or what type of content it's using.

There is not custom templates for each of these but we do have some practices for seeing how they work.

In single.php, which controls how an individual post is displayed, you'll see `get_template_part( 'content', get_post_format() );` which will echo out the post format selected in the admin area of wordpress.

Say you've selected "status" as the post format. That would transform the above code to this:

```
get_template_part( 'content', 'status' );
```

In this case you could have a content-status.php that controls how the posts with "status" as the selected format will be displayed.

These aren't really about template hierarchy, but using conditionals or variables to pull in code based on values selected in the wordpress admin area.

IF youre building your own theme, you do need to make sure to turn on the post formats option, AS WELL AS setting what options are available.

This is done in the functions.php file using the following code:

```
add_theme_support( 'post-formats', array( 'image', 'quote' ) );
```

This would turn on the option for users to select post formats as well as set "image" and "quote" as post format options.

Selecting these options don't actually change anything unless you properly utilize that `get_template_part()` function AND have a content-WHATEVER.php file created.


## Archive Templates in Wordpress
Archive templates are super helpful when building themes because they can work across a range of purposes.

archive.php serves as the catch all backup template.

But we can do a lot of customization based on dates or categories or authors using the other archive templates available.


## Date Archives
date.php is the default for archives by date.

In date.php we've got a basic template with a basic loop, but some conditional statements that check what kind of date archive we're looking at.

If we're looking at a year based archive, then display the month name as a header before displaying posts from that month.

If we're looking at a month archive, then don't display the month as an additional header (it's included in the title). 

## Category Archives
Unlike data archives category archives can be more specific.

category.php is the generic file to control category archives, but we can also create files that will control specific categories based on the slug or the id of the category. This is similar to what we were able to do with page. 

Blog posts with category "event" selected can override the category.php file if a category-event.php file exists.

Use can use the `body_class()` function here to customize the page based on the category archive.

In the above example, .category-event would get added to the <body> tag on this category page (regardless of whether category-event.php is used or not) and a specific CSS rule could be written for that class to alter styles.


## Author Archives
author.php manages the Author page archives.

Again, the author ID and author nice name (similar to the slug) can be used to create custom author pages based on which author we're viewing.

ex: author-4.php or author-nhogan.php


## An Important Review of Custom Post Type Setup
Wordpress provides a lot of flexibility regarding the templates managing custom post types, but you do have to pay some attention to how the custom post types are being setup.

When creating a Custom Post Type, we need to pay attention to a few advanced options.
1. Has Archive - Does this custom post type have an archive page at all. By default this is set to false, which means we have to use WP_Query in order to pull this data.
2. Rewrite - Helps setup the URL for custom post types and permalinks. Works in conjunction with the Custom Rewrite Slug.
  1. If your custom post type is "porfolio" you could set the Custom Rewrite Slug to "work" and would use "work" instead of the default "portfolio"

Like the categories, we can create a new file archive-portfolio.php to manage the listing of portfolio items.

The page used to control the look of a single custom post type is single-customposttype.php, otherwise it will just use single.php (like all other posts).


## Media Templates
If we select the Attachment Page as the Link To option when we add a piece of media to our content, then there is a special template that will manage the look of this page.

MIME types are used to determine how these items are displayed.

image.php overrides png.php overrides attachment.php


## Search Templates
search.php is going to control what the search results page looks like.

We can add the search form in two ways:
1. Add the search widget into one of our sidebars
2. Use the `get_search_form()` function

`get_search_form()` actually pulls searchform.php and inserts that code on the page. So if you need to customize the search form, you would do that at searchform.php.


## 404 Pages
404.php is what controls error pages on the wordpress site.



****************************************************************************************************
# Wordpress Hooks - Actions and Filters

## An Overview of Hooks in Wordpress
Hooks will significantly expand the functionality of wordpress, but might require more knowledge and experience with php to meet your needs.


## Definition of Terms - Actions vs Filters
1. Hooks - A generic term in Wordpress that refers to places where you can add your own code or change what Wordpress is doing or outputting by default. Two types of hooks exist in Wordpress, actions and filters.
2. Actions - A hook that is triggered at a specific time when Wordpress is running and let's you take an action.
  
   ex:
   * creating a widget when wordpress is initializing
   * sending a tweet when someone publishes a post
3. Filters - Allows you to get and modify Wordpress data before it is sent to the database or the browser.
  
   ex:
   * customizing how excerpts are displayed
   * adding in some custom code at the end of a blog post

Can be confusing at first to determine whether something is an action OR a filter. Important difference is that when you work with a filter, you'll receive some data and at the end return it back. Actions, on the other hand, you're not receiving and modifying any data, you're simply given a place in the wordpress run-time where you can execute your code.


## Actions and Filters in the Codex
* [codex.wordpress.org/Plugin_API/Filter_Reference](codex.wordpress.org/Plugin_API/Filter_Reference) - Lots of information about creating plugins and filters in general, as well as what filters are available for use. Lots of filters are applied to template tags that you'll recognize from theme development. 

  Some filters apply when we read from the database and others apply as we write to the database.

  Again, filters are working with data between the database and the browser, or vice versa.

* [codex.wordpress.org/Plugin_API/Action_Reference](codex.wordpress.org/Plugin_API/Action_Reference) - Actions different in that instead of manipulating data before or after it comes from the database or browser, we're inserting OUR code at certain points as wordpress is building out the site or admin area.

  For instance:
  * actions run during a typical page build
  * actions run when building out an admin page

  Similar to filters, there's also actions for different categories (posts or pages or comments, etc.) but instead of manipulating data we're executing our code at those points. 

  We can execute code when a post is being edited or deleted, when it's being published or when it's being saved. And so on.


## Dash for Documentation
Only avaialble for Mac.

Once you've installed Dash you'll be asked if you want to download documentation. This lets you download documentation from a ton of places online and lets you easily access them from keyboard shortcuts.

Setup a global search shortcut or hotkey combo that will automatically open up a search in the wordpress documentation.

This tool is extremely useful when you want to see the documentation on a specific action or filter or function or whatever. Use your hotkey to pull up the search, type the function name, read your info and quickly close the tool without having to go hunting online for the page you need.


## Working with `$wp_filter`
`$wp_filter` is another option to find out what hooks are available in wordpress.

Echo this out onto the screen let's you see native hooks, custom hooks that we've setup, and any third party plugin hooks that are being used.

In addition to seeing the hooks themselves, we also get to see the different functions that are tied into that hook.


## Query Monitor Plugin
A plugin that will show you, like the `$wp_filter`, what hooks are running and what functions are associated with them. 

Can actually split up hooks by front-end/back-end and what's core wordpress vs what's from installed plugins.


## Searching Wordpress Core
Looking the the wordpress core code is also an option for finding out more information about hooks.

Open up a text editor and use the advanced search to look at the entire wp install. Search for `add_filter( 'wp_title`.

This is the code that any function would use when it wants to tie into `wp_title`

In this example, twentyfouteen theme is using this filter. Typically the function they're calling is right above the hook, so you should be able to easily see the filter and what the filter is doing. 

New example. Instead of searching for `add_filter( 'wp_title` we're going to search for `add_action( 'init`.

  Be aware that the core wordpress code follows some standards re: their code, like the space between the opening parenthesis in "add_filter" and the attribute we're passing. Plugins might not follow these same standards and you might have to tweak your search accordingly.
    * add_action( 'init
    * add_action( "init
    * add_action('init
    * add_action("init


## The add_filter Function
`add_filter()` - This is the code used to add your own function into an existing hook.

We can see that the `add_filter()` function is accepting a few arguments.
1. The original hook you want to tie into (any filter)
2. The function you want to call (YOUR CODE)
3. The priority level (defaults to 10 and can leave empty if no change)
4. The number of accepted arguments (defaults to 1, since most filters will go get one thing and edit/return it - not always the case so make sure to include that if you need to send something other than 1)

Couple lessons back we edited the excerpt length. This was included as part of our theme in the functions.php file. 

```
function my_custom_excerpt_length( $length ) {
  return 20;
}
add_filter( 'excerpt_length', 'my_custom_excerpt_length', 999 );
```

So we're tieing into a filter called 'excerpt_length', and then calling our own custom function, 'my_custom_excerpt_length', and setting the priority to 999. High priority means that our function runs LATER (we want it to be the last thing that affects the 'excerpt_length').


## The remove_filter Function
`remove_filter()` - This is the code used to remove a function from an existing hook.

Similar to apply_filter we can see that this accept a handful of arguments:
1. The original hook you want to tie into (any filter)
2. The function you want to call (YOUR CODE)
3. The priority level (defaults to 10 and can leave empty if no change)

Since we're removing the function from the hook, we definitely don't need to pass a parameter and so this function doesn't ask for how many parameters.

Say we wanted to look at the_content filter and wanted to remove the `do_shortcode` function from that filter. This would make sure that shortcodes NEVER run inside of the_content.

Our code would look like this:

```
remove_filter( 'the_content', 'do_shortcode', 11 );
```

This goes to the_content filter, and removes the do_shortcode function and sets a priority of 11.

Basically this is useful if you don't like the way something is executing and want to stop it OR if you want to replace the way it executes with a function of your own.

```
remove_filter( 'the_content', 'do_something', 11 );
add_filter( 'the_content', 'do_something_instead', 11 );
```


## The apply_filters Function
`apply_filters()` - taking in a few parameters. 

1. The name of the filter we want it to have.
2. The default value.
3. One or more variables passed, that we can use within the filter functions.

```
// First create a custom function
function example_callback ( $string ) {
  $new_value = $string . " NEW!";
  return $new_value;
}
// Then hook it into a new example hook
add_filter( 'example_filter', 'example_callback' );

// Then use apply_filters in your code when you want the filter to run. This is what we would use in our plugin or theme that grants users access to filter a piece of info
echo $value = apply_filters( 'example_filter', 'default value' );
```


## Wordpress Filter Helper Functions
We're going to look at three helpful functions that help us write code re: filters.
1. `has_filter()` - Let's us do two things.
  1. Checks to see if certain filter exists, if it does then we can run our own code. Helpful if you want to tie into another hook if it exists.
  2. Checks to see if a specific function is tied into a specific hook. You could then run code dependant on that result. For instance, if a function is tied to a filter, then you could remove the function and do your own function.
2. `current_filter()` - This tells you the action or filter that is being run, that your code is tied in to. Helpful if you wrote a single function that operates on a lot of different hooks, but does so differently depending on the hook used. Like a sanitization function that operates everytime someone saves data. In certain places of your site you might want that code to operate a little differently. 
3. `is_main_query()` - Heplful for filters that apply within the main query. If you run multiple loops on a page or if you're running custom loops, you'll want to be able to identify whether it's the main loop and only affect code there. Other instances of the loop would be unaffected.


## Real World Examples of Wordpress Filters
Let's look at some real world examples of fitlers.

### Custom Title

```
function custom_wp_title( $title, $sep ) {
  global $page;

  // Add the site name.
  $title .= get_blogInfo( 'name' );

  //Add the site description for the home/front page.
  $site_description = get_bloginfo( 'description', 'display' );
  if ( $site_description && ( is_home() || is_front_page() ) ) {
    $title = "$title $sep $site_description";
  }

  return $title;
}
add_filter( 'wp_title', 'custom_wp_title', 20, 2 );
```

### body_class

```
function custom_body_classes ( $classes ) {
  if ( 'post' == get_post_type() ) {
    $classes[] = "custom-class";
  }
  return $classes;
}
add_filter( 'body_class', 'custom_body_classes' );
```

### manage_posts_columns

```
function manage_posts_columns_example( $columns ) {
  unset( columns['author'] );
  unset( columns['categories'] );
  unset( columns['tags'] );
  unset( columns['comments'] );
  return $columns
}
add_filter( 'manage_posts_columns', 'manage_posts_columns_example' );
```


## The `add_action` Function
`add_action()` - 
1. Takes the hook we latch on to
2. The function we want to add
3. The priority level
4. The number of accepted arguments

Example of `add_action()` in practice:

```
function add_google_font() {
  wp_enqueue_style( 'google_font', 'http://fonts.googleapis.com/css?family=Pacifico' );
}
add_action( 'wp_enqueue_scripts', 'add_google_font' );
```

Basically, when it's time for `wp_enqueue_scripts` to do it's thing, we're adding `add_google_font()` as one of the things we want done, which will run the `wp_enqueue_style()` function, which throws adds a style tag linking to the URL parameter.

This does not output any code. It just adds our function to the list of things that need to happen.


## The remove_action Function
`remove_action()` operates in the opposite fashion of add_action().

Instead of calling our a function that we want executed at a specific point in the wordpress build, we're saying DON'T do the specific function at the specific time of the wordpress build.

```
remove_action( 'wp_enqueue_scripts', 'add_google_font' );
```

  In the previous section we added the `add_google_font()` function to the list of things to do when wp_enqueue_scripts() runs.

  The above code, simply removes the `add_google_font()` function from the list of things to do in wp_enqueue_scripts.

This can apply to native functions, custom functions, or third-party functions. If a plugin you downloaded is using a hook to do action that you don't like, use this to remove that action, possibly replacing it with one of your own.

`remove_all_actions()` and `remove_all_filters()` will remove all the actions or filters from specified hook. you could even pass a priority to only remove actions with a priority of 11 or 10 or whatever you specify.


## The do_action Function
You place this in the code where you want an action hook to take place.

`do_action()` can take the name of the action and the arguments you want to pass (whether that's one or more) OR you can use do_action_ref_array() to pass the name of the action and an array that contains any arguments you want to pass.

```
function custom_footer() {
  do_action('my_footer');
}

function custom_footer_text() {
  echo "Custom Footer Text";
}
add_action( 'my_footer', 'custom_footer_text' );

// In your template code
custom_footer();
```


## Action Helper Functions
`has_action()` - allows you to see if a specific action hook exists, as well as if a specific function is tied into that hook.

  Could be used in an if statement to see if a function is tied to an ction hook, and if it is, removing it and adding your own function to that hook.

`current_filter()` - Technically, actions are a type of filter and so current_filter() works on both.


## Real World Examples of Wordpress Actions

1. wp_enqueue_scripts - Used many times in previous lessons and courses to add stylesheets or .js files to the header/footer of a page.

2. widgets_init - This runs when widgets are beginning to be setup in wordpress

3. init - We add actions to the init hook to call functions that build menus.

4. admin_menu - Could be used to remove options from the admin menu.


## Hooking Into Wordpress Plugins
Up to now we have primarily looked at tieing into the native hooks in wordpress.

Now we're going to look at how to create our own hooks that other developers can use to tie into our theme or plugins.


## Gravity Forms Example
`gform_submit_button` is a filter hook built into Gravity Forms.

```
add_filter("gform_submit_button", "form_submit_button", 10, 2);
function form_submit_button($button, $form) {
  return "<button class='button' id='gform_submit_button{$form["id"]}'><span>Submit</span></button>';
}
```


## Advanced Custom Fields Example
`load_field` - a filter that allows you to pull a field data and customize it before sending it out to the page.

If you were using Advanced Custom Fields on your site and wanted to display a custom field on your page you would need this:

```
<div class="custom-area">
  <?php the_field('custom_field'); ?>
</div>
```

The runs `the_field()` function and uses the 'custom_field' parameter to know which custom field to get. 

Using the filters you could customize how that field is presented.

****************************************************************************************************
# Wordpress Customizer API


## Introduction to the Course
We're going to cover how to integrate your wordpress theme with the live theme customizer option.

Taking an in-depth look at customizer in action and native customizer options as well as how to create your own custom settings.


## Settings - Customizer Terms
Settings - Is an individual customization option avaialble for changing in the theme customizer area.

Each individual option we have to change in the customizer area is a setting.

Some settings are default and come with the customizer (blog name, background color, background, etc.), but you can add your own settings to your own themes (like custom logo, font styles, etc.).

Settings are saved in wordpress using the `$wp_customize->add_setting()` funtion and they're available for access in the theme using the `$wp_customize->get_setting()` function.

That said, you can't add a setting without adding the code for a controller. Creating a new setting tells WP that the setting exists, but the code for the controller is what is displayed in the theme customizer.

In twentyfourteen theme Site Title is a setting and Tagline is a setting, but are managed with multiple controls (the actual text, the color of the text, the size of the text, etc.).

```
$wp_customize->add_setting( 'header_textcolo', array(
  'default' => '#000000",
  'transport' => 'refresh',
) );
```


## Controllers - Customizer Terms
Controller - the actual HTML element that someone uses to modify a setting.

Different types of setting will obviously have different types of controllers.

* The blog name would use a text input contoller whereas the color for a link would use a color picker controller, and selecting the log would use an image uploader controller.


## Sections and Panels - Customizer Terms
Sections - Different areas of the theme customizer divided by collapsible headings.

Wordpress has a few default sections

1. title_tagline
2. colors
3. header_image
4. background_image
5. navigation
6. widgets
7. static_front_page

Can add your own section to the customizer using the `$wp_customizer->add_section()`

Panel - a grouping of section in the theme customizer


## Transports - Customizer Terms
Transports - One of the parameters for a setting determining how a setting is updated and displayed in the preview area.

Two options:
1. Refresh - The preview area will "refresh" to show the updated setting
2. Post Message - The setting will change live in real-time


## The customize_register Action Hook
Add the following code to your functions.php page

```
function wpt_register_theme_customizer( $wp_customize ) {
  //var_dump( $wp_customize );
}
add_action( 'customize_register', 'wpt_register_theme_customizer' );
```

The comment on line 2 will pull all the customizable settings and controls and display the variable contents on the page. Not good for production, but excellent for debugging and finding out what you have to work with.


## Site Title and Tagline

```
function wpt_register_theme_customizer( $wp_customize ) {
  // Customize title and tagline sections to read "Site Name and Description
  $wp_customize->get_section('title_tagline')->title = __('Site Name and Description', 'wptthemecustomizer');
  
  // Customize label for the field controlling the site title to read "Site Name"
  $wp_customize->get_control('blogname')->label = __('Site Name', 'wptthemecustomizer');
  
  // Customize label for the field controlling the site description or tagline to read "Site Description"
  $wp_customize->get_control('blogdescription')->label = __('Site Description', 'wptthemecustomizer');
  
  // Update the transport option on the 'blogname' and 'blogdescription' settings from refresh to postMessage
  $wp_customize->get_setting( 'blogname' )->transport = 'postMessage';
  $wp_customize->get_setting( 'blogdescription' )->transport  = 'postMessage';
}
add_action( 'customize_register', 'wpt_register_theme_customizer' );

// Custom js for theme customizer
function wpt_customizer_js() {
  wp_enqueue_script(
    'wpt_theme_customizer',
    get_template_directory_uri() . '/js/theme-customizer.js',
    array( 'jquery', 'customize-preview' ),
    '',
    true
  );
}
add_action( 'customize_preview_init', 'wpt_customizer_js' );
```


## Create Custom Panels
`add_panel()` function to create new panels and rearrange existing sections to fall into new or existing panels

```
$wp_customize->add_panel( 'general_settings', array(
  'priority' => 10,
  'theme_supports' => '',
  'title' => __( 'General Settings', 'wptthemecustomizer' ),
  'description' => __( 'Controls the basic settings for the theme.', 'wpthemecustomizer' )
) );

$wp_customize->add_panel( 'design_settings', array(
  'priority' => 20,
  'theme_supports' => '',
  'title' => __( 'Design Settings', 'wptthemecustomizer' ),
  'description' => __( 'Controls the basic design settings for the theme.', 'wpthemecustomizer' )
) );

$wp_customize->get_section('title_tagline')->panel = 'general_settings';
$wp_customize->get_section('nav')->panel = 'general_settings';
$wp_customize->get_section('static_front_page')->panel = 'general_settings';
$wp_customize->get_section('header_text_styles')->panel = 'design_settings';
$wp_customize->get_section('background_image')->panel = 'design_settings';
$wp_customize->get_section('background_image')->priority = 1000;
$wp_customize->get_section('header_image')->panel = 'design_settings';
```


## An Overview of Custom Controls in Wordpress

### Adding our own custom settings

1. Create a setting
2. Create a controller
3. Adding code for postMessage updates
4. Necessary adjustments to theme template code


## Adding a Logo Uploader

### In functions.php

```
$wp_customize->add_section( 'custom-logo' array(
  'title' => __('Change Your Logo','wpthemecustomizer'),
  'panel' => 'design_settings',
  'priority' => 20
) );

$wp_customize->add_setting(
  'wpt-logo',
  array(
    'default' => get_template_directory_uri() . '/images/logo.png',
    //'transport' => 'postMessage'
  )
);

$wp_customize->aedd_control(
  new WP_Customize_Image_control(
    $wp_customize,
    'custom_logo',
    array(
      'label' => __( 'Change Logo', 'wptthemecustomizer' ),
      // Applies to the ID of the setting
      'section' => 'custom_logo',
      
      // Applies to the ID of the setting
      'settings' => 'wpt_logo',
      'context' => 'wpt-custom-logo'
    )
  )
);
```

### In index.php
```
// get_theme_mod() used to setup customization for 'wpt_logo', which is the setting ID back in functions.php
<?php if( get_theme_mod( 'wpt_logo' ) != "" ) : ?>
  <img id="logo" src="<?php echo get_theme_mod( 'wpt_logo' ); ?>">
<?php endif; ?>
```


## Making the Logo Uploader Work with postMessage

```
wp-customize( 'wpt_logo' , function( value ) {
  value.bind( function( to ) {
    if( to == '' ) {
      $(' #logo ').hide();
    } else {
      $(' #logo ' ).show();
      $(' #logo ').attr( 'src', to );
    }
  } );
});
```


## Custom Footer Text in the Theme Customizer

```
$wp_customize->(
  'wpt_footer_text',
  array(
    'default' => __( 'Custom Footer Text', 'wptthemecustomizer' ),
    'transport' => 'postMessage',
    // Since this text field WILL be saved to the DB you want to make sure it's sanitized first.
    'sanitize_callback' => 'sanitize_text'
  )
);

$wp_customize->add_control(
  // Generic object for new customization control
  new WP_Customize_Control(
    $wp_customize,
    'custom_footer_text',
    array(
      'label' => __( 'Footer Text', 'wptthemecustomizer' ),
      'section' => 'custom_footer_text',
      'settings' => 'wpt_footer_text',
      // Sets the new control as a text field
      'type' => 'text'
    )
  )
);
```

Further down in the functions.php file you need:

```
function sanitize_text( $text ) {
  return sanitize_text_field( $text );
}
```


## Custom Text Color Picker and Font-size Settings

```
// Add H1 Style Settings
$wp_customize->add_section( 'h1_styles' , array(
  'title' => __('H1 Styles', 'wptthemecustomizer' ),
  'panel' => 'design_settings',
  'priority' => 100
) );

$wp_customize->add_setting(
  'wpt_h1_color',
  array(
    'default' => #222222',
    'transport' => 'postMessage'
  )
);

$wp_customize->add_Control(
  new WP_Customize_Color_Control(
    $wp_customize,
    'custom_h1_color',
    array(
      'label' => __( 'Color', 'wptthemecustomzier' ),
      'section' => 'h1_styles',
      'settings' => 'wpt_h1_color'
    )
  )
);

$wp_customize->add_setting(
  'wpt_h1_font_size',
  array(
    'default' => 24px',
    'transport' => 'postMessage'
  )
);

$wp_customize->add_Control(
  new WP_Customize_Control(
    $wp_customize,
    'custom_h1_font_size',
    array(
      'label' => __( 'Font Size', 'wptthemecustomzier' ),
      'section' => 'h1_styles',
      'settings' => 'wpt_h1_font_size',
      // Creates a dropdown menu to choose font size
      'type' => 'select',
      
      // What are the options in our dropdown menu and their corresponding values
      'choices' => 'array(
        '22' => '22px',
        '28' => '28px',
        '32' => '32px',
        '42' => '42px',
      )
    )
  )
);
```


## Custom CSS Textarea in the Theme Customizer
Can't use postMessage for a CSS field in the customizer. Probably can but it's a bunch of extra work and probably better off not to bother.

```
// Add Custom CSS Textfield
$wp_customize->add_section( 'custom_css_field', array(
  'title' => __('Custom CSS', wpthemecustomzier'),
  'panel' => 'design_settings',
  'priority' => 2000
) );

$wp_customize->add_setting(
  'wpt_custom_css',
  array(
    'sanitize_callback' => 'sanitize_text'
  )
);

$wp_customize->add_control(
  new WP_Customize_Control(
    $wp_customize,
    'custom_css',
    array(
      'label' => __( 'Add custom CSS here', 'wptthemecustomizer' ),
      'section' => 'custom_css_field',
      'settings' => 'wpt_custom_css',
      'type' => 'textarea'
    )
  )
);
```

but down in the `style_header()` function we need a bit of code that will take our custom CSS and echo it onto the page:

```
<style>
  <?php if (get_theme_mod('wpt_custom_css') != '' ) {
    echo get_theme_mod('wpt_custom_css');
  } ?>
</style>
```

****************************************************************************************************
# Customizing the Wordpress Admin Area

## What are Admin Color Schemes
Color Schemes are basically skins that style what the admin screen looks like.

Powered by a CSS file that controls how the navigation and links, modules and windows, etc. look.


## Customizing Admin Color Schemes via a Plugin
Admin Color Schemes - plugin that gives us a bunch more options color schemes.

Admin Color Schemer - Allows you to create your own custom color scheme using color pickers.


## Customizing Admin Color Schemes from Scratch
Where do default color schemes live? `wp-admin/css/colors` folders for each scheme

Copy a CSS file from one of the default color schemes and head back to your theme - suggest using a child theme

Create a new folder in `/wp/content/child-theme-folder` called `admin-colors`. Now create a subfolder for the new scheme you're going to create.

Paste in the file you copied earlier.

Now that the file is there, we need to tell wordpress to look at it, which we'll do in our functions.php file.

```
function wpt_admin_color_schemes() {
  // get_theme_directory_uri() would get the parent theme, not the child theme so we use get_stlylesheet_directory_uri() which will look in child theme folder
  $theme_dir = get_stylesheet_directory_uri();

  wp_ admin_css_color(
    'treehouse', __( 'Treehouse' ),
    $theme_dir . '/admin-colors/treehouse/colors.min.css',
    array( '#384047', '#5bc67b', '#b38cc7', 'ffffff' )
  );
}

add_action('admin_init', 'wpt_admin_color_schemes');
```

Important to note the use of `get_stylesheet_directory_uri()` instead of `get_theme_directory_uri()` because "theme" will get the URL of the parent theme, whereas "styelsheet" will the URL of the child theme.

Could use conditionals in your functions.php to check the users role when they log in and default or disallow color scheme options based on that result.


## How to Customize the Wordpress Login Screen via functions.php
[codex.wordpress.org/Customizing_the_Login_Form](http://codex.wordpress.org/Customizing_the_Login_Form) - this breaks down all the different CSS, functions and custom hooks you'd need to customize the login screen from scratch.

We're not going to go find the login page file. Instead we're going to use `functions.php` and some hooks to alter the page.

Similar to front-end themes. You create a function in functions.php and enqueue styles and scripts to override the default login screen styles.

There are additional hooks you can get into to provide custom login or custom error messages.


## How to Customize the Wordpress Login SCreen Using a Plugin
Custom Login - plugin lets you customize the login screen.

## How and Why to Change Admin Navigation in Wordpress
Admin Nav - Links down the left side of the admin area. Links you to posts, pages, media, appearance, general, etc.

Most wordpress owners don't need to see all those options.

So we'll look at customizing the admin menu to manage which users see which links.


## How to Remove and Add Admin Menu Links via the functions.php File
[codex.wordpress.org/Function_Reference/remove_menu_page](http://codex.wordpress.org/Function_Reference/remove_menu_page)

Allows us to put in the `functions.php` the pages that we want to remove from the menu

```
function wpt_remove_menus() {
  remove_menu_page( index.php' );  // Dashboard
  remove_menu_page( edit.php' );  // Posts
  remove_menu_page( upload.php' );  // Media
  remove_menu_page( edit.php?post_type=page' );  / Pages
  remove_menu_page( edit_comments.php' ); // Comments
  remove_menu_page( themes.php' );  // Appearance
  remove_menu_page( plugins.php' ); // Plugins
  remove_menu_page( users.php' );  // Users
  remove_menu_page( tools.php' );  // Tools
  remove_menu_page( options-general.php' );  // Settings
}

add_action( "admin_menu', 'wpt_remove_menus' );
```

There is a function to add menu items, but unless you knew what you were building on that page, then you wouldn't need this. It will be covered under the Building Plugins Course.


## How to Customize the Wordpress Admin Menu with a plugin
Admin Menu Editor - Plugin lets you adjust what user roles are able to view which navigation is visible to users.


## Custom Dashboard Widgets in Wordpress
Dashboard is the default homepage after a user logs in.

Customizing this page is useful because you can provide custom messages after a user logs in. For instnace, "Welcome to a site, he's where you go to edit your homepage" etc.


## How to Add Custom Wordpress Dashboard Widgets via the functions.php File
Screen options are a per-user setting, meaning that I could not change the screen options for another user.

How do we create our own custom widget.

[codex.wordpress.org/Dashboard_Widgets_API](http://codex.wordpress.org/Dashboard_Widgets_API) - shows main function and some example code for how to use it.

```
function example_add_dashboard_widgets() {
  wp_add_dashboard_widget(
    'example_dashboard_widget', // Widget Slug
    'Example Dashboard Widget',  // Title
    'example_dashboard_widget_function'  //Display function
  );
}

add_action ( 'wp-dashboard_setup', 'example_add_dashboard_widgets' );

function example_dashboard_widget_function() {
  // Display text
  echo "Hello World, I'm a great Dashboard Widget',
}
```


## How to Add Custom Wordpress Dashboard Widgets via a Plugin
Custom Dashboard Help Widget - Gives us a nice form that let's us display text on the homepage

Allows for styling and let's you manage dashboard widgets globally (not just per user).


## Updating the Footer Text in the Admin Area in Wordpress
Custom Admin Footer Text Plugin

****************************************************************************************************
# How to Build a Wordpress Plugin

## Wordpress Plugin Project Overview
A plugin adds additinoal features to Wordpress.

## An Overview of Wordpress Actions and Filters
Wordpress development involves a lot of writing custom functions that hook in to wordpress core functionality or operating procedure.

Hook is basically a conditional statement of code that sees if anyone else has anything they'd like to run at that point.

```
function hook_example() {
  // Your code
  if ( $someone_else_has_code_to_add == true ) {
    // Run their code
  }
}
```

Wordpress has hooks embedded throughout it's code so that we can call our own functions just about any time we want.

HOOKS GIVE PLUGINS THEIR POWER

Applications with no hooks make it really hard to add additional code.

Wordpress hooks come in two forms:
1. Actions - let US do something when Wordpress does something that it provides a hook for.

   For example:
    
    * When someone publishes a post, send out a tweet with a link to that post.

* Filters - allow us to manipulate any data that Wordpress provides a hook for

   For example:

    * Wordpress provides a hook so that we can modify the main content of a post. We could take the post content and a "tweet this" button to the end of it.

Have to understand the difference between actions and filters so we can write good code that doesn't cause conflicts with other plugins.


## Examples of Wordpress Actions and Filters
[adambrown.info/p/wp_hooks](http://adambrown.info/p/wp_hooks) - probably the most referenced and comprehensive list of wordpress hooks


## Common Actions
* wp_enqueue_scripts - takes a function as its parameter. inside of the parameter function we enqueue a stylesheet (using `wp_enqueue_style()`) for use on the front-end of the site
* admin_head - takes a function as its parameter. inside of the parameter function we enqueue a stylesheet (using `wp_enqueue_style()`) to be used in the admin area of the site
* widgets_init - again, takes a function as its parameter. inside of the parameter function we use `register_widget()` to create a new widget.
* customize_register - takes a function as its parameter.


## Common Filters
* excerpt_more - determines how excess content is cut off if there's more content than can be displayed. Traditionally you'd see a "..." at the end of an excerpt. However, you can customize this to read "read more" and link to the full content. To do this, we have to hook into the excerpt_more filter
* the_content - gives us the ability to edit or manipulate the default content before it is displayed on the screen. For instance, appending a social sharing option to the end of the content.
* comments_template - can be used in a similar way as the_content to add social sharing to comments. Basically lets you use a custom comments template instead of the default one provided by wordpress.


## How to Create a Plugin Template with a Settings Page
Important to think about as plugin developers is namespacing. If we name the plugin folder `/treehouse-badges` and someone else has also used that name there's a chance these two would be conflicting with each other.
   `/wptreehouse-badges` helps avoid stepping on others' toes.

The same way a theme needs an index.php and a styles.css file our plugin will need a php with the same name as the plugin folder.

Similar to the comments in a themes styles that provides some meta data, we can add that kind of data as a comment to this file.

```
/*
* Plugin Name: Official Treehouse Badges Plugin
* Plugin URI: http://wptreehouse.com/wptreehouse-badges-plugin/
* Description: Provides both widgets and shortcodes to help you display your treehouse profile badges
* Version: 1.8
* Author: Zac Gordon
* Author URI: http://wp.zacgordon.com
* License: GPL2
*/
```

Now we write a function that allows us to add a link to the plugin settings page inside the admin menu.

```
/* 
  * Add a link to our plugin in the admin menu under 'Settings > Treehouse Badges'
*/

function wptreehouse_bages_menu() {
  /*
    * Use the add_options_page function 
    * add_options_page( $page_title, $menu_title, $capability, $menu-slug, $function )
  */

  add_options_page(
    'Official Treehouse Badges Plugin',
    'Treehouse Badges',
    'manage_options',
    'wptreehouse-badges',
    'wptreehouse_badges_options_page'
  );
}
add_action( 'admin_menu', 'wptreehouse_bages_menu' );

function wptreehouse_badges_options_page() {
  if( !current_user_can( 'manage_options' ) ) {
    wp_die( 'You do not have sufficient permission to access this page.' );
  }

  echo '</p>Welcome to our plugin page!</p>';
}
```


## Basic Markup for Wordpress Settings Pages
To see all the different markup options for the admin area we're going to use a plugin called [WordPress-Admin-Style](https://github.com/bueltge/WordPress-Admin-Style). 

This plugin creates a tab in the admin menu where you can select from a list of items and see the markup for how it's styled in the admin area.

We're going to use the 2-column format so copy that info from the provided documentation.

Then go into the plugin folder and create an `inc` folder to hold all of our include files. Inside of that inc folder create a new file called options-page-wrapper.php and paste in that code we copied above.

In our main page we'll edit the code, remove the "Welcome to our plugin" message and replace it with the following:

```
require( 'inc/options-page-wrapper.php' );
```

Head back to your includes file and start making edits to reflect what you actually want the content to look like (instead of using placeholder code) from the Wordpress-Admin-Style plugin.

First we'll need to build a form that asks for the treehouse username. 

Then we'll setup some code to show what the 20 most recent badges are. This is still only being displayed ont he backend of wordpress.

Create an images folder inside the plugin folder so we have a space where we can throw up placeholder images.

In order to link to the images in the folder, we'll need to know the URL to the folder.

Go back to your main php page and let's create a new function at the top of the page that establishes some global variables.
```
/*
  * Assign global variables
*/

$plugin_url = WP_PLUGIN_URL . 'wptreehouse-badges';
```

Then, inside of the wptreehouse_badges_options_page() function we need to call that global variable in order for it to be avaialble inside of the included page.

```
function wptreehouse_badges_options_page() {
  if ( !current_user_can( 'manage_options' ) ) {
    wp_die( 'You do not have sufficient permissions to access this page.' );
  }

  global $plugin_url;
  require( 'inc/options-page-wrapper.php' );
}
```


## Adding CSS to Wordpress Plugin Settings Pages
Earlier we talked about the `admin_head` hook to add stylesheets to the backend of our site. We're going to use that now to add some styles that will help make our plugin settings page look better.

```
function wptreehouse_badges_styles() {
  wp_enqueue_style( 'wptreehouse_badges_styles', plugins_url( 'wptreehouse-badges/wptreehouse-badges.css' ) );
}
add_action( 'admin_head', 'wptreehouse_badges_styles' );
```


## Working with Forms in a Wordpress Plugin Settings Page
In Wordpress, we use the POST format, which means the data is passed behind the scene and not in the URL.

In the form, in the include file, we're going to pass a hidden value that let's the page know (on reload) that the form was submitted.

Then, since the form action attribute is left blank and the main page will reload on form submit, we'll check whether the form was submitted and run out to treehouse for data if it was.

Obviously, we'll sanitize the data to ensure malicious code isn't submitted. Check that the username was actually submitted. Then we'll sanitize that field.

In our included file:

```
<form name="wptreehouse_username_form" method="post" action="">
  <input type="hidden name="wptreehouse_form_submitted" value="Y">

  <table class="form-table">
    <tr>
      <td>
        <label for="wptreehouse_username" id="wptreehouse_username_label">Treehouse Username</label>
      </td>

      <td>
        <input name="wptreehouse_username" id="wptreehouse_username" type="text" />
      </td>
    </tr>
  </table>
</form>
```

In the main file:
```
function wptreehouse_badges_options_page() {
  if ( !current_user_can( 'manage_options' ) ) {
    wp_die( 'You do not have sufficient permissions to access this page.' );
  }

  global $plugin_url;

  if( isset( $_POST['wptreehouse_form_submitted'] ) ) {
    $hidden_field = esc_html( $_POST['wptreehouse_form_submitted'] );

    if( $hidden_field == "Y" ) {
      wp_treehouse_username = esc_html( $_POST['wptreehouse_username'] );
    }
  }

  require( 'inc/options-page-wrapper.php' );
}
```

To test, add a short echo statement that spit out wp_treehouse_username

```
echo wp_treehouse_username;
```

Back in the included file we need to add some conditionals that check whether the `$wptreehouse_username` has been set or not.

```
<?php if ( !isset( $wptreehouse_username ) || $wptreehouse_username == '' ) : ?>
  <div class="postbox">
    // FORM
  </div> <!-- .postbox -->
<?php else : ?>
  <div class="postbox">
    // DISPLAY BADGES
  </div> <!-- .postbox -->
<?php endif; ?>
```

Reuse the conditional to check the sidebar too.


## CRUD with the Wordpress Options Table
Once we know how to accept form data we have to store it in the database so we can access it later.

Wordpress provides a table, called Options, that we will use for that purpose.

The Options table has four fields.
1. `option_id` - auto increments, so we don't actually have to fill this.
2. `option_name` - takes a unique name so we can find our plugin information in the database
3. `option_value` - stores all the plugin information that we want to save
4. `autoload` - defaults to yes. leave as is so that our information is available to us as soon as wordpress starts to run.

We want to store a couple of different pieces of information in the database:
* username
* profile feed
* last updated

We could store this information as separate entries in the database, but it's a better idea to store these values as an array and then add only a single entry to the DB.

MySQL doesn't actually allow for arrays to be stored in the DB, so we'll have to serialize the array into a string.

Normal PHP array:
```
options = array( 'username', 'profile_feed', 'last_updated');
```

A serialized array:

```
a:3:{i:0;s:8:"username";i:1;s:12:"profile_feed";i:2;s:12:"last_updated";}
```

Same data, just converted into a string.

When working with the options table we'll need to be able to Create, Read, Update, Delete data (CRUD).

Wordpress gives us some options for doing these tasks.
* add_option( 'option_name', 'option_value' )
* get_option( 'option_name' )
* update_option( 'options_name', 'option_value' )
* delete_option( 'option_name' )

Before we get started we need to create a new global variable array.

```
$options = array();
```

Then in our main function wptreehouse_badges_options_page() we need to call that new variable right after our other global variable.

```
global $plugin_url;
global $options;
```

After we've checked that the form was submitted and that the hidden field matches and we've pulled the username we can actually dump that right into the $options array, along with the current time.

```
$options['wptreehouse_username'] = $wptreehouse_username;
$options['last_updated'] = time();
```

Now we'll actually dump that info into the database using the functions we talked about earlier.

```
update_option( 'wptreehouse_badges', $options );
```

Outside of the conditional statement, we'll need to pull that information back out so we can use it to dynamically populate our page.

```
$options = get_option( 'wptreehouse_badges' );
```

Check whether the $options array is blank, and if not assign the value in the array assigned to wptreehouse_username to the variable $wptreehouse_username

```
if( $options != '' ) {
  $wptreehouse_username = $options['wptreehouse_username'];
}
```

Now the plugin settings page is working great. We add a name once, and it gets stored into the DB so when we come back to the page the information is still there. 

However, there's no options to remove/change the name we have stored in the DB so we need to create that option.

Copy the original form from the include file and let's paste it in the sidebar column below the gravatar and Badges/Points. This copied version of the form will only get displayed IF the wptreehouse_username is already set.
   
   Don't forget to change the "Save" value on the button to "Update".

   Also, echo out the current username into the field to autoload it.

```
<input name="wptreehouse_username" id="wptreehouse_username" type="text" value="<?php echo $wptreehouse_username; ?>">
```


## JSON as an API
When we pass data between two sites we often use an API. API stands for Advanced Programming Interface.

The Wordpress admin area serves as the interface for us to interact with all of the content stored in the database and files. In the case of interaction between two web applications, we often use an interface called JSON.

JSON is simply a text file with a specific structure and data that one site can provide to another. This is an example of a one-way interface; one site is passing JSON to another.

JSON - Javascript Object Notation. Really just a special type of javascript file.

Example of a simple JSON file:

```
{
  "treehouse_teachers": [
    {
      "first_name":"Zac",
      "last_name":"Gordon"
    },
    {
      "first_name":"Guil",
      "last_name":"Hernandez"
    },
      "first_name":"Jim",
      "last_name":"Hoskins"
    }
  ]
}
```

Very readable and very customizable:

```
{
  "treehouse_teachers": [
    {
      "first_name":"Zac",
      "last_name":"Gordon",
      blog_url": "http://wp.zacgordon.com"
    },
    {
      "first_name":"Guil",
      "last_name":"Hernandez",
      "treehouse_profile" : "http://teamtreehouse.com/guil"
    },
      "first_name":"Jim",
      "last_name":"Hoskins",
      "twitter_handle" : "@jimrhoskins"
    }
  ]
}
```

Important to note that JSON formatting is very specific and will fail if we don't format it properly.


## Getting and Storing a JSON Feed
In order to pull in the treehouse user data we're going to have to use a function called `wp_remote_get()`

`wp_remote_get( $url, $args )` - takes two parameters:
  
  * the URL it needs to pull in and
  * any special arguments

`timeout` should be one of your arguments. Because some JSON files are fairly long, we'll need to set the timeout to ensure we have enough time to pull all the data we need.

Let's go back to the main plugin page and we'll write a function to pull the JSON feed.

```
function wptreehouse_badges_get_profile( $wptreehouse_username ) {
  $json_feed_url = 'http://teamtreehouse.com/' . $wptreehouse_username . '.json';
  $args = array( 'timeout' => 120 );

  $json_feed = wp_remote_get( $json_feed_url, $args );

  $wptreehouse_profile = json_decode( $json_feed['body'] );

  return $wptreehouse_profile
}
```

Now move back up and after we check if the username is set we'll call our new function, assign it to a new variable, and dump that new variable of data into the DB. We'll also pull it out, just like we do with the username.

```
function wptreehouse_badges_options_page() {
  if ( !current_user_can( 'manage_options' ) ) {
    wp_die( 'You do not have sufficient permissions to access this page.' );
  }

  global $plugin_url;
  global $options;

  if( isset( $_POST['wptreehouse_form_submitted'] ) ) {
    $hidden_field = esc_html( $_POST['wptreehouse_form_submitted'] );

    if( $hidden_field == "Y" ) {
      wp_treehouse_username = esc_html( $_POST['wptreehouse_username'] );
      $wptreehouse_profile = $wptreehouse_badges_get_profile( $wptreehouse_username );

      $options['wptreehouse_useranme'] = $wptreehouse_username;
      $options['wptreehouse_profile'] = $wptreehouse_profile;
      $options['last_updated'] = time();

      update_options( 'wptreehouse_badges', $options );
    }
  }

  $options = get_option( 'wptreehouse_badges' );

  if( $options != '' ) {
    $wptreehouse_username = $options['wptreehouse_username'];
    $wptreehouse_profile = $options['wptreehouse_profile'];
  }

  require( 'inc/options-page-wrapper.php' );
}
```


## Parsing JSON with PHP
We've pulled the information from the treehouse site and stored it in our database. We'eve managed to decode that so that the returned JSON is an object containing only the info we need/want (['body']). Now we need to make PHP parse the JSON into something usable.

We're going to go into our included file and create a new box that will show our JSON output as we manuever and manipulate the data.

```
<div class="postbox">
  <div class="inside">
    <pre><code>
      <?php var_dump( $wptreehouse_profile ); ?>
    </code></pre>
  </div>
</div>
```

We can see ALL the profile data being displayed in the backend of wordpress now. So let's try and get the username and display just that.

```
<div class="postbox">
  <div class="inside">
    <p>
      <?php echo $wptreehouse_profile->{'name'}; ?>
    </p>

    <pre><code>
      <?php var_dump( $wptreehouse_profile ); ?>
    </code></pre>
  </div>
</div>
```

OK. That worked. So now let's try pulling in their profile URL.

```
<div class="postbox">
  <div class="inside">
    <p>
      <?php echo $wptreehouse_profile->{'name'}; ?>
    </p>

    <p>
      <?php echo $wptreehouse_profile->{'profile_url'}; ?>
    </p>

    <pre><code>
      <?php var_dump( $wptreehouse_profile ); ?>
    </code></pre>
  </div>
</div>
```

Those are both working so let's try to display some badges now.

```
<div class="postbox">
  <div class="inside">
    <p>
      <?php echo $wptreehouse_profile->{'name'}; ?>
    </p>

    <p>
      <?php echo $wptreehouse_profile->{'profile_url'}; ?>
    </p>

    <p>
      <?php echo $wptreehouse_profile->{'$badges'}[0]->{'name'}; ?>
    </p>

    <pre><code>
      <?php var_dump( $wptreehouse_profile ); ?>
    </code></pre>
  </div>
</div>
```

But this badge is actually given to everyone, so we're going to play around and try to get the second badge and the URL for where ist was obtained.

```
<div class="postbox">
  <div class="inside">
    <p>
      <?php echo $wptreehouse_profile->{'name'}; ?>
    </p>

    <p>
      <?php echo $wptreehouse_profile->{'profile_url'}; ?>
    </p>

    <p>
      <?php echo $wptreehouse_profile->{'badges'}[1]->{'courses'}[1]->{'title'}; ?>
    </p>

    <pre><code>
      <?php var_dump( $wptreehouse_profile ); ?>
    </code></pre>
  </div>
</div>
```

Now let's apply this logic to the loop we have higher up on the page that displays the last 20 badges.

```
<ul class="wptreehouse-badges">
  <?php for ( $i = 0; $i < 20; $i++ ) : ?>
    <li>
      <ul>
        <li>
          <img width="120px" src="<?php echo <?php echo $wptreehouse_profile->{'badges'}[$i]->{'icon_url'}; ?> />
        </li>

        <li class="wptreehouse-badge-name">
          <a href="#"><?php echo $wptreehouse_profile->{'badges'}[$i]->{'name'}; ?></a>
        </li>

        <li class="wptreehouse-project-name">
          <a href="#"><?php echo $wptreehouse_profile->{'badges'}[$i]->{'courses'}[1]->{'title'}; ?></a>
        </li>
      </ul>
    </li>
  <?php enfor; ?>
</ul>
```

Now we want to fill in the links. Unfortunately, some of the badges don't have links associated with them in the JSON, so we'll have to setup a conditional that checks if the link exist and if it does, fill it in as the href attribute. If not, don't make the text a link.

```
<ul class="wptreehouse-badges">
  <?php for ( $i = 0; $i < 20; $i++ ) : ?>
    <li>
      <ul>
        <li>
          <img width="120px" src="<?php echo <?php echo $wptreehouse_profile->{'badges'}[$i]->{'icon_url'}; ?> />
        </li>

        <?php if( $wptreehouse_profile->{'badges'}[$i]->{'url'} != $wptreehouse_profile->{'profile_url'}; ) : ?>
          <li class="wptreehouse-badge-name">
            <a href="<?php echo $wptreehouse_profile->{'badges'}[$i]->{'url'}; ?>"><?php echo $wptreehouse_profile->{'badges'}[$i]->{'name'}; ?></a>
          </li>
          
          <li class="wptreehouse-project-name">
            <a href="<?php echo $wptreehouse_profile->{'badges'}[$i]->{'courses'}[1]->{'url'}; ?>"><?php echo $wptreehouse_profile->{'badges'}[$i]->{'courses'}[1]->{'title'}; ?></a>
          </li>
        <?php else : ?>
          <li class="wptreehouse-badge-name">
            <?php echo $wptreehouse_profile->{'badges'}[$i]->{'name'}; ?>
          </li>
        <?php endif; ?>
      </ul>
    </li>
  <?php enfor; ?>
</ul>
```

Now we want to go back to the sidebar and fill in the username, which serves as an <h> tag and the users gravatar, as well as the correct points and badge counts.

```
<?php if ( isset( $wptreehouse_username ) && $wptreehouse_username != '' ) : ?>
  <div class="postbox">
    <h3><span><?php echo $wptreehouse_profile->{'name'}; ?>'s Profile</span></h3>
    <div class="inside">
      <p><img width="100%" class="wptreehouse-gravatar" src="<?php echo $wptreehouse_profile->{'gravatar_url'}; ?>" /></p>

      <ul> class="wptreehouse-badges-and-points">
        <li>Badges: <strong><?php echo count( $wptreehouse_profile->{'badges'} ); ?></strong></li>
        <li>Points: <strong><?php echo $wptreehouse_profile->{'points'}->{'total'}; ?></strong></li>
      </ul>

      <form name="wptreehouse_iusername_form" method="post" action="">
        <input type="hidden" name="wptreehouse_form_suumitted" value="Y">

        <p>
          <label for="wptreehouse_username">Username</label>
        </p>

        <p>
          <input name="wptreehouse_username" id="wptreehouse_username" type="text" value="<?php echo $wptreehouse_username; ?>">

          <input class="button-primary" type="submit" name="wptreehouse_username_submit" value="Update" />
        </p>
      </form>
    </div>
  </div>
<?php endif; ?>
```


## How to Create Wordpress Widgets
To build our widget we're going to use the register_widget function

In the main plugin page we need to create a new class.

```
// CREATES A NEW CLASS
class Wptreehouse_Badges_Widget extends WP_Widget {
  function wptreehouse_badges_widget() {
    //Instantiate the parent object
    parent::__construct( false, 'Official Treehouse Badges Widgets' );
  }

  // GIVING IT ABILITY TO DISPLAY CONTENT ON FRONT-END
  function widget( $args, $instance ) {
    // Widget output

    extract( $args );
    $title = apply_filters( 'widget_title', $instance['title'] );

    $options = get_option( 'wptreehouse_badges' );
    $wptreehouse_profile = $options['wptreehouse_profile'];

    // Instead of trying to code the front-end markup here, we'll do it in another file and include that below
    require( 'inc/front-end.php' );
  }

  // UPDATE CONTENT USER SAVES - Basically takes the old version of the widget info and replaces it with new version when user saves 
  function update( $new_instance, $old_instance ) {
    // Save widget options

    $instance = $old_instance;

    $instance['title'] = strip_tags($new_instance['title']);

    return $instance;
  }

  // WHAT DO WE WANT WIDGET TO LOOK LIKE ON ADMIN SIDE
  function form( $instance ) {
    // Output admin widget options form

    $title = esc_attr( $instance['title'] );

    // New file where we'll setup the actual HTML markup for how the widget displays in the admin area
    require( 'inc/widget-fields.php' );
  }
}

// FUNCTION TO REGISTER THE WIDGET
function wptreehouse_badges_register_widgets() {
  register_widget( 'Wptreehouse_Badges_Widget' );
}

// HOOK THAT FUNCTION TO WIDGETS_INIT
add_action( widgets_init', 'wptreehouse_badges_register_widgets' );
```

We need to create a two new files in the includes folder called `front-end.php` and `widget-fields.php`

```
<?php
  echo $before_widget;

  echo $before_title . $title . $after_title;

  echo $wptreehouse_profile->{'name'};

  echo $after_widget;
?>
```

```
<p>
  <label>Title</label>
  <input class="widefat" name="<?php echo $this->get_field_name('title); ?> type="text" value="<?php echo $title; ?>" />
</p>
```


## Adding Settings to a Wordpress Widget
When we look at the plugin widget in the widgets area in the wordpress admin you can see we only have one setting, Title.

We're going to add some more options.

First, we'll display a count of how many badges the user has, and then we'll let them input how many they want to display on the fron-front-end of the site.

Finally, we'll include a checkbox asking if they want to display tool tips on the front-end of the site.

Our first task will be to create these new options in the widget-fields.php

```
<p>
  <label>Title</label>
  <input class="widefat" name="<?php echo $this->get_field_name('title); ?> type="text" value="<?php echo $title; ?>" />
</p>

<p>Total Badges
  <?php echo count($wptreehouse_profile->{'badges'}); ?>
</p>

<p>
  <label>How many of your most recent badges would you like to display?</label>
  <input size="4" name="<?php echo $this->get_field_name('num_badges'); ?>" type="text" value="<?php echo $num_badges; ?>" />
</p>

<p>
  <label>Display tooltips?</label>
  <input type="checkbox" name="<?php echo $this->get_field_name('display_tooltips'); ?>" value="1" <?php checked( $display_tooltips, 1 ); ?> />
</p>
```

Now that we've built that area for the widget itself we need to come back to the form function in our new widget class and process those new fields.

```
function form( $instance ) {
  $title = esc_attr( $instance['title'] );
  $num_badges = esc_attr( $instance['num_badges'] );
  $display_tooltips = esc_attr( $instance['display_tooltips'] );

  $options = get_option( 'wptreehouse_badges' );
  $wptreehouse_profile = $options['wptreehouse_profile'];

  require( 'inc/widget-fields.php' );
}
```

We also need to update the Update function in the new widget class.

```
function update( $new_instance, $old_instance ) {
  $instance = $old_instance;

  $instance['title'] = strip_tags($new_instance['title']);
  $instance['num_badges'] = strip_tags($new_instance['num_badges']);
  $instance['display_tooltips'] = strip_tags($new_instance['display_tooltips']);

  return $instance;
}
```

Finally, we also need to update the widget function in the new widget class to display this info on the front-end of the site.

```
function widget( $args, $instance ) {
  // Widget output

  extract( $args );
  $title = apply_filters( 'widget_title', $instance['title'] );
  $num_badges = $instance['num_badges'];
  $display_tooltips = $instance['display_tooltips'];

  $options = get_option( 'wptreehouse_badges' );
  $wptreehouse_profile = $options['wptreehouse_profile'];

  // Instead of trying to code the front-end markup here, we'll do it in another file and include that below
  require( 'inc/front-end.php' );
}
```

Now that we've got the backend completely setup, we need to display the new fields on the front-end of the site. We do this in the `front-endp.php` file. This is going to mimic a lot of the code we used on the settings page of our widgets

```
<?php
  echo $before_widget;

  echo $before_title . $title . $after_title;
?>

<ul class="wptreehouse-badges frontend">
  <?php $total_badges = count( $wptreehouse_profile->{'badges'} ); ?>

  <?php for ( $i = $total_badges - 1; $i >= $total_badges - $num_badges; $i-- ) : ?>
    <li class="wptreehouse-badge">
      <img src="<?php echo $wptreehouse_profile->{'badges'}[1]->{'icon_url'}; ?>" />

      <?php if( $display_tooltips == '1' ) : ?>
        <div class="wptreehouse-badge-info">
          <p class="wptreehouse-badge-name">
          <a href="<?php echo $wptreehouse_profile->{'badges'}[$i]->{'url'}; ?>"><?php echo $wptreehouse_profile->{"badges'}[$i]->{'name'}; ?></a>
          </p>

          <?php if ( $wptreehouse_profile->{'badges'}[$i]->{'courses'}[1]->{'title'} != '' ) : ?>
            <p class="wptreehouse-badges-project"><a href="<?php echo $wptreehouse_profile->{'badges'}[$i]->{'courses']}[1]->{'url'}; ?>"><?php echo $wptreehouse_profile->{'badges"][$i]->{'courses'}[1]->{'title'}; ?></a></p>
          <?php endif; ?>

          <span class="wptreehouse-tooltip bottom"></span>
        </div>
      <?php endif; ?>
    </li>
  <?php endfor; ?>
</ul>

<?php echo $after_widget; ?>
```


## Adding Custom Styles to Plugin Front End
We need to load up a CSS and js file for the front-end, so we're going to change the `wptreehouse_badges_styles` function a bit.

```
function wptreehouse_badges_backend_styles() {
  wp_enqueue_style( 'wptreehouse_badges_backend_css', plugins_url( 'wptreehouse-badges/wptreehouse_-badges.css' );
}
add_action( 'admin_head', 'wptreehouse_badges_backend_styles' );

function wptreehouse_badges_frontend_scripts_and_styles() {
  wp_enqueue_style( 'wptreehouse_badges_frontend_css', plugins_url( 'wptreehouse-badges/wptreehouse_badges.css' );
  wp_enqueue_script( 'wptreehouse_badges_frontend_js', plugins_url( 'wptreehouse-badges/wptreehouse_badges.js', array('jquery'), '', true );
}
add_action( 'wp_enqueue_scripts', 'wptreehouse_badges_frontend_scripts_and_styles' );
```


## How to Create a Wordpress Shortcode
Shortcodes are going to let us display the same badges and tooltips anywhere a content edit field is used, including in pages and posts or custom post types.

[codex.wordpress.org/Shortcode_API](http://codex.wordpress.org/Shortcode_API)

Come into the main plugin file and let's start creating a shortcode.

```
function wptreehouse_badges_shortcode( $atts. $content = null ) {
  global $post;
  extract( shortcode_atts( array(
    'num_badges' => '8',
    'tooltip' => 'on'
  ), $atts ) );

  if( $tooltip == 'on' ) $tooltip = 1;
  if( $tooltip == 'off' ) $tooltip = 0;

  $display_tooltips = $tooltip;

  $options = get_option( 'wptreehouse_badges' );
  $wptreehouse_profile = $options['wptreehouse_profile'];

  require( 'inc/front-end.php' );
}
add_shortcode( 'wptreehouse_badges', 'wptreehouse_badges_shortcode' );
```

   Note that `wptreehouse_badges` is what a user would type in the content edit field to used the shortcode.

Also important to note that using require in this function would dump our shortcode at the top of the post. We need to wait until the shortcode is called in the content AND then call the required file.

We'll use buffering to accomplish this. buffering will hold this info in a sort of temporary storage until we're ready to call on it.

```
function wptreehouse_badges_shortcode( $atts, $content = null ) {
  global $post;
  extract( shortcode_atts( array(
    'num_badges' => '8',
    'tooltip' => 'on'
  ), $atts ) );

  if( $tooltip == 'on' ) $tooltip = 1;
  if( $tooltip == 'off' ) $tooltip = 0;

  $display_tooltips = $tooltip;

  $options = get_option( 'wptreehouse_badges' );
  $wptreehouse_profile = $options['wptreehouse_profile'];

  ob_start();

  require( 'inc/front-end.php' );

  $content = ob_get_clean();

  return $content;
}
add_shortcode( 'wptreehouse_badges', 'wptreehouse_badges_shortcode' );
```


## Adding AJAX to Plugins on the Front-End
Plugin is now fully functional, but there's one problem left. Our badges are only updated when we come into the backend and update the settings page.

We'll want to automate the process of updating the feed. Two ways to accomplish this:
1. From the server side
2. From the front-end

* Server side - when someone lands on a page we would check to see when the feed was last updated, see if it needs to be updated, update it, and pass the updated profile on to the page. All of that takes time, especially if the feed is particularly long. 
* Front-end - when someone visits a page, we load the full page with the most recent profile we have available, fire off an AJAX call to the server to check if the profile feed needs to be updated, if yes update the feed and have it ready the next time the page is loaded. Much faster than server side, but possibility of visitor not seeing the most up-to-date content.

```
function wptreehouse_badges_refresh_profile() {
  $options = get_option( 'wptreehouse_badges' );
  $last_updated = $options['last_updated'];

  $current_time = time();

  $update_difference $current_time - $last_updated;

  if( $update_difference > 286400 ) {
    $wptreehouse_username = $options['wptreehouse_username'];

    $options['wptreehouse_profile'] = wptreehouse_badges_get_profile( $wptreehouse_username );
    $options['last_updated'] = time();

    update_options( 'wptreehouse_badges', $options );
  }

  die();
}
```

Note the `die()` function at the end. This helps AJAX know when the entire function has been completed.

Now we need to take some steps to allow our javascriptto make AJAX calls directly to our plugin file. First step is to create a custom AJAX hook for the our custom refresh function.

Add the following to the last line of the above code:

```
add_action( 'wp_ajax_wptreehouse_badges_refresh_profile', 'wptreehouse_badges_refresh_profile' );
```

Now we need to insert a bit of javascript into the front end of our site using the wp_head hook.

```
function wptreehouse_badges_enable_frontend_ajax() {
?>
  <script>
    var ajaxurl = '<?php echo admin_url('admin-ajax.php'); ?>' ;
  </script>
  <?php
}
add_action( 'wp_head', 'wptreehouse_badges_enable_frontend_ajax' );
```

We have the code setup to call the AJAX necessary to update the feed. we just need the AJAX code itself in the .js file.

```
$.post(ajaxurl, {
  action: 'wptreehouse_badges_refresh_profile'
})
```


****************************************************************************************************
# WooCommerce Theme Development

## Default WooCommerce Template Files
`wp-content/plugins/woocommerce/templates` is where you can find all the default templates exist that woocommerce will use to display products and other related info.


## How to Override a Default Template File
[docs.woothemes.com/document/template-structure](http://docs.woothemes.com/document/template-structure)
1. Go to the WooCommerce templates fold and grab a file that we want to override. 
2. Now back out and create a folder called woocommerce inside of your childtheme. 
3. Paste that file into your folder.
4. Any edits made to this new file will override the default file.


## WooCommerce Template Functions
* [docs.woothemes.com/wc-apidocs/package-WooCommerce.Functions.html](http://docs.woothemes.com/wc-apidocs/package-WooCommerce.Functions.html) - list of all the functions available in the woocommerce templates.
* [docs.woothemes.com/document/conditional-tags](http://docs.woothemes.com/document/conditional-tags) - a list of all the conditional functions available in woocommerce templates
* [docs.woothemes.com/document/useful-functions](http://docs.woothemes.com/document/useful-functions) - useful core functions that might be helpful


## Template Files Updates
Takes a fair amount of work to update your custom files so suggestion is not to wait for a bunch of updates. Instead check and update regularly.


## An Introduction to WooCommerce Template Hooks
* [docs.woothemes.com/document/introduction-to-hooks-actions-and-filters](http://docs.woothemes.com/document/introduction-to-hooks-actions-and-filters) - short explanation of hooks and the two types of hooks
* [docs.woothemes.com/wc-apidocs/hook-docs.html](http://docs.woothemes.com/wc-apidocs/hook-docs.html) - reference list of all action and filter hooks


## The Main Shop Template
`wp-content/plugins/woocommerce/templates/archive-products.php`

`wp/content/plugins/woocommerce/templates/content-product.php`

These two pages control the bulk of a woocommerce listing page.


## Global Template Files
* `woocommerce/templates/global/wrapper-start.php` - executed prior to displaying any products
* `woocommerce/templates/global/wrapper-end.php` - executed after displaying all products
* `woocommerce/templates/global/sidebar.php` - displays a standard sidebar unless ther'es a sidebar-shop.php file
* `woocommerce/templates/global/quantity-input.php` - quantity of products option on the single product pages. unique functionality specific to woocommerce
* `woocommerce/templates/global/form-login.php`
* `woocommerce/templates/global/breadcrumb.php` - controls how the breadcrumbs are displayed and presented


## Loop Template Files
### How are multiple products being listed?
* `woocommerce/templates/loop/loop-start.php` - just an unordered list
* `woocommerce/templates/loop/loop-end.php` - closes the unordered list


## The Single Product Template
### How is a single product displayed?
* `woocommerce/templates/single-product.php` - template file is the skeleton for how a single product is displayed.
* `woocommerce/templates/content-single-product.php` - contains the bulk of the code controlling how single products are displayed

`single-product.php` is a frame that calls a variety of functions and pages, similar to the `archives-product.php` page.
`content-single-product.php` fills in the main section of that frame with actual product details


## Cart Template Files
* `woocommerce/templates/cart/cart.php` - primary wrapper for all of the cart.

cart is really just a form with different buttons that perform different actions


## Order Template Files
Controls how are displayed on payment confirmation as well as when a user logs back into their account to see past orders.

* `woocommere/tempaltes/order/order-details.php` is the primary shell for this info


## Account Template Files
If you allow customers to create accounts they can view past orders and update billing info, etc. Likewise, you can restrict what customers can view and access.

* `woocommerce/templates/myaccount/my-account.php` is the main page for controlling how this info is displayed


## Email Template Files
Send customized emails to your customers.

* `woocommerce/templates/emails`
* `woocommerce/templates/emails/email-styles.php`
* `woocommerce/templates/emails/email-header.php`
* `woocommerce/templates/emails/email-footer.php`

WooCommerce Email Test plugin - allows you to open emails in browser so you can see what your emails look like without having to go through the process


## Miscellaneous Template Files
* `woocommerce/templates/notices`
  * `notice.php`
  * `success.php`
  * `error.php`
* `woocommerce/templates/assets/css/woocommerce.scss`


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