.. _windows-env-guide:

===================================================
Appendix A: Windows Local Dev Environment Guide
===================================================

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 1: Download all of the packages here:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

https://github.com/codemyviews/windows-dev-environment-packages

You should install the applications in the following order:

#. Wamp Server - a standard installation is ok;
#. Libraries required by WAMP
   #. Vcredist_arm.exe
   #. Vcredist_x86.exe
#. Git - should be straight forward. This will also install git bash, which is a better terminal client to use;
#. Composer - see instructions `here <http://codezag.com/how-to-install-composer-wamp/>`_
#. Sublime Text - is not required if you use a different IDE

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 2: Restart Machine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you have WAMP completely installed, you should restart your computer.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 3: Start Wamp Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You will need to start the WAMP Server.  If you do not create a desktop shortcut for WAMP Server during installation, then you can go into your start menu and search for “START WAMP SERVER”

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 4: Install Apache Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you start WAMP, you should see the WAMP icon in the bottom right tray.  Right click on this icon, and then go to Apache, and click “Install Apache Service”

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 5: Install Apache Modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Within the Apache menu, click on “Apache Modules” and make sure the following modules are enabled:

* ssl_module
* Rewrite_module

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 6: Enabled PHP Extensions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Within the PHP menu in WAMP< click on “PHP Extensions” and make sure the following php extensions are enabled:

* php_openssl
* Php_curl
* Php_sockets

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 7: Edit Apache Config File
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Open this file in a text editor: *C:\wamp\bin\Apache#.#.#\conf\httpd.conf*

Find this line: *LoadModule vhost_alias_module modules/mod_vhost_alias.so* and make sure it is uncommented.

Find this line: *Include conf/extra/httpd-vhosts.conf* And make sure it is uncommented

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 8: Restart WAMP Services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Click the restart wamp services button in WAMP

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 9: Put WAMP Online
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Click the “Put WAMP Online” button in WAMP

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 10: Is it working?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For good measure, you should restart

You should be able to visit: http://localhost in your browser now.

If you see the WAMP page when you visit http://localhost, then WAMP has been installed.

.. note::
   Database management is straightforward with phpmyadmin.
   Visit http://localhost/phpmyadmin

   The default password for mysql is:
   ::

      username: root
      password:

   The password is empty.

.. note::
If you are taking over an existing project, there should be a backup of the latest database included in the project root.  You should import this via phpmyadmin to get all of the content and data loaded into your local dev environment.

-------------------------------------------------
Step 11: Installing a new site
-------------------------------------------------

This is a quick guide on how to install a new site on your local WAMP development environment.

This guide assumes that you install all of your code projects into a Code directory into the c:/wamp/www/ directory.

For example, if you have a project called “sample-project”, you would have the code installed into: c:/wamp/www/sample-project

The goal is to setup your local dev environment so that you can visit a url in your browser, for example: http://sample-project.dev, and have the local code display.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 12: Edit your host file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Open up this file in your text editor (eg Sublime Text): *c:\WINDOWS\system32\drivers\etc\hosts*

At the bottom of the hosts file, add the following line:

::

   127.0.0.1 sample-project.dev

.. note::
   You will need to right click on Sublime Text and click “Run as Administrator”.  If you do not do this, you will not be able to save the hosts file.  This file requires admin privileges to save.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 13: Add the vhost configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Open up this file in your text editor: *C:\wamp\bin\Apache#.#.#\conf\extra\httpd-vhosts.conf*

At the bottom of this file, add the following:

::

   <VirtualHost *:80>
       ServerAdmin dummy@testhost.example.com
       DocumentRoot "c:/wamp/www/sample-project/public"
       ServerName sample-project.dev
       ErrorLog "logs/sample-project.dev-error.log"
       CustomLog "logs/sample-project.dev-access.log" common
       <Directory "/">
           Deny from all Allow from 127.0.0.1
       </Directory>
   </VirtualHost>

.. note::
   You should update the DocumentRoot to whatever the root is of the project you are installing.  Most of the projects at Code My Views will have a public directory in them which is one level up from the project root.

   The ServerName must match the domain you added to your hosts file in the previous step.

   Restart WAMP after you save this file.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step 14: Does it work?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You should be able to visit http://sample-project.dev in your browser and see the project.

If you do not see the site loading, make sure you restarted WAMP.

Next steps can be found here - :ref:`installation`
