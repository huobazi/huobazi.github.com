---
layout: post
title: 博客园到Wordpress搬家成功！
comments: true
date: 2009-06-21 14:50
categories:
- LAMP
- 闲言碎语
- .Net其他
- 奇技淫巧
- Wordpress
- Blogging
---

<p>终于把在博客园的博客的数据导入到Wordpress内了，包括随笔/文章，图片,标签，评论等，是写了两个C# console程序做到的，程序我传到博客园了，如果有需要的朋友可以试试。但请注意，要自己在博客园后台备份RSS文件放到Reader的Data目录内，设置为编译选项为永远复制，运行后会生成一个Entry.xml并且把博客内的图片和分类、Tag、评论等抓下来，然后将此xml文件拷贝到Writer内，在代码内修改一下你的Wordress的数据库连接，然后跑一下Writer，就可以完成数据导入到Wordpress了，时间匆忙，代码写的很乱，有些地方是针对本人需求处理的，如果你想要直接运行此程序完成你的博客园博客到Wordpress的转换，<strong>那是不可能滴！</strong>你一定要有简单的C#调试基础哦。</p>
<p><a href="http://files.cnblogs.com/huobazi/MyBlogTools.rar">http://files.cnblogs.com/huobazi/MyBlogTools.rar</a></p>				
