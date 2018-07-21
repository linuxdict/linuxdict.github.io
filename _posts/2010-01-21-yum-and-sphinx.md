---
id: 486
title: Yum and Sphinx
date: 2010-01-21T23:54:09+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=486
permalink: /2010-01-yum-and-sphinx/
bttc_cache:
  - 1273362106:0
  - 1273362106:0
categories:
  - Howto
---
When run yum search xxx, got the following Error
  
Error Value: database disk image is malformed

A: run the following commands as &#8216;root&#8217; and one by one
  
yum clean metadata
  
yum clean dbcache
  
yum makecache

Sphinx search for wiki /opt/sphinx/etc/sphinx.conf (my e.g.)

`<!--more--> source src1<br />
{<br />
type					= mysql<br />
sql_host				= localhost<br />
sql_user				= wiki1<br />
sql_pass				= wikipass<br />
sql_db					= mediawiki<br />
sql_query	= SELECT page_id, page_title, page_namespace, old_id, old_text \<br />
FROM mywiki_page,mywiki_revision,mywiki_text \<br />
WHERE rev_id=page_latest AND old_id=rev_text_id<br />
sql_attr_uint			= page_namespace<br />
sql_attr_uint			= old_id<br />
sql_attr_timestamp		= date_added`

 ``

 `sql_ranged_throttle	= 0<br />
sql_query_info		= SELECT * FROM GL_text WHERE old_id=$id<br />
}<br />
source src1throttled : src1<br />
{<br />
sql_ranged_throttle			= 100<br />
}<br />
index wikipedia<br />
{<br />
source			= src1<br />
path			= /opt/sphinx/var/data/wikipedia<br />
docinfo			= extern<br />
mlock			= 0<br />
morphology		= none<br />
min_word_len		= 1<br />
charset_type		= sbcs<br />
html_strip				= 0<br />
}<br />
index wikipediastemmed : wikipedia<br />
{<br />
path			= /opt/sphinx/var/data/wikipediastemmed<br />
morphology		= stem_en<br />
}<br />
indexer<br />
{<br />
mem_limit			= 512M<br />
}<br />
searchd<br />
{<br />
log					= /opt/sphinx/var/log/searchd.log<br />
query_log			= /opt/sphinx/var/log/query.log<br />
read_timeout		= 5<br />
client_timeout		= 300<br />
max_children		= 30<br />
pid_file			= /opt/sphinx/var/log/searchd.pid<br />
max_matches			= 1000<br />
seamless_rotate		= 1<br />
preopen_indexes		= 0<br />
unlink_old			= 1<br />
mva_updates_pool	= 1M<br />
max_packet_size		= 8M<br />
max_filters			= 256<br />
max_filter_values	= 4096<br />
}<br />
`