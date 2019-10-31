---
id: 7
title: Venn diagram of items in languages
date: 2011-02-05T20:34:56+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=7
permalink: /2011/02/venn-diagram-of-items-in-languages/
redirect_from:
  - /sitecore/wordpress/2011/02/venn-diagram-of-items-in-languages/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
Ever wanted to get a quick insight into how the language versions of your content are used? No? Me neither. But here&#8217;s some code to get it anyway.

Just copy and paste the following code to an aspx file in your Sitecore installation and you&#8217;re good to go. To make more languages available, just edit the code. The Venn diagram is rendered by the <a title="Google Chart Tools" href="http://code.google.com/apis/chart/">Google Chart Tools</a>.

<img class="alignnone" src="/wp-content/uploads/screenshot_venn_diagram.JPG" alt="" width="602" height="790" />

{% gist 67d5d17a1a1a6b95a9752774210c74c8 %}