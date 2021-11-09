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

SQL语句中的单行注释使用 --

SQL语句中的多行注释采用 /*…*/

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
   - 表达式计算后的类型和原来的列类型不是一定相同的。会尽可能保证数据的正确。123



---

# 考点

1. 索引是什么
2. 索引要解决什么问题
3. 索引的应用场景
4. 索引的数据结构
   1. 为啥不用哈希
   2. 为啥不用二叉搜索树
   3. 啥是b树，有什么优势
   4. 什么是b+树，有什么优势
5. 其他



# 复习

1. mysql -h host -P 3306 -u root -pN331150871;

2. **create database if not exists hsp_db01 character set utf8 collate utf8_bin;**

3. **general_ci 不区分  utf8_bin 区分**

4. show databases;

5. **show create database hsp_db01;**

6. **drop database if exists hsp_db01;** 

7. **反引号** 区分关键字 

8. **datadump -u root -pN331150871 -B hsp_db01 hsp_db02 > /home/exercise/hsp_bf.sql;**

9. (只能在dos界面进行操作) source /home/exercise/hsp_bf.sql;

10. (需要进入任意一个数据库中)  datadump -u root -pN331150871 hsp_db01 name user > /home/exercise/hsp_bftable.sql;

11. create table `user` ( 
    int id,
    `name` verchar(20),
    ) character set utf8 collate utf8_bin engine default;
    
12. drop table table_name;

13. 无符号整数类型  INT UNSIGNED

    1. tinyint 1
    2. smallint 2
    3. mediumint 3
    4. int 4
    5. bigint 8
    6. bit(1~64) 默认1
    7. float 4
    8. double 8
    9. decimal(M,D) M默认10  D默认 0 M：1-65 D：0-30
    10. char(size)  size:1-255
    11. varchar(size)  size:1-2^16-1字节 / 对应字符集 (如果字符集是utf8，而存入的大多数字符是一个字符的英文，那么varchar的最大空间并没有占满)
    12. blob 二进制  可以定义其大小  最大 2^16-1字节
    13. text 最大2^16-1字节，longtext 2^32-1字节
    14. char的查询速度大于varchar

14. 修改表：

    1. 添加列 

       ~~~sql
       alter table table_name 
       add col_name datatype [default expr]
       after other_col;
       ~~~

    2. 修改列

       ~~~sql
       alter table table_name
       modify col_name datatype [default expr];
       ~~~

    3. 删除列

       ~~~sql
       alter table table_name
       drop col_name;
       ~~~

    4. 查看表结构

       ~~~sql
       desc table_name;
       ~~~

    5. 修改表名

       ~~~sql
       rename table table_name to new_table_name;
       ~~~

    6. 修改表字符集

       ~~~sql
       alter table table_name charset utf8;
       ~~~

    7. 修改列名

       ~~~sql
       alter table table_name change col_name new_col_name datatype [default expr];
       -- 感觉这不像是修改列名，更像是删除重新创建一个列，要不然也不会规定 type。如果不规定type呢？
       ~~~

15. insert into table_name(col1, col2)

    values(value1, value2), (), ();

16. update table_name
    set col_name=value, col_name=value + 10

    where expr ;

17. 规则：只有在创建/删除 database、table 时才会有 table。或许因为这两个命令是共享的，需要区分。

18. delete from table_name where expr;

19. select distinct col_name from table_name;

20. select (math+english) as total from table_name;

21. select * from name like '韩%';

22. select * from id between 10 and 90;

23. select * from student order by col_name desc/asc;

24. 合计 / 统计函数

    1. select count(col_name) as '计数器' from student where expr;
    2. select sum(col_name) '求和' from student where expr;
    3. select avg(col_name) as '平均'
    4. select max(col_name) as 
    5. select min(col_name) as 1

25. select * from table_name group by col1, col2 having expr;

26. 字符串相关函数

    1. 字符集：select charset(str) from table_name;
    2. 拼接: concat(str1, str2, ....)
    3. 判断存在: instr(str, str1)
    4. 转换大小写: lcase(str)  ucase(str)
    5. 从左、右取: left(str, num)  right(str, num)
    6. 长度：length(str)
    7. 替换：replace(str, search_str, replace_str);
    8. 比较：strcap(string1, string2);
    9. 截取：substring(str, head, length);
    10. 去空格：ltrim(str)  rtrim(str)  trim(str)

27. crtl+f  在 参考手册中 查找 字符串

28. 数学相关函数

    1. 绝对值：abs(num) 
    2. 二进制：bin(num)
    3. 向上取整：ceiling(num)
    4. 进制转换：conv(num, from, to)
    5. 保留小数位数：**format(num, length)**
    6. 十六进制：hex(num)
    7. 最小值：**least(num1, num2, num3)**
    8. 取余：mod(num, deno)
    9. 随机数：rand([seed])

29. 时间相关函数

    1. 当前日期：current_date()
    2. 当前时间：current_time()
    3. 当前时间戳：current_timestamp();
    4. 当前时间：now()
    5. 提取日期：date(datetime);
    6. 延长时间：**date_add(time, INTERVAL num type)**
    7. 缩短时间：**date_sub(time, INTERVAL num type)**
    8. 相差天数：datediff(time1, time2)
    9. 当差时间：timediff(time1, time2)
    10. 提取年数 、月数、日：year(time)  month(time)  day(time)
    11. 返回时间戳：unix_timestamp()
    12. 格式化时间戳：from_unixtime(time, '%Y-%m-%d %H:%i:%s')

30. 加密和系统函数

    1. 查询用户：user()
    2. 查询使用的数据库：**datebase()**
    3. MD5加密：md('123')  
       1. 用户密码管理：
       2. 先创建 char(32) not null default '';
       3. 插入 insert users values('hsp', MD('password'));
       4. 登录时的查找：select * from users where name='hsp' and MD('输入的密码')=MD('password');
    4. password加密：password('hsp');

31. 流程控制函数

    1. if：if(expr, expr_true, expr_false)

    2. ifnull：ifnull(主要的， 备用)

    3. case when expr1 then expr2 

       when expr3 then expr4

       else expr5

       end

    4. 比较运算符可以比较时间：current_date > '2021-01-19'  

    5. like的 %  _  ：name='韩%

       name='_顺%‘

    6. is null：name is null

32. 表结构：desc table_name

33. 多条件的order by：order by col1 desc , col2 desc; 

34. 分页查询：limit s, n            limit  n  offset   s;   --  s从0开始

    1. 公式 ：limit (第n页-1) * 每页数据量  ，每页数量 

35. group by job;

36. 命令的顺序 ：

    1. select col from table_name
       group by col

       having expr

       order by col

       limit s, n;

    2. having 必须是在 group 和 select 形成的临时表中进行 筛选

    3. order by 可以是任意列名

    4. limit 也是在临时表的基础上分页

37. 笛卡尔积：select * from table1, table2;

38. 笛卡尔积筛选规律：筛选条件 比 表的数量 少一个

39. 1



