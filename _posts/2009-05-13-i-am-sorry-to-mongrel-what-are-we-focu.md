---
id: 322
title: I am sorry to mongrel !
date: 2009-05-13T21:50:09+00:00
author: edyliu
layout: post
guid: http://www.enlamp.cn/?p=322
permalink: /2009-05-i-am-sorry-to-mongrel-what-are-we-focu/
bttc_cache:
  - 1273330855:0
  - 1273330855:0
categories:
  - Linux_D
tags:
  - ruby
  - server
---
I am sorry to mongrel ! What are we focuse on, Mongrel ?

Mongrel V.S. Passenger

just forget about Mongrel, and to know why ?
  
<!--more-->

ab -n 200 -c 100 http://192.168.0.82/
  
This is ApacheBench, Version 2.0.40-dev <$Revision: 1.146 $> apache-2.0
  
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
  
Copyright 2006 The Apache Software Foundation, http://www.apache.org/

Benchmarking 192.168.0.82 (be patient)
  
Completed 100 requests
  
Finished 200 requests

Server Software: Apache
  
Server Hostname: 192.168.0.82
  
Server Port: 80

Document Path: /
  
Document Length: 11748 bytes

Concurrency Level: 100
  
Time taken for tests: 3.17178 seconds
  
Complete requests: 200
  
Failed requests: 0
  
Write errors: 0
  
Total transferred: 2432000 bytes
  
HTML transferred: 2349600 bytes
  
Requests per second: 66.29 \[#/sec\] (mean)
  
Time per request: 1508.589 \[ms\] (mean)
  
Time per request: 15.086 \[ms\] (mean, across all concurrent requests)
  
Transfer rate: 787.16 [Kbytes/sec] received

Connection Times (ms)
                
min mean[+/-sd] median max
  
Connect: 0 94 512.6 2 3002
  
Processing: 4 134 48.2 143 205
  
Waiting: 3 132 48.4 142 203
  
Total: 17 229 492.3 146 3016

Percentage of the requests served within a certain time (ms)
    
50% 146
    
66% 173
    
75% 182
    
80% 184
    
90% 195
    
95% 215
    
98% 3010
    
99% 3013
   
100% 3016 (longest request)
  
[liuyongbing@centos53-edy bench]$ ab -n 200 -c 100 http://192.168.0.82:3000/
  
This is ApacheBench, Version 2.0.40-dev <$Revision: 1.146 $> apache-2.0
  
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
  
Copyright 2006 The Apache Software Foundation, http://www.apache.org/

Benchmarking 192.168.0.82 (be patient)

Completed 100 requests
  
Finished 200 requests

Server Software: Mongrel
  
Server Hostname: 192.168.0.82
  
Server Port: 3000

Document Path: /
  
Document Length: 11753 bytes

Concurrency Level: 100
  
Time taken for tests: 653.648753 seconds
  
Complete requests: 200
  
Failed requests: 32
     
(Connect: 0, Length: 32, Exceptions: 0)
  
Write errors: 0
  
Total transferred: 2407324 bytes
  
HTML transferred: 2350524 bytes
  
Requests per second: 0.31 \[#/sec\] (mean)
  
Time per request: 326824.371 \[ms\] (mean)
  
Time per request: 3268.244 \[ms\] (mean, across all concurrent requests)
  
Transfer rate: 3.60 [Kbytes/sec] received

Connection Times (ms)
                
min mean[+/-sd] median max
  
Connect: 0 5 7.1 1 21
  
Processing: 3285 240674 109397.6 305188 348438
  
Waiting: 3280 240664 109412.3 305187 348438
  
Total: 3286 240679 109395.7 305193 348438

Percentage of the requests served within a certain time (ms)
    
50% 305193
    
66% 325296
    
75% 333312
    
80% 336730
    
90% 339973
    
95% 344862
    
98% 347617
    
99% 348392
   
100% 348438 (longest request)