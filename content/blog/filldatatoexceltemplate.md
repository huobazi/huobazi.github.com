---
layout: post
title: 打开一个Excel模板文件填充数据另存为一个文件
comments: true
date: 2004-04-27
categories:
- ASP.NET
- Asp.net
- 它山之石
- Excel
- 代码片段
---

<p>最近做的东西要求打开一个Excel文件模板后填充数据<br />开始用OleDb连接该Excel文件更新老是出错误 “需要一个可更新的.....“<br /><a href="http://expert.csdn.net/Expert/topic/2992/2992809.xml?temp=.4825403">http://expert.csdn.net/Expert/topic/2992/2992809.xml?temp=.4825403</a><br />如果是access这个错误多半是权限引起的 可是我做的是winform 权限是admin啊<br />未果<br />后来用ODBC测试了几个字段 都成功了<br />开始写程序 后发现就有那么2个单元格不听话 提示参数错误<br />郁闷<br /><a href="http://expert.csdn.net/Expert/topic/3000/3000113.xml?temp=.3331262">http://expert.csdn.net/Expert/topic/3000/3000113.xml?temp=.3331262</a><br />仍未果<br />没办法翻google<br />获得<br /><a href="http://www.c-sharpcorner.com/winforms/ExcelReadMG.asp">http://www.c-sharpcorner.com/winforms/ExcelReadMG.asp</a><br />用com组件，可行哦，今早上csdn就有网友pm我问是如何搞定的<br />那就写到这里，<br />以下是部分代码，使用前要先按上文中的说明添加Com引用<br />...........<br /><span style="background-color: #d3d3d3;">string strFileName = </span><a href="mailto:Environment.CurrentDirectory+@%22%5Ctemplate%5Ctemplate.tpl"><span style="background-color: #d3d3d3;">Environment.CurrentDirectory+@"\template\template.tpl</span></a><span style="background-color: #d3d3d3;">";<br />    string strSaveFileName = </span><a href="mailto:Environment.CurrentDirectory+@%22%5Cexcel%5C%22+System.DateTime.Now.ToString().Replace(%22:%22,%22%22).Replace(%22-%22,%22%22).Replace"><span style="background-color: #d3d3d3;">Environment.CurrentDirectory+@"\excel\"+System.DateTime.Now.ToString().Replace(":","").Replace("-","").Replace</span></a><span style="background-color: #d3d3d3;">(" ","")+@".xls";<br />    Excel.Application ThisApplication = new Excel.ApplicationClass();<br />    Excel.Workbook ThisWorkBook;<br />    object missing = System.Reflection.Missing.Value;<br />    try<br />    { <br />     //加载Excel模板文件<br />     ThisWorkBook = ThisApplication.Workbooks.Open(strFileName,missing,missing,missing,missing,missing,missing,missing,missing,missing,missing,missing,missing);<br />     Excel.Worksheet ThisSheet = (Excel.Worksheet)ThisWorkBook.Sheets[1];<br />     ThisSheet.Cells[7,1] = dtEnd.ToShortDateString();<br />     progressBar.Value = 30;<br />     ThisApplication.Visible = false;<br />     DataRow dr = dt.Rows[0];<br />     for( int i=0; i     {<br />      ThisSheet.Cells[7,i+2] = dr[i].ToString();<br />      progressBar.Value +=1;<br />     }<br />     //更新数据后另存为新文件<br />     ThisSheet.SaveAs(strSaveFileName,missing,missing,missing,missing,missing,missing,missing,missing);<br />    }<br />    catch{}<br />    finally<br />    {<br />     ThisApplication.Quit();<br />     ThisWorkBook = null;<br />     ThisApplication = null;<br />     //dt = null;<br />    }<br />    try<br />    { //打开刚才生成的Excel文件<br />     Excel.Workbook NewWorkBook;<br />     NewWorkBook = NewApplication.Workbooks.Open(strSaveFileName,missing,missing,missing,missing,missing,missing,missing,missing,missing,missing,missing,missing);<br />     Excel.Worksheet NewSheet = (Excel.Worksheet)NewWorkBook.Sheets[1];<br />     NewApplication.Visible = true;</span></p>
<p>//也可以使用System.Diagnostics.Process.Start(strSaveFileName);来打开新文件</p>
<p>    }</p>
<p>打开Excel后进程内会多出一个excel进程<br />需要手工清理<br />参考这片文章</p>
<p><a href="http://www.eggheadcafe.com/articles/20021012.asp">http://www.eggheadcafe.com/articles/20021012.asp</a></p>
<p><a href="http://www.aspxboy.com/476/archive.aspx">http://www.aspxboy.com/476/archive.aspx</a></p>
<p></p>				
