---
layout: post
title: Vs2005的倒退?
comments: true
date: 2006-05-04 14:23
categories:
- ASP.NET
- Visual Studio
---

<p>String abc = 123.ToString;<br /><br />代码在Vs2003内编译将得到错误信息<br /><br /><font color="#0000ff">“<font size="2">在不带括号的情况下引用了方法.....</font>”</font><br /><br />在Vs2005（8.050727.42 /rtm 50727 4200）内编译则得到错误信息:<br /><br /><font color="#ff1493">“无法将方法组“ToString”转换为非委托类型“string”。您是要调用方法吗?”<br /></font><br />而上边代码等号右边的部分如果位于一个方法内做参数，那将得到一个错误信息：<br /><br /><font color="#ff1493">参数“1”: 无法从“方法组”转换为“string”<br /></font><br />语气上更加亲切了，比如多了个“您”字，可是语意上却更加看不懂了....</p>				
