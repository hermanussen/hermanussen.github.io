---
id: 100
title: CompiledDomainModel 0.5.5.0 released!
date: 2012-04-08T21:19:59+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=100
permalink: /2012/04/compileddomainmodel-0-5-5-0-released/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore modules
---
Though the <a href="http://trac.sitecore.net/CompiledDomainModel/wiki" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://trac.sitecore.net']);">CompiledDomainModel</a> Sitecore module is now a commonly used and deeply rooted part of our Sitecore development strategy within our organisation, that doesn&#8217;t mean that there&#8217;s no room for improvements.

That&#8217;s why I sometimes fix some bugs or add a few features. The easter bunny brings us release 0.5.5.0. And because I haven&#8217;t blogged about the previous release, I&#8217;ll also include the release notes for that one:

<img class="alignnone" title="CompiledDomainModel logo" src="/sitecore/CompiledDomainModel/cdm.png" alt="" width="563" height="346" /> 

Release 0.5.0.0:

  * Added support for relative fixed paths. So you can use a similar syntax as with fixed paths for paths within the content tree that have a fixed structure, but can be available in different locations.
  * The names of the DomainObjectSets are now included in the namespaces of the generated code. This allows for a better separation of projects/sites.
  * Items are now created by matching them by Sitecore ID, instead of template name
  * Some members made virtual
  * Compatibility with automatic databinding by turning it off during code generation
  * Fieldtype support added for 
      1. ImageField
      2. FileField
  * Generated code no longer uses XPath to get the descendants of a specific type; uses a &#8216;safer&#8217; way now
  * Added a GutterRenderer that displays the fixed paths and configured templates in the bar next to the content tree ([more info](http://hermanussen.eu/sitecore/wordpress/2011/03/the-sitecore-gutter/))
  * Generated code now starts with a prefix that can be used by external tools (like [this one](http://hermanussen.eu/sitecore/wordpress/2011/04/update-compileddomainmodel-from-visual-studio/)) to refresh the generated code.

Release 0.5.5.0:

  * Added &#8220;FromParent(&#8230;)&#8221; static method to create relative fixed paths by resolving the child item by itself
  * Added the option to the global settings to remove dependencies with the CDM module
  * Added IItemWrapperCore, to allow dependencies with generated code to be removed.
  * Better way of determining template and contributing template hierarchy.
  * Fixed a bug that deals with a rather exotic NullReferenceException in the ConfigurationUtil class.

You can find downloads on the <a title="CDM releases page" href="http://trac.sitecore.net/CompiledDomainModel/wiki/Releases" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://trac.sitecore.net']);">Releases page</a>. If you have any questions, just let me know!