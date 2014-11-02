---
title: 'Changing the Upload Directory in WordPress 2.0 &#8211; Duke'
author: eliot
layout: post
permalink: /01/01/changing-the-upload-directory-in-wordpress-20-duke/
categories:
  - Blog
  - Wordpress
---
I was googling around looking for info about changing the default image upload directory as well as the reason why the WordPress developers removed this once inherit feature. I didn&#8217;t find much.

I just hacked the config file (wp-config.php) to define the uploads directory by adding this line of code:

`define('UPLOADS','images');`

Th admin function that executes the upload looks for this definition at line 840 of the wp-includes/functions-post.php file.

You can insert whatever directory you&#8217;d like to use for images in place of &#8216;images&#8217; in the code above starting of course from the root directory where WordPress is displayed.

I also stumbled upon [this plugin][1] that restores the WordPress 1.5+ upload options in the admin area:

Seems like it would have been beneficial to keep those options in tact since many many WP users are going to be upgrading. I&#8217;m sure that in a good number of cases, users will have setup a different images directory because of the use of WYSIWYG plugins or otherwise.

I&#8217;m definately loving the ability to resize the editing box, though.

 [1]: http://www.ilfilosofo.com/blog/old-style-upload/