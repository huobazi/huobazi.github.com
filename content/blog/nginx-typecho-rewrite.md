---
layout: post
title: nginx下typecho的rewrite
comments: true
date: 2009-07-09
categories:
- LAMP
- Typecho
- LAMP
- nginx
- Rewirte
- 代码片段
---

<p>导数据到typecho的时候是在localhost的windows xp系统上用的apache,部署时用的是nginx<br />先是发现无法登陆按照<a href="http://forum.typecho.org/viewtopic.php?f=4&amp;t=238&amp;p=852&amp;hilit=nginx#p852" target="_blank">这篇帖子</a>内的方法配置了vhost.conf，发现可以登陆了，接着又出现了<br />无法编辑post的问题，具体症状见<a href="http://forum.typecho.org/viewtopic.php?f=4&amp;t=270" target="_blank">这篇帖子</a>,甚是郁闷啊，google+baidu 找到一片描写wp的<br />rewrite的<a href="http://hi.baidu.com/3322/blog/item/95d254e7594a012bb93820bb.html" target="_blank">帖子</a>,因typecho与wp笔记像，抱着试试看的想法,在测试站点试验了一下，嘿嘿<br />能用，转寄在此，备忘</p>
<p><!--more--></p>
<pre>
location / {
        index index.html index.php;
        if (-f $request_filename/index.html){
            rewrite (.*) $1/index.html break;
        }
        if (-f $request_filename/index.php){
            rewrite (.*) $1/index.php;
        }
        if (!-f $request_filename){
            rewrite (.*) /index.php;
        }
    }
</pre>
<p>同时感谢<a class="titlink" title="Atrhis的空间 http://hi.baidu.com/3322" href="http://huobazi.aspxboy.com/3322">Atlantis</a>  :-)</p>				
