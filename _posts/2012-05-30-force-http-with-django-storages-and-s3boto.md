---
title: Force HTTP With Django Storages and S3Boto
author: eliot
layout: post
permalink: /05/30/force-http-with-django-storages-and-s3boto/
aktt_notify_twitter:
  - no
categories:
  - Code
tags:
  - django
  - heroku
---
A new website I&#8217;ve been working on ([hasthat.com][1]) is built using Django and hosted on Heroku. Because Heroku doesn&#8217;t have persistent file storage, I&#8217;m using [django-storages][2] with the s3boto storage backend to seamlessly use Amazon S3 for the image upload functionality of the site.

When I first put up the site and watched it get indexed by Google, I noticed that these uploaded images weren&#8217;t displayed in the cached previews of pages. Okay, I thought, it&#8217;s probably because Google takes longer to index images with new sites.

A couple weeks passed. Still no images showing in preview. It turns out that Google wasn&#8217;t indexing the images because they were being served through django-storages and s3boto over https. As an  aside, it&#8217;s sort of interesting that Google takes the approach of not indexing secure-served images. Or maybe it&#8217;s just https with S3. Oh well. It&#8217;s also interesting that the s3boto backend defaults to returning secure s3 objects.

But anyway, in order to force s3boto to return s3 objects over http, you need to add this to your settings.py:

<pre>AWS_S3_SECURE_URLS = False</pre>

Almost immediately after making this change, the Google cached previews changed to showing the non-secured images.

Good to go!

 [1]: http://hasthat.com "Store your things on the web"
 [2]: http://django-storages.readthedocs.org/en/latest/index.html