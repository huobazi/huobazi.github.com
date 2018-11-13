---
layout: post
title: 如何在ItemDataBound内获得DataGrid的列名称HeaderText
description: 如果 AutoGenerateColumns="false" 使用绑定列，模板列 则比较好办，直接使用 YourDataGrid.Columns[编号].HeaderText 获得 可是,如果AutoGenerateColumns="true" ,就比较麻烦了,因为这时YourDataGrid.Columns.Count是0 但是可以变通做到。
date: 2004-04-05
tags:
- ASP.NET
- Asp.net
- 代码片段
---

如果 AutoGenerateColumns="false" 使用绑定列，模板列 
则比较好办，直接使用 YourDataGrid.Columns[编号].HeaderText 获得 
可是,如果 AutoGenerateColumns="true" ,就比较麻烦了,因为这时YourDataGrid.Columns.Count是0 
但是可以变通做到。

```
<%@ Page Language="C#" Debug="true" %>
<%@ Import Namespace="System.Data" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="gb2312" lang="gb2312">
<head>
<title> ItemDataBoundGetColumnName </title>
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<meta name="title" content="" />
<meta name="author" content="活靶子,Huobazi,www.AspxBoy.com" />
<meta name="subject" content="" />
<meta name="language" content="gb2312" />
<meta name="keywords" content="" />
<meta name="Copyright" content="www.AspxBoy.com" />
<meta name="robots" content="all" />
<script language="c#" runat="server">
void BindGrid()
{
		DataTable dt = new DataTable();
        DataRow dr;
        dt.Columns.Add(new DataColumn("IntegerValue", typeof(Int32)));
        dt.Columns.Add(new DataColumn("StringValue", typeof(string)));
        dt.Columns.Add(new DataColumn("DateTimeValue", typeof(DateTime)));
        dt.Columns.Add(new DataColumn("BoolValue", typeof(bool)));
        dt.Columns.Add(new DataColumn("CurrencyValue", typeof(double)));
        for (int i = 0; i < 36; i++) {
            dr = dt.NewRow();
            dr[0] = i;
            dr[1] = "项 " + i.ToString();
            dr[2] = DateTime.Now;
            dr[3] = (i % 2 != 0) ? true : false;
            dr[4] = 1.23 * (i+1);
            dt.Rows.Add(dr);
        }
  dg.DataSource= dt;
  dg.DataBind();
}
void Page_Load(object o, EventArgs e)
{
	 dg.PagerStyle.Mode = PagerMode.NumericPages;
	 if(!IsPostBack)
	 {
		BindGrid();
	 }
}
 
void btnClick(object o , EventArgs e)
{
	 Response.Write("页面回发,但是不执行ItemDataBound");
}
 
void PageChange(object o , DataGridPageChangedEventArgs e)
{
	 dg.CurrentPageIndex = e.NewPageIndex;
	 BindGrid();
}
void ItemDataBound(object o , DataGridItemEventArgs e)
{
	 if(e.Item.ItemIndex > -1 )//必须
	 {
		  DataRowView drv = (DataRowView)e.Item.DataItem;
		  for (int i=0; i<drv.Row.Table.Columns.Count ; i++)
		  {  
			Response.Write(drv.Row.Table.Columns[i].ColumnName + "  ");
		  }
	 }
}
</script>
 
</head>
<body>
<form runat="server">
  <ASP:DataGrid id="dg" runat="server"       
   HeaderStyle-BackColor="#aaaadd"
   AutoGenerateColumns="true"
   AllowPaging="true"
   PageSize="6"
    OnItemDataBound="ItemDataBound"
    OnPageIndexChanged="PageChange"
  >
  </asp:DataGrid>
  </br>
   <asp:button id="btn" runat="server" onclick="btnClick" Text="我是按钮,按我一下"></asp:button>
   <p>在AutoGenerateColumns="false"使用绑定列或者模板列的时候只需要使用 </P>
   <p><font color="blut">YourDataGrid.Columns[编号].HeaderText</font> 去获取
  </P>
</form>
</body>
</html>
 
```