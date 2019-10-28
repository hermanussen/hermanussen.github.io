---
id: 251
title: Generating Sitecore code without TDS
date: 2015-04-20T22:40:29+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=251
permalink: /2015/04/generating-sitecore-code-without-tds/
redirect_from:
  - /sitecore/wordpress/2015/04/generating-sitecore-code-without-tds/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore modules
---
In the past, I&#8217;ve used my own <a title="CDM" href="https://github.com/hermanussen/CompiledDomainModel" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://github.com']);">Compiled Domain Model</a> module on projects. It generates wrapper classes based on your Sitecore templates (among other things). But recently, I&#8217;ve been working with <a title="Glass Mapper" href="http://glass.lu/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://glass.lu']);">Glass Mapper</a>.

Glass Mapper doesn&#8217;t wrap Sitecore items, but rather maps Sitecore items to objects. The result is somewhat similar; you can work with strong-typed classes/interfaces and extend them if you want.

There are several ways you can configure Glass Mapper. One of the ways is by using attributes. The attributes map the classes/interfaces and their properties to Sitecore templates and fields. This works very well and is very flexible, but it can be a bit tedious to do manually.

That&#8217;s why generating the code is a good option. If you&#8217;re using <a title="TDS" href="http://www.hhogdev.com/products/team-development-for-sitecore/overview.aspx" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://www.hhogdev.com']);">TDS</a>, then you can <a title="Code Generation with TDS" href="http://hedgehogdevelopment.github.io/tds/chapter6.html" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://hedgehogdevelopment.github.io']);">easily generate code</a>.

But if you can&#8217;t use TDS (e.g. because of the costs), then here&#8217;s a good alternative. Kern Herskind Nightingale did <a title="Kern's code generation" href="http://herskind.co.uk/blog/2011/04/sitecore-tds-t4-text-template" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://herskind.co.uk']);">something similar</a> before. But my implementation supports:

  1. Generate individual files for each template
  2. Configure which paths to generate classes/interfaces for
  3. Generate interfaces for Glass Mapper (but it is easily adaptable to other frameworks)

For more information, look at the <a title="Sitecore.CodeGenerator documentation" href="https://github.com/hermanussen/sitecore.codegenerator#readme" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://github.com']);">documentation here</a>, and you can clone/fork the project on <a title="Sitecore.CodeGenerator on GitHub" href="https://github.com/hermanussen/sitecore.codegenerator" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://github.com']);">GitHub here</a>.

<div id="attachment_253" style="width: 849px" class="wp-caption alignleft">
  <a href="/wp-content/uploads/2015/04/idog_generated_code_example.png" ><img aria-describedby="caption-attachment-253" class="size-full wp-image-253" title="IDog interface example generated using Sitecore.CodeGenerator" src="/wp-content/uploads/2015/04/idog_generated_code_example.png" alt="IDog interface example generated using Sitecore.CodeGenerator" width="839" height="385" srcset="/wp-content/uploads/2015/04/idog_generated_code_example.png 839w, /wp-content/uploads/2015/04/idog_generated_code_example-300x137.png 300w" sizes="(max-width: 839px) 100vw, 839px" /></a>
  
  <p id="caption-attachment-253" class="wp-caption-text">
    IDog interface example generated using Sitecore.CodeGenerator
  </p>
</div>