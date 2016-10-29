=================
Helper Functions
=================

------------------------
Helper::image
------------------------

The **Helper::image()** function helps you output an image that is stored as a custom field.  When we store an image into a custom field, we will always store the attachment_id associated with the image.  By passing that ID to the Helper::image, in addition to your expected image size, you can automatically generate the <img> tag.

For example, this:

::

   {{ Helper::image(get_field('profile_image'), 'attorney', array('class' => 'pull-left')) }}

Would generate this:

::

   <img src="http://path-to-image/size/profile-image.jpg" alt="Image Alt Text" title="Image Title Text" class="pull-left" />

------------------------
asset()
------------------------

The asset helper function allows you to easily return an absolute URL to a file in the assets directory of the theme.  For example, if you want to get the URL to a image in the assets/images directory, you can use the function like so:

::

   <img src="{{ asset('images/image-name.png') }}" />
