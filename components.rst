.. todo:: update code samples to blade

===================
Theme Components
===================

In this section, you will learn about the key components that make up the Vanilla WordPress theme.  It is critical that you understand each of these terms as it will help you correctly model your static front end site into a completely dynamic WordPress theme.

**Goal**

The end goal in building a custom WordPress theme is to make it as easy as possible for the end user to update the content of their site.

The input into this process is static HTML/CSS.  The expected output is a very easy to use WP theme using the various components you have available to you below.

When you are building out a WP theme, it is important to think of the end user experience.  How can you setup the theme so it is as easy and foolproof as possible for the end user.

--------------------------
Templates
--------------------------

The Vanilla theme uses the Laravel Blade template engine to power the theme files.  For more details on Blade, you can read the documentation here: https://laravel.com/docs/5.1/blade

Blade makes it much easier and faster to template out your static front end into the Vanilla WordPress theme by providing a much cleaner and fluid syntax.

Templates are broken out into three different sections:

#. Layouts
#. Views
#. Partials

~~~~~~~~~~~~~~~~~~~~~~~~~
Layouts
~~~~~~~~~~~~~~~~~~~~~~~~~

Take a look at your HTML files from your front end.  Chances are that many of them share common elements.  For example, it is likely that each of your pages uses the same header and same footer.  We will use layouts to allow for the various pages on your site that share a similar layout.  The layout files will go in the `layouts` directory in the theme.  In most cases, your theme will only require one layout, but there is no reason why your theme could not have multiple layouts.  For reference, here is the default layout that we use in the theme:

::

   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1">
       <title>{{ wp_title('') }}</title>


       @yield('head')

       {{ wp_head() }}


       <!--[if lt IE 9]>
       <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
       <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
       <![endif]-->
   </head>
   <body>


   @yield('content')


   {{ wp_footer() }}
   </body>
   </html>

~~~~~~~~~~~~~~~~~~~~~~~~~
Views
~~~~~~~~~~~~~~~~~~~~~~~~~

If you are unfamiliar with the MVC (Model View Controller) pattern, then you likely have not heard the word View before.  Views are an easy concept to grasp.  Views represent what the user of your site actually see.  For example, your theme will likely have a home page, an about page, a contact page, etc.  Each of these pages will use a unique template, and each of these unique templates is what we call a "View".  For each of your static HTML files that you have in your front end, we will turn them into a reusable "view" that will be placed into the views directory in the Vanilla theme.  Our goal is to convert each of the static HTML files you have into a completely dynamic view, that can then be re-used throughout the theme.


It is important to think of every single unique page on your site.  For example, if you also have a custom 404 page, this is another view that will exist in your theme, and thus, we will create another View file for it in the theme.  Other examples of common Views in your theme:

#. Blog index page (a feed of blog posts)
#. Blog single page (a single blog post)
#. Blog category page (a feed of blog posts from a specific category)
#. Search results page
#. Product page

The most important concept to remember is that we are creating these views so that they are reusable and completely dynamic.  For example, if you have a Product view, it may be re-used to show several different products on the site.

~~~~~~~~~~~~~~~~~~~~~~~~~
Partials
~~~~~~~~~~~~~~~~~~~~~~~~~

