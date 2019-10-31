---
id: 170
title: 'Sitecore unit testing with test fixtures &#8211; media library support added'
date: 2012-06-24T22:31:56+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=170
permalink: /2012/06/sitecore-unit-testing-with-test-fixtures-media-library-support-added/
redirect_from:
  - /sitecore/wordpress/2012/06/sitecore-unit-testing-with-test-fixtures-media-library-support-added/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
I recently wrote a post on [Sitecore unit testing with test fixtures]({% post_url 2012-06-10-sitecore-unit-testing-with-test-fixtures %} "Link to post about Sitecore unit testing with test fixtures"). I&#8217;ve now added support for the media library (updated in <a title="The FixtureDataProvider project on GitHub" href="https://github.com/hermanussen/Sitecore-FixtureDataProvider">the project on GitHub</a>).

So now, you can also unit test code that imports an image into the media library.

{% gist 58da78cfab0db2a4e7d91868cb80d06d %}

And here&#8217;s some code to check if it works correctly.

{% gist 570c556e02ab7cbc7ca854ddb23072e6 %}