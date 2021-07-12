---
title: MYSQL笔记
date:  2021-02-25 15:00:36
cover: https://raw.githubusercontent.com/PureKits/hexo_pictures_source/main/MYSQL_20210225.png
tags: 
- MYSQL
- 编程
- 水博客
categories: MYSQL
---



一名沙雕大学生的MYSQL学习笔记

<!-- more -->





# MYSQL

[TOC]



---



### MYSQL  连接



使用二进制方式进入mysql命令提示符下来连接mysql数据库

````mysql
Purekit@Mac ~~ mysql -u root -p
enter password:    *输入密码*
````

接下来就进入到了mysql命令操作中

````mysql
mysql> exit;  *或者quit*  //退出mysql//   
````



---



### MYSQL 创建数据库



##### create命令创建数据库 

````mysql
mysql > CREATE  DATABASE database_name ；
````



##### 了解数据库和表

````mysql
show databases;//返回当前所有的数据库

show tables;//返回当前数据库下可用的表

show columns from table_name ;//返回表结构
````



##### 选择使用数据库**USE**

````mysql
mysql > use rootme ;
Database changed
````

> 执行以上命令后，你就已经成功选择了**rootme** 数据库，在后续的操作中都会在**rootme**数据库中执行



---



### MYSQL  数据类型

> MySQL中定义数据字段的类型对你数据库的优化是非常重要的。

> MySQL支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型。



##### 数值类型

> MySQL支持所有标准SQL数值数据类型。这些类型包括严格数值数据类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据类型(FLOAT、REAL和DOUBLE PRECISION)。关键字INT是INTEGER的同义词，关键字DEC是DECIMAL的同义词。BIT数据类型保存位字段值，并且支持MyISAM、MEMORY、InnoDB和BDB表。作为SQL标准的扩展，MySQL也支持整数类型TINYINT、MEDIUMINT和BIGINT。下面的表显示了需要的每个整数类型的存储和范围。

| 类型          | 大小                                    | 范围（有符号）                                               | 范围（无符号）                                               | 用途             |
| :------------ | :-------------------------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ | ---------------- |
| tiyint        | 1byte                                   | (-128，127)                                                  | (0，255)                                                     | 小整数值         |
| smallint      | 2bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值         |
| mediumint     | 3bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值         |
| int or intger | 4bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，18 446 744 073 709 551 615)                              | 大整数值         |
| bigint        | 8bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 极大整数值       |
| float         | 4bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 单精度  浮点数值 |
| double        | 8bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 依赖于M和D的值                                               | 双精度 浮点数值  |
| decimal       | 对decimal（m,d)，如果m>d,为，m+2否则d+2 | 依赖于M和D的值                                               |                                                              | 小数值           |



##### **日期和时间类型**

> 表示时间值的日期和时间类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。每个时间类型有一个有效值范围和一个"零"值，当指定不合法的MySQL不能表示的值时使用"零"值。TIMESTAMP类型有专有的自动更新特性，将在后面描述。

| 类型      | 大小（bytes） | 范围                                                         | 格式                | 用途                     |
| --------- | ------------- | ------------------------------------------------------------ | ------------------- | ------------------------ |
| data      | 3             | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| time      | 3             | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| year      | 1             | 1901/2155                                                    | YYYY                | 年份值                   |
| datatime  | 8             | 1000-01-01 00:00:00/9999-12-31 23:59:59                      | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| timestamp | 4             | 1970-01-01 00:00:00/2038结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07 | YYYYMMDDHHMMSS      | 混合日期和时间值，时间戳 |



##### **字符串类型**

> 字符串类型指CHAR、VARCHAR、BINARY、VARBINARY、BLOB、TEXT、ENUM和SET。该节描述了这些类型如何工作以及如何在查询中使用这些类型。

| 类型       | 大小                  | 用途                           |
| ---------- | --------------------- | ------------------------------ |
| char       | 0-255bytes            | 定长字符串                     |
| varchar    | 0-65535bytes          | 变长字符串                     |
| tinyblob   | 0-255bytes            | 不超过255个字符的二进制字符串  |
| tinytext   | 0-255bytes            | 段文本字符串                   |
| blob       | 0-65bytes             | 二进制形式的长文本字符串       |
| text       | 0-65  535 bytes       | 长文本数据                     |
| mediumblob | 0-16 777 215  bytes   | 二进制形式的中等长度的文本数据 |
| mediumtext | 0-16 777 215  bytes   | 中等长度的文本数据             |
| longblob   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据       |
| longtext   | 0-4 294 967 295 bytes | 极大文本数据                   |



---



### MYSQL 表的创建

创建mysql数据表需要以下信息：

* > 表名
* > 表字段名
* > 定义每个表字段



以下为创建mysql数据表_**table** 的sql通用语法：

````mysql
CREATE TABLE  table_name (column_name column_type);
````



##### **create table  **

> 以下我们将创建数据表**root**：

````mysql
Purekit@Mac~~ mysql -u root -p
Enter password:*******
mysql> use rootme;
Database changed
mysql> CREATE TABLE root(
   -> id INT NOT NULL AUTO_INCREMENT,
   -> name  VARCHAR(100) NOT NULL,
   -> address VARCHAR(100) NOT NULL,
   -> nowtime  DATE,
   -> PRIMARY KEY (id )
   -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.16 sec)
mysql>
````

> >  注意：命令终止符为分号 ;  ,

- > 如果你不想字段为 **NULL** 可以设置字段的属性为 **NOT NULL**， 在操作数据库时如果输入该字段的数据为**NULL** ，就会报错。

- > AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。

- > PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。

- > ENGINE 设置存储引擎，CHARSET 设置编码。



以下将使用mysql 命令检索创建表结构

````mysql
describe table_name ; //可以简写为 desc

or

show create table table_name ; //查看创建表的语句

or

show columns from table_name ;//同 desc 命令作用一样
````



 ![image-20200501110909834](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200501110909834.png)





---



### MYSQL INSERT INTO 



以下为向mysql数据表中插入数据通用的**insert  into table_ name  values** sql 语法：

````mysql
INSERT  INTO table_name (field1 ,  field2 , .......fieldN )
													values 
													(values1 , values2 , .......valuesN);
如果数值是字符型，必须使用单引号或者双引号，如“values”。
````



以下我们向**root**表中插入三条数据：

````mysql
purekit@mac~~ mysql -u root -p
enter password:*******
mysql > use rootme ;
Database changed 
mysql > INSERT INTO root
     -> VALUES
     -> (1,"学习 PHP", "菜鸟教程", NOW());
Query OK, 1 rows affected, 1 warnings (0.01 sec)
mysql >  INSERT INTO root
     -> VALUES
     -> (2,"学习 MySQL", "菜鸟教程", NOW());
Query OK, 1 rows affected, 1 warnings (0.01 sec)
mysql > INSERT INTO root
     -> VALUES
     -> (3,"JAVA 教程", "RUNOOB.COM", NOW());
Query OK, 1 rows affected (0.00 sec)
mysql >
````



接下来我们可以通过以下语句查询数据表数据：

`读取数据表`

`select  * from root ; `

`输出结果`

 ![image-20200501112856984](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200501112856984.png)



---



### SELECT  检索

> 数据库使用**select**语句进行查询数据



以下为在mysql数据库中查询数据通用的**select**语法：

````mysql
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]
````

- > 查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件
- > SELECT 命令可以读取一条或者多条记录。
- > 你可以使用星号（*）来代替其他字段，SELECT语句会返回表的所有字段数据
- > 你可以使用 WHERE 语句来包含任何条件
- > 你可以使用 LIMIT 属性来设定返回的记录数
- > 你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0



使用样本数据库 **websites**

 ````mysql
