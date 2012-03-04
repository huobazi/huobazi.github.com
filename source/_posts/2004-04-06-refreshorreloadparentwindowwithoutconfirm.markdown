---
layout: post
title: 弹出窗口刷新它的父页面后。出现不重新发送信息，则无法刷新网页
comments: true
date: 2004-04-06 17:04
categories:
- ASP.NET
- Asp.net
- 奇技淫巧
---

<p>做的东西弹出一个窗口处理某些动作后刷新父窗口<br />用<br />window.opener.location.reload();<br />刷新<br />如果父窗口在此之前如果有过提交数据的动作，则会出现这么个讨厌的对话筐<br />“不重新发送信息，则无法刷新网页”<br />痛苦......<br />CSDN搜索未果(有几贴都是用Response.Redirect的方法，但我这里是刷父窗口)。<br />痛苦.<br />........<br />翻我的<a href="http://www.aspxboy.com/private/showthread.asp?threadid=148"><strike>小本本</strike></a> 后找到办法<br />用<br />window.opener.location.href=window.opener.location.href<br />去刷新（其实是重定位了一下）父窗口<br />可行。<br />总结： <font style="BACKGROUND-COLOR: #ee82ee">不能一棵树上掉死</font> :P</p>				
