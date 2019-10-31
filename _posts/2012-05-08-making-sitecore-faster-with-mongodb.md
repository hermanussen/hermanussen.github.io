---
id: 107
title: Making Sitecore faster with MongoDB
date: 2012-05-08T21:58:49+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=107
permalink: /2012/05/making-sitecore-faster-with-mongodb/
redirect_from:
  - /sitecore/wordpress/2012/05/making-sitecore-faster-with-mongodb/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore modules
---
Most Sitecore implementations that I&#8217;ve worked with are backed by SQL Server for storing the content. If you look at the database model, you will see that it is quite simple. It is designed around the key principles of the CMS itself (items and field values), rather than the data structure of the content.

This data structure is not only very simple, it also doesn&#8217;t really need any relationships besides the one between items and field values (for different languages and versions). In fact, everything comes down to just items and some data related to those particular items. A document-oriented database instead of a relational database may be a better fit!

With this in mind, I attempted to create a data provider for Sitecore that works with <a title="MongoDB website" href="http://www.mongodb.org/">MongoDB</a>. And after a few months of not working on it at all, I finally finished it in the last few evenings. Since it has not been properly tested and very likely has some major bugs still in it, I ask you to regard this as a VERY experimental implementation.

Nevertheless, I encourage anyone who is interested to play around with the module that I&#8217;ve shared on the Sitecore Shared Source website. You can find the MongoDBDataProvider <a title="MongoDBDataProvider" href="http://trac.sitecore.net/MongoDBDataProvider/wiki/WikiStart">here</a>.

**Setting up the module**

Here are some easy steps to get started with the MongoDB data provider.

  1. <a title="MongoDB quickstart for Windows" href="http://www.mongodb.org/display/DOCS/Quickstart+Windows">Install MongoDB</a> on your local machine and start it (no need to create a database)
  2. Get the latest source code from <del>SVN</del> <a title="MongoDB DataProvider" href="https://github.com/hermanussen/MongoDataProvider">GitHub</a>
  3. Build the project
  4. Copy the dll and dependencies (MongoDB.Bson and MongoDB.Driver) to the bin folder in your Sitecore site
  5. Copy MongoDataProvider.config to your App_Config/Include folder
  6. Copy Transfer.aspx and TestDataProvider.aspx to your website
  7. Open Transfer.aspx in your browser and select the database you want to copy into MongoDB
  8. Open the Sitecore desktop and open the mongodb database to see if everything is working correctly

After setting things up, you can also change the database that your website works with (go to the <sites /> element in your web.config) to the &#8220;mongodb&#8221; database.

**Measuring the speed**

I&#8217;ve said it before:

> In my opinion, any performance improvement (especially if it has significant drawbacks) must be proven to be worth it!

So I&#8217;ve made a page that tests the performance of any DataProvider that you select. It disregards any caching and tests several different operations a bunch of times and returns how long it took to run the operations. This might actually come in handy if you want to check your own custom made DataProvider.

Go to TestDataProvider.aspx and select the SQL Server data provider and the MongoDB data provider if you want to check the performance gain on your machine. My results are as follows:

