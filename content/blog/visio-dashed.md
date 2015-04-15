---
layout: post
title: 【How to】解决Visio虚线复制到word中变为实线
comments: true
date: 2009-10-10
categories:
- 闲言碎语
- 推荐阅读
- 它山之石
- Visio
- 虚线
- 实线
- Word
---

<p>添加 MetafileDashLineAsSolid 到以下注册表位置，类型DWORD。</p>
<p> • Visio 2007<br />HKEY_CURRENT_USER\Software\Microsoft\Office\12.0\Visio\Application<br />• Visio 2003<br />HKEY_CURRENT_USER\Software\Microsoft\Office\11.0\Visio\Application<br />属性值：</p>
<p>• 0：虚线或虚线行执行不替换为实线。<br />• 1：虚线或虚线极端情形中行只替换为实线。 100 倍的原始文件大小时可能导致文件大小中增加例如, 替换实线为虚线或虚线行。 <br />• 2：替换实线用于当合理虚线或虚线行。 这是默认值。 <br />• 3：始终替换为实线虚线或虚线行。 </p>
<p> </p>				
