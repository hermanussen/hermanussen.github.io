---
id: 159
title: T-SQL pocket knife code
date: 2012-06-21T22:24:26+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=159
permalink: /2012/06/t-sql-pocket-knife-code/
redirect_from:
  - /sitecore/wordpress/2012/06/t-sql-pocket-knife-code/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
Sometimes I like to dive into the SQL databases that hold all of our precious Sitecore content and go wild. No really; sometimes the Sitecore tree, XPath builder or search function are just not the easiest tools to research a particular problem. Once you understand the database schema of Sitecore (which is not that difficult), querying the databases directly can be of great help.

Here is a script that creates 2 handy functions that you can use to make querying Sitecore data just a little easier:



After running this script (be sure to change the statement in line 1 to match your database name), you can write queries such as this one:  


This results in:

[<img class="size-full wp-image-160 alignnone" title="Screenshot of the result of the previous query" src="/wp-content/uploads/2012/06/screenshot_query_result.png" alt="Screenshot of the result of the previous query" width="635" height="142" srcset="/wp-content/uploads/2012/06/screenshot_query_result.png 635w, /wp-content/uploads/2012/06/screenshot_query_result-300x67.png 300w" sizes="(max-width: 635px) 100vw, 635px" />](/wp-content/uploads/2012/06/screenshot_query_result.png)

Since the SC_GetPath function uses recursion, make sure your query does not go out of control. SQL Server does <a title="Article about SQL Server recursion limit" href="http://www.sqlservercentral.com/blogs/juggling_with_sql/2011/06/04/maximum-recursion-possible-with-cte-in-sql-server-2005-2008/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://www.sqlservercentral.com']);">not allow too many recursions</a> by default.