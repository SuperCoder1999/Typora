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

1. dos界面登录mysql：mysql -h host -P 3306 -u root -pN331150871;

2. 创建数据库：**create database if not exists hsp_db01 character set utf8 collate utf8_bin;**

3. **general_ci 不区分  utf8_bin 区分**

4. 显示所有数据库：show databases;

5. 显示创建数据库的命令：**show create database database_name;**

6. 删除数据库：**drop database if exists hsp_db01;** 

7. **反引号** 区分关键字 

8. 备份数据库：**datadump -u root -pN331150871 -B database_name1 database_name2 > /home/exercise/hsp_bf.sql;**

9. 恢复数据库：(只能在dos界面进行操作) source /home/exercise/hsp_bf.sql;

10. 备份表：(需要进入任意一个数据库中)  datadump -u root -pN331150871 database_name table_name1 table_name2 > /home/exercise/hsp_bftable.sql;

11. 创建表：create table `user` ( 
    int id,
    `name` verchar(20),
    ) character set utf8 collate utf8_bin engine default;
    
12. 删除表：drop table table_name;

13. 无符号整数类型  INT UNSIGNED ----  类型 下午 进行详细复习

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

15. 在表中插入数据：insert into table_name(col1, col2)

    values(value1, value2), (), ();

16. 更新表数据：update table_name
    set col_name=value, col_name=value + 10

    where expr ;

17. 规则：只有在创建/删除 database、table 时才会有 table。或许因为这两个命令是共享的，需要区分。

18. 删除表记录：delete from table_name where expr;

19. 查找表记录：select distinct col_name from table_name;

20. 带有表达式的查找：select (math+english) as total from table_name;

21. like 操作符：select * from name like '韩%';

22. where运算符：select * from id between 10 and 90;

23. 排序：select * from student order by col_name desc/asc;

24. 合计 / 统计函数

    1. select count(col_name) as '计数器' from student where expr;
    2. select sum(col_name) '求和' from student where expr;
    3. select avg(col_name) as '平均'
    4. select max(col_name) as 
    5. select min(col_name) as 1

25. 分组：select * from table_name group by col1, col2 having expr;

26. 字符串相关函数

    1. 字符集：select charset(str) from table_name;
    2. 拼接: concat(str1, str2, ....)
    3. 判断存在: instr(str, str1)
    4. 转换大小写: lcase(str)  ucase(str)
    5. 从左、右取: left(str, num)  right(str, num)
    6. 长度：length(str)
    7. 替换：replace(str, search_str, replace_str);
    8. 比较大小：strcap(string1, string2);
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

    1. 查询登录用户：user()
    2. 查询使用的数据库：select **datebase()**;
    3. MD5加密：md5('123')  
       1. 用户密码管理：
       2. 先创建 char(32) not null default '';
       3. 插入 insert users values('hsp', MD5('password'));
       4. 登录时的查找：select * from users where name='hsp' and MD5('输入的密码')=MD5('password');
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

39. 单列子查询

    1. 单行子查询：select * from emp where deptno=(select deptno from emp where ename='smith');
    2. 多行子查询：select * from emp where job in (select job from emp where ename='smith');

40. 多列子查询：select * from emp where (ename, deptno)=(select ename, deptno from emp where ename='smith');

41. 子查询作为临时表：
    select temp.*, dept.dname

    from dept, (

    select count(*), deptno from emp

    where deptno='10') as temp

    where temp.deptno=dept.deptno;

42. 多表查询 all = max()  any=min()
    select * from where sal > all (select sal from emp);

    select * from where sal > (select MAX(sal) from emp);

43. 蠕虫复制：

    1. 复制别人  insert into  table_name(col1, col2) select col1, col2 from table_name_from;
    2. 自我复制：insert into table_name   select * from table_name_from;
    
44. 去重：

    1. 先创建一个临时表temp
    2. select into temp (select distinct * from table_name);
    3. 清空 table_name
    4. 将temp表内容转移到table_name中，将temp表删除

45. 复制表结构：create table table_name like table_name_from;

46. 合并查询：select ename, sal from table1 union all select ename, sal from table2; union all - 不去重  union - 去重

47. 表外连接

    1. 左外连接 ：select ename, sal from emp left join dept on ename='smith';
    2. 右连接：select ename, sal from emp right join dept on ename='smith';

48. 主键约束：

    1. id int primary key,
    2. ( primary key(id, ename) );

49. 非空约束：not null

50. 唯一约束：unique   (null可以有多个)

51. 外键 约束：foreign key(col_name) references table_name(col_name);

52. check：sql语法支持，但是没有作用。check(expr) 

53. 自增长(一般搭配unique\primary key使用)：id int primary key auto_increment;

    1. 插入有三种方式
    2. 修改自增长起始值：alter table table_name auto_increment=100;

