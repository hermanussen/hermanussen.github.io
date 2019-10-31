---
id: 257
title: 'Monitor your Sitecore server&#8217;s health'
date: 2015-10-03T17:51:12+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=257
permalink: /2015/10/monitor-your-sitecore-servers-health/
redirect_from:
  - /sitecore/wordpress/2015/10/monitor-your-sitecore-servers-health/
aktt_notify_twitter:
  - 'no'
categories:
  - code snippets
---
Having a website up and running reliably requires that you monitor its health. You should always be using a monitoring tool like Pingdom (there are many others). That way, you can get notified when the website is down.

Now, there are several ways of making sure that things are ok at runtime. For example:

  * <a title="Sitecore's HeartBeat.aspx for Load Balancer Health Checks " href="https://www.paragon-inc.com/resources/blogs-posts/sitecores_heartbeat_page_for_load_balancer_health_checks">Sitecore&#8217;s HeartBeat.aspx for Load Balancer Health Checks</a> &#8211; Standard page in Sitecore that does some limited checks. It&#8217;s a good idea to monitor this page.
  * <a title="Sitecore Diagnostics Toolset" href="https://marketplace.sitecore.net/en/Modules/S/Sitecore_Diagnostics_Toolset.aspx">Sitecore Diagnostics Toolset</a> &#8211; A desktop application that does various checks to see if your Sitecore implementation is correctly working, with regard to things like security, indexing, performance and scalability. It&#8217;s a smart idea to use this tool periodically, but it won&#8217;t be helpful for monitoring purposes.

Personally, I like to monitor more than just if a website is up. I also want to know if key parts of the system are functioning properly, like connections to other systems, if certain content is available and if my indexes are ok. These checks may be very specific to my implementation.

That&#8217;s why I created a simple drop-in .aspx script that you can easily configure to check these things. You can find it in <a title="Gist of SitecoreChecks.aspx" href="https://gist.github.com/hermanussen/9d4ea1b77602e02609cc" target="_blank">this Gist on Github</a>. Example output:

[<img class="aligncenter size-full wp-image-263" title="success" src="/wp-content/uploads/2015/10/success1.png" alt="" width="574" height="622" srcset="/wp-content/uploads/2015/10/success1.png 574w, /wp-content/uploads/2015/10/success1-276x300.png 276w" sizes="(max-width: 574px) 100vw, 574px" />](/wp-content/uploads/2015/10/success1.png)

It&#8217;s quite easy to configure and extend. Just read through the implementation of the Page_Load(&#8230;) method. Some more details here:

**Security**

You&#8217;ll want to limit who gets to use the monitoring page, to prevent abuse and prevent hackers from getting details about your implementation. This is especially important if the checks you are doing may impact system performance significantly. Make sure your monitoring tool&#8217;s requests to the page match your security settings here.



&nbsp;

**Adding checks**

You can add checks to do when the page is requested by adding them to the ChecksRun collection. Some examples are in the code below. They include checking specific items&#8217; presence in databases and having versions and layout/presentation. They also include checking if search indexes contain enough items, if certain url&#8217;s are reachable from the server and if configuration is specified correctly.

It&#8217;s also easy to implement your own specific types of checks. Add them to the region &#8220;actual checks&#8221; as classes that implement the ISitecoreCheck interface (or use the SitecoreCheckBase class).  


&nbsp;

**Tags**

You may not always want to run the same checks. Perhaps some checks should only be performed at night and some checks may be specific to your DTAP or CM/CD servers specifically. You can use tags to limit which tests are run, as demonstrated in the example below. And then you can specify which tags are applicable by specifiying them &#124;-separated in the url parameter &#8220;tags&#8221;. The url //SitecoreChecks.aspx?tags=fail would result in the following:

[<img class="aligncenter size-full wp-image-261" title="fail" src="/wp-content/uploads/2015/10/fail.png" alt="" width="519" height="506" srcset="/wp-content/uploads/2015/10/fail.png 519w, /wp-content/uploads/2015/10/fail-300x292.png 300w" sizes="(max-width: 519px) 100vw, 519px" />](/wp-content/uploads/2015/10/fail.png)

  
&nbsp;

Let me know if you have any questions/suggestions.