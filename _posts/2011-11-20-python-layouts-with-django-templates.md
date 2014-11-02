---
title: Easy Python Layouts With Django Templates on Google App Engine
author: eliot
layout: post
permalink: /11/20/python-layouts-with-django-templates/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Blog
  - Code
tags:
  - gae
  - google app engine
  - layouts
  - python
---
I&#8217;m working on a Python app and my natural tendency is to create a default layout a la Ruby, CakePHP or many other MVC frameworks. This layout acts as a main wrapper around the rendered view file. It contains the main HTML tags including HTML HEADER and BODY tags. Let&#8217;s call this file layout.html and store it in our main app directory (or within a sub-directory like /views/ would make sense too).

So a simple layout would look like:

We want to reuse that layout for all of our views across the site which is  a little tricky on Google App Engine because the approach in the template examples I&#8217;ve seen all use an approach where single files are merged with template values, rendered and then written out as the response. So when outputting the homepage using a file in the app directory index.html as the view, the recommended approach looks like this: 

The goal though is to always render our view file within our general layout. The above approach would always need the wrapper HTML as given in the first code example above in each view. So index.html would need the main wrapper HTML as well as say if we were rending the view about.html in a separate request handler.

Here&#8217;s a function that will first render the view (e.g. index.html, about.html) with any template values we pass it.

Once this rendered view is returned we can that pass this as the &#8220;view&#8221; value to our general layout.html and output it. So the request handler would like this: 

It would be fun and useful to develop a simplified layout and view rendering class further out to make the syntax even cleaner in the request handler.  Also, items like a page&#8217;s unique title tag could be passed in with the layout_values as well as page specific js and css. Also, this code could easily be adapted for use outside of Google App Engine.