---
id: 246
title: Sitecore Code Challenge 1
date: 2014-12-14T15:27:19+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=246
permalink: /2014/12/sitecore-code-challenge-1/
redirect_from:
  - /sitecore/wordpress/2014/12/sitecore-code-challenge-1/
aktt_notify_twitter:
  - 'no'
categories:
  - fun
---
Someone once told me about <a title="Pex for fun" href="http://www.pex4fun.com/">Pex for fun</a>. And ever since, I occasionally visit the website to solve some C# coding puzzles. Essentially, it requires you to implement some code and have unit tests for it pass. But you don&#8217;t know the implementation of the unit tests.

I thought about how we could do something similar with Sitecore, and came up with a way to do it. If you follow the steps below, you&#8217;ll have a .sln with a project that compiles and has unit tests. But the tests all fail.

It&#8217;s your job to make sure the code passes the unit tests. But the relevant code in the unit tests is hidden inside an obfuscated DLL (can&#8217;t be easily decompiled).

The failing assertions  in the unit tests, will give you detailed hints though. And if you succeed in getting the unit tests to pass, your project can be deployed to Sitecore and will actually be usable!

Since this is quite a new way of getting to know Sitecore in a fun way, I&#8217;m bringing this to the community as an experiment. I&#8217;m very interested to learn your experiences:

  * Are you able to finish the puzzle?
  * Is it fun trying to solve the puzzle?
  * Any feedback for creating a second challenge (if this one turns out to be a success)?

Follow these steps to get started:

  1. Download <a title="Sitecore code challenge 01" href="/sitecore/codechallenges/Sitecore.CodeChallenge01.zip">this ZIP file</a> and extract it.
  2. Copy &#8220;Sitecore.Kernel.dll&#8221; to the folder &#8220;Binaries&#8221; (I&#8217;ve tested with version 7.2 rev 140526, but it will probably work with other versions as well).
  3. Open the project in Visual Studio and build the project.
  4. Run the unit tests using a runner that supports xUnit (I&#8217;m using <a title="xUnit.net VS runner" href="http://xunit.github.io/docs/running-tests-in-vs.html">xUnit.net VS runner,</a> which is free)
  5. The tests are ordered into steps. Go through the steps in  order and look at the reported errors for hints on how to solve the puzzle.

Let me know if you are able to finish this first code challenge! Have fun!