---
id: 271
title: Post content audit messages to Slack from Sitecore
date: 2015-12-13T23:18:52+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=271
permalink: /2015/12/post-content-audit-messages-to-slack-from-sitecore/
redirect_from:
  - /sitecore/wordpress/2015/12/post-content-audit-messages-to-slack-from-sitecore/
aktt_notify_twitter:
  - 'no'
categories:
  - sitecore modules
---
The Sitecore community has certainly <a title="Sitecore Slack" href="http://sitecorefun.baziret.com/2015/09/join-the-sitecore-chat/">embraced Slack</a>. If you want to join your fellow Sitecore developers, be sure to follow the <a title="Sitecore Slack" href="http://sitecorefun.baziret.com/2015/09/join-the-sitecore-chat/">link</a> and get it up and running. It&#8217;s great to see so many people from the community sharing knowledge about all things Sitecore in this awesome chat application.

We&#8217;ve been using Slack with our team internally at our company as well. And we love having great integrations with our build server, JIRA, Pingdom, Sentry and others (some of which are custom built).

It was about time that we helped our content editors out by providing an integration with Sitecore itself. That&#8217;s why I built <a title="Sitecore.Slack.IncomingWebhookForEvents on GitHub" href="https://github.com/hermanussen/Sitecore.Slack.IncomingWebhookForEvents">the Sitecore.Slack.IncomingWebhookForEvents module</a>. Whenever someone edits a content item, publishes or installs a package, others will know about it through Slack!

[<img class="aligncenter size-full wp-image-273" title="slack_integration_example" src="/wp-content/uploads/2015/12/slack_integration_example.png" alt="" width="1062" height="498" srcset="/wp-content/uploads/2015/12/slack_integration_example.png 1062w, /wp-content/uploads/2015/12/slack_integration_example-300x140.png 300w, /wp-content/uploads/2015/12/slack_integration_example-1024x480.png 1024w" sizes="(max-width: 1062px) 100vw, 1062px" />](/wp-content/uploads/2015/12/slack_integration_example.png)

Follow the <a title="Instructions on module GitHub page" href="https://github.com/hermanussen/Sitecore.Slack.IncomingWebhookForEvents#sitecoreslackincomingwebhookforevents">instructions on the GitHub page</a> to install this module (using NuGet) for your project.