---
layout: post
title: 好像是 sqlserver mangage studio express 的bug
comments: true
date: 2006-09-21
tags:
- 闲言碎语
---

<p>sqlserver 2005 express<br />使用 sqlserver mangage studio express <br /><br />创建一个测试用表<br />CREATE TABLE [dbo].[test](<br /> [id] [int] IDENTITY(1,1) NOT NULL,<br /> [name] [varchar](50) COLLATE Japanese_CI_AS NULL<br />) ON [PRIMARY]<br /><br />执行 insert test ([name]) values('sdfsdf');  多次。<br /><br />创建一个存储过程<br />create PROCEDURE [dbo].[xxx]</p>
<br /><p>AS<br />update test set [name] = 'aaa' where id =  2<br /><br /><br />然后<br /><br />ALTER PROCEDURE [dbo].[xxx]</p>
<br /><p>AS<br />update testxx32453463465346436x set [name] = 'aaa' where id =  2<br /><br />竟然不进行语法检查，而且执行成功了<br /><br />执行被alter过的过程时才会报错误<br /><br />Msg 208, Level 16, State 1, Procedure xxx, Line 10<br />对象名  'testxx32453463465346436x ' 无效。</p>
<br /><p>(1 row(s) affected)<br /></p>				
