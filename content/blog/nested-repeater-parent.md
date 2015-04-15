---
layout: post
title: Repeater,DataList等嵌套如何绑定父repeater字段?
comments: true
date: 2009-12-11
tags:
- ASP.NET
- DataList
- Repeater
---

<p>嘿嘿，其实Container有个Parent属性,把它转换为RepeaterItem再取其DataItem</p>
<p>DataBinder.Eval(((System.W</p>
<div style="font-size: 9pt; color: #000000; direction: ltr;">eb.UI.WebControls.Repeat erItem)Container.Parent.Parent.Parent).DataItem</div>				
