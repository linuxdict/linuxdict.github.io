---
id: 443
title: Use Google Js API or YUI if u can
date: 2009-07-31T01:39:07+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=443
permalink: /2009-07-use-google-js-api-or-yui-if-u-can/
bttc_cache:
  - 1273344708:0
  - 1273344708:0
categories:
  - LAMP
tags:
  - LAMP
  - linux
  - tips
---
at the title, benefits in short
  
1. the Google use CDN, so the clients can browser faster than your own server.
  
2. use it can save ur bandwidth and network usage
  
3. Increases Number Of Parallel Downloads

but in China, maybe not well enough, because the Google is f**ked sometimes.

Refer:<!--more-->


  
http://codefusionlab.blogspot.com/2009/07/offloading-all-js-files-to-google.html

Offloading ALL JS Files To Google

If you didn’t know it already, Google provides an API which you can use to call Javascript libraries hosted on their server for you to use on your website. Google currently provides the following Javascript Libraries from their server:

* jQuery
  
* jQuery UI
  
* Prototype
  
* script.aculo.us
  
* MooTools
  
* Dojo
  
* SWFObject
  
* Yahoo! User Interface Library (YUI)
  
* Ext Core
  
* More to be added, if not already present

Now, you might ask why would you want to let Google host your Javascript files instead of yourself. To let make you have a better idea of what Google’s AJAX Library API is about, you’re recommended to watchthis video:

Let me provide you with some rock solid reasons why you need to let Google host your files.

Google’s CDN Is Faster Than Your Host
  
No matter how good your web hosting package is, it just cannot beat Google’s CDN (Content Distribution Network). Google runs many servers and has servers in many countries which mirror data across the globe. When downloading static data from Google, the underlying architecture automatically detects the geographically closest server and download the files from there. This simple action drastically reduces the time needed for your files to download. Using a CDN is recommended by Yahoo! Exceptional Performance Rules.

Increases Number Of Parallel Downloads
  
According to the HTLM 1.1 specification, which most modern browsers obey, only two parallel downloads can be done from a single hostname. Therefore if you use Google for your hosting, you maximize your parallel download performance, since you will have another hostname (google.com) serving files.

Better Caching
  
Now, suppose many persons are using Google’s AJAX Library API to power their websites, and you are using it too. If your visitors come to visit your website after visiting another website using Google’s AJAX Library API, then the Javascript file will still be in your cache and if it has not been changed, your visitors’ browsers might not even need to download the file(s).

Save Bandwidth
  
Finally, you also get to save some of your bandwidth, thus saving you money. If you are on a budget hosting plan, then this might be helpful in cutting down costs and relieving your server of stress.

Calling The AJAX Library On Your Website
  
To insert the AJAX Library in your website, you have 2 ways of calling it. Either you use the google.load() approach which goes this way:
  
Google AJAX Library API Load

Then you have the more direct way of calling the library, using the following piece of code:
  
Google AJAX Library API Load Simple Way

Now, the above method, using the Google AJAX Library API, enables you call javascript libraries which are already present on Google servers.