---
layout: post
title: 不改程序, 创建同一个程序不同服务名的方法
comments: true
date: 2009-08-06
categories:
- .Net其他
- C#
- Windows
- Service
- 批处理
---

<p>以往写windows service都需要个ProjectInstaller和serviceInstaller并配置serviceName，这样build出来的exe在install成windows service时我们会：</p>
<pre>@echo 安装WindowService
@Set Path=C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727;
@Set svn_dir=%cd%
installutil %svn_dir%\MyServiceDemo.exe
pause
@echo 成功！</pre>
<p>但服务名被我们编译在程序里了，如果这个exe想被装很多次服务怎么办呢？<br />今天从同事Martin Jia那里学来一个好方法，可以不用ProjectInstaller、serviceInstaller这种东西，直接安装exe为windows service并在安装时指定服务名称</p>
<p><!--more--></p>
<p>安装服务：</p>
<pre>sc create 服务名 binpath= "路径" displayname= "显示名"</pre>
<p>卸载服务</p>
<pre>sc delete 服务名</pre>				
