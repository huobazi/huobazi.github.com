---
layout: post
title: 还记得 Page.SmartNavigation 属性么，此属性已被否决。
comments: true
date: 2006-06-29 16:55
categories:
- ASP.NET
- Asp.net
---

<p><span style="color: #ff0000;"><strong><span style="color: #000000;">还记得在.Net 1.x 中我们为了保持在页面回发后 保持滚动条位置的做法么？<br />Page.SmartNavigation 可以做到，但会带来这样那样的问题。<br />我们也曾经用这样那样的方法实现这个效果，如：</span></strong></span></p>
<p><a href="http://huobazi.cnblogs.com/archive/2004/09/20/ScrollPage.aspx"><span style="color: #0000ff;">http://huobazi.cnblogs.com/archive/2004/09/20/ScrollPage.aspx</span></a><br /><a href="http://www.cnblogs.com/birdshome/archive/2004/12/13/76521.html"><span style="color: #0000ff;">http://www.cnblogs.com/birdshome/archive/2004/12/13/76521.html</span></a></p>
<p><span style="color: #000000;">在.Net 2.0 中，该类型被描述为：<br /></span> <br /><span style="color: #000000;">[<span style="color: #0000ff;">ObsoleteAttribute</span>("The recommended alternative is Page.SetFocus and Page.MaintainScrollPositionOnPostBack. http://go.microsoft.com/fwlink/?linkid=14202")]<br /><span class="keyword">public</span> bool <span class="identifier">SmartNavigation</span> { <span class="keyword">get</span>; <span class="keyword">set</span>; }</span></p>
<p><br /><span style="color: #ff0000;"><strong>注意：此属性现在已过时。</strong></span></p>
<p> </p>
<p>获取或设置指示是否启用智能导航的值。</p>
<p>同时在备注内有提到：</p>
<p><strong>SmartNavigation</strong> 属性已被<strong>否决</strong>。请改用 <a href="ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.NETDEVFX.v20.chs/cpref13/html/O_T_System_Web_UI_Page_SetFocus.htm"><span style="color: #002c99;">SetFocus</span></a> 方法和 <a href="ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.NETDEVFX.v20.chs/cpref13/html/P_System_Web_UI_Page_MaintainScrollPositionOnPostBack.htm">MaintainScrollPositionOnPostback </a>属性。</p>
<p>园子里<a href="http://birdshome.cnblogs.com/">birdshome</a> 也早有post了 <a id="viewpost1_TitleUrl" href="http://birdshome.cnblogs.com/archive/2005/06/20/177404.html"><strong><span style="color: #223355;">SmartNavigation在Fx2.0中下岗了</span></strong></a></p>				
