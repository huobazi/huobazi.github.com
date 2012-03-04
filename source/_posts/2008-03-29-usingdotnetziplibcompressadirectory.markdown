---
layout: post
title: 使用dotNetZipLib轻松压缩目录/文件夹
comments: true
date: 2008-03-29 14:45
categories:
- ASP.NET
- Asp.net
- .Net其他
- dotNetZipLib
- 代码片段
---

<div><span style="font-family: Verdana;">.net1.1时代我们选SharpZipLib<br />.net2.0时代我们选System.IO.Compression名称空间下的东东<br />.net3.0时代我们选System.IO.Packaging名称空间下的东东。<br />今天发现CodePlex上有个好东西，另压缩如此之Easy。。。</span></div>
<p> </p>
<p><span style="font-family: Verdana;"></span></p>
<div style="padding-right: 5px; padding-left: 4px; font-size: 13px; padding-bottom: 4px; width: 98%; word-break: break-all; padding-top: 4px; background-color: #eeeeee; border: #cccccc 1px solid;">
<span style="color: #000000">  ZipFile zip </span><span style="color: #000000">=</span><span style="color: #000000"> </span><span style="color: #0000ff">new</span><span style="color: #000000"> ZipFile(directo</span><span style="color: #000000">outputFileName);<br />            zip.TrimVolumeFromFullyQualifiedPaths </span><span style="color: #000000">=</span><span style="color: #000000"> </span><span style="color: #0000ff">true</span><span style="color: #000000">;<br />            zip.TempFileFolder </span><span style="color: #000000">=</span><span style="color: #000000"> Path.GetTempPath();<br />            zip.Comment<br />                </span><span style="color: #000000">=</span><span style="color: #000000"> </span><span style="color: #0000ff">string</span><span style="color: #000000">.Format(</span><span style="color: #800000">"</span><span style="color: #800000">A zip archives。{0}  {1}</span><span style="color: #800000">"</span><span style="color: #000000">,  Environment.NewLine, DateTime.Now.ToString());<br />            zip.AddDirectory(directory, </span><span style="color: #0000ff">string</span><span style="color: #000000">.Format(</span><span style="color: #800000">"</span><span style="color: #800000">MyFolder-{0}</span><span style="color: #800000">"</span><span style="color: #000000">, DateTime.Now.ToShortDateString()));<br />            zip.Save();</span>
</div>
<p>那就是</p>
<p></p>
<h1 class="ProjectHeader NoMargin"><a id="ctl00_ctl00_WideContent_ProjectTitleControl1_ProjectTitleLink" class="NoUnderline" tabindex="0" href="http://www.codeplex.com/DotNetZip"><span id="ctl00_ctl00_WideContent_ProjectTitleControl1_TitleLabel">DotNet Zip Library</span></a></h1>
<p> </p>
<p> <br /></p>				
