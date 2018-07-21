---
id: 311
title: 'ruby &#038; gems  gem install extension_name'
date: 2009-05-04T00:00:53+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=311
permalink: /2009-05-ruby-gems-gem-install-extension_name/
bttc_cache:
  - 1273358472:0
categories:
  - Linux_D
tags:
  - tips
---
ruby & gems

gem install extension_name -v version
  
gem uninstall extension_name -v version

I met a problem when I install the mysql
  
it&#8217;s caused by the mysql extension search /usr/local for mysql develop files
  
ln -s /usr/include/mysql /usr/local/include/
  
ln -s /usr/lib/mysql /usr/local/lib/

when I started the app that created with ruby
  
it show the warning:
  
boot.rb:20:Warning: Gem::SourceIndex#search support for String patterns is deprecated

we can change the boot.rb on line 20
  
rails\_gem = Gem.cache.search(&#8216;rails&#8217;, &#8220;=#{rails\_gem\_version}.0&#8221;).sort\_by { |g| g.version.version }.last
  
&#8220;Gem.cache.search&#8221;, just replace &#8220;search&#8221; with &#8220;find_name&#8221;.
  
or changed into
  
rails\_gem = Gem.cache.search(Gem::Dependency.new(‘rails’,“~>#{version}.0”)).sort\_by { |g| g.version.version }.last