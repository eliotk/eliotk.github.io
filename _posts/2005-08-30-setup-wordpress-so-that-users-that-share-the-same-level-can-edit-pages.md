---
title: Setup WordPress so that users that share the same level can edit pages
author: eliot
layout: post
permalink: /08/30/setup-wordpress-so-that-users-that-share-the-same-level-can-edit-pages/
categories:
  - Blog
  - Code
---
I&#8217;m in the midst of modding WordPress to act like a CMS for a site that I&#8217;m building. I wanted users of the same level to be able to edit pages. By changing line 20 in the admin/edit-pages.php file, it worked like a charm.

The original line looked like this:

`AND ($wpdb->users.user_level < = $user_level OR $wpdb->posts.post_author = $user_ID)`

I simply shifed the user_level check to allow page edits on pages that were created by users with levels either less than *or* equal to the active user&#8217;s level. New code looks like this:

`AND ($wpdb->users.user_level < = $user_level OR $wpdb->posts.post_author = $user_ID)`