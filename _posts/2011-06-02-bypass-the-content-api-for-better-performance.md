---
id: 74
title: Bypass the content API for better performance
date: 2011-06-02T15:26:06+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=74
permalink: /2011/06/bypass-the-content-api-for-better-performance/
redirect_from:
  - /sitecore/wordpress/2011/06/bypass-the-content-api-for-better-performance/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
The Sitecore content API provides a very easy way of accessing your content. It is highly optimized for performance with internal caching. You can find a great overview of the different query strategies <a title="Options for querying items from Sitecore" href="http://firebreaksice.com/options-for-querying-items-from-sitecore/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://firebreaksice.com']);">here</a>.

But in some specific cases, the API will not provide you with the right tools to get what you want, with the performance that you want. In those cases you have 2 options:

  1. Persist a more suitable representation of your data. E.g.: output caching, Sitecore caching, Lucene indexing.
  2. Strip some overhead, so functionality that is not needed at that point can be skipped. An example will follow.

Both of these methods have their drawbacks, so it is important to evaluate them when choosing a solution. Some drawbacks for the first method:

  1. More storage/memory is needed.
  2. The data representation must be kept consistent with the original data (can result in bugs that are hard to spot if implemented incorrectly).

Drawbacks of the second method:

  1. Relies on the underlying implementation. You may have to change the implementation with future upgrades.
  2. If the stripped functionality turns out to be needed in the future, the implementation may become unsuitable.

**An example of the second method  
** 

If we want to get the descendant nodes of a certain item, we can easily use the content API:



But if we want to limit the descendants to items with a certain template, this is a better method:  


However, in this case, we will not get items with template &#8216;Jpeg&#8217; or &#8216;Pdf&#8217;. Those templates inherit from the &#8216;File&#8217; template. So if we want to get all descendants that inherit from the &#8216;File&#8217; template, we need a helper method:



You could make this into an extension method if you want. Here&#8217;s how we can use this method to get all the descendants that inherit from &#8216;File&#8217;:



This will be quite slow if there are many descendants. We will bypass the content API and query the SQL server database directly to make it much faster.



Place the query in a stored procedure if you want to use this method in production. For reference, <a title="Accessing hierarchical node structures from sql" href="http://bloggingabout.net/blogs/program.x/archive/2008/07/29/sitecore-accessing-hierarchical-node-structures-from-sql.aspx" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://bloggingabout.net']);">here is a different article</a> which discusses bypassing the content API.

**Measuring speed**

In my opinion, any performance improvement (especially if it has significant drawbacks) must be proven to be worth it! So I&#8217;ve measured the speed of this method and a simpler one against the normal Sitecore way of doing things. Here&#8217;s the result:

<img class="alignnone" title="Speed measuring results" src="/wp-content/uploads/bypass_content_api_screenshot.png" alt="" width="519" height="161" /> 

As you can see, the performance gain can be significant. So if the drawbacks are acceptable, this may be a good option. Here is the aspx so you can test it for yourself: