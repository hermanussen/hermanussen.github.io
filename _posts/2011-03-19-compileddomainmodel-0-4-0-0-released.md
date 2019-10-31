---
id: 27
title: CompiledDomainModel 0.4.0.0 released!
date: 2011-03-19T17:36:55+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=27
permalink: /2011/03/compileddomainmodel-0-4-0-0-released/
redirect_from:
  - /sitecore/wordpress/2011/03/compileddomainmodel-0-4-0-0-released/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore modules
---
I&#8217;ve been working on my code generating Sitecore module called <a href="http://trac.sitecore.net/CompiledDomainModel/wiki">CompiledDomainModel</a>. We&#8217;ve been using the module on a project for a large energy company&#8217;s website. As it is the first real project that the module is being used on, we obviously found some bugs and we needed some extra features. Some of the feedback has been used to make some changes to the module. These changes have now been included in a new release (version 0.4.0.0).

This release also includes a code generation template that can be used to generate a WCF service (experimental). It is possible for any application that can consume a WCF service, to read and write content to Sitecore. And all of this can be done in a typed way: e.g. a template called Product with fields ProductId, ProductName and ProductDescription will be available in the WSDL as a type.

I&#8217;ve also created a demo Silverlight application that can consume the WCF service. It&#8217;s similar to the RSS feed reader demo application. But I haven&#8217;t created a package that can be downloaded for it. If you want to run the demo application, you&#8217;ll have to get it from the shared source SVN repository.

Working with the module has been making my daily life as a Sitecore developer (increasingly) easier. I&#8217;ve been getting some good feedback from my colleagues, who are generally quite positive about it as well. It takes a bit of getting used to, but you will see many advantages once you get into it. It&#8217;s been great seeing the fruits of my labour!

If you&#8217;re not getting what this post is about exactly, then check out the <a title="CDM demo video" href="http://www.youtube.com/watch?v=ApngdILYpkA">demo video</a> I made a while ago.