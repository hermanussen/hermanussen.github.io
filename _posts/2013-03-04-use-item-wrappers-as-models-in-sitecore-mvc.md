---
id: 179
title: Use item wrappers as models in Sitecore MVC
date: 2013-03-04T19:48:20+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=179
permalink: /2013/03/use-item-wrappers-as-models-in-sitecore-mvc/
redirect_from:
  - /sitecore/wordpress/2013/03/use-item-wrappers-as-models-in-sitecore-mvc/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
I&#8217;ve been experimenting with Sitecore 6.6 MVC lately. I love the very clean Razor views. And if you&#8217;re used to working with a rich domain model that wraps your Sitecore items, then you&#8217;ll hardly ever need a controller rendering (because your view-logic will be on your model). Most of the layouts and sublayouts will be view renderings.

Now, when developing in ASP.NET Web forms, I will usually have a base class for my controls that has a generic type parameter that reflects what type of item it will take as a datasource. This way, I can easily access the right fields in a strong-typed fashion. And I wanted this same setup in MVC.

So, after completing the steps in this blog post, you will be able to make a Razor view like this:



Line-by-line explanation:

  1. Declare the model to be a IRenderingModel-derived type (this way, it will be initialized in the same way as the default rendering model). The generic type parameter shows that this particular view will take any item that has the &#8220;Page&#8221;-template or a template that inherits from it as its datasource.
  2. Use an extension to the SitecoreHelper to reference the &#8220;Title&#8221; field. It uses a lambda expression, so that the helper method can ensure that the &#8220;renderField&#8221; pipeline is run; this ensures that among other things, the page-editor support will be preserved.
  3. The same as #2, but for the &#8220;Text content&#8221; field.

**Side-note: I use my own <a title="CDM" href="http://marketplace.sitecore.net/en/Modules/Compiled_Domain_Model.aspx" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://marketplace.sitecore.net']);">CompiledDomainModel module</a> (CDM) to generate wrapper classes based on Sitecore templates. So the following example code will use it as well. But you can probably easily adapt the following code to work with your mapping/wrapping framework. The code is from a project that I will soon use in a presentation for the <a title="SUGNL" href="http://www.sugnl.net/" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://www.sugnl.net']);">SUGNL</a> (hence, the UnitTestingDemo namespace).**

The following code is for the RenderingModel. It allows access to the datasource itemwrapper in the type you want. Notice that the &#8220;out&#8221; keyword is used before the generic type parameter declaration. This means that the type is covariant, so that you can use a base type in your model declaration at the top of the Razor view (e.g. IRenderingModel<PageBase> instead of IRenderingModel<Page>).



To create the RenderingModel, we need to plug the following in to the &#8220;mvc.GetModel&#8221; pipeline.



Hook this code up to the &#8220;mvc.GetModel&#8221; pipeline using the following configuration (use a config file in the &#8220;/App_Config/Include&#8221; folder to make a nice patch of this):



Now, when you make a rendering, be sure to add &#8220;typedmodel=1&#8221; to the parameters field in Sitecore for that rendering. That way, the &#8220;mvc.GetModel&#8221; pipeline will know when to create a typed model.

And you&#8217;re all set to use the typed model in your Razor views. But there&#8217;s one thing left; the lambda syntax support. This works in the same way as the CdmFieldRenderer control from a [previous blog post](http://hermanussen.eu/sitecore/wordpress/2011/05/better-fieldrenderer-usage-with-cdm/ "Better FieldRenderer usage with CDM"). You can use the following helper class:



To be able to use this extension without having to import it every time, you can add it to the &#8220;/Views/Web.config&#8221; file, like this:



I know it takes a little time to setup, but it makes your Razor views very clean and you&#8217;ll have code-completion for your field names. If you want, you can compile your Razor views at build-time by editing your MVC project file and setting &#8220;<MvcBuildViews>true</MvcBuildViews>&#8221;.

Next week, I&#8217;ll be doing a presentation on unit testing with test fixtures and I&#8217;ll also get into unit testing the Razor view that I mentioned here. The whole project and the slides will be available for download on this blog afterwards.