mysql> select * from websites;
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  1 | Google   | www.google.com   |     1 | USA     |
|  2 | taobao   | www.taobao.com   |    13 | CN      |
|  3 | weibo    | www.weibo.com    |    20 | CN      |
|  4 | facebook | www.facebook.com |     3 | USA     |
|  5 | JD       | www.JD.com       |    10 | CN      |
+----+----------+------------------+-------+---------+
5 rows in set (0.00 sec)

mysql>
 ````



##### 检索单个列

````mysql
select 字段名 from table_name ;
````

````mysql
mysql> select name from websites;
+----------+
| name     |
+----------+
| Google   |
| taobao   |
| weibo    |
| facebook |
| JD       |
+----------+
5 rows in set (0.00 sec)

mysql>
````



##### 检索多个列

````mysql
mysql> select name , id , country from websites;
+----------+----+---------+
| name     | id | country |
+----------+----+---------+
| Google   |  1 | USA     |
| taobao   |  2 | CN      |
| weibo    |  3 | CN      |
| facebook |  4 | USA     |
| JD       |  5 | CN      |
+----------+----+---------+
5 rows in set (0.00 sec)

mysql>
````



##### 检索所有列

> 使用通配符（ * ） 检索

````mysql
mysql> select * from websites;
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  1 | Google   | www.google.com   |     1 | USA     |
|  2 | taobao   | www.taobao.com   |    13 | CN      |
|  3 | weibo    | www.weibo.com    |    20 | CN      |
|  4 | facebook | www.facebook.com |     3 | USA     |
|  5 | JD       | www.JD.com       |    10 | CN      |
+----+----------+------------------+-------+---------+
5 rows in set (0.00 sec)
````



##### 检索不同的行

> 在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。**DISTINCT** 关键词用于返回唯一不同的值。

**SELECT DISTINCT 语法**

````mysql
SELECT DISTINCT column_name,column_name
FROM table_name;
````

**使用distinct**

> 下面的 SQL 语句仅从 "Websites" 表的 "country" 列中选取唯一不同的值，也就是去掉 "country" 列重复值：

````mysql
mysql> select country from websites;//没有使用 distinct
+---------+
| country |
+---------+
| USA     |
| CN      |
| CN      |
| USA     |
| CN      |
+---------+
5 rows in set (0.00 sec)

mysql>


mysql> select distinct  country from websites;
+---------+
| country |
+---------+
| USA     |
| CN      |
+---------+
2 rows in set (0.00 sec)

mysql>
````



##### 限制结果

> SELECT语句返回所有匹配的行，它们可能是指定表中的每个行。为了返回第一行或前几行，可使用LIMIT子句。

````mysql
mysql> select * from websites
    -> limit 2;
+----+--------+----------------+-------+---------+
| id | name   | url            | alexa | country |
+----+--------+----------------+-------+---------+
|  1 | Google | www.google.com |     1 | USA     |
|  2 | taobao | www.taobao.com |    13 | CN      |
+----+--------+----------------+-------+---------+
2 rows in set (0.00 sec)

mysql>
````



##### 完全限定表名、字段名

````mysql

mysql> select websites.name from websites;
+----------+
| name     |
+----------+
| Google   |
| taobao   |
| weibo    |
| facebook |
| JD       |
+----------+
5 rows in set (0.00 sec)

mysql>

mysql> select websites.name from rootme.websites;
+----------+
| name     |
+----------+
| Google   |
| taobao   |
| weibo    |
| facebook |
| JD       |
+----------+
5 rows in set (0.00 sec)

mysql>
````



---

 

### ORDER BY 排序检索

> 我们知道从 MySQL 表中使用 SQL SELECT 语句来读取数据。如果我们需要对读取的数据进行排序，我们就可以使用 MySQL 的 **ORDER BY** 子句来设定你想按哪个字段哪种方式来进行排序，再返回搜索结果。



以下是SQL **SELECT**语句使用**ORDER BY** 子句将查询数据**排序后**在返回数据：

````mysql
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
ORDER BY field1 [ASC [DESC][默认 ASC]], [field2...] [ASC [DESC][默认 ASC]]
````

- > 你可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。

- > 你可以设定多个字段来排序。

- > 你可以使用 **ASC** 或 **DESC** 关键字来设置查询结果是按**升序**或**降序**排列。 默认情况下，它是按**升序**排列。

- > 你可以添加 WHERE...LIKE 子句来设置条件。





##### **ASC（升序）** 

> 以下将在SQL **SELECT**语句中使用**ORDER BY **子句来读取mysql数据表**root**中的数据：  默认是升序排列

````mysql
mysql> select * from websites order by id asc ;
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  1 | Google   | www.google.com   |     1 | USA     |
|  2 | taobao   | www.taobao.com   |    13 | CN      |
|  3 | weibo    | www.weibo.com    |    20 | CN      |
|  4 | facebook | www.facebook.com |     3 | USA     |
|  5 | JD       | www.JD.com       |    10 | CN      |
+----+----------+------------------+-------+---------+
5 rows in set (0.00 sec)

mysql>

````



##### **DESC(降序）**

````mysql
mysql> select * from websites order by id desc ;
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  5 | JD       | www.JD.com       |    10 | CN      |
|  4 | facebook | www.facebook.com |     3 | USA     |
|  3 | weibo    | www.weibo.com    |    20 | CN      |
|  2 | taobao   | www.taobao.com   |    13 | CN      |
|  1 | Google   | www.google.com   |     1 | USA     |
+----+----------+------------------+-------+---------+
5 rows in set (0.00 sec)

mysql>
````



##### 按多个列排序

````mysql
mysql> select * from websites
    -> order by name ,id;
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  4 | facebook | www.facebook.com |     3 | USA     |
|  1 | Google   | www.google.com   |     1 | USA     |
|  5 | JD       | www.JD.com       |    10 | CN      |
|  2 | taobao   | www.taobao.com   |    13 | CN      |
|  3 | weibo    | www.weibo.com    |    20 | CN      |
+----+----------+------------------+-------+---------+
5 rows in set (0.00 sec)

mysql>
````



---



### WHERE 过滤数据 

> 我们知道从mysql表中使用**sql  select **语句来读取数据

> 如需有条件地从表中选取数据，可将**where**子句添加到**select** 语句中



以下是利用**select where** 从数据表中读取数据的通用语法

````mysql
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
[WHERE condition1 [AND [OR]] condition2.....
````

- > 查询语句中你可以使用一个或者多个表，表之间使用逗号**,** 分割，并使用WHERE语句来设定查询条件。
- > 你可以在 WHERE 子句中指定任何条件。
- > 你可以使用 AND 或者 OR 指定一个或多个条件。
- > WHERE 子句也可以运用于 SQL 的 DELETE 或者 UPDATE 命令。
- > WHERE 子句类似于程序语言中的 if 条件，根据 MySQL 表中的字段值来读取指定的数据。



##### WHERE 可使用操作符

> 以下为操作符列表，可用于 WHERE 子句中下表中实例假定 A 为 10, B 为 20

| 操作符  | 描述                                                         | 实例                     |
| ------- | ------------------------------------------------------------ | ------------------------ |
| =       | 等号，检测两个值是否相等，如果相等返回true                   | （ A = B ）返回false     |
| <> , != | 不等于，检测两个值是否相等，如果不相等返回true               | （ A != B )  返回true    |
| >       | 大于号，检测左边的值是否大于右边的值如果左边的值大于右边的值返回true | （ A > B ) 返回false     |
| >=      | 大于等于号，检测左边的值是够大于获等于右边的值，如果左边的值大于或等于右边的值返回true | （ A >= B ) 返回true     |
| <       | 小于号，检测左边的值是否小于右边的值如果小于返回true         | （ A < B ) 返回ture      |
| <=      | 小于等于号，检测左边的是否小于或者等于右边的值如果成立返回ture | （ A <= B ) 返回ture     |
| between | 在指定的两个值之间 A--B之间                                  | 返回 A--B 之间的所有数据 |



##### 检查单个值

