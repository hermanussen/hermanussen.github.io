---
id: 219
title: Index page editor proof pages with Sitecore 7
date: 2014-01-30T23:33:05+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=219
permalink: /2014/01/index-page-editor-proof-pages-with-sitecore-7/
redirect_from:
  - /sitecore/wordpress/2014/01/index-page-editor-proof-pages-with-sitecore-7/
aktt_notify_twitter:
  - 'no'
categories:
  - sitecore modules
---
After competing in the <a title="First ever Sitecore Hackathon" href="http://sitecorehackathon.org/first-ever-sitecore-hackathon/">Sitecore hackathon</a> last weekend, I got excited. So when <a title="Kyle Heon on Twitter" href="https://twitter.com/kyleheon">Kyle Heon</a> posted a particular Tweet today, I immediately knew what I would be doing this evening; create a new (small) project on GitHub.

<blockquote class="twitter-tweet" lang="en">
  <p>
    So how does <a href="https://twitter.com/search?q=%23Sitecore&src=hash">#Sitecore</a> v7 Search work when your page is comprised of page editor components?
  </p>
  
  <p>
    — Kyle Heon (@kyleheon) <a href="https://twitter.com/kyleheon/statuses/428901346398728192">January 30, 2014</a>
  </p>
</blockquote>



And here you can find the <a title="Sitecore Html Crawler" href="https://github.com/hermanussen/sitecore-html-crawler">result</a>. Basically, I created a computed field that actually does a http request and downloads the page that you are indexing.

The reason you would want to do this, is because of how content composition in the page editor works. You can add components to a page that reference separate Sitecore items as associated content (a.k.a. datasources). But the content of those referenced items is indexed separately and therefore difficult to search for using Sitecore.ContentSearch (Sitecore 7 search) &#8211; if you want &#8216;pages&#8217; to be the result, like regular site searches usually need.

You can find more information, including installation instructions, on the GitHub page for <a title="Sitecore Html Crawler on GitHub" href="https://github.com/hermanussen/sitecore-html-crawler">Sitecore Html Crawler</a> (just scroll down a little).

There are some limitations to this approach that you should know about.

  1. This doesn&#8217;t really work well with wildcard items, because they can only be indexed once; not for every item that you want to display on the wildcard item&#8217;s page. You would need to change the actual indexer to support that, or handle the difficulty of it in your search query.
  2. I&#8217;ve only tested this with Lucene. I think changing the configuration a little could make it work for other providers such as Solr.