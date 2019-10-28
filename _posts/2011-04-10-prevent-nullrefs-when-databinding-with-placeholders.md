---
id: 43
title: Prevent nullrefs when databinding with placeholders
date: 2011-04-10T16:21:42+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=43
permalink: /2011/04/prevent-nullrefs-when-databinding-with-placeholders/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
I love databinding. It allows me to keep view-logic in ascx/aspx files so I don&#8217;t have to read long code-behind files laden with initialization logic and page lifecycle related crap.

Databinding works better with WPF and Silverlight than it does with ASP.NET. But in my humble opinion it still beats the alternative in ASP.NET.

One very annoying problem I&#8217;ve run into when using databinding in ASP.NET is the use of placeholders. The placeholder is a control that we use as the equivalent of an if-statement in C#. If the &#8220;Visible&#8221; property evaluates as true, only then the contents are rendered.

This works well in most cases. But when you use databinding it sort of breaks. For example:



This code will work perfectly fine, unless &#8220;SomeProperty&#8221; evaluates to null, because the contents of the placeholder are always evaluated! This problem is especially annoying with Sitecore FieldRenderers, which don&#8217;t allow the &#8220;Item&#8221; property to be null. A simple fix to this problem is to repeat the null-check within the placeholder, like so:



But if you would have a more complicated condition, many unsafe binding statements within the placeholder or nesting of several placeholders, this fix can prove to be quite cumbersome.

So I tried to find a good workaround for this problem and I observed the repeater control. It does not have this problem, because the contents of &#8220;ItemTemplate&#8221; will never be evaluated if the collection in the datasource is empty. This is what I came up with:  


That works really well! I used the repeater as a placeholder and now, if &#8220;SomeProperty&#8221; evaluates to null, there will be no problem; the contents of &#8220;ItemTemplate&#8221; are never evaluated by the databinder.

Still, this is quite an ugly workaround, because it&#8217;s pretty verbose and not really intuitive to programmers. So we need a better solution.

And I found one! I created a custom control that derives from the PlaceHolder control. The only difference in behaviour is that the contents of the control are not evaluated by the databinder if the &#8220;Visible&#8221; property is null. Here&#8217;s the code for the control:



This is a pretty simple change, but it makes life so much easier. If we import the control and use it in the following way, we no longer have to worry about nullref problems:



Happy coding!