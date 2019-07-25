---
layout: post
title: '两个DropDownList在Repeater、DataList、DataGrid内的连动和冒泡事件(BubbleEvent) '
comments: true
date: 2006-04-08
tags:
- ASP.NET
- Asp.net
- DataGrid
- GridView
- 代码片段
- Grid
- DataList
- Repeater
- DropDownList
- BubbleEvent
---

<p><span style="font-size: medium;"><strong>两个DropDownList在Repeater、DataList、DataGrid内的连动和冒泡事件(BubbleEvent)<br /></strong><span style="font-size: small;">        问题</span><strong>:</strong></span> <a href="http://community.csdn.net/Expert/topic/4670/4670056.xml?temp=3.944033E-02" target="_blank">http://community.csdn.net/Expert/topic/4670/4670056.xml?temp=3.944033E-02</a><br />        刚看第一眼觉得在第一个DDL的SelectedIndexChanged事件内绑定第二个DDL就ok了，页面上写或者ItemDataBound内写事件挂接代码都可以。打开VS写测试却发现有点<span style="color: #ff0000;"><strong><span style="text-decoration: underline;">障碍</span></strong></span>哦，<br /><span style="color: #008000;"><span style="text-decoration: underline;"><em>在SelectedIndexChanged内要知道去绑定哪个行哪个列的DDL要费些周折</em></span></span>。<br /><strong><span style="color: #0000ff;">只有从DDL一级一级的向上找Parent最后找到DataGridItem，再利用其ItemIndex定位到行然后FindControl到要绑定的DDL</span></strong>，最终可以实现，好像比较累哦。<br />        随又想到DataGrid的ItemCommand事件，但发现WebControl内只有<a href="http://msdn.microsoft.com/library/chs/default.asp?url=/library/CHS/cpref/html/frlrfSystemWebUIWebControlsButtonClassTopic.asp"><strong><span style="color: #a52a2a;">Button</span></strong></a><span style="color: #a52a2a;"> </span><a href="http://msdn.microsoft.com/library/chs/default.asp?url=/library/CHS/cpref/html/frlrfSystemWebUIWebControlsImageButtonClassTopic.asp"><strong><span style="color: #a52a2a;">ImageButton</span></strong></a><span style="color: #a52a2a;"> <strong><span style="text-decoration: underline;"><a href="http://msdn.microsoft.com/library/chs/default.asp?url=/library/CHS/cpref/html/frlrfsystemwebuiwebcontrolslinkbuttonclasstopic.asp">LinkButton</a></span></strong></span>有<a href="http://msdn.microsoft.com/library/chs/default.asp?url=/library/CHS/cpref/html/frlrfsystemwebuiwebcontrolslinkbuttonclasscommandnametopic.asp">CommandName</a>属性和 <a href="http://msdn.microsoft.com/library/chs/default.asp?url=/library/CHS/cpref/html/frlrfsystemwebuiwebcontrolslinkbuttonclasscommandargumenttopic.asp">CommandArgument</a>属性，并可以将事件<span style="text-decoration: underline;"><strong><a href="http://msdn.microsoft.com/library/chs/default.asp?url=/library/CHS/cpguide/html/cpconbubblingcommandevent.asp">上浮（冒泡）</a>.</strong></span><a href="http://msdn.microsoft.com/library/chs/default.asp?url=/library/CHS/cpref/html/frlrfsystemwebuiwebcontrolsdropdownlistclasstopic.asp">DropDownLis</a>t先天不足！真是郁闷~~~~~ 能不能自己改造呢？<span style="color: #ff0000; background-color: #000080;"><strong>动手试试</strong></span>就知道了。</p>
<code><span style="color: #000000">
&lt;%@ Page Language="C#" Debug="true" %&gt;
<br />&lt;%@ Import Namespace="System.Data" %&gt;
<br />&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;
<br />&lt;html xmlns="http://www.w3.org/1999/xhtml" xml:lang="gb2312" lang="gb2312"&gt;
<br />&lt;head&gt;
<br />&lt;title&gt; ItemDataBoundGetColumnName &lt;/title&gt;
<br />&lt;meta http-equiv="Content-Type" content="text/html; charset=gb2312" /&gt;
<br />&lt;meta name="title" content="" /&gt;
<br />&lt;meta name="author" content="活靶子,Huobazi,www.AspxBoy.com" /&gt;
<br />&lt;meta name="subject" content="" /&gt;
<br />&lt;meta name="language" content="gb2312" /&gt;
<br />&lt;meta name="keywords" content="" /&gt;
<br />&lt;meta name="Copyright" content="www.AspxBoy.com" /&gt;
<br />&lt;meta name="robots" content="all" /&gt;<br /><br />&lt;script language="c#" runat="server"&gt;
<br />void BindGrid()
<br />{
<br />        DataTable dt = new DataTable();
<br />        DataRow dr;
<br />        dt.Columns.Add(new DataColumn("IntegerValue", typeof(Int32)));
<br />        dt.Columns.Add(new DataColumn("StringValue", typeof(string)));
<br />        dt.Columns.Add(new DataColumn("DateTimeValue", typeof(DateTime)));
<br />        dt.Columns.Add(new DataColumn("BoolValue", typeof(bool)));
<br />        dt.Columns.Add(new DataColumn("CurrencyValue", typeof(double)));
<br />        for (int i = 0; i &lt; 36; i++) {
<br />            dr = dt.NewRow();
<br />            dr[0] = i;
<br />            dr[1] = "项 " + i.ToString();
<br />            dr[2] = DateTime.Now;
<br />            dr[3] = (i % 2 != 0) ? true : false;
<br />            dr[4] = 1.23 * (i+1);
<br />            dt.Rows.Add(dr);
<br />        }
<br />  dg.DataSource= dt;
<br />  dg.DataBind();
<br />}
<br />void Page_Load(object o, EventArgs e)
<br />{
<br />     dg.PagerStyle.Mode = PagerMode.NumericPages;
<br />     if(!IsPostBack)
<br />     {
<br />        BindGrid();
<br />     }
<br />}
<br /> 
<br />void btnClick(object o , EventArgs e)
<br />{
<br />     Response.Write("页面回发,但是不执行ItemDataBound");
<br />}
<br /> 
<br />void PageChange(object o , DataGridPageChangedEventArgs e)
<br />{
<br />     dg.CurrentPageIndex = e.NewPageIndex;
<br />     BindGrid();
<br />}
<br />void ItemDataBound(object o , DataGridItemEventArgs e)
<br />{
<br />     if(e.Item.ItemIndex &gt; -1 )//必须
<br />     {
<br />          DataRowView drv = (DataRowView)e.Item.DataItem;
<br />          for (int i=0; i&lt;drv.Row.Table.Columns.Count ; i++)
<br />          { 
<br />            Response.Write(drv.Row.Table.Columns[i].ColumnName + "&amp;nbsp;&amp;nbsp;");
<br />          }
<br />     }
<br />}
<br />&lt;/script&gt;<br /><br />&lt;/head&gt;
<br />&lt;body&gt;
<br />&lt;form runat="server"&gt;
<br />  &lt;ASP:DataGrid id="dg" runat="server"      
<br />   HeaderStyle-BackColor="#aaaadd"
<br />   AutoGenerateColumns="true"
<br />   AllowPaging="true"
<br />   PageSize="6"
<br />    OnItemDataBound="ItemDataBound"
<br />    OnPageIndexChanged="PageChange"
<br />  &gt;
<br />  &lt;/asp:DataGrid&gt;
<br />  &lt;/br&gt;
<br />   &lt;asp:button id="btn" runat="server" onclick="btnClick" Text="我是按钮,按我一下"&gt;&lt;/asp:button&gt;<br />在AutoGenerateColumns="false"使用绑定列或者模板列的时候只需要使用 <br /><br />&lt;font color="blut"&gt;YourDataGrid.Columns[编号].HeaderText&lt;/font&gt; 去获取
<br />  <br />&lt;/form&gt;
<br />&lt;/body&gt;
<br />&lt;/html&gt;</span>
</code><p><a href="http://www.aspxboy.com/Files/71/66/284.Aspx" target="_blank">http://www.aspxboy.com/Files/71/66/284.Aspx</a></p>
<p> </p>				
