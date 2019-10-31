---
id: 63
title: Design Structure Matrix (DSM) for your content tree
date: 2011-05-29T18:27:38+01:00
author: Robin Hermanussen
layout: post
background: '/img/bg-index.jpg'
guid: http://hermanussen.eu/sitecore/wordpress/?p=63
permalink: /2011/05/design-structure-matrix-dsm-for-your-content-tree/
redirect_from:
  - /sitecore/wordpress/2011/05/design-structure-matrix-dsm-for-your-content-tree/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - code snippets
---
A <a title="Introduction to DSM" href="https://dsmweb.org/introduction-to-dsm/">design structure matrix</a> (or dependency structure matrix) can help you to analyze the dependencies of your system and spot potential problems. This is especially useful when analyzing code, like you can do with the <a title=".NET Reflector" href="http://www.reflector.net/">.NET Reflector</a> Add-In you can find <a title="Dependency Structure Matrix PlugIn for .NET Reflector" href="http://tcdev.free.fr/">here</a>.

Since certain aspects of your system structure can also be derived from the Sitecore content tree, I thought it might be useful to make a DSM for that. The aspx at the end of this post can be used to analyze the dependencies in your content tree!

**An example of how this can be useful:**

Let&#8217;s say you have a multisite Sitecore environment that currently has 3 websites (A, B and C). Some parts of the websites are quite similar and developers have copied different items between the websites. Website B is (functionally) essentially a subsite of site A. You could say that website B &#8216;depends&#8217; on website A. And actually, since website A will have a link to site B, website A also depends on website B. Website C should be completely independent.

<img class="aligncenter" title="Image 1" src="/wp-content/uploads/dsm_1.png" alt="" width="167" height="389" /> 

Now, I have opened the DSM aspx. After selecting the master database, expanding all the relevant nodes and selecting the websites, I am now ready to create a DSM. After clicking the &#8220;Update DSM data&#8221; button, I can see the following:

<img class="alignnone" title="Image 2" src="/wp-content/uploads/dsm_2.png" alt="" width="212" height="121" /> 

From this matrix, I can see the following (start reading by choosing a row and then choose the cell; the numbers in the top row reference the items in the column on the left):

&#8211; Website A (or one of its descendants) has 1 link to website B (or one of its descendants).  
&#8211; Website B (or one of its descendants) has 3 link to website A (or one of its descendants).  
&#8211; Website C (or one of its descendants) has 1 link to website B (or one of its descendants).

That last one could be a problem! Website C should have no links to the other websites. This probably happened because I copied something from website B to website C and I forgot to change the link.

To see where the problem is exactly, I click on the table cell (coordinate: 1.3 Website C, 1.2). The information in the next image is displayed:

<img class="alignnone" title="Image 3" src="/wp-content/uploads/dsm_3.png" alt="" width="526" height="96" /> 

The menu configuration for website C references a page in website B, instead of a page in website C. After I correct this error, I click &#8220;Update DSM data&#8221; again. Now the matrix looks like this:

<img class="alignnone" title="Image 4" src="/wp-content/uploads/dsm_4.png" alt="" width="214" height="122" /> 

That&#8217;s better; Only websites A and B now have references to each other.

If I need a more detailed look, I can select anything that I think is relevant in the tree. So the aspx page could look like this:

[<img class="alignnone" title="Image 5" src="/wp-content/uploads/dsm_5.png" alt="" width="1225" height="515" />](/wp-content/uploads/dsm_5.png)

You have to get used to reading this type of matrix, but it can be a very useful tool. This example is obviously quite simple; more complex situations may be found in the &#8220;real world&#8221;.

The tool is not exclusively for solving problems. It can also be helpful for quickly understanding how a system is setup.

Just copy the following code to an aspx file and you&#8217;re ready to use the tool:

{% gist 3f58ba9c31d8652a59738d028b458e20 %}