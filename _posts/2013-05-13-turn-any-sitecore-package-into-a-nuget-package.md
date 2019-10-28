---
id: 208
title: Turn any Sitecore package into a NuGet package
date: 2013-05-13T23:03:22+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=208
permalink: /2013/05/turn-any-sitecore-package-into-a-nuget-package/
redirect_from:
  - /sitecore/wordpress/2013/05/turn-any-sitecore-package-into-a-nuget-package/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore modules
---
I recently posted this idea on Twitter:

<blockquote class="twitter-tweet">
  <p>
    @<a href="https://twitter.com/kevinobee" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://twitter.com']);">kevinobee</a> @<a href="https://twitter.com/kayeenl" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://twitter.com']);">kayeenl</a> Btw, I was thinking that it shouldn&#8217;t be too hard to make a cmd line util that converts <a href="https://twitter.com/search/%23Sitecore" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://twitter.com']);">#Sitecore</a> packages into <a href="https://twitter.com/search/%23NuGet" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://twitter.com']);">#NuGet</a>
  </p>
  
  <p>
    — Robin Hermanussen (@knifecore) <a href="https://twitter.com/knifecore/status/331512623944318976" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://twitter.com']);">May 6, 2013</a>
  </p>
</blockquote>

And it didn&#8217;t take me that long to actually implement it. Follow these steps to turn any Sitecore package into a NuGet package and share it with the world.

  1. Download the <a title="Command line tool direct download" href="/wp-content/uploads/CreateSitecoreNuGetPackage.exe" onclick="javascript:_gaq.push(['_trackEvent','download','/wp-content/uploads/CreateSitecoreNuGetPackage.exe']);">CreateSitecoreNuGetPackage.exe file here</a> or build it yourself with <a title="CreateSitecoreNuGetPackage on GitHub" href="https://github.com/hermanussen/CreateSitecoreNuGetPackage" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://github.com']);">the code from GitHub</a>.
  2. Put the files &#8220;Sitecore.Kernel.dll&#8221; and &#8220;Sitecore.Zip.dll&#8221; in the same folder.
  3. Create your package in the Package Manager and export the ZIP file.
  4. Run the following command from the command line:  
    CreateSitecoreNuGetPackage [PATH\_TO\_SITECORE_PACKAGE]
  5. Use the <a title="NuGet Package Explorer" href="http://npe.codeplex.com/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://npe.codeplex.com']);">NuGet Package Explorer</a> to open the generated  .nuspec file and improve the metadata if needed.
  6. Publish the package to a repository, like <a title="nuget.org" href="http://nuget.org" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://nuget.org']);">nuget.org</a>.

Now, everyone will be able to install/uninstall your package through NuGet. Remember that you need to install Sitecore Rocks and attach your project before installing the package.

Some links to pages that helped me creating this:

  * <a title="http://blog.velir.com/index.php/2012/12/04/create-and-deploy-sitecore-modules-with-nuget/" href="http://blog.velir.com/index.php/2012/12/04/create-and-deploy-sitecore-modules-with-nuget/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://blog.velir.com']);">http://blog.velir.com/index.php/2012/12/04/create-and-deploy-sitecore-modules-with-nuget/</a>
  * <a title="http://vsplugins.sitecore.net/Sitecore-NuGet.ashx" href="http://vsplugins.sitecore.net/Sitecore-NuGet.ashx" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://vsplugins.sitecore.net']);">http://vsplugins.sitecore.net/Sitecore-NuGet.ashx</a>
  * <a title="http://www.sitecore.net/Community/Technical-Blogs/John-West-Sitecore-Blog/Posts/2011/06/Attach-a-Sitecore-Rocks-Connection-to-a-Visual-Studio-Project.aspx" href="http://www.sitecore.net/Community/Technical-Blogs/John-West-Sitecore-Blog/Posts/2011/06/Attach-a-Sitecore-Rocks-Connection-to-a-Visual-Studio-Project.aspx" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://www.sitecore.net']);">http://www.sitecore.net/Community/Technical-Blogs/John-West-Sitecore-Blog/Posts/2011/06/Attach-a-Sitecore-Rocks-Connection-to-a-Visual-Studio-Project.aspx</a>

I will be very interested to hear your feedback, as **I haven&#8217;t been able to test this very well**. If this utility catches on, I might make a version that you can use from the package manager directly.

Happy NuGetting 😛