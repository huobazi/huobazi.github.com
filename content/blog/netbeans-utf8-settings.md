---
layout: post
title: 调整netbeans6.5设置使之默认使用utf-8存储文件
comments: true
date: 2009-08-19
tags:
- LAMP
- netbeans
- utf-8
---

<p>netbeans默认使用ANSI存储的，我们一般希望它采用utf-8来存储，按照如下方法可以实现这个要求</p>
<p>1)  找到你的Netbeans安装目录下的etc文件夹,如D:\Program Files\NetBeans 6.5\etc<br />2)  用文本编辑器打开netbeans.conf<br />3)  找到netbeans_default_options这一句(注意#号开头的行的是注释)<br />4)  在最后面加上一个空格,再加入-J-Dfile.encoding=UTF-8</p>
<p>如我现在的设置:</p>
<p><!--more--></p>
<pre># ${HOME} will be replaced by JVM user.home system property
netbeans_default_userdir="${HOME}/.netbeans/6.5"

# Options used by NetBeans launcher by default, can be overridden by explicit
# command line switches:
netbeans_default_options="-J-client -J-Xverify:none -J-Xss2m -J-Xms32m -J-XX:PermSize=32m -J-XX:MaxPermSize=200m -J-Dapple.laf.useScreenMenuBar=true -J-Dsun.java2d.noddraw=true -J-Dfile.encoding=UTF-8"
# Note that a default -Xmx is selected for you automatically.
# You can find this value in var/log/messages.log file in your userdir.
# The automatically selected value can be overridden by specifying -J-Xmx here
# or on the command line.

# If you specify the heap size (-Xmx) explicitely, you may also want to enable
# Concurrent Mark &amp; Sweep garbage collector. In such case add the following
# options to the netbeans_default_options:
# -J-XX:+UseConcMarkSweepGC -J-XX:+CMSClassUnloadingEnabled -J-XX:+CMSPermGenSweepingEnabled
# (see http://wiki.netbeans.org/wiki/view/FaqGCPauses)

# Default location of JDK, can be overridden by using --jdkhome &lt;dir&gt;:
netbeans_jdkhome="C:\Program Files\Java\jre6"

# Additional module clusters, using ${path.separator} (';' on Windows or ':' on Unix):
#netbeans_extraclusters="/absolute/path/to/cluster1:/absolute/path/to/cluster2"

# If you have some problems with detect of proxy settings, you may want to enable
# detect the proxy settings provided by JDK5 or higher.
# In such case add -J-Djava.net.useSystemProxies=true to the netbeans_default_options.</pre>				
