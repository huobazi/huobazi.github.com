---
layout: post
title: VirtualBox内的Linux和宿主Windows的文件共享
comments: true
date: 2010-12-25 23:58
categories:
- LAMP
- linux
- VirtualBox
- Putty
- PSCP
- Ubuntu
---

<p>VirtualBox内的Linux和宿主Windows的文件共享<br />（1）安装增强功能<br />（2）分配数据空间，制定一个名称，假设为“temp”<br />（3）挂载， mount -t vboxsf temp /mnt</p>
<p><!--more--></p>
<p>OK了<br />另外，反之共享Linux路径，然后在windows内映射网络驱动器即可。</p>
<p>BTW:使用http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html内的PSCP.exe也可以<br />但我没有去试验。<strong></strong></p>				
