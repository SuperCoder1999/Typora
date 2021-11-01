1. 账户：root 密码：N331150871

---

# 数据库day1

## 常见类型

1. int
2. double
3. decimal
4. varchar
5. text

## 数据库操作

1. create database [库名]; 创建数据库
2. show databases [库名]; 查询数据库
3. drop database [库名]; 删除数据库
4. use [库名]; 使用数据库

## 数据表操作

1. create table [表名] (列名 数据类型);   创建表
2. desc [表名]; 查看表结构
3. show tables; 查看表单
4. drop table [表名];  删除表

## 插入操作

1. 全列插入

   insert (into可省略) [表名] values (对应的列数据); 

2. 指定列插入

   insert into [表名] (若干指定列) values (对应的列数据); 没有插入数据的列默认填充null

3. 一次插入多条记录

   insert into [表明] (列数据), (列数据);

---

# 数据库day2

## 查询操作

1. select * from [表名]; 全列查询
2. select [列名], [列名] from [表名];  指定列查询
3. select [列名], [列名]+[列名];  查询字段为表达式(针对查到的列进行一定的表达式计算)
   - 表达式计算后的类型和原来的列类型不是一定相同的。会尽可能保证数据的正确。