<table>
  <colgroup>
    <col width="86" />
    <col width="227" />
    <col width="227" />
    <col width="227" />
  </colgroup>
  <tbody>
    <tr>
      <td width="86" height="32">
        <span><strong>Operation</strong></span>
      </td>
      
      <td width="227">
        <span><strong>Duration (in milliseconds) – SQL</strong></span>
      </td>
      
      <td width="227">
        <span><strong>Duration (in milliseconds) – MongoDB with safe mode ON</strong></span>
      </td>
      
      <td width="227">
        <span><strong>Duration (in milliseconds) – MongoDB with safe mode OFF</strong></span>
      </td>
    </tr>
    
    <tr>
      <td height="17">
        <span>Create</span>
      </td>
      
      <td>
        <span>3723</span>
      </td>
      
      <td>
        <span>1057</span>
      </td>
      
      <td>
        <span>776</span>
      </td>
    </tr>
    
    <tr>
      <td height="17">
        <span>Add versions</span>
      </td>
      
      <td>
        <span>5333</span>
      </td>
      
      <td>
        <span>2750</span>
      </td>
      
      <td>
        <span>2181</span>
      </td>
    </tr>
    
    <tr>
      <td height="32">
        <span>Change some field values</span>
      </td>
      
      <td>
        <span>7005</span>
      </td>
      
      <td>
        <span>1325</span>
      </td>
      
      <td>
        <span>1092</span>
      </td>
    </tr>
    
    <tr>
      <td height="17">
        <span>Get parent id&#8217;s</span>
      </td>
      
      <td>
        <span>2075</span>
      </td>
      
      <td>
        <span>318</span>
      </td>
      
      <td>
        <span>328</span>
      </td>
    </tr>
    
    <tr>
      <td height="17">
        <span>Get child id&#8217;s</span>
      </td>
      
      <td>
        <span>901</span>
      </td>
      
      <td>
        <span>275</span>
      </td>
      
      <td>
        <span>279</span>
      </td>
    </tr>
    
    <tr>
      <td height="32">
        <span>Get item definitions</span>
      </td>
      
      <td>
        <span>2026</span>
      </td>
      
      <td>
        <span>351</span>
      </td>
      
      <td>
        <span>348</span>
      </td>
    </tr>
    
    <tr>
      <td height="32">
        <span>Get item versions</span>
      </td>
      
      <td>
        <span>2051</span>
      </td>
      
      <td>
        <span>693</span>
      </td>
      
      <td>
        <span>676</span>
      </td>
    </tr>
    
    <tr>
      <td height="32">
        <span>Get field values</span>
      </td>
      
      <td>
        <span>1986</span>
      </td>
      
      <td>
        <span>656</span>
      </td>
      
      <td>
        <span>678</span>
      </td>
    </tr>
    
    <tr>
      <td height="17">
        <span>Delete</span>
      </td>
      
      <td>
        <span>9379</span>
      </td>
      
      <td>
        <span>372</span>
      </td>
      
      <td>
        <span>44</span>
      </td>
    </tr>
    
    <tr>
      <td height="17">
        <span><strong>Total</strong></span>
      </td>
      
      <td>
        <span>34479</span>
      </td>
      
      <td>
        <span>7798</span>
      </td>
      
      <td>
        <span>6401</span>
      </td>
    </tr>
  </tbody>
</table>

Note that the <a title="MongoDB safe mode explanation" href="http://stackoverflow.com/questions/4604868/mongodb-c-sharp-safemode-official-driver">safe mode</a> in MongoDB makes writing to the database more reliable, and also a little slower (you can find a setting for this in MongoDataProvider.config). Turning the safe mode off might be interesting on content delivery environments, because that&#8217;s where the performance really matters and you can always re-publish something if you need to (though it would be very annoying if this would be needed).

Here&#8217;s a chart with the results:

[<img class="size-full wp-image-124 alignnone" title="DataProvider speed measurement results" src="/wp-content/uploads/2012/05/DataProvider-speed-measurement-results.png" alt="DataProvider speed measurement results" width="999" height="362" srcset="/wp-content/uploads/2012/05/DataProvider-speed-measurement-results.png 999w, /wp-content/uploads/2012/05/DataProvider-speed-measurement-results-300x108.png 300w" sizes="(max-width: 999px) 100vw, 999px" />](/wp-content/uploads/2012/05/DataProvider-speed-measurement-results.png)

This may seem very impressive, but keep in mind that these results do NOT necessarily translate into similar improvements in speed for your entire website. A few things to keep in mind:

  * Both the MongoDB data provider and this speed measurement tool have just been developed and have not had a chance to mature. Both are very likely to have serious bugs and may disregard some matters that definitely should be regarded. I&#8217;d be happy to hear from you if you would like to point out some of the things I have missed.
  * Sitecore relies heavily on caching on different levels. That&#8217;s why a site (or an individual page) may be very slow only on the first request. Perhaps if your content editors publish content very often and the cache needs to be cleared on each publish, it may be a good idea to look for a faster data provider such as this module.
  * The SQL Server data provider has some internal caching that I&#8217;m not sure the MongoDB data provider is exactly on par with. That means that the MongoDB data provider might actually be slower than the SQL Server data provider in a &#8216;real world scenario&#8217;.

Anyway, it&#8217;s been great fun trying this different approach to storing Sitecore data and I hope you enjoyed reading about it!