> mysql执行匹配时不区分大小写

````mysql
mysql> select * from websites
    -> where id = 4;			//返回 id 列等于 4 数据
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  4 | facebook | www.facebook.com |     3 | USA     |
+----+----------+------------------+-------+---------+
1 row in set (0.00 sec)

mysql>
````



##### 空值检查（NULL）

> NULL  无值 ，他与字段包含0、空字符串仅仅包含空格不同
>
> SELECT语句有一个特殊的WHERE子句，可用来检查具有NULL值的列。 这个WHERE子句就是IS NULL子句。：



##### 使用binary区分检索大小写

> **MySQL 的 **WHERE子句的字符串比较是不区分大小写的。 你可以使用 **BINARY** 关键字来设定 WHERE 子句的字符串比较是区分大小写的.

````mysql
BINARY 关键字
mysql> select * from root where binary address = 'runoob.com';
Empty set (0.00 sec)

mysql> select * from root where binary address = 'RUNOOB.COM' ;
+----+---------------+------------+------------+
| id | name          | address    | nowtime    |
+----+---------------+------------+------------+
|  3 | JAVA 教程     | RUNOOB.COM | 2020-05-01 |
|  4 | 学习 Python   | RUNOOB.COM | 2020-05-01 |
+----+---------------+------------+------------+
2 rows in set (0.00 sec)

mysql>
````

> 实例中使用了 **BINARY** 关键字，是区分大小写的，所以 **address='runoob.com'** 的查询条件是没有数据的.



---



### AND & OR 操作符 

> AND & OR 运算符用于基于一个以上的条件对记录进行过滤。

> 如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

> 如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。



##### **AND**

> 添加检索的附加条件 and（和）

````mysql
mysql> select * from websites
    -> where country = 'USA'
    -> and alexa < 10 ;
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  1 | Google   | www.google.com   |     1 | USA     |
|  4 | facebook | www.facebook.com |     3 | USA     |
+----+----------+------------------+-------+---------+
2 rows in set (0.00 sec)

mysql>
````



##### **OR**

> 添加检索的附加条件or（或者）

````mysql
mysql> select * from websites
    -> where country = 'CN'
    -> or country = 'USA' ;
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  1 | Google   | www.google.com   |     1 | USA     |
|  2 | taobao   | www.taobao.com   |    13 | CN      |
|  3 | weibo    | www.weibo.com    |    20 | CN      |
|  4 | facebook | www.facebook.com |     3 | USA     |
|  5 | JD       | www.JD.com       |    10 | CN      |
+----+----------+------------------+-------+---------+
5 rows in set (0.00 sec)

mysql>
````



##### 计算次序 AND&OR

> 当and or操作符在一个where语句中使用时就要考虑到计算次序的问题
>
> and 要比or优先  所以先进行and操作符工作 在进行or操作符工作

````mysql
mysql> select * from schools
    -> where type = 985 or type = 211 and address = 'Beijing' ;
+----+--------------------+------+---------+------+
| id | name               | type | address | area |
+----+--------------------+------+---------+------+
|  1 | 北京大学          | 985  | beijing | 7000 |
|  2 | 清华大学           | 985  | Beijing | 5886 |
|  3 | 北京科技大学       | 211  | Beijing | 1200 |
|  5 | 电子科技大学       | 985  | Chengdu | 5000 |
|  6 | 武汉大学           | 985  | Wuhan   | 5195 |
+----+--------------------+------+---------+------+
5 rows in set (0.00 sec)

mysql>
````



因为计算优先级的原因所以要进行综合检索的话要用（） 分隔开附加条件

````mysql
mysql> select * from websites
    -> where alexa > 1
    -> and ( country = 'CN' or country = 'USA' );
+----+----------+------------------+-------+---------+
| id | name     | url              | alexa | country |
+----+----------+------------------+-------+---------+
|  2 | taobao   | www.taobao.com   |    13 | CN      |
|  3 | weibo    | www.weibo.com    |    20 | CN      |
|  4 | facebook | www.facebook.com |     3 | USA     |
|  5 | JD       | www.JD.com       |    10 | CN      |
+----+----------+------------------+-------+---------+
4 rows in set (0.00 sec)

mysql>
````



##### IN 操作符

> 圆括号在WHERE子句中还有另外一种用法。IN操作符用来指定条件范 围，范围中的每个条件都可以进行匹配。IN取合法值的由逗号分隔的清 单，全都括在圆括号中。
>
> WHERE子句中用来指定要匹配值的清单的关键字，功能与OR 相当。

````mysql
mysql> select * from schools
    -> where address in ('wuhan' , 'Beijing');
+----+--------------------+------+---------+------+
| id | name               | type | address | area |
+----+--------------------+------+---------+------+
|  1 |  北京大学          | 985  | beijing | 7000 |
|  2 | 清华大学           | 985  | Beijing | 5886 |
|  3 | 北京科技大学       | 211  | Beijing | 1200 |
|  6 | 武汉大学           | 985  | Wuhan   | 5195 |
+----+--------------------+------+---------+------+
4 rows in set (0.00 sec)

mysql>
````



##### NOT 操作符

> WHERE子句中的NOT操作符有且只有一个功能，那就是否定它之后所 跟的任何条件。

````mysql
mysql> select * from schools
    -> where address not in('wuhan','Beijing');
+----+--------------------+------+-----------+------+
| id | name               | type | address   | area |
+----+--------------------+------+-----------+------+
|  4 | 郑州大学           | 211  | Zhengzhou | 5700 |
|  5 | 电子科技大学       | 985  | Chengdu   | 5000 |
+----+--------------------+------+-----------+------+
2 rows in set (0.00 sec)

mysql>
````

> 为什么使用NOT？对于简单的WHERE子句，使用NOT确实没有什么优 势。但在更复杂的子句中，NOT是非常有用的。例如，在与IN操作符联合 使用时，NOT使找出与条件列表不匹配的行非常简单。



---



### MYSQL UPDATE 

> 如果我们需要修改或更新 MySQL 中的数据，我们可以使用 SQL **UPDATE** 命令来操作。



以下是 **UPDATE** 命令修改 MySQL 数据表数据的通用 SQL 语法：

````mysql
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
````

- > 你可以同时更新一个或多个字段。
- > 你可以在 WHERE 子句中指定任何条件。
- > 你可以在一个单独表中同时更新数据。



**SQL UPDATE 语句：**

````mysql
mysql> update root set name = '学习 C++' where id = 3 ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from root where id = 3 ;
+----+------------+------------+------------+
| id | name       | address    | nowtime    |
+----+------------+------------+------------+
|  3 | 学习 C++   | RUNOOB.COM | 2020-05-01 |
+----+------------+------------+------------+
1 row in set (0.00 sec)

mysql>
````



<b>警告</b>：在更新记录时要格外小心！在上面的实例中，如果我们省略了 WHERE 子句，如下所示：

````mysql
UPDATE Websites
SET alexa='5000', country='USA'
````

> 执行以上代码会将 Websites 表中所有数据的 alexa 改为 5000，country 改为 USA。执行没有 WHERE 子句的 UPDATE 要慎重，再慎重。



---



### MYSQL DELETE 

> 你可以使用 SQL 的 **DELETE FROM** 命令来删除 MySQL 数据表中的记录。



以下是 SQL **DELETE** 语句从 MySQL 数据表中删除数据的通用语法：

````mysql
DELETE FROM table_name
WHERE some_column=some_value;
````

- > 如果没有指定 WHERE 子句，MySQL 表中的所有记录将被删除。
- > 你可以在 WHERE 子句中指定任何条件
- > 您可以在单个表中一次性删除记录。



**DELETE 语句：**

> 从命令行中删除数据

````mysql
mysql> use rootme;
Database changed
mysql> delete from root where id = 3 ;
Query OK, 1 row affected (0.23 sec)
````



**删除所有数据**

