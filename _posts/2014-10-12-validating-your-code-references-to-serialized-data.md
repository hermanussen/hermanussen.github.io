---
id: 241
title: Validating your code references to serialized data
date: 2014-10-12T21:04:18+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=241
permalink: /2014/10/validating-your-code-references-to-serialized-data/
redirect_from:
  - /sitecore/wordpress/2014/10/validating-your-code-references-to-serialized-data/
aktt_notify_twitter:
  - 'no'
categories:
  - code snippets
---
Sitecore developers often need to reference content items from their code. E.g.: a template or branch ID for an import function or reading a global setting that&#8217;s stored in the content tree. Using IDs is usually preferred over using paths, because paths may change. It&#8217;s considered good practice to keep those ID references in a class with constants, like this:



After recently contributing some serialization logic to <a title="Sitecore.FakeDb.Serialization" href="https://github.com/sergeyshushlyapin/Sitecore.FakeDb#fakedb-serialization">Sitecore.FakeDb</a>, I got the idea to write unit tests that validate if these constants have values that are actually in Sitecore. We can use TDS or Unicorn serialized data to validate this.

The following unit test does just that (uses NUnit, FluentAssertions, Sitecore.FakeDb and Sitecore.FakeDb.Serialization):



Just pass in the types (that have Sitecore IDs as static properties) using the &#8220;Values&#8221; attribute.

But I didn&#8217;t stop there. At my company, we&#8217;re currently working on a project that uses <a title="Glass Mapper" href="http://glass.lu/">Glass Mapper</a>. Glass Mapper can use attributes to link mapped classes to the correct Sitecore templates. And in a similar way, properties can be linked to field IDs.



I wanted to validate all those IDs as well, and also check if the field IDs are on the right templates.

That&#8217;s why I wrote the following unit test. It finds all the types that have attributes like this and deserializes the corresponding templates. It also checks if the fields are there.

To use it, you need to pass in one type from the assembly that you want to test (or multiple) using the &#8220;Values&#8221; attribute.



Since I&#8217;m quite new to using Glass Mapper, I&#8217;d be interested to get some feedback on this. I&#8217;m pretty sure there&#8217;s more that can be tested.

Bye!