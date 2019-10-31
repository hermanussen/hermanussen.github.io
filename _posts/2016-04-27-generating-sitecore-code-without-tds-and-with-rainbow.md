---
id: 277
title: Generating Sitecore code without TDS and with Rainbow
date: 2016-04-27T19:05:00+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=277
permalink: /2016/04/generating-sitecore-code-without-tds-and-with-rainbow/
redirect_from:
  - /sitecore/wordpress/2016/04/generating-sitecore-code-without-tds-and-with-rainbow/
aktt_notify_twitter:
  - 'no'
categories:
  - sitecore modules
---
About a year ago, [I posted about a way to generate code]({% post_url 2015-04-20-generating-sitecore-code-without-tds %} "Previous post") from your Sitecore data without the need to use TDS. Since then, a new version of <a title="Unicorn" href="https://www.nuget.org/packages/Unicorn/">Unicorn</a> was released, that supports a new serialization format called <a title="Rainbow serialization format" href="https://www.nuget.org/packages/Rainbow">Rainbow</a>.

[<img class="aligncenter size-full wp-image-278" title="rainbow" src="/wp-content/uploads/2016/04/rainbow.jpg" alt="" width="400" height="400" srcset="/wp-content/uploads/2016/04/rainbow.jpg 400w, /wp-content/uploads/2016/04/rainbow-150x150.jpg 150w, /wp-content/uploads/2016/04/rainbow-300x300.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />](/wp-content/uploads/2016/04/rainbow.jpg)

The description on <a title="Rainbow on GitHub" href="https://github.com/kamsar/Rainbow">Rainbow&#8217;s GitHub page</a>: _An advanced serialization and comparison system for Sitecore. Designed for easy merging with YAML-based serialization, and a generic merge/deserialization framework. Works well with Unicorn, or by itself._

Unfortunately, the code generator didn&#8217;t support this format. But with a little tweaking, I&#8217;ve now added support for it!

You can follow <a title="Configure code generation for your project" href="https://github.com/hermanussen/sitecore.codegenerator#adding-code-generation-to-your-project">the same instructions</a> as described before. And after that, <a title="Specific changes for Rainbow support" href="https://github.com/hermanussen/sitecore.codegenerator#using-unicorns-rainbow-format">apply some specific changes to enable Rainbow support</a>.

Happy code generating!