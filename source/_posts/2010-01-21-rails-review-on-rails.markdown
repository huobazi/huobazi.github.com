---
layout: post
title: 优化Rails数据库查询性能 -- rails_reviewer插件
comments: true
date: 2010-01-21 20:28
categories:
- LAMP
- Rails
- Mysql
- rails_reviewer
---

<p>发现一个很棒的插件<a href="http://github.com/dsboulder/query_reviewer" target="_blank"> rails_reviewer</a>插件</p>
<p>安装:</p>
<div class="source" style='font-family: "[object HTMLOptionElement]","Consolas","Lucida Console","Courier New"; color: #e6e1dc; background-color: #111111;'>
<span style="color: #e6e1dc;">$</span> <span style="color: #e6e1dc;">script</span><span style="color: #e6e1dc;">/</span><span style="color: #e6e1dc;">plugin</span> <span style="color: #e6e1dc;">install</span> <span style="color: #e6e1dc;">git</span><span style="color: #a5c261;">:/</span><span style="color: #e6e1dc;">/</span><span style="color: #e6e1dc;">github</span><span style="color: #e6e1dc;">.</span><span style="color: #e6e1dc;">com</span><span style="color: #e6e1dc;">/</span><span style="color: #e6e1dc;">dsboulder</span><span style="color: #e6e1dc;">/</span><span style="color: #e6e1dc;">query_reviewer</span><span style="color: #e6e1dc;">.</span><span style="color: #e6e1dc;">git</span><br /><span style="color: #e6e1dc;">$</span> <span style="color: #e6e1dc;">rake</span> <span style="color: #e6e1dc;">query_reviewer</span><span style="color: #a5c261;">:setup</span>
</div>
<p>完毕后重启server,页面左上角浮动一个SQL CRITICAL浮动窗口，里面记录页面加载时执行的所有SQL以及优化建议等。</p>
<p>强烈推荐 !!!</p>				
