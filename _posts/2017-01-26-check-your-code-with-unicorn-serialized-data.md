---
id: 284
title: Check your code with Unicorn serialized data
date: 2017-01-26T09:59:10+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=284
permalink: /2017/01/check-your-code-with-unicorn-serialized-data/
aktt_notify_twitter:
  - 'no'
categories:
  - sitecore modules
---
I was looking into Roslyn recently and figured that it would be useful for checking whether Sitecore ID&#8217;s and paths that are used in code are correct or not. I wanted it to check this with the Unicorn serialized data that I have.

That&#8217;s why I created an analyzer that does just that. I&#8217;m curious to get some feedback on it so I can improve things.

[<img class="aligncenter size-full wp-image-289" title="check_serialized_data_analyzer" src="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/check_serialized_data_analyzer.png" alt="" width="851" height="209" srcset="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/check_serialized_data_analyzer.png 851w, http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/check_serialized_data_analyzer-300x73.png 300w" sizes="(max-width: 851px) 100vw, 851px" />](http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/check_serialized_data_analyzer.png)

Integrate this into your build using <a title="Rainbow data analyzer on NuGet" href="https://www.nuget.org/packages/RainbowDataAnalyzer/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://www.nuget.org']);">NuGet</a> or use the <a title="Rainbow data analyzer on Visual Studio Gallery" href="https://marketplace.visualstudio.com/items?itemName=hermanussen.SitecoreRainbowDataAnalyzer" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://marketplace.visualstudio.com']);">Visual Studio Gallery to install the extension</a>. Get more info and <a title="Source code on GitHub for Rainbow data analyzer" href="https://github.com/hermanussen/RainbowDataAnalyzer" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://github.com']);">the source on GitHub</a> (the main page contains installation instructions).

Update: field names and ID&#8217;s are now also supported.[<img class="aligncenter size-full wp-image-293" title="field_validation" src="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_validation.png" alt="" width="576" height="119" srcset="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_validation.png 576w, http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_validation-300x61.png 300w" sizes="(max-width: 576px) 100vw, 576px" />](http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_validation.png)

Update 2: field names and ID&#8217;s can now also be validated against a template.[<img class="aligncenter size-full wp-image-295" title="field_on_template_checking" src="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking.png" alt="" width="887" height="276" srcset="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking.png 887w, http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking-300x93.png 300w" sizes="(max-width: 887px) 100vw, 887px" />](http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking.png)

Update 3: a tooltip will now be displayed for ID&#8217;s, to show the full path of the item. Similarly, a tooltip will be displayed for paths to show the ID.[<img class="aligncenter size-full wp-image-297" title="path_tooltip" src="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/path_tooltip.png" alt="" width="835" height="113" srcset="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/path_tooltip.png 835w, http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/path_tooltip-300x40.png 300w" sizes="(max-width: 835px) 100vw, 835px" />](http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/path_tooltip.png)

Update 4: fields that are decorated with Glass Mapper attributes can now also be validated against a template.[<img class="aligncenter size-full wp-image-299" title="field_on_template_checking_glass" src="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking_glass.png" alt="Field on template checking for Glass Mapper" width="1165" height="152" srcset="http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking_glass.png 1165w, http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking_glass-300x39.png 300w, http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking_glass-1024x133.png 1024w" sizes="(max-width: 1165px) 100vw, 1165px" />](http://hermanussen.eu/sitecore/wordpress/wp-content/uploads/2017/01/field_on_template_checking_glass.png)