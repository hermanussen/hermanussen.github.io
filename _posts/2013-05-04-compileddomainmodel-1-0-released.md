---
id: 201
title: CompiledDomainModel 1.0 released!
date: 2013-05-04T17:34:51+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=201
permalink: /2013/05/compileddomainmodel-1-0-released/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore modules
tags:
  - cdm
---
This was a little overdue; my Sitecore code generation module, CompiledDomainModel, has been used in many projects and the code has matured enough to justify a 1.0.0.0 version number. A very important addition was made in this release.

Release 1.0.0.0:

  * Added &#8220;Platform Mode&#8221;, that can be used if generated code needs to be in separate files (e.g. when there are multiple DLL&#8217;s where generated code is needed)
  * NuGet support added

**Platform Mode**

This is a feature that has been requested by several people. If you have multiple projects or logic that is used in several DLL&#8217;s, then you need a way to divide the generated classes up into multiple files.

To make this possible, you should first check the &#8220;Platform Mode&#8221; checkbox on the settings item (/sitecore/system/Modules/CompiledDomainModel/Settings):

<img class="alignnone" title="CDM Platform Mode" src="/sitecore/static/cdm_platform_mode.png" alt="" width="958" height="558" /> 

Note that the wrapper classes need to be resolved globally when using the platform mode. To make that possible, there is a dependency on the module itself. So you can&#8217;t use the &#8220;Remove dependencies&#8221; function when you want to use the platform mode.

If you generate the code now, you&#8217;ll see that a comment is generated:  


As is explained, you must now make url&#8217;s to generate code that is specific to your project. In this case, you could generate code for the platform project and the specific &#8220;SomeProject&#8221; project. Using the following url&#8217;s, you can do that:

  1. http://sitecoredemo/sitecore/shell/Applications/CompiledDomainModel/CodeGenerator.aspx?platformsets=Core|PlatformTemplatesSet|PlatformFixedPaths
  2. http://sitecoredemo/sitecore/shell/Applications/CompiledDomainModel/CodeGenerator.aspx?platformsets=SomeProjectTemplatesSet|SomeProjectFixedPathsSet

These url&#8217;s will only generate the code for the DomainObjectSets and FixedPathSets (check the [documentation](http://hermanussen.eu/sitecore/CompiledDomainModel/Documentation/default.htm#chapter2 "CDM docs") for an explanation about these sets) that are referenced in the url.

**NuGet support**

You can now install <a title="NuGet CDM" href="https://nuget.org/packages/CompiledDomainModel" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://nuget.org']);">CompiledDomainModel through NuGet</a>. I based the package on <a title="Article about deploying Sitecore modules with NuGet" href="http://blog.velir.com/index.php/2012/12/04/create-and-deploy-sitecore-modules-with-nuget/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://blog.velir.com']);">this excellent article</a>.

Steps:

  1. You need to have <a title="Sitecore Rocks" href="http://visualstudiogallery.msdn.microsoft.com/44a26c88-83a7-46f6-903c-5c59bcd3d35b" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://visualstudiogallery.msdn.microsoft.com']);">Sitecore Rocks</a> installed in Visual Studio
  2. You need to connect your project to your Sitecore website
  3. Open the Package Manager Console and run **Install-Package CompiledDomainModel**

<img class="alignnone" title="CDM NuGet installed" src="/sitecore/static/cdm_nuget_installation.png" alt="" width="574" height="290" /> 

Of course you are not required to install CDM this way. You can still use the regular package on the [Releases page](http://hermanussen.eu/sitecore/CompiledDomainModel/Releases/ "Releases page").

Happy CDM-coding!