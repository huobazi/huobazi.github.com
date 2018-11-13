---
layout: post
title: 将MySQL 的数据导入 PostgreSQL
date: 2012-09-12
comments: true
tags: 
- Ruby
- MySQL
- PostgreSQL
- Postgres
---

开始学习使用PostgreSQL, 先尝试将MySQL数据导入到PostgreSQL

## 安装PostgreSQL

```bash
sudo apt-get install postgresql postgresql-client postgresql-contrib  
```
基本按照[http://wiki.ubuntu.org.cn/PostgreSQL](http://kiki.ubuntu.org.cn/PostgreSQL)进行设置就OK了

## 安装开发工具

```bash
sudo apt-get install libpq-dev pgadmin3
```
PgAdmin3 这是一个桌面 GUI 工具, 可以很方便的管理 PostgreSQL

## 用到的RubyGems

在 Gemfile 中增加：
```ruby
gem "pg" 
gem "mysql2"
```
然后 
```bash
bundle install
```
<!--more-->

### 完整的 Ruby 代码

```
# coding: utf-8
require 'mysql2'
require 'pg'

mysql_client = Mysql2::Client.new(:host => "localhost", :username =>"root", :password => "pa$$word", :database => "my_test", :encoding => "utf8")

postgres_client = PG::Connection.new(:host => "localhost", :dbname => 'mydb', :user => "postgres", :password => "pa$$word")
postgres_client.set_client_encoding('utf8')

mysql_result = mysql_client.query('select `code`,`name`,`level` from `chinese_regions`')

step = 0
mysql_result.each do |row|

  the_code = row['code']
  the_name = row['name']
  the_level = row['level'].to_i
  insert_sql_test = "insert into chinese_regions (\"code\",\"name\",\"level\") values ('#{the_code}','#{the_name}','#{the_level}');"
  postgres_client.exec(insert_sql_test)

  step += 1
  puts '-' + step.to_s + '-' + the_code + '--' + the_name + '--' + the_level.to_s

end

```

Run 啊 Run 啊的就 OK 了

