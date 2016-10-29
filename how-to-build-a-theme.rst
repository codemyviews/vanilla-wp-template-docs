=========================
How To Build a WP Theme
=========================

This guide will walk you through the steps of converting your static HTML/CSS files into a custom WordPress theme using the Vanilla WordPress Boilerplate by Code My Views.

This guide assumes you have already followed the setup guide from the documentation link above.

.. todo::
   add sample views to the theme

------------------------------------------
Step 1: Views, Partials and Layouts
------------------------------------------

The first step in any WP theme build is identifying each of the unique HTML views that your theme will have.  For each unique HTML page that you have, you should create a view.

**Views**

To create a view, create a new file in the views directory in your theme.  For example, if your theme has a unique home page template, you can create a file called home.blade.php and place it in the views directory.

Here is what a sample view looks like:

https://github.com/codemyviews/vanilla-wp-boilerplate/blob/master/public/wp-content/themes/base-theme/views/page-sample-custom-page-template.blade.php

**Layouts**

Once you have turned each of the HTML files into a view, you should next look at which HTML pages use the same layout. If all of your views have the same exact header and
footer, you likely can extract all of this into one layout.

Please see the same *master.blade.php* layout here: https://github.com/codemyviews/vanilla-wp-boilerplate/blob/master/public/wp-content/themes/base-theme/layouts/master.blade.php

**Partials**

In cases where your views use similar elements, you can extract these into partials.

Create partials by adding a new file to the partials directory.  Partials can be loaded into any view by using:

::

   @include('partials/name-of-partial')

------------------------------------------
Step 2: Assets
------------------------------------------

At this point, you should have successfully moved over all of your static HTML/CSS into the theme, and then partialed it out into views, partials and layouts.

The next step is to copy over all static assets (JavaScript, CSS, images, font files, etc.).  All of the static assets can be copied over to the assets directory in your theme.  All of the CSS should be compiled down into one file called theme.css.  All of the JavaScript should be compiled down into one files called theme.js.  For more info on how to use Gulp to make this happen, read this: Guide to Gulp.

------------------------------------------
Step 3: Data Model
------------------------------------------

At this point, you should have completely moved over all of the static views and static assets for your site.

The next step is to map out how you will make the content on each view dynamic, and controlled through the WordPress admin panel.

In many cases, the default WordPress data model which contains posts and pages, will work just fine.  If your theme only needs posts and pages, then you can simply turn each of the views you created into a “Custom Page Template” in WordPress, and then assign them to any page you create in WordPress.

In the case where your theme has more data than just posts and pages, for example, if you want a feed of products, you need to create custom post types.

In the theme-config.php file, you can register post types in the **load_custom_post_types()** method.

In the theme-config.php file, you can also register custom taxonomies.

------------------------------------------
Step 4: View Mapping
------------------------------------------

At this point, we should have all views created, and also the entire structure of the data created.

WordPress, by default, depending on which page a user is viewing will load a different file in the theme automatically.  You can see the WordPress template hiearchy here: https://developer.wordpress.org/files/2014/10/template-hierarchy.png


View mapping involves making sure that the views we created get served on the correct page.  For example, when a user is visiting a product detail page, or a single blog post, we want to make sure they see the product detail view, or the single blog post view.

**Product Detail View Example**

View file: views/product.blade.php
WordPress template hierarchy loads: single-product.php

Create single-product.php and contents of this file should be:

::

   @include('views/product')

**Single Blog Post Example**


View file: **views/blog-post.blade.php**

WordPress template hierarchy loads: **single.php**

Create single.php and contents of this file should be:

::

   @include('views/blog-post’)

**Custom Page Template - Contact**

View file: **views/contact.blade.php**
WordPress template hierarchy loads: **$custom.php**

Just be sure to place this at the top of the views/contact.blade.php and WordPress will automatically register your view as a custom page template.

::

   <?php /* Template Name: Contact Page Template */ ?>

------------------------------------------
Step 5: Dummy Content and Menus
------------------------------------------

At this point, you should have all of your views registered and being mapped to the correct WordPress template file.

The next best step is to login to the wp-admin on your local dev environment and create all of the pages, posts, and custom post types (i.e. sample products) that you will need.  This will also allow you to test to make sure that all of the views are loading correctly.

Things to check:

#. Do all of your custom page templates show up as options when creating a new page?
#. When you view your blog post, does it load your blog post view?
#. If you have any custom post types, do their single post pages load the correct view?

Since you are already in wp-admin, it is a good time to also create any of the site menus that are needed on the theme.  You can define the menus in **set_menus()** in the theme-config.php, and then you should also update the HTML code in the views so that it uses **wp_nav_menu()** to load the menu.

------------------------------------------
Step 6: Options Panels
------------------------------------------

If this theme has any global options, we can now create the options panels that are needed.

By  default, all of the themes have a “Header and Footer” Options panel enabled.  If you needed to add additional options panels, you can do so in the **load_options_panel()** method in theme-config.php

------------------------------------------------------------
Step 7: Custom Field Definitions, Sidebars and Shortcodes
------------------------------------------------------------

At this point, you should actually be able to click around your entire site and see all of the views loading, and navigation menus working.  However, all of the views still are serving static content.


The next step is to determine how to make each of the views dynamic so that all of the content is being loaded from the database, via Custom Fields that are created in the theme.


For each of the views, you need to determine the most efficient and user friendly way to output the content from the CMS to the page.

.. todo:: need more info about this.

------------------------------------------
Step 8: Make the views dynamic
------------------------------------------

Now that you have all of the custom fields created, you need to update the views so they are being served from the custom fields.

.. todo:: need more info about this.

---------------------------------------------
Step 9: Endpoints and Advanced Functionality
---------------------------------------------

Create endpoints in the endpoints directory for any advanced functionality.

Examples of advanced functionality:

#. Contact form
#. Advanced search queries
#. Mailing list subscription
#. Payment forms

------------------------------------------
Step 10: Testing, and production ready
------------------------------------------

Checklist:

#. Make sure to export all ACF fields into the field-groups directory (**wp acf export**)
#. Export a copy of your local database and place in project root (**wp db export**)
#. Commit code to project repo