---
layout: post
title: DataGrid点击删除按钮弹出确认对话框一个好办法
comments: true
date: 2004-04-05
tags:
- ASP.NET
- Asp.net
- 代码片段
---

<p><font color="#3366cc"><strong>原文地址<br /><a href="http://expert.csdn.net/Expert/topic/2852/2852126.xml?temp=.4770471">http://expert.csdn.net/Expert/topic/2852/2852126.xml?temp=.4770471</a> <br /></strong></font><font color="#3366cc"><strong>其中<br />wf5360308(峰)</strong></font>提供的方法<br />datagrid-》属性生成器-》列-》添加按钮列-》删除-》文本(T)-&gt;在文本框里加上：<br />&lt;div id="de" onclick="JavaScript:return confirm('确定删除吗？')"&gt;删除&lt;/div&gt;<br /><br />不错的办法哦～<br /></p>				
