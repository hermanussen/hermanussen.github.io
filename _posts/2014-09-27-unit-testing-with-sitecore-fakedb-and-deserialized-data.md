---
id: 226
title: Unit testing with Sitecore.FakeDb and deserialized data
date: 2014-09-27T19:14:44+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=226
permalink: /2014/09/unit-testing-with-sitecore-fakedb-and-deserialized-data/
redirect_from:
  - /sitecore/wordpress/2014/09/unit-testing-with-sitecore-fakedb-and-deserialized-data/
aktt_notify_twitter:
  - 'no'
categories:
  - sitecore modules
---
Recently, I watched the excellent <a title="SVUG session about Sitecore.FakeDb" href="https://www.youtube.com/watch?v=9IgKrI3Y_Z0">SVUG presentation by Pavel Veller on YouTube</a>. I was impressed by the way Sitecore.FakeDb works. It&#8217;s much easier to configure than my [FixtureDataProvider]({% post_url 2012-06-10-sitecore-unit-testing-with-test-fixtures %} "Previous post about unit testing with the FixtureDataProvider"), has tighter isolation and is (because of that) much faster.

Even though the syntax for setting up your test data is very easy and short with Sitecore.FakeDb, I think that it can be a lot of work to setup things for a unit test. Besides, those of us using TDS or Unicorn are already putting a lot of information about the structure of items under source control. It would be a shame if we could not use that information.

That&#8217;s why I propose a hybrid approach: use DbItem and DbTemplate to setup your tests and where needed, deserialize individual items/templates. This can have the benefit of not having to initialize as much, as well as bringing your serialized data into the test scope.

On that last note: if a template field is renamed and then synchronized with TDS, then if the code you are unit testing relies on that field name&#8230; it will fail. Which can be very helpful during development.

I&#8217;ve added a project called Sitecore.FakeDb.Serialization to the FakeDb project. It&#8217;s usage is entirely optional and adds 2 important classes: DsDbItem and DsDbTemplate (Ds = Deserialized). They inherit from their regular Sitecore.FakeDb counterparts. But instead of having to define the field values, they load them from the filesystem.

You can easily mix these approaches. Here&#8217;s an example of a unit test using both:



&nbsp;

You can find these changes in <a title="Sitecore.FakeDb fork on GitHub" href="https://github.com/hermanussen/Sitecore.FakeDb">my fork on GitHub</a>. To use them, you need to do the following afer you&#8217;ve setup Sitecore.FakeDb:  
&#8211; Add a reference from your unit test project to Sitecore.FakeDb.Serialization.  
&#8211; Edit the App.config file and add the following section (change the folders to point to your serialized data, or add/remove folders as needed):



&nbsp;

Have fun coding!