---
layout: post
title: 在自定义控件中实现ICallbackEventHandler接口不经过回发而实现客户端回掉
comments: true
date: 2007-07-23 14:49
categories:
- ASP.NET
- Asp.net
- 自定义控件
- 代码片段
---

<p> <br /></p>
<p><span>在自定义控件中实现</span><strong><span>ICallbackEventHandler</span></strong><strong><span>接口</span></strong><span>不经过回发而实现客户端回掉</span> <br /><span>Asp.Net2.0</span><span>中新增了</span><span><a href="ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.NETDEVFX.v20.chs/cpref13/html/T_System_Web_UI_ICallbackEventHandler.htm">ICallbackEventHandler</a></span><span>接口，</span><span>用于指示控件可以作</span><span>为</span><span>服</span><span>务</span><span>器的回</span><span>调</span><span>事件的目</span><span>标</span><span>。</span><br /><span>MSDN</span><span>中的描述</span><span>:</span><br /></p>
<p align="left"><span>实现</span><span> <strong><span>ICallbackEventHandler</span></strong><span> </span></span><span>接口的控件的示例包括</span><span> GridView</span><span>、</span><span>DetailsView </span><span>和</span><span> TreeView </span><span>控件。当回</span><span>调</span><span>事件以</span><span>实现</span><span>了</span><span> <strong><span>ICallbackEventHandler</span></strong><span> </span></span><span>接口的控件</span><span>为</span><span>目</span><span>标时</span><span>，将把事件</span><span>变</span><span>量作</span><span>为</span><span>参数</span><span>传递</span><span>来</span><span>调</span><span>用</span><span> <span><a href="ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.NETDEVFX.v20.chs/cpref13/html/M_System_Web_UI_ICallbackEventHandler_RaiseCallbackEvent_1_16219e3a.htm"><span>RaiseCallbackEvent</span></a> </span></span><span>方法以</span><span>处</span><span>理</span><span>该</span><span>事件，并且</span><span><a href="ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.NETDEVFX.v20.chs/cpref13/html/M_System_Web_UI_ICallbackEventHandler_GetCallbackResult.htm"><span>GetCallbackResult</span></a> </span><span>方法返回回</span><span>调</span><span>的</span><span>结</span><span>果</span><span>。</span></p>
<p align="left"><strong><span>ICallbackEventHandler</span></strong><span>成员有：</span></p>
<table border="0" cellpadding="0" width="98%"><tbody>
<tr>
<td valign="top">
<p></p>
<p align="left"><strong> </strong><br /></p>
<p></p>
<p> </p>
</td>
<td valign="top">
<p></p>
<p align="left"><strong><span>名称</span></strong><strong><span> </span></strong><br /></p>
<p></p>
<p> </p>
</td>
<td valign="top">
<p></p>
<p align="left"><strong><span>说</span></strong><strong><span>明</span></strong><strong><span> </span></strong><br /></p>
<p></p>
<p> </p>
</td>
</tr>
<tr>
<td valign="top">
<p></p>
<p align="left"> <br /></p>
<p></p>
<p> </p>
</td>
<td valign="top">
<p></p>
<p align="left"><span><a href="ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.NETDEVFX.v20.chs/cpref13/html/M_System_Web_UI_ICallbackEventHandler_GetCallbackResult.htm"><span>GetCallbackResult</span></a> </span><br /></p>
<p></p>
<p> </p>
</td>
<td valign="top">
<p></p>
<p align="left"><span>返回以控件</span><span>为</span><span>目</span><span>标</span><span>的回</span><span>调</span><span>事件的</span><span>结</span><span>果。</span><span> </span><br /></p>
<p></p>
<p> </p>
</td>
</tr>
<tr>
<td valign="top">
<p></p>
<p align="left"> <br /></p>
<p></p>
<p> </p>
</td>
<td valign="top">
<p></p>
<p align="left"><span><a href="ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.NETDEVFX.v20.chs/cpref13/html/M_System_Web_UI_ICallbackEventHandler_RaiseCallbackEvent_1_16219e3a.htm"><span>RaiseCallbackEvent</span></a> </span><br /></p>
<p></p>
<p> </p>
</td>
<td valign="top">
<p></p>
<p align="left"><span>处</span><span>理以控件</span><span>为</span><span>目</span><span>标</span><span>的回</span><span>调</span><span>事件。</span><span> </span><br /></p>
<p></p>
<p> </p>
</td>
</tr>
</tbody></table>
<p> <br /><span>如下代码实现一个不经过回发而实现客户端回掉的</span><span>CheckBox</span></p>
<p></p>
<div><span>。<br /></span></div>
<p><span><br />//------------------------------------------------------------------------------&lt;br /&gt;// &lt;copyright company="Meibo Wu www.AspxBoy.com"&gt;&lt;br /&gt;// Copyright (c) www.AspxBoy.com All rights reserved.&lt;br /&gt;// &lt;/copyright&gt;&lt;br /&gt;//------------------------------------------------------------------------------&lt;br /&gt;using System;&lt;br /&gt;using System.Drawing;&lt;br /&gt;using System.Collections;&lt;br /&gt;using System.ComponentModel;&lt;br /&gt;using System.Web;&lt;br /&gt;using System.Web.UI;&lt;br /&gt;using System.Web.UI.WebControls;&lt;br /&gt;namespace HBZ&lt;br /&gt;{&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// A Asynchronous AutoPostback Checkbox Control&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;[DefaultEvent("CheckedChanged")]&lt;br /&gt;[ControlValueProperty("Checked")]&lt;br /&gt;[DefaultProperty("Text")]&lt;br /&gt;public class AsynchronousCheckBox : WebControl, INamingContainer, ICallbackEventHandler&lt;br /&gt;{&lt;br /&gt;#region Delegates&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// The delegate for the checked changed event&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="sender" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="e" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;public delegate void CheckedChangedEventHander(object sender, CheckChangedEventArgs e);&lt;br /&gt;#endregion&lt;br /&gt;#region Events&lt;br /&gt;private static readonly object eventCheckedChanged;&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// The checked changed event.&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;public event CheckedChangedEventHander CheckedChanged&lt;br /&gt;{&lt;br /&gt;add&lt;br /&gt;{&lt;br /&gt;Events.AddHandler(eventCheckedChanged, value);&lt;br /&gt;}&lt;br /&gt;remove&lt;br /&gt;{&lt;br /&gt;Events.RemoveHandler(eventCheckedChanged, value);&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;#endregion&lt;br /&gt;#region Constructors&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Static Constructor&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;static AsynchronousCheckBox()&lt;br /&gt;{&lt;br /&gt;eventCheckedChanged = new object();&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Constructor&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;public AsynchronousCheckBox()&lt;br /&gt;: base(HtmlTextWriterTag.Input)&lt;br /&gt;{&lt;br /&gt;}&lt;br /&gt;#endregion&lt;br /&gt;#region Properties&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Gets or sets a value indicating whether the Lable Text&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;[Description("Gets or sets a value indicating whether the Lable Text")]&lt;br /&gt;public virtual string Text&lt;br /&gt;{&lt;br /&gt;get&lt;br /&gt;{&lt;br /&gt;return (string)ViewState["Text"];&lt;br /&gt;}&lt;br /&gt;set&lt;br /&gt;{&lt;br /&gt;this.ViewState["Text"] = value;&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Gets or sets a value indicating whether the 'Client CallBack Script Name'&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;[Description("Gets or sets a value indicating whether the 'Client CallBack Script function Name'")]&lt;br /&gt;public string ClientCallBackScript&lt;br /&gt;{&lt;br /&gt;get&lt;br /&gt;{&lt;br /&gt;object o = ViewState["ClientCallBackScript"];&lt;br /&gt;return o == null ? "null" : o.ToString();&lt;br /&gt;}&lt;br /&gt;set&lt;br /&gt;{&lt;br /&gt;ViewState["ClientCallBackScript"] = value;&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Gets or sets a value indicating whether the checkbox 's checked&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;[Description("Gets or sets a value indicating whether the checkbox 's checked")]&lt;br /&gt;public bool Checked&lt;br /&gt;{&lt;br /&gt;get&lt;br /&gt;{&lt;br /&gt;object o = ViewState["Checked"];&lt;br /&gt;return o == null ? false : (bool)o;&lt;br /&gt;}&lt;br /&gt;set&lt;br /&gt;{&lt;br /&gt;ViewState["Checked"] = value;&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Gets or sets a value indicating whether the Text 's cssClass&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;[Description("Gets or sets a value indicating whether the Text 's cssClass")]&lt;br /&gt;public string TextCss&lt;br /&gt;{&lt;br /&gt;get&lt;br /&gt;{&lt;br /&gt;return (string)ViewState["TextCss"];&lt;br /&gt;}&lt;br /&gt;set&lt;br /&gt;{&lt;br /&gt;ViewState["TextCss"] = value;&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Gets or sets a value indicating whether the Label 's position&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;public virtual TextAlign TextAlign&lt;br /&gt;{&lt;br /&gt;get&lt;br /&gt;{&lt;br /&gt;object o = ViewState["TextAlign"];&lt;br /&gt;if (o != null)&lt;br /&gt;{&lt;br /&gt;return (TextAlign)o;&lt;br /&gt;}&lt;br /&gt;return TextAlign.Right;&lt;br /&gt;}&lt;br /&gt;set&lt;br /&gt;{&lt;br /&gt;if ((value &lt;textalign.left) || (value &gt; TextAlign.Right))&lt;br /&gt;{&lt;br /&gt;throw new ArgumentOutOfRangeException("value");&lt;br /&gt;}&lt;br /&gt;ViewState["TextAlign"] = value;&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;#endregion&lt;br /&gt;#region Render Meghods&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;///&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="writer" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;protected override void Render(HtmlTextWriter writer)&lt;br /&gt;{&lt;br /&gt;if (TextAlign == TextAlign.Left)&lt;br /&gt;{&lt;br /&gt;RenderLabel(writer);&lt;br /&gt;base.Render(writer);&lt;br /&gt;}&lt;br /&gt;else&lt;br /&gt;{&lt;br /&gt;base.Render(writer);&lt;br /&gt;RenderLabel(writer);&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Render Label&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="writer" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;private void RenderLabel(HtmlTextWriter writer)&lt;br /&gt;{&lt;br /&gt;if (string.IsNullOrEmpty(Text))&lt;br /&gt;{&lt;br /&gt;return;&lt;br /&gt;}&lt;br /&gt;writer.Write("&lt;label");&lt;br /&gt;writer.WriteAttribute("for", ClientID);&lt;br /&gt;if (!string.IsNullOrEmpty(TextCss))&lt;br /&gt;{&lt;br /&gt;writer.WriteAttribute("class", TextCss);&lt;br /&gt;}&lt;br /&gt;writer.Write("&gt;");&lt;br /&gt;writer.Write(Text);&lt;br /&gt;writer.WriteEndTag("label");&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Override the AddAttributesToRender method&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="writer" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;protected override void AddAttributesToRender(HtmlTextWriter writer)&lt;br /&gt;{&lt;br /&gt;if (base.Page == null)&lt;br /&gt;{&lt;br /&gt;base.Page.VerifyRenderingInServerForm(this);&lt;br /&gt;}&lt;br /&gt;string callbackReference&lt;br /&gt;= Page.ClientScript.GetCallbackEventReference(this, "this.checked", ClientCallBackScript, null);&lt;br /&gt;writer.AddAttribute(HtmlTextWriterAttribute.Onclick, callbackReference);&lt;br /&gt;writer.AddAttribute(HtmlTextWriterAttribute.Type, "checkbox");&lt;br /&gt;if (Checked)&lt;br /&gt;{&lt;br /&gt;writer.AddAttribute(HtmlTextWriterAttribute.Checked, "checked");&lt;br /&gt;}&lt;br /&gt;if (!Enabled)&lt;br /&gt;{&lt;br /&gt;writer.AddAttribute(HtmlTextWriterAttribute.Disabled, "disabled");&lt;br /&gt;}&lt;br /&gt;if (!string.IsNullOrEmpty(ToolTip))&lt;br /&gt;{&lt;br /&gt;writer.AddAttribute(HtmlTextWriterAttribute.Title, ToolTip);&lt;br /&gt;}&lt;br /&gt;base.AddAttributesToRender(writer);&lt;br /&gt;}&lt;br /&gt;#endregion&lt;br /&gt;#region On Checked Changed&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Invoke the check changed event.&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="sender" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="e" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;protected virtual void OnCheckedChanged(object sender, CheckChangedEventArgs e)&lt;br /&gt;{&lt;br /&gt;CheckedChangedEventHander hander = Events[eventCheckedChanged] as CheckedChangedEventHander;&lt;br /&gt;if (hander != null)&lt;br /&gt;{&lt;br /&gt;Checked = e.Checked;&lt;br /&gt;hander(this, e);&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;#endregion&lt;br /&gt;#region ICallbackEventHandler Members&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Get the result of a client side callback.&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;/// &lt;returns&gt;The callback result string.&lt;/returns&gt;&lt;br /&gt;public string GetCallbackResult()&lt;br /&gt;{&lt;br /&gt;return Checked.ToString();&lt;br /&gt;}&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;/// Raise the client callback event&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="eventArgument" class="mceItemParam"&gt;&lt;/span&gt;The event arguments.&lt;/param&gt;&lt;br /&gt;public void RaiseCallbackEvent(string eventArgument)&lt;br /&gt;{&lt;br /&gt;bool isChecked = Boolean.Parse(eventArgument);&lt;br /&gt;CheckChangedEventArgs args = new CheckChangedEventArgs(isChecked);&lt;br /&gt;OnCheckedChanged(this, args);&lt;br /&gt;}&lt;br /&gt;#endregion&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;//------------------------------------------------------------------------------&lt;br /&gt;// &lt;copyright company="Meibo Wu www.AspxBoy.com"&gt;&lt;br /&gt;// Copyright (c) www.AspxBoy.com All rights reserved.&lt;br /&gt;// &lt;/copyright&gt;&lt;br /&gt;//------------------------------------------------------------------------------&lt;br /&gt;using System;&lt;br /&gt;using System.Drawing;&lt;br /&gt;using System.Collections;&lt;br /&gt;using System.ComponentModel;&lt;br /&gt;using System.Web;&lt;br /&gt;using System.Web.UI;&lt;br /&gt;using System.Web.UI.WebControls;&lt;br /&gt;namespace HBZ&lt;br /&gt;{&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;///&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;public class CheckChangedEventArgs:EventArgs&lt;br /&gt;{&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;///&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;///&lt;br /&gt;&lt;span name="_isChecked" class="mceItemParam"&gt;&lt;/span&gt;&lt;/param&gt;&lt;br /&gt;public CheckChangedEventArgs(bool _isChecked)&lt;br /&gt;{&lt;br /&gt;isChecked = _isChecked;&lt;br /&gt;}&lt;br /&gt;private bool isChecked = false;&lt;br /&gt;/// &lt;summary&gt;&lt;br /&gt;///&lt;br /&gt;/// &lt;/summary&gt;&lt;br /&gt;public bool Checked&lt;br /&gt;{&lt;br /&gt;get&lt;br /&gt;{&lt;br /&gt;return isChecked;&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;}&lt;br /&gt;<br />         <a href="http://www.aspxboy.com/private/5504/default.aspx">http://www.aspxboy.com/private/5504/default.aspx<br /></a></span></p>				