> 您可以在不删除表的情况下，删除表中所有的行。这意味着表结构、属性、索引将保持不变：

````mysql
DELETE FROM table_name;

OR

DELETE * FROM table_name;
````

> 注释：在删除记录时要格外小心！因为您不能重来！



---



### LIKE 通配符过滤 

> SQL**LIKE** 子句中使用百分号 **%**字符来表示任意字符，类似于UNIX或正则表达式中的星号 *****。如果没有使用百分号 **%**, LIKE 子句与等号 **=** 的效果是一样的    (我自己的理解相当于模糊搜索的意思)



以下是 **SQL SELECT **语句使用 **LIKE** 子句从数据表中读取数据的通用语法：

````mysql
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
````

- > 你可以在 WHERE 子句中指定任何条件。

- > 你可以在 WHERE 子句中使用LIKE子句。

- > 你可以使用LIKE子句代替等号 **=**。

- > LIKE 通常与 **%** 一同使用，类似于一个元字符的搜索。

- > 你可以使用 AND 或者 OR 指定一个或多个条件。

- > 你可以在 DELETE 或 UPDATE 命令中使用 WHERE...LIKE 子句来指定条件。



##### **% 替代字符检索**

> 以下是我们将**root**表中获取的**address**字段中以**com**结尾的所有数据记录：

````mysql
mysql> use rootme;
Database changed
mysql> select * from root where address like '%COM' ;
+----+---------------+------------+------------+
| id | name          | address    | nowtime    |
+----+---------------+------------+------------+
|  3 | 学习 C++      | RUNOOB.COM | 2020-05-01 |
|  4 | 学习 Python   | RUNOOB.COM | 2020-05-01 |
+----+---------------+------------+------------+
2 rows in set (0.00 sec)

mysql>
````



##### **like 可用通配符**

> 通配符可用于替代字符串中的任何其他字符。在 SQL 中，通配符与 SQL LIKE 操作符一起使用。SQL 通配符用于搜索表中的数据。

| 通配符                      | 描述                       |
| --------------------------- | -------------------------- |
| %                           | 替代0个或多个字符          |
| _                           | 替代一个字符               |
| [charlist]                  | 字符列中任何单一字符       |
| [^charlist]  or [!charlist] | 不再字符列中的任何单一字符 |



---

·

### UNION 

> MySQL UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。多个 SELECT 语句会删除重复的数据。



##### UNION 操作符语法：

````mysql
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT]
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
````

> > **参数**

- > **expression1, expression2, ... expression_n**: 要检索的列。

- > **tables:** 要检索的数据表。

- > **WHERE conditions:** 可选， 检索条件。

- > **DISTINCT:** 可选，删除结果集中重复的数据。默认情况下 UNION 操作符已经删除了重复数据，所以 DISTINCT 修饰符对结果没啥影响。

- > **ALL:** 可选，返回所有结果集，包含重复数据。

- > **UNION 语句**：用于将不同表中相同列中查询的数据展示出来；（不包括重复数据）

- > **UNION ALL 语句**：用于将不同表中相同列中查询的数据展示出来；（包括重复数据）



##### **演示数据库**

> 在本演示中我们将使用**rootme**数据库

> 下面选自**websites**表的数据：

````mysql
mysql> select * from websites ;
+----+----------+------------------+-------+--------+
| id | name     | url              | alexa |country |
+----+----------+------------------+-------+--------+
|  1 | Google   | www.google.com   |     1 | USA    |
|  2 | taobao   | www.taobao.com   |    13 | CN     |
|  3 | weibo    | www.weibo.com    |    20 | CN     |
|  4 | facebook | www.facebook.com |     3 | USA    |
|  5 | JD       | www.JD.com       |    10 | CN     |
+----+----------+------------------+-------+--------+
5 rows in set (0.00 sec)

mysql>
````

下面是**apps**表的数据：

````mysql
mysql> select * from apps;
+----+----------+----------------+--------+
| id | app_name | url            |country |
+----+----------+----------------+--------+
|  1 | QQ       | im.qq.com      | CN     |
|  2 | weibo    | www.weibo.com  | CN     |
|  3 | weixin   | www.weixin.com | CN     |
+----+----------+----------------+--------+
3 rows in set (0.00 sec)

mysql>
````



##### **UNION**

> 下面的 SQL 语句从 "Websites" 和 "apps" 表中选取所有**不同的**country（只有不同的值）：

````mysql
mysql> select country from websites
    -> union
    -> select country from apps
    -> order by country ;
+--------+
|country |
+--------+
| CN     |
| USA    |
+--------+
2 rows in set (0.00 sec)

mysql>
````

> <i>**注释:**UNION 不能用于列出两个表中所有的country。如果一些网站和APP</i>



##### **UNION ALL**

> 下面的 SQL 语句使用 UNION ALL 从 "Websites" 和 "apps" 表中选取**所有的**country（也有重复的值）：

````mysql
mysql> select country from websites
    -> union all
    -> select country from apps
    -> order by country ;
+--------+
|country |
+--------+
| CN     |
| CN     |
| CN     |
| CN     |
| CN     |
| CN     |
| USA    |
| USA    |
+--------+
8 rows in set (0.00 sec)

mysql>
````



##### 带有**WHERE**的 **UNION ALL** 

> 下面的 SQL 语句使用 UNION ALL 从 "Websites" 和 "apps" 表中选取**所有的**中国(CN)的数据（也有重复的值）：

````mysql
mysql> select country ,name from websites
    -> where country = 'CN'
    -> union all
    -> select country ,name from apps
    -> where country = 'CN'
    -> order by country;
+---------+--------+
| country | name   |
+---------+--------+
| CN      | taobao |
| CN      | weibo  |
| CN      | JD     |
| CN      | QQ     |
| CN      | weibo  |
| CN      | weixin |
+---------+--------+
6 rows in set (0.00 sec)

mysql>
````





---





### 正则表达式(REGEXP)

> 正则表达式是一组由字母和符号组成的特殊文本, 它可以用来从文本中找出满足你想要的格式的句子.

> 一个正则表达式是在一个主体字符串中从左到右匹配字符串时的一种样式. "Regular expression"这个词比较拗口, 我们常使用缩写的术语"regex"或"regexp". 正则表达式可以从一个基础字符串中根据一定的匹配模式替换文本中的字符串、验证表单、提取字符串等等.

> 想象你正在写一个应用, 然后你想设定一个用户命名的规则, 让用户名包含字符,数字,下划线和连字符,以及限制字符的个数,好让名字看起来没那么丑. 

**我们使用以下正则表达式来验证一个用户名:**

![image-20200504151108460](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504151108460.png)



##### **基本匹配**

正则表达式其实就是在执行搜索时的格式, 它由一些字母和数字组合而成. 例如: 一个正则表达式 `the`, 它表示一个规则: 由字母`t`开始,接着是`h`,再接着是`e`.

![image-20200504155636791](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504155636791.png)      

正则表达式`123`匹配字符串`123`. 它逐个字符的与输入的正则表达式做比较.

正则表达式是大小写敏感的, 所以`The`不会匹配`the`.

 ![image-20200504155708420](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504155708420.png)

简单匹配演示

````mysql

mysql> select * from websites
    -> where name regexp 'Goo';
+----+--------+----------------+-------+---------+
| id | name   | url            | alexa | country |
+----+--------+----------------+-------+---------+
|  1 | Google | www.google.com |     1 | USA     |
+----+--------+----------------+-------+---------+
1 row in set (0.00 sec)

````





##### **元字符**

> 正则表达式主要依赖于元字符. 元字符不代表他们本身的字面意思, 他们都有特殊的含义. 一些元字符写在方括号中的时候有一些特殊的意思. 以下是一些元字符的介绍:

