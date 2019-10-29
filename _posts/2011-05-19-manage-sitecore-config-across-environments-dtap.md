---
id: 56
title: Manage Sitecore config across environments (DTAP)
date: 2011-05-19T07:24:27+01:00
author: Robin Hermanussen
layout: post
guid: http://hermanussen.eu/sitecore/wordpress/?p=56
permalink: /2011/05/manage-sitecore-config-across-environments-dtap/
redirect_from:
  - /sitecore/wordpress/2011/05/manage-sitecore-config-across-environments-dtap/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - sitecore tips
---
Managing different Sitecore environments can be quite cumbersome. One of the things that I think is annoying is managing the configuration. In my Web.config alone, I currently have 2910 lines of Sitecore configuration, excluding the different configuration files in App_Config! I&#8217;m sure others have found this annoying as well. Here&#8217;s a way of making things a lot easier.

**Disclaimer: by no means do I claim that this is the best way of doing this. If you know a better way, then please let me know!**

<span style="text-decoration: underline;">The problem:</span>

The problem is not that we have a lot of configuration; that is actually a good thing! But when you have separate environments, like in a <a title="Wikipedia article about DTAP" href="http://en.wikipedia.org/wiki/Development,_testing,_acceptance_and_production">DTAP</a> (Development, Testing, Acceptance and Production) setup, small changes to the configuration for each environment may be required. Here are a few suggestions for possible differences:

  * Different connectionstrings
  * Different dataFolder, mediaFolder, tempFolder
  * Different cache sizes
  * Different Sitecore databases for websites (in development, it can be helpful to work on the master database directly)

If you copy all the config files when deploying to a different environment, you will have to go through all of the configuration to make the environment specific changes. And if you do not copy all the config files, you will have to make all the normal changes (that are not environment specific) by hand. Chances are, you may forget something in both cases.

<span style="text-decoration: underline;">A solution that we have used in the past:</span>

We have made a folder structure containing the Web.config, ConnectionStrings.config and any other config file that contains environment specific settings for each environment. It looked similar to this:  
> Web.config (development version can be in the original location)  
> App_Config  
>> ConnectionStrings.config  
> TEST  
>> Web.config  
>> App_Config  
>>> ConnectionStrings.config  
> ACC  
&#8230;

This appears to be better, because you know exactly what you need to include in your deployment. But with this approach, you rely on all the developers for keeping everything consistent; if someone makes a change to the DEV version of a config file and forgets to make the same changes for the other environments, the whole thing breaks.

Moreover, if you want to check the consistency between the different files, you will have to wade through these huge config files. A good diff tool like <a title="WinMerge website" href="http://winmerge.org/">WinMerge</a> can only go so far in helping you with this.

<span style="text-decoration: underline;">A better solution:</span>

I really would like to have only the differences between the environments in separate files. So the file structure as mentioned before is useful only if:

  * Only the Web.config file is used. No other config files please!
  * The Web.config needs to be as small as possible, containing only the environment specific Sitecore settings.

Luckily, putting all the Sitecore config in a separate file is quite easy. I made a new config file under App_Config called Sitecore.config and I copied the entire <sitecore /> section into it. Then I made the Web.config point to it, like this:  


That cleans up the Web.config nicely! Why not externalize everything in the Web.config? Well, because the other configuration can be implemented differently (it is not specific to Sitecore) and may rely on the configuration being specified in the Web.config. Furthermore, the Web.config may be changed by IIS Manager. Be aware of this!

<span style="text-decoration: underline;">Environment specific settings:</span>

But this still does not solve our problem, because now we would need different versions of Sitecore.config for each environment. This would give us the same problems.

Again, Sitecore has a nice built in solution for this problem. The differences between the environments will mostly be references to file paths, urls or arbitrary strings. So all we really need in most cases is a simple text replace. Sitecore uses the <sc.variable />  element for this.

So let&#8217;s move some variables that were copied to the Sitecore.config back to the Web.config first.



Now we have a nice base to work from.

<span style="text-decoration: underline;">The ConnectionStrings.config:</span>

The connection strings are not in the <sitecore /> section. So we need a way to include them in the Web.config. Turns out, this is pretty easy. However, **I must warn you here**: I did see something that worried me with <a title=".NET Reflector website" href="http://reflector.red-gate.com/">.NET Reflector</a> in ConfigModifier.dll, so I&#8217;m not sure that this solution will never break. It appears to read the connection strings directly from the App_Config/ConnectionStrings.config path. I may be mistaken, and I&#8217;ve had no problems with it so far. But if you want to be sure, then skip this step for now.

Change the connectionStrings section in your Web.config file, like this:  


Don&#8217;t forget to remove the original ConnectionStrings.config file to avoid confusion.

<span style="text-decoration: underline;">Specifying differences:</span>

From now on, if you want to make something environment specific, you do the following:

  1. Replace the string in Sitecore.Config with a meaningful variable, for example  
    
  2. Then add a <sc.variable /> element to the Web.config for each environment (or only do it for DEV and use a diff tool before the deployment to see what you need to change)  
    

Here is a simple example of what your <sitecore /> section may look like for one environment in particular:



<span style="text-decoration: underline;">Checking configuration:</span>

So there you have it. An easier way of managing configuration across multiple environments. This way, you can always just Copy the App_Config folder and quickly identify differences between environments by comparing the cleaned up Web.config files.

Finally, I&#8217;d like to point out an easy way to check the current configuration of a Sitecore website. This allows you to see if your configuration changes worked out correctly. Go to this location on your site: /sitecore/admin/ShowConfig.aspx.