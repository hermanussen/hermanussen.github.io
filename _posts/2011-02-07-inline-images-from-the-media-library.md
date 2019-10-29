---
id: 12
title: Inline images from the media library
date: 2011-02-07T23:13:08+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=12
permalink: /2011/02/inline-images-from-the-media-library/
redirect_from:
  - /sitecore/wordpress/2011/02/inline-images-from-the-media-library/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
I&#8217;m not sure if this has been done before, but I thought it would be fun to code a ASP.NET control based on the sc:Image from Sitecore. I wanted to create an inline image (based on the <a title="Data URI scheme on Wikipedia" href="http://en.wikipedia.org/wiki/Data_URI_scheme">Data URI scheme</a>). This could be useful for improving performance in some cases.

I&#8217;m not really certain that it is even a useful control in its current form. But it should be easy enough to convert this control so that it can be used in a dynamic CSS file. If you seriously want to use this, check out <a title="Inline Images with Data URLs" href="http://www.websiteoptimization.com/speed/tweak/inline-images/">this page</a>.

Here&#8217;s the code:  


And if you want to use it in your page, register the control:  


And you&#8217;ll be able to use it like any Sitecore image (including the MaxWidth and MaxHeight properties):  


Hell yeah!