In the name of DRY (Don't Repeat Yourself), we place any front end code that is used across more than 1 view into a specific partial.  For example, if both your "Home Page" view and your "Product" view has a newsletter HTML on it, we can copy the code for the newsletter, place it into a partial, and then load the partial in both of the views using:

::

   @include('partials/name-of-partial')

Any time you find two views using the same block of HTML, you should partial it out into a file in the `partials` directory.  Never have the same code in two different places.

--------------------------
Posts
--------------------------

Posts are enabled by default in every WordPress theme.  Posts are meant to store a feed of blog posts within the CMS.  In order to use posts within this theme, you will need a front end HTML view to display the posts.

Posts, by default, also have categories enabled which allow you to group certain posts together.

Posts, by default, also have tags enabled.  Tags are similar to categories.  The only difference are that tags are not hierarchical so a tag cannot be a child of another tag, whereas categories can have parent and children categories.

--------------------------
Pages
--------------------------

Pages are also enabled by default in every WordPress theme.  From an architecture standpoint, Pages and Posts are almost identical to each other within the WordPress framework.  The only differences between pages and posts is that (1) pages are hierarchical, so a page can have a parent page and many children pages and (2) pages do not have category or tags associated with them (although you certainly can enable this behavior if you wanted to).


A unique feature to pages is that you can also create Custom Page Templates, and then assign the custom page templates to specific pages on your site.  For example, you may have an About Us page, and you have a custom about page you want to use.  You can simply create a new file in the “views” directory called “about.blade.php”, and use the below as a template:

::

   @layout('layouts/master')
   <?php /* Template Name: About Page Template */ ?>

   @section('content')
   <?php while ( have_posts() ) : the_post(); ?>
       <!-- your html goes here -->
   <?php endwhile ?>
   @endsection

--------------------------
Custom Post Types
--------------------------

Post Types refer to the data of your WP theme.  Both “Posts” and “Pages” that we just covered, are “post types” within WordPress that are enabled by default.

WordPress gives you the ability to create more post types if your theme requires it.

In many cases, your theme will not require you to create any additional post types, and the **post** and **page** post types will fulfill all the needs of your theme.

However, let's assume that the site you are building has other data types.  For example, maybe your site has client testimonials that are displayed in various parts of the site.  Or, if you are building a portfolio on your site, you will have many different portfolio items.  Finally, if you are selling something on your site, you may have a list of products.  In each of those cases, you will need to create a Custom Post Type (CPT) so that you will be able to easily store this data in your theme.

Within the theme-config.php, it is easy to add an additional post type within the **load_custom_post_types()** method.

--------------------------
Taxonomies
--------------------------

Taxonomies can be used to sort and filter your post types.  By default, WordPress includes the following taxonomies:

#. Categories - categories, by default, only exist on the "Posts" post type.  Categories allow you to group many posts together.
#. Tags - tags, by default, also only exists on the "Posts" post type.  Tags also allow you to group many posts together.

The main difference between categories and tags is that categories are hierarchical and tags are not.  This means that categories can have parent and children categories, whereas tags cannot.

In the Post Types section, we explained how you can create "Custom Post Types".  We can also create "Custom Taxonomies" and assign them to the Post Types in the theme which us allows us to filter the posts.  For example, if we have a Products CPT, we may want to be able to filter these Products by their color.  We can create a Custom Taxonomy called "Color" and then assign it to the Products CPT.  This would allow us to then add Colors, and assign them to the products.

Within the theme-config.php, you can create custom taxonomies and assign them to post types within the **load_custom_taxonomies()** method.

--------------------------
Menus
--------------------------

Your theme likely has a navigation menu (or two menus, or many).  For example, you may have a menu in the header, and also a menu in the footer.  Menus in WordPress allow you to dynamically control which pages are outputted into the menus.

Within the theme-config.php, you can create and define menus within the **set_menus()** method.

--------------------------
Options panels
--------------------------

Within the Vanilla theme, you can create custom Options Panels that will then appear in wp-admin.  You can assign ACF field groups to these option panels.  The purpose of the Options Panels is to give the theme some Global configuration options.  For example, perhaps you want the user to be able to update the logo on the site.  You can create an Options panel called "Header Options", and then create a field group on this Options panel called "Header Logo".  The user will then be able to update the logo dynamically in wp-admin.

Within the theme-config.php, you can create custom options panels within the **load_options_panel()** method.

--------------------------
Custom Fields
--------------------------

Every custom page template, post type, options panel, custom taxonomy may have additional data associated with it.  For example, on your product posts, you will want to be able to store the color of your product, pricing information, and customer reviews.  Or, on your about us custom page template, you may want to store a group of client testimonials.

For each area on the site where we have custom data to be stored, we will create an Advanced Custom Fields field group, and then create fields that will allow the user to easily update the content on that specific page, post, options panel, or taxonomy.

--------------------------
Media Library
--------------------------

The Media Library is a powerful tool included by default within the WordPress core.  Whenever you upload an image to WordPress through wp-admin, it is using the WordPress media library, and a copy of the image is stored in the Media Library in the theme.

One of the great features of the Media Library is that it can also automatically crop each image that is uploaded to a specific group of sizes.

Your theme likely has many images that exist in various parts of the site.  For example, if you have products on your site, each product might have an image.  You will create a ACF field group that allows the user to upload and change the image that is associated with the product.  In an ideal world, the user would upload the perfect sized image of the product so that it displays properly on the site.  But often times, a user will upload an image that is too big, or not the right size.  By defining Image Sizes in your theme, WordPress will automatically crop the image so that it is the perfect size.

Within the Vanilla theme, you can define these image sizes in the theme-config.php - just look in the **set_image_sizes()** method.

--------------------------
WYSIWYG Editor
--------------------------

The "What You See Is What You Get" (WYSIWYG) editor is built into WordPress by default.  This allows the user to update the content section on the page or post.

An important rule of thumb here is to never place blocks of HTML directly into the WYSIWYG editor.  For example, on the home page, your HTML for the testimonial section may look like this:

::

   <div class="testimonial-item">
       <h3>Testimonial</h3>
       <blockquote>
           <p>Here is my testimonial</p>
           <cite>- James Jiggins, CEO CMV</cite>
       </blockquote>
   </div>

Often times, you will be tempted to simply copy and paste this HTML block directly into the WYSIWYG on your home page in wp-admin.  This is something we never recommend, and instead, you should create a ACF field group that allows the user to fill out the content for the Testimonial, and then you should dynamically generate the HTML in the View.

So what is the WYSIWYG editor used for?  On many views, we entirely disable the WYSIWYG editor, and instead only have ACF field groups on the page.  However, on pages where there are long blocks of long-form content (for example, a blog post) the user will be able to edit the content there, and add h1 --> h6 tags and other basic content styles to the post.

--------------------------
Sidebars
--------------------------

To define a new custom sidebar widget area, please see the **load_sidebars()** method in the theme-config.php file.

--------------------------
Shortcodes
--------------------------

In the case where you want users to be able to add more dynamic content to a WYSIWYG, we use Shortcodes.  Shortcodes allow the user to automatically generate HTML into a WYSIWYG box.  For example, we have a testimonial shortcode that looks like this:

::

   [testimonial text="Here is my testimonial" by="James Jiggins, CEO CMV"]

We would then have a file in the `shortcodes` directory in the theme, and when the user places the shortcode into the WYSWIYG box, when the user views the page on the front end, the template for the shortcode would be outputted.

To define a new shortcode, please see the **load_shortcodes()** method in the theme-config.php file.

-------------------------
Endpoints
-------------------------

If your theme needs any advanced functionality on the front end, other than simply outputting content from the CMS, than you can create an endpoint.  For example, if you have a contact form on your contact us page template, you will need to setup a contact form endpoint that your form on the front end can POST to.

Please see the contact-form.php file in the endpoints directory for a sample endpoint.

In addition, please see the contact-form.blade.php in the forms directory for a sample form that submits to the created endpoint.

The main idea behind endpoints is that for all forms within the theme, we make POST requests to the admin-ajax.php file within WordPress core.  Within our POST request, we can include any custom POST data that we want, as long as we also pass in an additional parameter called “action”.  The “action” POST value should be equal to the “action” param that is setup in your endpoint file in the endpoints directory  (the $action_param value at the top of endpoints/contact-form.php).

--------------------------
The Loop
--------------------------

The loop is an important concept to grasp that exists within all WordPress installations.

Default WordPress loop code looks like this:

::

   <?php if ( have_posts() ) :
      <? while ( have_posts() ) : the_post(); ?>
         <! -- post data here -->
      <?php endwhile; ?>
   <?php else: ?>

   <!-- no posts found -->

   <?php endif; ?>

The WordPress loop will try to determine which post data it should output based off of what page you are currently viewing on the site.

For example, if you are currently on a “http://sitename.dev/about”, and you have a page created on the site called “About”, the WordPress loop will simply contain all of the data it knows about the single “page” called About.

However, if you are viewing “http://sitename.dev/blog”, and you have a page created called “Blog”, and that page is defined as your “blog feed” page in wp-admin options, then the WordPress loop will instead loop through all of your blog posts .

The WordPress loop is a bit confusing, and is better to just play around with it in your local dev environment to get familiar with it.

This document also will be quite helpful once you get more into advanced WordPress development: https://developer.wordpress.org/files/2014/10/template-hierarchy.png

--------------------------
WP_Query
--------------------------

If you wanted to completely ignore the WordPress loop, and not include it anywhere in your theme, you could easily do that, and instead simply use WP_Query.

WP_Query is a powerful class that will give you access to all of the data that is stored in your theme.  Any data associated with any posts, pages, or custom post types you created can easily be queried, paginated, and returned using the `WP_Query class <https://codex.wordpress.org/Class_Reference/WP_Query>`_.

As a code sample, let’s assume we wanted to return the past 15 testimonial posts from our site.

Let’s also assume that on our site, we sort our testimonials by “Year Received”, and thus, we have a custom taxonomy for the testimonials called “testimonial year”.

In my query, I only want to return the testimonial posts that are from 2015.  Here is the code:

::

   <?php
       $options = array(
           'post_type' => 'testimonial',
           'orderby' => 'date',
           'posts_per_page' => 15,
           'tax_query' => array(
               array(
                   'taxonomy' => 'testimonial-year',
                   'field' => 'name',
                   'terms' => array('2015')
               )
           )
       );


       $testimonials = new WP_Query( $options );
       while( $testimonials->have_posts() ) : $testimonials->the_post();
   ?>


   <!-- include the partial that have the HTML/CSS for the testimonial.


   @include('partials/testimonial')


   <?php
       endwhile;
       wp_reset_postdata();
   ?>

