==============
Overview
==============

This documentation was created to accompany the `Vanilla WordPress Boilerplate <https://github.com/codemyviews/vanilla-wp-boilerplate>`_  by `Code My Views <https://codemyviews.com>`_.

---------------------
Motivation
---------------------

The purpose of the Vanilla boilerplate is to simplify the process of taking static HTML/CSS and templating it out into a custom WordPress theme.

The end goal in building a custom WordPress theme is to make it as easy as possible for the end user to update the content of their site.

The input into this process is static HTML/CSS.  The expected output is a very easy to use WP theme using the various components you have available to you below.

When you are building out a WP theme, it is important to think of the end user experience.  How can you setup the theme so it is as easy and foolproof as possible for the end user.

---------------------
Pre-Requisites
---------------------

Before you can really benefit from this starter theme, you should have an already completed front end (HTML/CSS/JavaScript) of the site you are building.  This starter theme will simplify the process of taking the static HTML/CSS/JavaScript that you have created, and then integrating it into WordPress so that all of the content and pages are controlled via the WordPress CMS.

.. _installation:

-------------------------------------------
Installation
-------------------------------------------

If you do not already have a local development environment setup, you will need to do that.  Depending on whether you use Mac, Linux, or Windows for you local environment, we have a few guides.

.. todo::
   add installation guides for unix systems

* Mac / Linux Dev Environment Setup (tbd)
* :ref:`windows-env-guide`

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 1: Clone the repository from Github
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   git clone git@github.com:codemyviews/vanilla-wp-boilerplate.git ~/Code/sample-project.dev

During this step, we also recommend renaming the theme folder to the name of your theme.  By default, the theme folder is called *base-theme*, but you can name this whatever you want.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 2: Composer Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you do not already have Composer installed on your computer, you will need to download and install it here: https://getcomposer.org .

Once you have Composer installed on your machine, you will need to open your Terminal (or `Git Bash <https://git-scm.com/downloads>`_ if you are on Windows) and then move to the root of the project directory and install the composer dependencies.

::

   cd ~/Code/sample-project.dev
   composer install

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 3: Create .env file in project root
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Within the project root that you cloned from Github, you will see a file called *.env.example*.  Create a copy of this file and call it: *.env*

Within the *.env* file, update the values to match the values of your local dev environment.

Here is a sample .env file:
::

   WP_DEBUG=false

   THEME_NAME=wordpress-starter-template
   DB_NAME=sample-project
   DB_USER=homestead
   DB_PASSWORD=secret
   DB_HOST=192.168.35.40

   WP_HOME=http://sample-project.dev
   WP_SITEURL=http://sample-project.dev

   AUTH_KEY='I[z(B/7@SfM+/0jc-69g&s,?&;ZGi-f{vvuJSh=7!>MkUF|6|LddV?i[W(#5-(L?'
   SECURE_AUTH_KEY='-qP,OJsa 9MIu(I1T4$f{c+y$GEZq<NF84X/~HL{{D5Gw#3GyO DW#84|.pO#^#.'
   LOGGED_IN_KEY=''}vl}r-A|72AI,#Z|0&#pNxC3Fu -)b|HA!zM1TLx4!]sCAW_BYp@#`E;hEm8uluV'
   NONCE_KEY='J[HDf&`lIE X]QQ;f<A(DMQx^>a+uCG-J4OTUOK!OH0==P9h@k?6FnS$P)2h~=f@'
   AUTH_SALT='T$wP9:j,X1.]IyWqI+R`>XqjL(KLSJS67cdgg7g`B{QsL~Vg{Gt*6ymI;Tb3:R|@'
   SECURE_AUTH_SALT=';c,xJR?f$Si_z$ Hm|dZvrS/_mC<wqoNjpm8 ARRU3sfDS1X!+6$>bAk0ZU7~e{,'
   LOGGED_IN_SALT='>*Bh2A&|v#ICPE-ARoVRrM-k+/;!b.8V?N%:u#fIozlBKM9B(^mn|ha?-+aZNlL['
   NONCE_SALT='LRWOV$5U90_Thc,SPc8&!_-F-:-caR2sV;R$~qbu#9J[Tl{nu4#$6Mi=gDw FQic'

   TABLE_PREFIX=wp_

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 4: Create local MySQL database
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You need to create a new MySQL database in your local dev environment. The name of the database should match the value of DB_NAME from the *.env* file you created in the previous step.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 5: Serve site in local dev environment and view site
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As a final step, you will need to ensure that you setup the site to be served within your local dev environment.  Please follow the instructions in your local dev environment setup guide if you have questions about this.  The important detail to note here is that the public path for the Vanilla boilerplate theme is this:

::

   ~/Code/sample-project.dev/public

Once you have the site setup to run locally, you will be able to visit the site in your browser at whatever domain you setup for serving.  For example, http://sample-project.dev .

As a last step, you should visit the URL http://sample-project.dev/wp-admin in your browser to finish the installation.

When you finish this step, you should be able to login to your wp-admin area, and then activate the boilerplate theme.
