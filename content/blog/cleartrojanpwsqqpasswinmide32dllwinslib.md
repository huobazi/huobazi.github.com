---
layout: post
title: 记Trojan.PWS.QQPass,winmide32.dll,wins.lib的清除
comments: true
date: 2006-03-08
tags:
- 闲言碎语
---

<p>机器中标，竟然有提示您的QQ已在别处登陆，亏得俺是QQ会员，不一会儿手机收到藤讯短信<br />提示QQ密码被修改，随发个“16”回去，取回密码，在打开QQ准备登陆时，<br />诺顿报警如下：<br /><font color="#0000ff" size="2">扫描类型： 实时防护 扫描<br />事件： 已发现病毒！<br />病毒名称: Trojan.PWS.QQPass<br />文件： C:\WINDOWS\system32\winmide32.dll<br />位置：C:\WINDOWS\system32<br />计算机：WUMEIBO<br />用户：武眉博<br />采用的操作：清除 失败 : 删除 失败 : 拒绝访问<br />发现的日期： 2006年3月8日  13:31:48</font></p>
<br /><p><font color="#0000ff" size="2">扫描类型： 实时防护 扫描<br />事件： 已发现病毒！<br />病毒名称: Trojan.PWS.QQPass<br />文件： C:\WINDOWS\system32\wins\wins.lib<br />位置：C:\WINDOWS\system32\wins<br />计算机：WUMEIBO<br />用户：武眉博<br />采用的操作：清除 失败 : 删除 失败 : 拒绝访问<br />发现的日期： 2006年3月8日  13:59:57<br /></font>Google , Baidu 找到一堆“Trojan.PWS.QQPass”的信息，然而都不是我机器上这2个文件。<br />进入32目录试图，手工删除，提示 磁盘保护云云... 删除不掉。<br />在注册表内搜索“winmide32.dll”有两个键值，删除，再搜，又回来了，再删，再搜，又回来<br />技穷，只好重启，F8，命令行安全模式。<br />进入32目录<br />attrib -s winmide32.dll<br />del winmide32.dll<br />进入wins目录<br />attrib -s wins.lib<br />del wins.lib<br />重新启动，Win+Run+Regedit 搜索winmide32.dll，删除两个键值。<br />重新启动，32目录，wins目录均无原来那2文件，注册表内也F3不到它们了。</p>
<br /><p>运行QQ，登陆窗口输入密码的时候诺顿再不报警。登陆成功。</p>
<br /><p>不知道是否彻底清除，观察几天。先写这些，如有异样，随时更新。 </p>				