| 元字符 | 描述                                                       |
| ------ | ---------------------------------------------------------- |
| .      | 句号匹配但个字符除了换行符                                 |
| [ ]    | 字符种类  匹配方括号内的任意字符                           |
| [^ ]   | 否定的字符种类，匹配除了方括号内的任意字符                 |
| *      | 匹配 >= 个重复在 * 之间的字符                              |
| +      | 匹配  >= 1 个重复在 + 号之间的字符                         |
| ?      | 标记 ？ 之前的字符为可选                                   |
| {n,m}  | 匹配 num 个中括号之前的字符（n <= num <= m)                |
| {xyz}  | 字符集，匹配与xyz完全相等字符串（大小写很敏感  要区分好）  |
| \|     | ’ 或 ‘ 运算符匹配符号之间前或后的字符                      |
| \      | 转义字符 用于匹配一些保留的字符`[ ] ( ) { } . * + ? ^ $ \` |
| ^      | 从开始行开始匹配                                           |
| &      | 从末端开始匹配                                             |





##### **点运算符 <font color = red>`.`</font>**

`.`是元字符中最简单的例子. `.`匹配任意单个字符, 但不匹配换行符. 例如, 表达式`.ar`匹配一个任意字符后面跟着是`a`和`r`的字符串.

 ![image-20200504155745504](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504155745504.png)

简单匹配演示

````mysql
mysql> select * from root
    -> where name regexp '.PHP' ;
+----+------------+--------------+------------+
| id | name       | address      | nowtime    |
+----+------------+--------------+------------+
|  1 | 学习 PHP   | 菜鸟教程     | 2020-05-01 |
+----+------------+--------------+------------+
1 row in set (0.00 sec)

mysql>
````





##### **字符集 [ ]**

字符集也叫做字符类. 方括号用来指定一个字符集. 在方括号中使用连字符来指定字符集的范围. 在方括号中的字符集不关心顺序. 例如, 表达式`[Tt]he` 匹配 `the` 和 `The`.

 ![image-20200504160603979](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504160603979.png)

方括号的句号就表示句号. 表达式 `ar[.]` 匹配 `ar.`字符串

 ![image-20200504160641950](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504160641950.png)

简单检索演示

````mysql
mysql> select name ,url from  websites
    -> where url regexp '[.]co';
+----------+------------------+
| name     | url              |
+----------+------------------+
| Google   | www.google.com   |
| taobao   | www.taobao.com   |
| weibo    | www.weibo.com    |
| facebook | www.facebook.com |
| JD       | www.JD.com       |
+----------+------------------+
5 rows in set (0.00 sec)

mysql>
````





##### **否定字符集[ ^ ]**

一般来说 `^` 表示一个字符串的开头, 但它用在一个方括号的开头的时候, 它表示这个字符集是否定的. 例如, 表达式`[^c]ar` 匹配一个后面跟着`ar`的除了`c`的任意字符.

 ![image-20200504202133675](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504202133675.png)

简单检索演示

```` mysql
mysql> select * from apps ;
+----+--------+----------------+---------+
| id | name   | url            | country |
+----+--------+----------------+---------+
|  1 | QQ     | im.qq.com      | CN      |
|  2 | weibo  | www.weibo.com  | CN      |
|  3 | weixin | www.weixin.com | CN      |
+----+--------+----------------+---------+
3 rows in set (0.01 sec)

mysql> select * from apps
    -> where name regexp 'wei[^xin]';
+----+--------+---------------+---------+
| id | name   | url           | country |
+----+--------+---------------+---------+
|  2 | weibo  | www.weibo.com | CN      |
+----+--------+---------------+---------+
1 row in set (0.00 sec)

mysql>
````





##### 重复次数

**`*` 号 **

`*`号匹配 在`*`之前的字符出现`大于等于0`次. 例如, 表达式 `a*` 匹配以0或更多个a开头的字符, 因为有0个这个条件, 其实也就匹配了所有的字符. 表达式`[a-z]*` 匹配一个行中所有以小写字母开头的字符串.

 ![image-20200504203357614](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504203357614.png)

`*`字符和`.`字符搭配可以匹配所有的字符`.*`. `*`和表示匹配空格的符号`\s`连起来用, 如表达式`\s*cat\s*`匹配0或更多个空格开头和0或更多个空格结尾的cat字符串.

 ![image-20200504203911726](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504203911726.png)

**`+` 号**

`+`号匹配`+`号之前的字符出现 >=1 次个字符. 例如表达式`c.+t` 匹配以首字母`c`开头以`t`结尾,中间跟着任意个字符的字符串.

 ![image-20200504204014305](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504204014305.png)

**`?` 号**

在正则表达式中元字符 `?` 标记在符号前面的字符为可选, 即出现 0 或 1 次. 例如, 表达式 `[T]?he` 匹配字符串 `he` 和 `The`

 ![image-20200504204056836](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504204056836.png)

 ![image-20200504204147595](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504204147595.png)





##### **`{}`号**

在正则表达式中 `{}` 是一个量词, 常用来一个或一组字符可以重复出现的次数. 例如, 表达式 `[0-9]{2,3}` 匹配 2～3 位 0～9 的数字.

 ![image-20200504204247694](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504204247694.png)

我们可以省略第二个参数. 例如, `[0-9]{2,}` 匹配至少两位 0~9 的数字.

如果逗号也省略掉则表示重复固定的次数. 例如, `[0-9]{3}` 匹配3位数字

 ![image-20200504204329859](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504204329859.png)

 ![image-20200504204339945](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504204339945.png)





##### **`(...)`特征标群**

特征标群是一组写在 `(...)` 中的子模式. 例如之前说的 `{}` 是用来表示前面一个字符出现指定次数. 但如果在 `{}` 前加入特征标群则表示整个标群内的字符重复 N 次. 例如, 表达式 `(ab)*` 匹配连续出现 0 或更多个 `ab`.*

*我们还可以在 `()` 中用或字符 `|` 表示或. 例如, `(c|g|p)ar` 匹配 `car` 或 `gar` 或 `par`.

 ![image-20200504204646157](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504204646157.png)





##### **`|` 或运算**

或运算符就表示或, 用作判断条件.

例如 `(T|t)he|car` 匹配 `(T|t)he` 或 `car`.

 ![image-20200504205650455](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504205650455.png)





##### **转码特殊字符**

反斜线 `\` 在表达式中用于转码紧跟其后的字符. 用于指定 `{ } [ ] / \ + * . $ ^ | ?` 这些特殊字符. 如果想要匹配这些特殊字符则要在其前面加上反斜线 `\`<

例如 `.` 是用来匹配除换行符外的所有字符的. 如果想要匹配句子中的 `.` 则要写成 `\.` 以下这个例子 `\.?`是选择性匹配`.`

 ![image-20200504205903859](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504205903859.png)





##### **锚点`^` `$`**

在正则表达式中，想要匹配开头的或者结尾的字符串就要使用到锚点 `^` 指定开头`$`指定结尾

**`^`**

`^` 用来检查匹配的字符串是否在所匹配字符串的开头.

例如, 在 `abc` 中使用表达式 `^a` 会得到结果 `a`. 但如果使用 `^b` 将匹配不到任何结果. 因为在字符串 `abc` 中并不是以 `b` 开头.

例如, `^(T|t)he` 匹配以 `The` 或 `the` 开头的字符串.

 ![image-20200504210511980](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504210511980.png)

 ![image-20200504210527180](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504210527180.png)

**`$` 号**

同理于 `^` 号, `$` 号用来匹配字符是否是最后一个.

例如, `(at\.)$` 匹配以 `at.` 结尾的字符串.

 ![image-20200504211527714](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504211527714.png)

 ![image-20200504211540483](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504211540483.png)





##### **简写字符集**

| 简写 | 描述                                                |
| ---- | --------------------------------------------------- |
| .    | 除去换行符外的所有字符                              |
| \w   | 匹配所有字母数字，等同于：`[a-zA-Z0-9_]`            |
| \W   | 匹配所有非字母数字，即符号，等同于 ：`[ ^ \w]`      |
| \d   | 匹配数字：`[0-9]`                                   |
| \D   | 匹配非数字：`[ ^ \d]`                               |
| \s   | 匹配所有空格字符, 等同于: ` [ \t \n \f \r \p {Z} ]` |
| \S   | 匹配所有非空格字符: `[^\s]`                         |
| \f   | 匹配一个换页符                                      |
| \n   | 匹配一个换行符                                      |
| \r   | 匹配一个回车符                                      |
| \t   | 匹配一个制表符                                      |
| \v   | 匹配一个垂直制表符                                  |
| \p   | 匹配 CR/LF (等同于 `\r\n`)，用来匹配 DOS 行终止符   |





##### 前后关联约束

**?=...` 前置约束(存在)**

