---
id: 79
title: Sitecore Editor Android App
date: 2011-09-08T20:25:41+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=79
permalink: /2011/09/sitecore-editor-android-app/
redirect_from:
  - /sitecore/wordpress/2011/09/sitecore-editor-android-app/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore tips
---
As a former Java developer and Android phone owner, I wanted to try out some Android development. The Android platform is based on Java technology, so it wasn&#8217;t too hard to figure out. I got the idea to develop an alternative content editor for Sitecore.

It wasn&#8217;t too difficult to connect to Sitecore and do some basic actions like traversing the content tree, getting databases and getting item fields. I just used the standard Service.asmx (located in: /sitecore/shell/WebService/service.asmx). Using the ksoap2-android library for connecting to the service, I implemented the basic features.

The app is far from complete and has not been tested very thoroughly, but it does support the following features:

  * Log in to Sitecore using the login screen (the url and user name are saved for next time)
  * Choose what database you want to connect to (&#8216;master&#8217; would be the best option for most people)
  * Traverse the content tree by selecting the item to traverse into for each level in the content tree (displays the icons too)
  * Press items a little longer to popup a choice menu for other actions
  * Rename items
  * Edit the raw values of the items (language/version can be selected at the top)
  * Choose between viewing the standard Sitecore fields or not
  * The Sitecore path where you are will be displayed at the bottom of the screen
  * Tested on my Samsung Galaxy S II with Android 2.3, but it should work on Android 2.2+

<p style="text-align: left;">
  <img class="aligncenter" title="Login screen" src="http://hermanussen.eu/sitecore/SitecoreEditor/login_screen.png" alt="" width="246" height="406" /><img class="aligncenter" title="Traverse items screen" src="http://hermanussen.eu/sitecore/SitecoreEditor/traversal_screen.png" alt="" width="245" height="403" /><img class="aligncenter" title="Edit item screen" src="http://hermanussen.eu/sitecore/SitecoreEditor/edit_item_screen.png" alt="" width="244" height="405" />If this is to become a serious App to be used by content editors on the road, I think a lot more basic features will have to be added. Publishing/unpublishing, adding and deleting items, and having more than just raw value support would be the bare minimum. I welcome any feedback on this and I would like to know if people are seriously interested in this.
</p>

If you want to give it a go on your Android phone, then capture the following QR code on your phone or hit the image (it&#8217;s also a link) to download the App.

[<img class="aligncenter" title="Sitecore Editor Android App" src="https://chart.googleapis.com/chart?cht=qr&chs=300x300&chl=http%3A%2F%2Fhermanussen.eu%2Fsitecore%2FSitecoreEditor%2FSitecoreEditor.apk" alt="" width="300" height="300" />](http://hermanussen.eu/sitecore/SitecoreEditor/SitecoreEditor.apk)Please note that the app is not available on the Android Market. But all you need to do is change one setting to allow this. A very good explanation can be found <a title="Applications outside the Android Market" href="http://www.androidcentral.com/just-browsing-applications-outside-android-market" onclick="javascript:_gaq.push(['_trackEvent','outbound-article','http://www.androidcentral.com']);">here</a>.

Also, the CM server needs to be publically accessible, or your Android device should have access to the internal network (with the CM server on it) in order for the application to work. Otherwise, the App will not be able to connect to the webservice.