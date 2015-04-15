---
layout: post
title: python的对象驻留
comments: true
date: 2009-08-21
tags:
- LAMP
- python
- 对象驻留
- 字符串驻留
---

<p>在C#中为了提高性能使用了<a title="字符串驻留" href="http://www.google.com.sg/search?hl=zh-CN&amp;source=hp&amp;q=string+interning&amp;aq=f&amp;oq=" target="_blank">字符串驻留技术</a>，而在Python中不光是字符串，连整数都有使用类似的驻留技术哦，看下面的测试：</p>
<pre>C:\Documents and Settings\Marble Wu&gt;python
Python 2.6.2 (r262:71605, Apr 14 2009, 22:40:02) [MSC v.1500 32 bit (Intel)] on
win32
Type "help", "copyright", "credits" or "license" for more information.
&gt;&gt;&gt; a=1
&gt;&gt;&gt; b=1
&gt;&gt;&gt; id(1)
10446048
&gt;&gt;&gt; id(a)
10446048
&gt;&gt;&gt; import sys
&gt;&gt;&gt; sys.getrefcount(a)
245
&gt;&gt;&gt; sys.getrefcount(b)
245
&gt;&gt;&gt;</pre>
<p><span style="font-family: Courier New; background-color: #eaf7ff;">其实也很容易理解，因为在Python<a title="Python的对象" href="http://wiki.woodpecker.org.cn/moin/PythonEssentialRef3" target="_blank">一切皆对象</a></span></p>				
