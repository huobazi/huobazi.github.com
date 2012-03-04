---
layout: post
title: Scroll Page 表单提交后页面重新滚回原来滚动条所在位置
comments: true
date: 2004-09-20 13:55
categories:
- ASP.NET
- 前端开发
- Asp.net
---

<p>作者<span style="text-decoration: underline;"><span style="color: #800080;"><a href="http://scottwater.com/">scottwater</a><br /></span></span>原文地址：<a href="http://scottwater.com/articles/ScrollPage">http://scottwater.com/articles/ScrollPage</a><br />感谢<a href="http://scottwater.com/">scottwater</a>先生！<br />我做了一点修改，使其支持横向滚动条位置的记忆</p>

```
using System;
using System.IO;
using System.Text;
using System.Text.RegularExpressions;
using System.Web.UI;

namespace ShangGu.XaTaxi.Components
{
 /// <summary>
/// Summary description for ScrollPage.
/// </summary>
public class ScrollPage : System.Web.UI.Page
 {
public ScrollPage()
 {

}

private bool _useScrollPersistence = true;
 /// <summary>
/// There could be PostBack senarios where we do not want to remember the scroll position. Set this property to false
/// if you would like the page to forget the current scroll position
/// </summary>
public bool UseScrollPersistence
 {
 get {return this._useScrollPersistence;}
set {this._useScrollPersistence = value;}
}

private string _bodyID;
/// <summary>
/// Some pages might already have the ID attribute set for the body tag. Setting this property will not render the ID or change
/// the existing value. It will simply update the javascript written out to the browser.
/// </summary>
public string BodyID
 {
 get {return this._bodyID;}
 set {this._bodyID = value;}
}


//Last chance. Do we want to maintain the current scroll position
protected override void OnPreRender(EventArgs e)
 {
if(UseScrollPersistence)
 {
RetainScrollPosition();
}
base.OnPreRender (e);
}

protected override void Render(HtmlTextWriter writer)
 {
//No need processing the HTML if the user does not want to maintain scroll position or already has
//set the body ID value
if(UseScrollPersistence)
 {
TextWriter tempWriter = new StringWriter();
base.Render(new HtmlTextWriter(tempWriter));
if(BodyID == null)
 {
writer.Write(Regex.Replace(tempWriter.ToString(),"<body","<body id="thebody" ",RegexOptions.IgnoreCase));
}
//=++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
//
//2004－9－16 武眉博 修正了因BodyID不空时造成javascript错误的bug
//
//=++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
else
 {
writer.Write(Regex.Replace(tempWriter.ToString(),"<body","<body id=""+BodyID+"" ",RegexOptions.IgnoreCase));

}
}
else
 {
base.Render(writer);
}
}

//=++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
//
//2004－9－20 武眉博 增加了隐藏文本域"__SCROLLPOS_LEFT"，以增加对横向滚动条位置的记忆功能
//
//=++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
private static string saveScrollPosition = "<script language='javascript'>function saveScrollPosition() {{document.forms[0].__SCROLLPOS_TOP.value = {0}.scrollTop;document.forms[0].__SCROLLPOS_LEFT.value = {0}.scrollLeft ;}}{0}.onscroll=saveScrollPosition;</script>";
private static string setScrollPosition = "<script language='javascript'>function setScrollPosition() {{{0}.scrollTop ="{1}"; {0}.scrollLeft ="{2}"}}{0}.onload=setScrollPosition;</script>";

//Write out javascript and hidden field
private void RetainScrollPosition()
 {
RegisterHiddenField("__SCROLLPOS_TOP", "0");
RegisterHiddenField("__SCROLLPOS_LEFT", "0");
string __bodyID = BodyID == null ? "thebody" : BodyID;
RegisterStartupScript("saveScroll", string.Format(saveScrollPosition,__bodyID));

if(Page.IsPostBack)
 {
RegisterStartupScript("setScroll", string.Format(setScrollPosition,__bodyID, Request.Form["__SCROLLPOS_TOP"],Request.Form["__SCROLLPOS_LEFT"]));
}
}
}
}
```