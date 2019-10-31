---
id: 17
title: The inverse Sitecore tree
date: 2011-02-13T21:57:14+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=17
permalink: /2011/02/the-inverse-sitecore-tree/
redirect_from:
  - /sitecore/wordpress/2011/02/the-inverse-sitecore-tree/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
Oh yes, that&#8217;s right. I&#8217;ve made an inverse Sitecore tree. Despite that it almost certainly will never be of any use to anyone, I&#8217;ve made it.

Why? Well, I just thought it would be fun to do. The items that have no children are displayed in a long list, grouped by their common parents. You can expand them to traverse their ancestors. Here&#8217;s a screenshot:

<img class="alignnone" title="Inverse Sitecore tree" src="/wp-content/uploads/screenshot_inverse_sitecore_tree.JPG" alt="Inverse Sitecore tree" width="158" height="788" /> 

Here&#8217;s the code (just copy it to a file named InverseContentTreeViewer.aspx):