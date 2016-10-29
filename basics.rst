============
The Basics
============

---------------------
WordPress Core
---------------------

Please note that within this project, we are not only including the Vanilla theme, but also WordPress core in its entirety.  The reason why we include the latest version of WordPress within the project repository itself is because it makes it easier to automate deployments of sites that are built using the Vanilla boilerplate template.  If you wanted to remove WordPress core, and simply install the theme manually into WordPress somewhere else, that would work as well.

With that being said, as a best practice, even though we include WordPress in the project repository, you should never edit or delete any of the core WordPress files that exist in the wp-admin or wp-includes directory.  This is where all of the default WordPress magic exists, and there is no need to edit anything here.  In fact, editing files here may cause issues for you in the future in the event that you update the WordPress version because this will replace all files in `wp-admin` and `wp-includes` directories.  Also, as a general best practice, you should never edit core files in any project.

---------------------
Directory Structure
---------------------

This is the directory structure of the Vanilla theme itself.  The theme directory is in `public/wp-content/themes`, which is where all of your theme coding and customization will happen.

* **assets** - All static assets
   * **compiled** - This directory should largely be untouched by you.  This is where compiled assets end up.  More on this later.
   * **js** - Javascript files
      * **plugins** - All JavaScript plugins your front end uses go here
      * **custom** - All custom JavaScript or jQuery should go here
      * **sass** - Default SASS directory (this can also be a less/ directory if your front end uses less).  You should place all of your SCSS or LESS files in this directory.
      * **images** - Place all of the images from your front end into this directory.
      * **fonts** - If your front end uses any custom fonts, you can place the font files in this directory.
* **core** - This is all of the core theme files.  This is where the magic of the Vanilla theme happens.
* **endpoints** - This is where we place any endpoints that are needed in the theme.  For example, if your theme has a contact form, you will likely create a file in this directory called contact-form.php.
* **field-groups** - This directory contain the code that generates the various Advanced Custom Fields that are needed in the theme
* **views** - All views for the theme
* **forms** - This is an optional directory where you can store any form partials
* **layouts** - Fundamental layouts of the templates
* **partials** - Various includes (Header, Footer, etc.)
* **shortcodes** - If your theme will have any custom shortcodes, you can place the template files for the shortcodes in this directory.
* **sidebars** - For any custom sidebars, you can place them in this directory.
* **views** - This is where all of the different views will go for your theme
* **404.php** - the default 404 template for the Vanilla theme.  This can be customized as you see fit.
* **functions.php** - This file behaves just as a functions.php file would behave in any WordPress theme.  You can place any WP customization code here as needed
* **gulpfile.js** - This file is what we use to compile all of the JavaScript and SASS/LESS from the assets directory into the assets/compiled directory
* **package.json** - This file defines the Node.js packages that are required for the gulpfile to work correctly (more on this later)
* ** screenshot.png** - This is the screenshot that appears on the theme activation page in wp-admin.  Feel free to replace this with any image you want.
* **theme-config.php** - The config file for Vanilla.  This is where the bulk of the configuration will happen for your theme.
* **style.css** - This is the default stylesheet.  You can update the name of the theme, and the author, in this file.

---------------------
What’s Included
---------------------

~~~~~~~~~~~~~~~~~~~~~~~~~
Latest WP Core
~~~~~~~~~~~~~~~~~~~~~~~~~

When you clone from our Github repository, the code will always include the latest stable version of WordPress.

~~~~~~~~~~~~~~~~~~~~~~~~~
Gravity Forms Plugin
~~~~~~~~~~~~~~~~~~~~~~~~~

We always recommend Gravity Forms as the best plugin to use for form submission management and so we include it within the repository.  There are no hard dependencies on Gravity Forms so if you wanted to remove this or replace it with a different contact form plugin, that would be fine.

~~~~~~~~~~~~~~~~~~~~~~~~~~~
Advanced Custom Fields Pro
~~~~~~~~~~~~~~~~~~~~~~~~~~~


We bundle ACF5 directly into the theme itself because it relies on the ACF5 Options Panel functionality and we also use Advanced Custom Fields heavily during WP development.  For the time being, the theme does not work well without ACF5, but on a future release, we may have a version of the theme that does not use ACF5.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Laravel Blade Templating Engine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Blade templating engine, developed for Laravel, has also been included in this theme.

.. todo:: Update link after updating blade version.

Blade makes the front end templates much cleaner and organized, and you can read more documentation about blade here: https://laravel.com/docs/5.2/blade.

--------------------
Theme Config File
--------------------

If you are already a WordPress developer, the power of the Vanilla theme comes with the theme-config.php file where you can quickly define and utilize all of the various WordPress components, all in one place.

I recommend opening up the theme-config.php and reading the comments of the file to see all of the various options/settings there are available: `theme-config.php <https://github.com/codemyviews/vanilla-wp-boilerplate/blob/master/public/wp-content/themes/base-theme/theme-config.php>`_

The following configuration options are currently available:

#. Global theme options
#. Custom post type options
#. Custom taxonomy options
#. Shortcode options
#. Custom sidebar options
#. Theme option panels
#. Theme menu options
#. Media library image options

--------------------
Asset Pipeline
--------------------

For all of your static assets (CSS files, images, custom @font-face fonts, JavaScript code, etc.), we like to use Gulp to manage.  All of these files will exist within the assets directory of the theme, and you can read more about Gulp here: Guide to Gulp.


The Vanilla theme is all driven by the gulpfile.js which is included in the theme.  The output of the gulpfile is a theme.js file and a theme.css file - these are the two files that also outputted automatically into the <head> and footer of each page using the Vanilla boilerplate.
