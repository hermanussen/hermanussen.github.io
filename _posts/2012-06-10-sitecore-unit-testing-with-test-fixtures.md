---
id: 148
title: Sitecore unit testing with test fixtures
date: 2012-06-10T20:58:09+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=148
permalink: /2012/06/sitecore-unit-testing-with-test-fixtures/
redirect_from:
  - /sitecore/wordpress/2012/06/sitecore-unit-testing-with-test-fixtures/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore tips
---
Unit testing logic that uses the Sitecore content API is not very easy. Alistair Deneys has written some very good articles on it <a title="Unit Testing in Sitecore is Not Scary" href="http://adeneys.wordpress.com/2010/11/20/unit-testing-in-sitecore-is-not-scary/">here</a> and <a title="Mocking Sitecore" href="http://adeneys.wordpress.com/2012/04/13/mocking-sitecore/">here</a>. The second article describes how to use mocking. I prefer that approach over testing on a running Sitecore website (integration testing), because I want my tests to be fast and I don&#8217;t like the risk of breaking my Sitecore website by messing up the database.

But mocking can be very tedious. Having to setup all the mocks for your tests can take a lot of time and that may be used as an excuse not to unit test your code at all. Setting up large <a title="Test Fixture on Wikipedia" href="http://en.wikipedia.org/wiki/Test_fixture#Software">test fixtures</a> can be very time consuming as well.

Since I recently [made a Sitecore DataProvider]({% post_url 2012-05-08-making-sitecore-faster-with-mongodb %} "MongoDB DataProvider article"), I&#8217;ve gotten somewhat familiar with that concept. So now I created a DataProvider that works in-memory. On startup, it loads Sitecore items from sources like Sitecore packages and serialized data (should work with TDS items as well). That should make it much easier to create test fixtures with your own items and templates! After your tests have run, your changes will be lost. That way, your tests can never &#8216;harm&#8217; any database.

I&#8217;ve shared the code <a title="Sitecore FixtureDataProvider" href="https://github.com/hermanussen/Sitecore-FixtureDataProvider">here on GitHub</a> (I wanted to try GitHub). Here are some steps to help you set things up:

  1. <span style="line-height: 19px;"><a title="Download a ZIP file with the code" href="https://github.com/hermanussen/Sitecore-FixtureDataProvider/zipball/master">Download the project</a> or pull it from GitHub.</span>
  2. <span style="line-height: 19px;">Make sure all the project references are working.</span>
  3. <span style="line-height: 19px;">Edit the SampleTestProject.dll.config file and change the absolute paths to correspond with the paths on your machine.</span>
  4. <span style="line-height: 19px;">Run the unit tests in SampleTestProject (they should pass).</span>

There are three projects in the solution:

  1. <span style="line-height: 19px;"><strong>FixtureDataProvider</strong> &#8211; This is the project that contains the DataProvider. If you inherit your unit testing class from SitecoreUnitTestBase, then some basic Sitecore stuff will be configured for you before the tests are executed.</span>
  2. <span style="line-height: 19px;"><strong>SampleSitecoreProject</strong> &#8211; This project contains some logic that utilizes the Sitecore content API. More specifically, it can read <a title="KML Tutorial" href="https://developers.google.com/kml/documentation/kml_tut">KML</a> and makes Sitecore items for every <a title="Placemark part of the KML tutorial" href="https://developers.google.com/kml/documentation/kml_tut#placemarks">Placemark</a> (containing a description and the coordinates of the placemark): {% gist 0bf4d628490e7dc171c2e4ac895fac11 %}
  3. <span style="line-height: 19px;"><strong>SampleTestProject</strong> &#8211; This project contains the SampleTestProject.dll.config file, which is kind of like a very minimal Web.config (without the need for an actual website to be running). The project also contains a data folder that has some serialized items and a zip package (the test fixture data). And you&#8217;ll also find some KML files to be imported. The UnitTest class contains the test of the previous code: {% gist 9c8c7bdf45231a9349818b48f2161eee %}
     
Some important points I want to make:
  
  <ul>
    <li>
      Events and cache are disabled by default. So if you need to test those aspects, you&#8217;ll have to do some extra work.
    </li>
    <li>
      Though I attempted to emulate the SQL DataProvider as much as possible, I can not guarantee that it behaves in the exact same way at all times. Remember that unit testing can never replace integration testing and functional testing altogether.
    </li>
    <li>
      <del>I have not yet implemented support for media</del> (I might add support for that later, and for the MongoDB DataProvider as well). &#8211; Implemented (not yet for the MongoDB DataProvider)
    </li>
  </ul>
  
  <p>
    Happy testing! And let me know if you have any questions or ideas!
  </p>