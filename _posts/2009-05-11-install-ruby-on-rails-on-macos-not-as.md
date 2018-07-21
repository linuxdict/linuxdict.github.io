---
id: 316
title: Install Ruby On Rails on MacOS as common user
date: 2009-05-11T21:16:16+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=316
permalink: /2009-05-install-ruby-on-rails-on-macos-not-as/
bttc_cache:
  - 1273330855:0
  - 1273330855:0
categories:
  - Linux_D
tags:
  - mac
  - ruby
---
Install Ruby On Rails on MacOS ( not as admin user )

1. install ruby

get the ruby sources from the ruby-lang.org, we take ruby-1.8.6-p368.tar.bz2 for e.g.
  
tar xvf ruby-1.8.6-p368.tar.bz2 && cd ruby-1.8.6-p368
  
./configure &#8211;prefix=/User/yourname/ruby && make && make install

2.set the enviorment
  
edit the ~/.bash_profile, change the PATH=/User/yourname/ruby/bin:$PATH
  
source ~/.bash_profile and u can check by command: ruby -v

3. install gems
  
get the gems from rubyforge.org , we take rubygems-1.3.3.tgz for e.g.
  
tar xvf rubygems-1.3.3.tgz && cd rubygems
  
ruby setup.rb
  
<!--more-->

4. install rails and other extension
  
gem install rail -v 1.2.5

5. mysql extension installation notes
  
get mysql from www.mysql.com, we recommand to use mysql-5.1.34-osx10.5-x86.dmg
  
http://dev.mysql.com/get/Downloads/MySQL-5.1/mysql-5.1.34-osx10.5-x86.dmg/from/p ick
  
get the contents:
  
mv ~/mysql-5.1.34-linux-i686-glibc23 ~/mysql
  
gem install mysql -v 2.7
  
it will show some errors:

Building native extensions. This could take a while&#8230;
  
ERROR: Error installing mysql:
      
ERROR: Failed to build gem native extension.

/Users/wugang/ruby//bin/ruby extconf.rb
  
checking for mysql_query() in -lmysqlclient&#8230; no
  
&#8230;.
  
checking for main() in -lnsl&#8230; no
  
checking for mysql_query() in -lmysqlclient&#8230; no

Gem files will remain installed in /Users/username/ruby/lib/ruby/gems/1.8/gems/mysql-2.7 for inspection.

cd /Users/username/ruby/lib/ruby/gems/1.8/gems/mysql-2.7
  
edit the extconf.rb
  
delete some unsupported lib such as -lcrypto .
  
ruby extconf.rb &#8211;with-mysql-lib=~/mysql/lib &#8211;with-mysql-include=~/mysql/include &#8211;with-mysql-config=~/mysql/bin/mysql_config
  
make && make install

it works.
  
Note: change PATH enviorment in the ~/.bash_profile