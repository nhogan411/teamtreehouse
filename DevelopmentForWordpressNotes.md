# Local Wordpress Development

## Installing a Local Web Server on a Mac

[mamp.info](http://mamp.info/) - click to download MAMP

Install MAMP

Applications > MAMP Folder > MAMP

To get MAMP up and running click Start Servers

   This starts both Apache and MySQL

   Should also open MAMP start page in browser

If we remove MAMP from URL we can get to the root directory of the server

This file is actually in the MAMP Folder > htdocs folder

Customizing Your Local Server Setup on a Mac
Remove the :8888 from the URL
To do this, open MAMP > Preferences > Ports > "Set to default Apache and MySQL ports" > OK
This sets the local host to default :80, which means you don't have to have the port in the URL at all.
localhost/SITENAME will work
2. Change folder location of where we store files
Common to create a Sites folder in their home directory
Open MAMP > Preferences > Apache > Select new location

Installing a Local Web Server on a PC
XAMPP > XAMPP for Windows > Download the latest version
Use Installer version
Run Installer
Uncheck BitNami
After finish XAMPP will open automatically.
Start Apache and MySQL services
localhost/xampp/splash.php default 
Files are stored in C drive > XAMPP folder > htdocs folder 

Installing Wordpress Locally
Go to wordpress.org and download wordpress
Create a new folder in the Sites folder called localwp.com
Don't install directly into Sites folder because it becomes difficult to deal with multiple installs
Copy all the files from the downloaded wordpress install into the localwp.com folder.
Open MAMP control panel > Open Start Page > PHPMyAdmin
Databases > Create new database called localwp
Users > Create new user: wpuser
Set host: localhost
Check All for global access to database
localhost/localwp.com to proceed to installation script
Create a Config file
Enter DB info
Submit
Run Install
Enter Site and WP User details
Uncheck Privacy
Install Wordpress
Log In
Important to note that MAMP Servers need to be on to run Wordpress locally

Migrating Wordpress from Local to Live Server
FTP into site and drag ALL items from localwp.com folder into the public_html folder on the server
Log into cpanel and create a new MySQL database.
Use name localwp for DB name
Use wpuser as the username
Use same password as the local install
Make sure user has all privleges
Note the final username and database name because we'll need this for the config file
Go back to MAMP and open start page.
Go to PHPMyAdmin > localwp database > Export tab
Custom Export
Everything selected
Save as output file to text
Database is successfully backed up
Go back to cpanel and open PHPMyAdmin
Click into new database that we created > Import new file from our local development that we just exported
Database info is now on live server
Go back to FTP and find wp_config.php > Open and Edit
Still has all DB info from local site
Update with info from live site
DB_Collate tells WP to find site somewhere else
define('WP_HOME', 'http://liveurlthatyoubought.com');
define('WP_SITEURL', 'http://liveurlthatyoubought.com');
Make sure you have the 'http://'
All setup but should probably use a plugin to Find & Replace all links that might still be pointing at localhost. This can effect images too.
Install and active Search and Replace plugin
Go to Search and Replace plugin
Enter Search URL from local site
http://localhost/localwp.com
 Enter Replace URL for new site
http://liveurlthatyoubought.com
Good idea to run process in reverse if you're going to start developing locally again.




****************************************************************************************************
# Build a Website with Wordpress


****************************************************************************************************
# PHP for Wordpress


****************************************************************************************************
# Wordpress Theme Development


****************************************************************************************************
# The Wordpress Template Hierarchy


****************************************************************************************************
# Wordpress Hooks - Actions and Filters


****************************************************************************************************
# Wordpress Customizer API


****************************************************************************************************
# Customizing the Wordpress Admin Area


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