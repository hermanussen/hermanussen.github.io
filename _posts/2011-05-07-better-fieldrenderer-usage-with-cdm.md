---
id: 50
title: Better FieldRenderer usage with CDM
date: 2011-05-07T12:44:08+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=50
permalink: /2011/05/better-fieldrenderer-usage-with-cdm/
redirect_from:
  - /sitecore/wordpress/2011/05/better-fieldrenderer-usage-with-cdm/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
We&#8217;ve been using <a title="CDM Shared Source Module page" href="http://trac.sitecore.net/CompiledDomainModel/wiki">CompiledDomainModel</a> for several projects now. And we keep inventing new ways to make things even better.

Yesterday I was brainstorming with some colleagues about a better way of using the Sitecore FieldRenderer in combination with CDM. I found a very neat new way of doing this. But I&#8217;d like to share some of the different options, so that you can choose the best one for you.

**Traditional FieldRenderer without CDM:**

{% gist 4882c1c861f7e981078c3afb996bb3a8 %}

  * Simple implementation
  * Spelling errors result in not displaying anything instead of an error
  * Not wrapped, so no custom functionality can be placed on the item

**Use CDM without FieldRenderer:**

{% gist 7d56c38060fd6c16586966de0091f782 %}

  * Easy implementation
  * Typed access
  * The rendering pipeline is not used, so the page editor will not make this output editable

**Traditional FieldRenderer with CDM (currently the most used with CDM):**

{% gist 80f13e2feb5a68481fcfedae42c1b853 %}

  * A bit of a pain to unwrap the Sitecore item every time
  * Spelling errors result in compilation errors, which is great!
  * The FieldName can refer to a field from an entirely different type (though this is not a very common mistake)

**Custom FieldRenderer with CDM:**

{% gist 4f4f0206c1563fed06315535d2b56b85 %}

  * The same as the previous one, but without the need to unwrap the Sitecore item every time
  * You need to use a non-standard control

**Custom FieldRenderer with CDM and lambda expression:**

{% gist dc13e39bf306aa134e2763153793de0a %}

  * The best possible type-safety
  * Only usable in .NET 4
  * You need to use a non-standard control

The last one is the nicest one in my opinion. You can use it as if you are not using a field renderer at all, and still get all the benefits of a fieldrenderer (use of the rendering pipeline and editable in the page editor).

It works by using the <a title="MSDN about Expression Trees" href="http://msdn.microsoft.com/en-us/library/bb397951.aspx">expression tree</a> of the passed-in lambda expression and reflection to determine the name of the field. It shouldn&#8217;t be too hard to create similar controls for sc:Link and sc:Image. Here&#8217;s the code:

{% gist 2ffb022f9cddef2120efb5ba155d39b0 %}

Good luck!