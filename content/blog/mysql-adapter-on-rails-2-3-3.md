---
layout: post
title: Mysql adapter on Rails 2.3.3
comments: true
date: 2009-08-29
categories:
- LAMP
- Rails
- 奇技淫巧
- Mysql
- RoR
---

<p>安装好Ruby on Rails 2.3.3后，运行简单的页面提示如下错误“<span style="color: #ff0000;"><strong>The bundled mysql.rb driver has been removed from Rails 2.2. Please install the mysql gem and try again: gem install mysql”</strong></span></p>
<p> gem 了n次也不成，搞了一早上，才google到一个比较山寨的方法解决</p>
<pre>1.  download older MySQL client library, for example one from InstantRails: http://instantrails.rubyforge.org/svn/trunk/InstantRails-win/InstantRails/mysql/bin/libmySQL.dll

2.  copy the downloaded file to C:\Ruby\bin (or wherever you installed Ruby) 

3. restart MySQL server</pre>
<p>另参考：<a href="http://www.ruby-forum.com/topic/160358">http://www.ruby-forum.com/topic/160358</a>和<a href="http://rdc.taobao.com/blog/qa/?p=523">http://rdc.taobao.com/blog/qa/?p=523</a></p>				