54. 索引

    1. 主键索引、唯一索引都可以通过创建表的时候，一起声明
    2. 创建索引
       1. 创建普通(唯一)索引:
          1. create [unique] index index_name on table_name(col);
          2. alter table table_name add index [index_name] col_name;
       2. 创建主键索引：alter table table_name add primary key(col_name);
    3. 删除索引
       1. 删除普通(唯一)索引 - *唯一索引的删除方式不知道*
          1. drop index index_name on table_name;
          2. alter table table_name drop index index_name;
       2. 删除主键索引：alter table table_name drop primary key;
    4. 查询索引：
       1. show index(es) from table_name;
       2. show keys from table_name;
       3. desc table_name;
    5. 一般什么情况下使用索引：
       1. 查询频繁
       2. 增删改 不频繁
       3. where 语句中常用到
       4. 重复率低的字段

55. 事务

    1. 事务是什么：事务用于保证数据的一致性，它由dml语句组成，该组的dml语句要么全部成功执行，要么全部失败。
    2. 事务的命令：
       1. 开启事务：start transcation; / set autocommit=off;
       2. 设置保存点：savepoint a;
       3. 回退事务：rollback a;
       4. 返回事务开启状态：rollback;
       5. 提交事务：commit;

56. 全文索引要求存储引擎：MyISAM 事务要求引擎：InnoDB

57. inner join

58. [力扣182](https://leetcode-cn.com/problems/duplicate-emails/submissions/) 临时表单独用

59. [力扣183](https://leetcode-cn.com/problems/customers-who-never-order/submissions/)  力扣 中的临时必须 取别名。不只 力扣需要对临时表取别名，这是 sql语法规定的。

60. 

61. 隔离级别

    1. 隔离级别引出的问题：
       1. 脏读：在当前会话事务未提交前 读了别人事务中未提交的操作
       2. 不可重复读：在当前会话事务未提交前 读了别人提交的修改、删除的记录
       3. 幻读：在当前会话事务未提交前 读到了别人插入的数据
    2. 隔离级别划分：
       1. 读未提交(Read uncommitted) ：会产生脏读、不可重复读、幻读
       2. 读提交(Read committed)：会产生不可重复读、幻读
       3. 可重复度(Repeatable read)：不会产生 脏读、不可重复读、幻读
       4. 可串行化(Serializable)：不会产生脏读、不可重复读、幻读，并且会加锁(同一时刻，只有一个会话进入事务)
    3. 查看、设置事务隔离级别
       1. 查看当前会话隔离级别：select @@tx_isolation;
       2. 查看系统当前会话隔离级别：select @@global.tx_isolation;
       3. 设置当前会话隔离级别：set session transcation isolation level 级别名
       4. 设置系统当前会话隔离级别：set global session transcation isolation level 级别名
       5. 默认事务隔离界别：Repeatable read;
    4. 事务的ACID特性
       1. 原子性（Atomicity）
       2. 一致性（Consistency）
       3. 隔离性（Isolation）
       4. 持久性（Durability）

62. 存储引擎：

    1. MySQL支持6中存储引擎，常用的三个：InnoDB、MyISAM、Memory
    2. 存储引擎的命令操作
       1. 显示所有的存储引擎：show engines;
       2. 显示特定表的存储引擎：show table status from database_name where name='table_name' \G
       3. 修改表的存储引擎：alter table table_name engine=MyISAM;    ----  和修改表的 字符集有点像

63. 关于 语句结束符：由以上三个图对比可知：
    “;”和“\g”没啥区别，作用完全一样，运行的结果都是以表格的形式表现出来；
    “\G”则是相当于把表旋转90°变成了纵向；
    当然，三者运行后的结果内容都是一样的，大家如果查询的时候结果比较多，建议用“\G”，这样看起来顺眼一点且方便读取。

64. 视图：

    1. 视图的操作命令
       1. 创建视图：create view view_name as (select ename, deptno from emp);
       2. 修改视图显示的列(相当于删除重建)：alter view view_name as (select ename from emp);
       3. 显示视图结构：desc view_name;
       4. 显示创建该视图的命令：**show create view view_name** (目前有了 数据库、视图的创建命令，创建表的命令：show create table table_name;)
       5. 删除视图：drop view view_name, view_name2;
    2. 视图文件后缀：.frm

65. 用户管理

    1. 用户表位置：mysql.user;
    2. 字段：host user authentication_string
    3. 
    4. 用户管理命令：
       1. 创建用户：create user 'user_name'@'host' identified by 'password';
       2. 查看用户：select * from mysql.user;
       3. 删除用户：drop user 'user_name'@'host';
       4. 修改用户密码：
          1. 修改自己的密码：** set password=password('密码');
          2. 修改他人密码：**set password for 'user_name'@'host'=password('密码');**
       5. 给用户授权：grant 权限列表 on database_name.table_name TO user_name@'host' identified by 'password';
       6. 收回用户授权：revoke 权限列表 on database_name.table_name from 'user_name'@'host';
       7. 刷新权限：flush privileges;1
