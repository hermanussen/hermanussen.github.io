---
id: 35
title: Update CompiledDomainModel from Visual Studio
date: 2011-04-05T22:29:27+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=35
permalink: /2011/04/update-compileddomainmodel-from-visual-studio/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
My friend and I were talking about the CompiledDomainModel module the other day. He suggested that it would be a little easier if you could update the code from Visual Studio.

A few options were discussed, until we arrived at a rather nifty one. The generated code would start with a certain prefix, followed by a url that can be used to regenerate the code. Then, a Visual Studio plugin or macro could refresh the code by downloading it from that location.

Well, I&#8217;ve implemented just that! The code needed in CompiledDomainModel can be found in the current trunk version in SVN and I´ll add it to the release notes for the next release. The macro for updating generated code can be found on this page.

The following steps should be taken to generate code from Visual Studio (I&#8217;ve tested this with VS2010, and I&#8217;m not sure if it will work with VS2008):

  1. Make sure you have the CompiledDomainModel version from the trunk (or the release after 0.4.1.0, when it&#8217;s released)
  2. Generate the code and paste it into a file in your solution in Visual Studio
  3. Install the macro  
    _Now, you&#8217;re all set up to use the macro, so you can skip the first 3 steps next time_
  4. Open the generated file from the Solution Explorer and make sure it is checked out of source control (if configured)
  5. Run the macro
  6. Choose to reload the file from the file system when asked about it

You may notice a few things that are not that convenient yet:

  * You have to actually open the file before regenerating it &#8211; This was the quickest way I could figure this out. If anyone knows how to get the selected file from the solution explorer, then please let me know!
  * You have to check out the file from source control &#8211; The file must be writable. The macro writes the generated code directly to the filesystem, because writing it in the editor turned out te be way too slow. Perhaps source control can be controlled from the macro as well, but I don&#8217;t know how to do that.
  * The module needs to be accessible to anonymous users, as the macro isn&#8217;t authenticated in Sitecore. But this is not really a problem in a development environment. This does mean that the comment always says &#8220;User &#8216;sitecore\Anonymous&#8217; generated this file.&#8221;.

I&#8217;ve never coded a macro before; I&#8217;ve never even coded in VB.NET before (yes, I said the UGLY word). But even with these minor issues, the macro does seem to make things a little easier if you need to regenerate the code often.

Here&#8217;s the code for the macro. Have fun!