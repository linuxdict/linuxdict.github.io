---
id: 600
title: Installing Perl modules
date: 2010-10-30T17:26:16+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=600
permalink: /2010-10-installing-perl-modules/
categories:
  - Howto
tags:
  - perl
  - tips
---
Perl modules may be installed using the CPAN module or from source.
  
CPAN method
  
perl -MCPAN -e shell (to get an interactive CPAN shell)
  
perl -MCPAN -e &#8216;install Time::JulianDay&#8217; (if you know the name of the module, you can install it directly without interacting with the CPAN shell)

Manually install from source
  
1. Download the Perl module from CPAN or other site.
  
2. Extract the tarball.
  
3. Run perl Makefile.PL
  
4. Run make
  
5. Run make test (optional)
  
6. Run make install
  
<!--more-->


  
Within the CPAN shell:
  
i /expression/ will search for a Perl module containing expression, and
  
install module will install the module.

Example:
  
perl -MCPAN -e shell
  
i /JulianDay/
  
install Time::JulianDay

Note: if you are behind a firewall, you may wish to use passive FTP with Perl&#8217;s Net::FTP module. Set the environment variable FTP_PASSIVE 1 (or any non-zero value) to use passive FTP when downloading Perl modules through CPAN.

Manual installation

To manually install a Perl module:

1. Download the Perl module from CPAN or other site.
  
2. Extract the tarball.
  
3. Run perl Makefile.PL
  
4. Run make
  
5. Run make test
  
6. Run make install

Note: you should use the same compiler to build Perl modules that you used to build Perl. For example, if you are building Perl modules with gcc and are using a version of Perl that was supplied with your distribution (ex. Solaris 8 includes Perl 5.005_03), you may run into errors.

Example: building Perl DBI with gcc on Solaris 8 system with Perl 5.005 (part of the Solaris 8 release).

cc: unrecognized option \`-KPIC&#8217;
  
cc: language depend not recognized

The Makefile for Perl modules is created using flags for SUNWspro (the compiler used to build Perl 5.005 for the Solaris 8 release), not gcc. As a workaround, you could build Perl from source using the gcc compiler, or obtain a packaged version of Perl that is built with gcc, such as those at Sunfreeware. This comp.lang.perl.modules post has more information.
  
Checking for existence of a Perl module
  
An easy way to check for the existence of a Perl module on your system (technically, in Perl&#8217;s @INC array, a list of directories Perl searches when attempting to load modules) is to run perl -e &#8216;use module;&#8217;

Example:

perl -e &#8216;use HTML::Parser;&#8217;

If nothing is returned, Perl was able to locate the module. Otherwise, you will see Can&#8217;t locate HTML/Parser.pm in @INC.

Source from: http://www.brandonhutchinson.com/installing\_perl\_modules.html