---
id: 31
title: The Sitecore Gutter
date: 2011-03-25T20:34:10+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=31
permalink: /2011/03/the-sitecore-gutter/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
No, this isn&#8217;t a sad article about unemployed Sitecore developers. And I&#8217;m still gainfully employed, thank you very much.

Instead, this article is about a Sitecore feature that a colleague pointed out to me recently. I hadn´t noticed it before, but it seems pretty useful to me.

When you right-click in the bar left of the content tree, you&#8217;ll get a nice dropdown allowing you to select an option (or multiple options). It&#8217;s called the quick action bar, but I call it the gutter (I&#8217;ll explain later). There are some very useful options there that can give you a quick insight into what&#8217;s going on with your content items and you can also use it to manipulate the items.

<img class="alignnone" title="Sitecore gutter" src="/sitecore/wordpress/wp-content/uploads/sitecore_gutter.png" alt="" width="147" height="224" /> 

For example, I&#8217;ve found the &#8220;Presentation Overriden&#8221; option to be quite useful. If selected, it displays an icon next to any item that does not have the standard presentation settings from the item&#8217;s template selected. This can prevent annoying problems, if you accidentaly changed the presentation settings for an individual item and you don&#8217;t see why the changes on the standard values seem to have no effect. You can click the icon to remove the overriden settings.

Anyway, this function gave me an idea: what if you could control the behaviour of the icons in the gutter dynamically, say, through the Sitecore rules engine? That would be pretty cool, because you would not have to do any coding to quickly see what items comply with a certain condition.

So I got to work, and quickly found the icons in the core database (/sitecore/content/Applications/Content Editor/Gutters). This is where I got the name: since the items are called GutterRenderers, it only seems logical to call it the gutter (or not&#8230; whatever).

I added a new item with the right template (/sitecore/templates/Sitecore Client/Content editor/Gutter Renderer) and set the values as displayed in the image below.

<img class="alignnone" title="Settings" src="/sitecore/wordpress/wp-content/uploads/sitecore_rule_based_gutter_settings.png" alt="" width="599" height="257" /> 

Please note that the datasource and fieldname point to an item&#8217;s field in the master database. That item&#8217;s field is a &#8220;Rules&#8221; field and can be used to set the condition.

<img class="alignnone" title="Rule based gutter rules" src="/sitecore/wordpress/wp-content/uploads/sitecore_rule_based_gutter_rules.png" alt="" width="272" height="88" /> 

All that was needed now was to implement the RuleBasedGutterRenderer.RuleBased class. Which is what I did:



So now all you have to do is set a rule in that field and you are ready to go (be sure to clear the Sitecore cache and refresh the Sitecore desktop after changing the rule).

<img class="alignnone" title="The resulting gutter" src="/sitecore/wordpress/wp-content/uploads/sitecore_rule_based_gutter_display.png" alt="" width="502" height="261" />