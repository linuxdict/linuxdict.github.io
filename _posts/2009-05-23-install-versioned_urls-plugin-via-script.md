---
id: 328
title: Install versioned_urls plugin
date: 2009-05-23T08:37:30+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=328
permalink: /2009-05-install-versioned_urls-plugin-via-script/
bttc_cache:
  - 1273330854:0
  - 1273330854:0
categories:
  - linux
  - Linux_D
tags:
  - ruby
  - server
  - tips
---
Install versioned_urls plugin via
  
script/plugin install http://svn.lingr.com/plugins/versioned_urls

Add appropriate rewriting and cache-header-pushing configuration to your web servers, e.g., for lightty:
  
url.rewrite-once = ( &#8220;^/(.*.(css|js|gif|png|jpg)).v[0-9.]+$&#8221; => &#8220;/$1&#8221; )
  
expire.url = ( &#8220;/stylesheets/&#8221; => &#8220;access 10 years&#8221; ,
                            
&#8220;/javascripts/&#8221; => &#8220;access 10 years&#8221;,
                            
&#8220;/images/&#8221; => &#8220;access 10 years&#8221; )

More details
  
http://blog.dannyburkes.com/2006/11/2/versioned-urls-for-rails/