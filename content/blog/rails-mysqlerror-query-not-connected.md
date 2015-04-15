---
layout: post
title: 'rails里Mysql::Error: query: not connected'
comments: true
date: 2010-01-15
categories:
- LAMP
- 闲言碎语
- Rails
- Mysql
---

<p>从ubuntu换回了win7后又慢慢开始折腾以前在本本上跑的一些LAMP网站， php和 mysql还是用以前的xampp里的，仍然可以用。</p>
<p>重装了 ruby 1.8.6, rails 2.3.5 等...发现运行rails网站，弹出messagebox提示找不到libmysql.dll尝试把mysql/bin里的dll来regsvr32，不可，直接拷贝到system32目录下错误没了，但打开网站仍然报错，终端显示“Mysql::Error: query: not connected...."</p>
<p><!--more--></p>
<p>google来了结果</p>
<p><a href="http://topic.csdn.net/u/20090823/12/2775f2e7-a73a-45b3-a047-5ed9330871cd.html" target="_blank">http://topic.csdn.net/u/20090823/12/2775f2e7-a73a-45b3-a047-5ed9330871cd.html</a></p>
<p><a href="http://xiaolife.com/wordpress/rails-2-3-dbmigrate-issue-with-mysql-5-1-3/" target="_blank">http://xiaolife.com/wordpress/rails-2-3-dbmigrate-issue-with-mysql-5-1-3/</a></p>
<p>猛然间想起来这些个问题上次玩的时候也出现过，真晕，还是写下来，希望SY一遍胜过脑子记忆千遍吧</p>				