`?=...` 前置约束(存在), 表示第一部分表达式必须跟在 `?=...`定义的表达式之后.

返回结果只满足第一部分表达式. 定义一个前置约束(存在)要使用 `()`. 在括号内部使用一个问号和等号: `(?=...)`.

前置约束的内容写在括号中的等号后面. 例如, 表达式 `(T|t)he(?=\sfat)` 匹配 `The` 和 `the`, 在括号中我们又定义了前置约束(存在) `(?=\sfat)` ,即 `The` 和 `the` 后面

 ![image-20200504215141378](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215141378.png)

**`?<= ...` 后置约束-存在**

后置约束-存在 记作`(?<=...)` 用于筛选所有匹配结果, 筛选条件为 其前跟随着定义的格式. 例如, 表达式 `(?<=(T|t)he\s)(fat|mat)` 匹配 `fat` 和 `mat`, 且其前跟着 `The` 或 `the`.

 ![image-20200504215301345](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215301345.png)

**`?` 后置约束-排除**

后置约束-排除 记作 `(? 用于筛选所有匹配结果, 筛选条件为 其前不跟着定义的格式. 例如, 表达式 `(? 匹配 `cat`, 且其前不跟着 `The` 或 `the`.





##### 标志

| 标志 | 描述                                             |
| ---- | ------------------------------------------------ |
| i    | 忽略大小写                                       |
| g    | 全局搜索                                         |
| m    | 多行的: 锚点元字符 `^` `$` 工作范围在每行的起始. |

**忽略大小写 (Case Insensitive)**

修饰语 `i` 用于忽略大小写. 例如, 表达式 `/The/gi` 表示在全局搜索 `The`, 在后面的 `i` 将其条件修改为忽略大小写, 则变成搜索 `the` 和 `The`, `g` 表示全局搜索.

 ![image-20200504215640289](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215640289.png)

 ![image-20200504215650541](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215650541.png)

**全局搜索 (Global search)**

修饰符 `g` 常用语执行一个全局搜索匹配, 即(不仅仅返回第一个匹配的, 而是返回全部). 例如, 表达式 `/.(at)/g` 表示搜索 任意字符(除了换行) + `at`, 并返回全部结果.

 ![image-20200504215729995](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215729995.png)

 ![image-20200504215740333](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215740333.png)

**多行修饰符 (Multiline)**

多行修饰符 `m` 常用语执行一个多行匹配.

像之前介绍的 `(^,$)` 用于检查格式是否是在待检测字符串的开头或结尾. 但我们如果想要它在每行的开头和结尾生效, 我们需要用到多行修饰符 `m`.

例如, 表达式 `/at(.)?$/gm` 表示在待检测字符串每行的末尾搜索 `at`后跟一个或多个 `.` 的字符串, 并返回全部结果.

 ![image-20200504215822817](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215822817.png)

 ![image-20200504215834224](/Users/haohongxin/Library/Application Support/typora-user-images/image-20200504215834224.png)



---





### 创建计算字段



##### 拼接字段

> 字段（field） 基本上与列（column）的意思相同，经常互换使 用，不过数据库列一般称为列，而术语字段通常用在计算字段的 连接上。

> 拼接（concatenate） 将值联结到一起构成单个值。
>
> 解决办法是把两个列拼接起来。在MySQL的SELECT语句中，可使用 Concat()函数来拼接两个列。

**Concat**

> Concat() 拼接串， 即把多个串连接起来形成一个较长的串。

```mysql
mysql> select concat(name ,'(',country,')')
    -> from websites
    -> order by name ;
+-------------------------------+
| concat(name ,'(',country,')') |
+-------------------------------+
| facebook(USA)                 |
| Google(USA)                   |
| JD(CN)                        |
| taobao(CN)                    |
| weibo(CN)                     |
+-------------------------------+
5 rows in set (0.00 sec)

mysql>
```

**RTrim（ ） & LTRim（ ）**

> RTrim()函数去掉值右边的所有空格。通过使用RTrim()，各个 列都进行了整理。相反LTrim去掉左边的空格   以及Trim（）去掉左右两边的空格

```mysql
select  concat(rtrim(name) ,'(',rtrim(country),')')
from websites 
order by name ;

mysql> select  concat(rtrim(name) ,'(',rtrim(country),')')
    -> from websites
    -> order by name ;
+---------------------------------------------+
| concat(rtrim(name) ,'(',rtrim(country),')') |
+---------------------------------------------+
| facebook(USA)                               |
| Google(USA)                                 |
| JD(CN)                                      |
| taobao(CN)                                  |
| weibo(CN)                                   |
+---------------------------------------------+
5 rows in set (0.01 sec)

mysql>
```

**使用别名**

> 从上面的concat拼接可以看出但是新的计算返回的列名 实际上没有名字他只是一个值为了解决这个问题 sql支持列别名 别名（alias）是一个字段或值的替换名。别名用AS关键字赋予

```mysql
mysql> select concat(name ,'(',country,')')  as  app_name
    -> from websites
    -> order by name;
+---------------+
| app_name      |
+---------------+
| facebook(USA) |
| Google(USA)   |
| JD(CN)        |
| taobao(CN)    |
| weibo(CN)     |
+---------------+
5 rows in set (0.00 sec)

mysql>
```

> 分析上面的语言可以看出之前的拼接语句被别名app_name 代替





##### 执行算术计算

> 计算字段的另一常见用途是对检索出的数据进行算术计算。

**算术操作符**

| 操作符 | 描述 |
| ------ | ---- |
| +      | 加   |
| -      | 减   |
| *      | 乘   |
| /      | 除   |



```mysql
mysql> create table jisuan(
    -> number_1 int(8) not null,
    -> number_2 int(9) not null,
    -> primary key(number_1)
    -> ) charset = utf8;
Query OK, 0 rows affected, 3 warnings (0.01 sec)

mysql> desc jisuan;
+----------+------+------+-----+---------+-------+
| Field    | Type | Null | Key | Default | Extra |
+----------+------+------+-----+---------+-------+
| number_1 | int  | NO   | PRI | NULL    |       |
| number_2 | int  | NO   |     | NULL    |       |
+----------+------+------+-----+---------+-------+
2 rows in set (0.01 sec)

mysql> insert into jisuan values
    -> (8,4),
    -> (3,5),
    -> (5,2),
    -> (3,7);
    
ERROR 1062 (23000): Duplicate entry '3' for key 'jisuan.PRIMARY'//这里说是主键数值重复了 那我们删除主键在测试

mysql> alter table jisuan drop primary key; //删除主键
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> insert into jisuan values  (8,4), (3,5), (5,2), (3,7);
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0//成功插入

mysql> select number_1 * number_2 from jisuan // 使用 * 号计算
    -> where number_1 = 3
    -> order by number_1 ;
+---------------------+
| number_1 * number_2 |
+---------------------+
|                  15 |
|                  21 |
+---------------------+
2 rows in set (0.01 sec)

mysql> select number_1 + number_2 from jisuan  //使用 + 号进行加计算
    -> order by number_1;
+---------------------+
| number_1 + number_2 |
+---------------------+
|                   8 |
|                  10 |
|                   7 |
|                  12 |
+---------------------+
4 rows in set (0.01 sec)

mysql>

```



---



### 使用数据处理函数







##### **文本处理函数**

| 函数          | 描述                                          |
| ------------- | --------------------------------------------- |
| left ( )      | 返回串左边的字符                              |
| right ( )     | 返回串右边的字符                              |
| lrtrim（）    | 去掉串左边的空格                              |
| rtrim（）     | 去掉串右边的空格                              |
| lower（）     | 将串转换为小写                                |
| upper（）     | 将串转换为大写                                |
| length（）    | 返回串的长度                                  |
| locate（）    | 找出串的一个字串                              |
| soundex （）  | 返回串的soundex值（匹配所有发音类似的数据名） |
| substring（） | 返回子串的字符                                |

> 的SOUNDEX需要做进一步的解释。SOUNDEX是一个将任何文 本串转换为描述其语音表示的字母数字模式的算法。SOUNDEX考虑了类似 的发音字符和音节， 使得能对串进行发音比较而不是字母比较。

```mysql
mysql> select upper(name) as app_name  //使用 upper 函数使字符转换为大写
    -> from websites ;
+----------+
| app_name |
+----------+
| GOOGLE   |
| TAOBAO   |
| WEIBO    |
| FACEBOOK |
| JD       |
+----------+
5 rows in set (0.01 sec)

mysql>
```





##### 日期和时间处理函数

> 表中例举了常用的日期和时间处理函数

| 函数          | 描述                           |
| ------------- | ------------------------------ |
| AddDate()     | 增加一个日期（天、周等）       |
| AddTime()     | 增加一个时间（时、分等）       |
| CurDate()     | 返回当前日期                   |
| Curtime()     | 返回当前时间                   |
| Date()        | 返回日期时间的日期部分         |
| DateDiff()    | 计算两个日期之差               |
| Date_Add()    | 高度灵活的日期运算函数         |
| Date_Format() | 返回一个格式化的日期或时间串   |
| Day()         | 返回一个日期的天数部分         |
| DayOfWeek()   | 对于一个日期，返回对应的星期几 |
| Hour()        | 返回一个时间的小时部分         |
| Minute()      | 返回一个时间的分钟部分         |
| Month()       | 返回一个日期的月份部分         |
| Now()         | 返回当前日期和时间             |
| Second()      | 返回一个时间的秒部分           |
| Time()        | 返回一个日期时间的时间部分     |
| Year()        | 返回一个日期的年份部分         |

> 使用employees表进行演示  employees 表可能有点复杂  后面我们会把本书的建表语句以及数据库导出打包

```mysql
mysql> select * from employees;
+--------+-----------+-----+--------------+-----------+--------------+------------+-------+------------+------+-----+
| E_ID   | E_name    | sex | Professional | education | Political    | birth      | marry | Gz_time    | D_id | bz  |
+--------+-----------+-----+--------------+-----------+--------------+------------+-------+------------+------+-----+
| 100100 | 李明      | 男  | 副教授       | 硕士      | 党员         | 1967-02-01 | 否    | 1989-09-01 | B001 | 是  |
| 100101 | 李小光    | 男  | 讲师         | 本科      | 党员         | 1985-03-01 | 否    | 1990-10-02 | B001 | 是  |
| 100102 | 张伟键    | 男  | 教授         | 本科      | 党员         | 1965-05-06 | 是    | 1987-07-08 | B003 | 是  |
| 100103 | 石小华    | 女  | 教授         | 硕士      | 党员         | 1978-06-07 | 是    | 1992-01-01 | A001 | 是  |
| 100104 | 黄莉      | 女  | 助讲         | 硕士      | 群众         | 1986-03-04 | 否    | 2001-05-06 | A002 | 是  |
| 100105 | 余明平    | 男  | 教授         | 硕士      | 党员         | 1960-05-12 | 是    | 1983-04-05 | B001 | 是  |
| 100106 | 苏小明    | 男  | 教授         | 硕士      | 群众         | 1956-04-13 | 是    | 1983-04-03 | B003 | 是  |
| 100107 | 汤光明    | 男  | 教授         | 硕士      | 群众         | 1983-01-04 | 是    | 2007-12-06 | A004 | 是  |
| 100108 | 谢建设    | 男  | 副教授       | 博士      | 民进         | 1987-02-08 | 否    | 2006-08-15 | A005 | 是  |
| 100109 | 胡晓群    | 女  | 讲师         | 博士      | 党员         | 1990-09-28 | 否    | 2012-05-23 | B005 | 是  |
| 100330 | 李正中    | 男  | 副教授       | 硕士      | 群众         | 1978-10-29 | 否    | 1995-10-01 | B002 | 是  |
| 100331 | 王君君    | 女  | 教授         | 博士      | 党员         | 1956-11-18 | 否    | 1978-12-07 | B003 | 是  |
| 100332 | 赵剑      | 男  | 讲师         | 博士      | 党员         | 1967-12-25 | 否    | 1989-04-08 | B005 | 是  |
| 100333 | 欧阳      | 女  | 副教授       | 博士      | 民进         | 1966-03-08 | 否    | 1988-02-09 | B003 | 是  |
| 200100 | 李明义    | 男  | 讲师         | 硕士      | 党员         | 1965-04-17 | 否    | 1987-08-10 | B005 | 是  |
| 200101 | 孙美灵    | 男  | 讲师         | 硕士      | 党员         | 1977-05-16 | 否    | 1998-09-11 | B003 | 是  |
| 200102 | 王世明    | 男  | 副教授       | 硕士      | 党员         | 1976-03-21 | 否    | 1996-07-21 | A004 | 是  |
| 200103 | 张平娜    | 女  | 讲师         | 硕士      | 党员         | 1989-04-23 | 否    | 2008-06-22 | A001 | 是  |
| 200104 | 李美丽    | 女  | 讲师         | 博士      | 九三学社     | 1982-12-01 | 是    | 1992-05-01 | B001 | 是  |
| 200105 | 苏珍珍    | 女  | 副教授       | 本科      | 党员         | 1966-08-11 | 是    | 1985-08-01 | B003 | 是  |
| 200220 | 张白燕    | 女  | 讲师         | 博士      | 群众         | 1987-05-01 | 是    | 2011-09-02 | A001 | 是  |
| 200221 | 李青青    | 女  | 副教授       | 本科      | 群众         | 1964-10-06 | 是    | 1989-04-03 | A001 | 是  |
+--------+-----------+-----+--------------+-----------+--------------+------------+-------+------------+------+-----+
22 rows in set (0.01 sec)

mysql> select E_name, E_ID,sex from employees
    -> where date(Gz_time) between '1990-10-02' and '2000-10-02' ;
+-----------+--------+-----+
| E_name    | E_ID   | sex |
+-----------+--------+-----+
| 李小光    | 100101 | 男  |
| 石小华    | 100103 | 女  |
| 李正中    | 100330 | 男  |
| 孙美灵    | 200101 | 男  |
| 王世明    | 200102 | 男  |
| 李美丽    | 200104 | 女  |
+-----------+--------+-----+
6 rows in set (0.00 sec)

mysql>
```



##### 数值处理函数

| 函数     | 描述                 |
| -------- | -------------------- |
| Abs（ ） | 返回一个数的绝对值   |
| exp（）  | 返回一个数的值数值   |
| mod（）  | 返回除操作的余数     |
| rand（） | 返回一个随机数       |
| sin（）  | 返回一个角度的正弦   |
| cos（）  | 返回一个角度的余弦   |
| tan（）  | 返回一个角度的正切   |
| sqrt（） | 返回一个角度的平方根 |
| pi（）   | 返回圆周率           |



---



### 汇总数据（聚集函数）



##### 聚集函数

> 聚集函数（aggregate function） 运行在行组上，计算和返回单个值的函数。

sql中使用的聚集函数

| 函数      | 描述             |
| --------- | ---------------- |
| avg（）   | 返回某列的平均值 |
| max（）   | 返回某列的最大值 |
| min（）   | 返回某列的最小值 |
| sum（）   | 返回某列的和     |
| count（） | 返回 某列的行数  |



##### AVG（）函数

> 求取某列的平均值

```mysql
mysql> select avg(number_1) as avg_number_1
    -> from jisuan ;
+--------------+
| avg_number_1 |
+--------------+
|       4.7500 |
+--------------+
1 row in set (0.01 sec)

mysql>
```



##### MAX（）函数 

> 返回某列的最大值

```mysql
mysql> select max(number_1) as max_number_1
    -> from jisuan ;
+--------------+
| max_number_1 |
+--------------+
|            8 |
+--------------+
1 row in set (0.00 sec)

mysql>
```



##### count（）函数

> COUNT()函数进行计数。可利用COUNT()确定表中行的数目或符合特 定条件的行的数目。
>
> 使用COUNT(*)对表中行的数目进行计数，不管表列中包含的是空 值（NULL）还是非空值。  使用 COUNT(column) 对特定列中具有值的行进行计数， 忽略NULL值。

```mysql
mysql> select count(number_1) as
    -> count_number_1
    -> from jisuan ;
+----------------+
| count_number_1 |
+----------------+
|              4 |
+----------------+
1 row in set (0.01 sec)

mysql>
```





##### 聚集不同的值

> 之前在select部分使用distinct语句去除重复值检索
>
> 以上五个函数都称为聚集函数 以上5个聚集函数都可以如下使用：
>
> 对所有的行执行计算，指定ALL参数或不给参数（因为ALL是默认 行为）；  只包含不同的值，指定DISTINCT参数。

```mysql
mysql> select * from jisuan;
+----------+----------+
| number_1 | number_2 |
+----------+----------+
|        8 |        4 |
|        3 |        5 |
|        5 |        2 |
|        3 |        7 |
+----------+----------+
4 rows in set (0.00 sec)

mysql> select avg(distinct number_1)
    -> as avg_number
    -> from jisuan;
+------------+
| avg_number |
+------------+
|     5.3333 |
+------------+
1 row in set (0.01 sec)

mysql>
```

> 这样就可以排除重复值排除一些重复的值以来提高平均值的品质





##### 组合聚集函数

> 目前为止的所有聚集函数例子都只涉及单个函数。但实际上SELECT 语句可根据需要包含多个聚集函数

````mysql
mysql> select avg(number_1),
    -> max(number_1),
    -> min(number_1),
    -> count(*) from jisuan ;
+---------------+---------------+---------------+----------+
| avg(number_1) | max(number_1) | min(number_1) | count(*) |
+---------------+---------------+---------------+----------+
|        4.7500 |             8 |             3 |        4 |
+---------------+---------------+---------------+----------+
1 row in set (0.01 sec)

mysql>
````





---





### 数据分组



##### 创建分组

> 分组是在SELECT语句的GROUP BY子句中建立的

GROUP BY 语法

````mysql
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
````

数据库employee_tbl 

````msyql
mysql> select * from employee_tbl ;
+----+--------+---------------------+--------+
| id | name   | date                | singin |
+----+--------+---------------------+--------+
|  1 | 小明   | 2016-04-22 15:25:33 |      1 |
|  2 | 小王   | 2016-04-20 15:25:47 |      3 |
|  3 | 小丽   | 2016-04-19 15:26:02 |      2 |
|  4 | 小王   | 2016-04-07 15:26:14 |      4 |
|  5 | 小明   | 2016-04-11 15:26:40 |      4 |
|  6 | 小明   | 2016-04-04 15:26:54 |      2 |
+----+--------+---------------------+--------+
6 rows in set (0.01 sec)

````

检索出他们的登陆次数

````mysql
mysql> select name, count(*)使用 count 函数计数
    -> from employee_tbl  
    -> group by name ;  依据 name 列分组
+--------+----------+
| name   | count(*) |
+--------+----------+
| 小明   |        3 |
| 小王   |        2 |
| 小丽   |        1 |
+--------+----------+
3 rows in set (0.00 sec)

mysql>
````

在具体使用GROUP BY子句前，需要知道一些重要的规定。

​	 GROUP BY子句可以包含任意数目的列。这使得能对分组进行嵌套， 为数据分组提供更		细	致的控制。

 	 如果在GROUP BY子句中嵌套了分组，数据将在最后规定的分组上进行汇总。换句话		说，	在建立分组时，指定的所有列都一起计算 （所以不能从个别的列取回数据）。
 	
 	 GROUP BY 子句中列出的每个列都必须是检索列或有效的表达式 （但不能是聚数）。		如果在 SELECT 中使用表达式， 则必须在GROUP BY子句中指定相同的表达式。不能		使用	别名。

​	  除聚集计算语句外，SELECT语句中的每个列都必须在GROUP BY子句中给出。

​	  如果分组列中具有NULL值，则NULL将作为一个分组返回。如果列中有多行NULL值，		它	们将分为一组。 

​	  GROUP BY子句必须出现在WHERE子句之后，ORDER BY子句之前。





##### 过滤分组

> 我们将使用 having 过滤分组  之前说的 where 只能过滤行 

````mysql
mysql> select name ,count(*)
    -> from employee_tbl
    -> group by name
    -> having count(*) >= 2 ;//使用 having 过滤分组
+--------+----------+
| name   | count(*) |
+--------+----------+
| 小明   |        3 |
| 小王   |        2 |
+--------+----------+
2 rows in set (0.00 sec)

mysql>
````

分组和排序之间的关系

| order by                                     | group by                                                |
| -------------------------------------------- | ------------------------------------------------------- |
| 排序产生的输出                               | 分组行 但输出可能不是分组的排序                         |
| 任意列都可以使用（甚至非选择的列也可以使用） | 只可能使用选择列或表达式列 而且必须使用每个选择列表达式 |
| 不一定需要                                   | 如果与聚集函数一起使用列（或表达式）则必须使用          |



##### select 语句顺序

| 子句     | 说明                 | 是否必须使用                 |
| -------- | -------------------- | ---------------------------- |
| select   | 要返回的列或者表达式 | 是                           |
| from     | 从中检索数据的表     | 尽在从表中选择数据的时候使用 |
| where    | 行级过滤             | 否                           |
| group by | 分组说明             | 仅在按组计算聚集是使用       |
| having   | 组级过滤             | 否                           |
| order by | 输出排序顺序         | 否                           |
| limit    | 要检索的行数         | 否                           |



### 使用子查询



##### 使用子查询进行过滤

> SQL还允许创建子查询（subquery），即嵌套在其他查询中的查询。 为什么要这样做呢？理解这个概念的最好方法是考察几个例子

````mysql
mysql> select * from departments  where id = (select D_id from employees where E_name = '李明' );   //简单的字查询演示  这样就省去了连续查询两个表的繁琐过程
+------+--------------+
| id   | name         |
+------+--------------+
| B001 | 信息学院     |
+------+--------------+
1 row in set (0.00 sec)

mysql>
````





---





### 联结表



##### 关系表

> 关系表的设计就是要保证把信息分解成多个表，一类数据 一个表。各表通过某些常用的值（即关系设计中的（relational））互相关联

外键（foreign key） 外键为某个表中的一列，它包含另一个表的主键值，定义了两个表之间的关系。

使用联结表的原因 

> 如果数据存储在多个表中，怎样用单条SELECT语句检索出数据？
>
> 答案是使用联结。简单地说，联结是一种机制，用来在一条SELECT 语句中关联表，因此称之为联结。使用特殊的语法，可以联结多个表返 回一组输出，联结在运行时关联表中正确的行。







