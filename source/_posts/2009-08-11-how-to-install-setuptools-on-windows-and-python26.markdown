---
layout: post
title: 如何在windows xp下安装python2.6的setuptools
comments: true
date: 2009-08-11 21:34
categories:
- LAMP
- Windows
- python
- setuptools
- ez_setup
---

<p>最近开始学python，要安装很多egg文件，但发现<a href="http://pypi.python.org/pypi/setuptools#downloads">http://pypi.python.org/pypi/setuptools#downloads</a>没有python2.6的MS Windows installer版本，google了一把，用如下方法解决：</p>
<p><!--more--></p>
<p>1. 下载 setuptools-0.6c9.tar.gz<br />2. 下载 setuptools-0.6c9-py2.6.egg （放在同一个目录）<br />3. 用7-zip或者其他解压工具打开 setuptools-0.6c9.tar.gz ，并且把里面的 ez_setup.py 文件解压到同一个目录里。<br />4. 打开cmd窗口，并进入你刚才下载和解压文件的目录里。（例如： d:\downloads\）<br />5. 输入 python ez_setup.py setuptools-0.6c9-py2.6.egg</p>
<p>提示如下:</p>
<pre>E:\temp&gt;python ez_setup.py setuptools-0.6c9-py2.6.egg
Processing setuptools-0.6c9-py2.6.egg
Copying setuptools-0.6c9-py2.6.egg to c:\python26\lib\site-packages
Adding setuptools 0.6c9 to easy-install.pth file
Installing easy_install-script.py script to C:\Python26\Scripts
Installing easy_install.exe script to C:\Python26\Scripts
Installing easy_install-2.6-script.py script to C:\Python26\Scripts
Installing easy_install-2.6.exe script to C:\Python26\Scripts

Installed c:\python26\lib\site-packages\setuptools-0.6c9-py2.6.egg
Processing dependencies for setuptools==0.6c9
Finished processing dependencies for setuptools==0.6c9
Processing setuptools-0.6c9-py2.6.egg
Removing c:\python26\lib\site-packages\setuptools-0.6c9-py2.6.egg
Copying setuptools-0.6c9-py2.6.egg to c:\python26\lib\site-packages
setuptools 0.6c9 is already the active version in easy-install.pth
Installing easy_install-script.py script to C:\Python26\Scripts
Installing easy_install.exe script to C:\Python26\Scripts
Installing easy_install-2.6-script.py script to C:\Python26\Scripts
Installing easy_install-2.6.exe script to C:\Python26\Scripts

Installed c:\python26\lib\site-packages\setuptools-0.6c9-py2.6.egg
Processing dependencies for setuptools==0.6c9
Finished processing dependencies for setuptools==0.6c9

E:\temp&gt;</pre>				
