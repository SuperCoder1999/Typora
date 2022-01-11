创建的数据库

---

1. 学习JdbcTemplate时创建的user_db
   还有其下的表 :

   ```mysql
   CREATE TABLE `t_book` (
     `user_id` bigint(20) NOT NULL,
     `username` varchar(100) NOT NULL,
     `ustatus` varchar(50) NOT NULL,
     PRIMARY KEY (`user_id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8
   
   create table t_account(
   id varchar(20) primary key,
   username varchar(50) not null,
   money int default 0);
   insert into t_account values("1", "lucy", 1000);
   insert into t_account values("2", "mary", 1000);
   ```