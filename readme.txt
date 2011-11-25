=== Wordpress Logger ===
Tags: log,logging,debug,php,safari,firefox,firebug,firephp,console,development
Requires at least: 2.5
Tested up to: 2.7.1
Stable tag: 0.3

Display log messages during plugin and theme development on the console in Safari and Firefox (with Firebug) browsers.

== Description ==

Display log messages from PHP in the browser console in Safari, Firefox (with firebug), and Opera (with the new Dragonfly debugging environment). Essential debugging tool for 
plugin and theme developers. You no longer have to use 'print_r' statements from PHP to figure out what is going
on in the code, which more often than not, messes up the DOM and HTML layout. Displays complex PHP structures like arrays and objects 
in pretty print.

**Features**

* Log debug messages directly from themes and plugins.
* Display log messages in the browser console, without muddying up the browser display.
* Displays complex structures such as arrays and objects in pretty print.
* Shows the line number and file from where the message was logged ( you won't lose track of log statements ).

For more info, comments, and feature requests, visit [the plugin homepage](http://www.turingtarpit.com/2009/05/wplogger "Wordpress Logger").

== Installation ==


**Installing from the Admin Panel**

1. Select the *Add New* subpanel from the *Plugins* panel.
1. Type in "wordpress-logger" in the search field and click the **Search** button.
1. Identify the "Wordpress Logger" from the plugin list and click on its *install* action.
1. Click on the **Install Now** button in the resulting dialog.
1. Click on the *Activate Plugin* link.

**Installing manually**

1. Verify that you have PHP5, which is required for this plugin.
1. Upload the whole *wordpress-logger* folder into the */wp-content/plugins/* directory.
1. Activate the plugin through the Plugins panel in WordPress.

**Requirements**

* **Make sure that your theme template has a footer ( *index.php* should have a *get_footer()* function call at the end).**
* Turn on the console in your browser:
	* **Firefox:** The [Firebug](http://getfirebug.com/ "Firebug home page") extension needs to be installed and activated. 
	* **Safari:** Show the *Error Console* from the *Debug*/*Develop* menu. See FAQ section for details on how to enable the *Debug* menu.

**Usage**

After activating the plugin, the following PHP function call can log any PHP expression to the console log. 

     `$wplogger->log( php_expression [, message_type] );`


The message_type is optional and can be any one of the following constants:

* WPLOG_ERR
* WPLOG_WARNING
* WPLOG_INFO
* WPLOG_DEBUG

**Examples**

**Logging from template files** - inside the loop to display post IDs.

	`<?php $wplogger->log( 'Post ID: '.$post->ID ); ?>`
	` `
	`Output:`
	` `
	`[Information: from line 20 in file index.php] Post ID: 125`
	`[Information: from line 20 in file index.php] Post ID: 116`
	`[Information: from line 20 in file index.php] Post ID: 65`

**Logging from PHP files (e.g. functions.php)** ( always a good idea to check if $wplogger is available ). Note the message type set to *warning* through the second parameter.

	`if ($wplogger) $wplogger->log( get_option('active_plugins'), WPLOG_WARNING );`
	` `
	`Output:`
	` `
	`[Warning: from line 55 in file functions.php] array (`
	`	  0 => 'wplogger/wplogger.php',`
	`	  1 => '12seconds-widget/12seconds-widget.php',`
	`	  2 => 'get-the-image/get-the-image.php',`
	`)`

**Logging from plugins** - inside a plugin function. Note the global statement to get $wplogger into current scope.

	`global $wplogger; $wplogger->log( 'No images attached to this post', WPLOG_ERR );`
	` `
	`Output:`
	` `
	`[Error: from line 206 in file get-the-image.php] No images attached to this post`
	
== Screenshots ==

1. Console log output in the Firefox Browser with the Firebug extension.
2. Console log output in the Safari Browser.
3. Opera Dragonfly Error Console output in the Opera Browser.

== Frequently Asked Questions ==

= How to enable the *Debug* / *Develop* menu in Safari? =
* On [OSX](http://www.macosxhints.com/article.php?story=20030110063041629). 
* On [Windows](http://robrohan.com/2007/06/11/enable-debug-mode-on-safari-windows-error/).

= How to show the error console in Opera? =
1. Select the *Tools > Advanced > Developer Tools* menu.
1. Click on the *Error Console* tab in the Opera Dragonfly console.

== Credits ==

Code that forces the wplogger plugin to load first was adapted from the WordPress 
[FirePHP plugin](http://inchoo.net/wordpress/wordpress-firephp-plugin/ "FirePHP plugin") 
developed by Ivan Weiller.

This plugin is based on [PEAR Log](http://pear.php.net/package/Log "PEAR Log"), the logging framework that is part of the
PHP PEAR library. Current maintainers Jon Parise, Jan Schneider, and Chuck Hagenbuch. PEAR Log is based on code first
developed for the Horde 1.3 framework - original authors Chuck Hagenbuch, and Jon Parise.

== Release Notes ==

**0.3** : Added support for Opera ;

**0.2.2** : Fixed formatting issues in *readme.txt* file;

**0.2.1** : Added more detail to the *readme.txt* file;

**0.2** : First official public release;

**0.1** : First internal release;