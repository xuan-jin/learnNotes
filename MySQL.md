# MySQL

## 数据库基本操作

```mysql
cd C:\Program Files\MySQL\MySQL Server 5.7
mysqld --initialize-insecure --user=root
		首先定位到Mysql Server 5.7，再创建data文件夹
		
net stop mysql57		停止mysql服务
net start mysql57		启动mysql服务

mysql -u root -p		以root身份登录
show databases;			显示所有数据库

create database student;	
		创建student库
create database if not exists student;
		创建student数据库-如果student库不存在的话
create database `datebase`;
		加上反引号，可强制创建以关键字为名称的库

drop database student;		
		删除student库
drop database if exists student;
		删除student数据库-如果student库存在的话
drop database if exists `database`;
		删除`database`

show create database student;	
		显示该数据库student是如何创建出来的

create database if not exists `student` charset=gbk;
		在创建时设置该库（student）的字符编码格式gbk/（utf8）

alter database teacher charset=gbk;
		修改数据库teacher字符编码-> alter

```



## 表的操作

```mysql
use xuanjin_school;			
		使用该数据库/指定到该数据库xuanjin_school
show tables;
		显示出该数据库中有多少表，
		
create table student();
		在xuanjin_school这个数据库中创建一个名为student的表
create table student(
    id int,					该表中的几个参数
    name varchar(30),		在数据库中字符类型一般用varchar
    age int					各参数之间用逗号隔开，最后加分号
	);

// 更高级的
create table teacher(
	id int auto_increment primary key comment '主键id',
    name varchar(30) not null comment '老师的名字',
    phone varchar(20) unique comment '电话号码'，
    address varchar(100) default '暂时未知' comment '住址'
	)engine=innodb;
	
		    auto_increment		自动增长，（必须为主键 primary key)
		    primary key			主键，最主要的，靠它来区分这张表,主键不一定自增长
		    unique				唯一键，该字段不能有重复数据
		    comment				注释
    		not null			不能为空
			default				如果未填，则默认为其填充''
			engine=innodb;		MySQL存储引擎

一个表中只能有一个主键，但是可以有多个唯一键

show create table teacher;
		展示该表teacher是如何创的
desc teacher;
		查看表的结构
		
drop table if exists student;
drop table if exists student, teacher;
		删除表-如果该表存在的话,可以一次删除多个

alter table student add phone varchar(20);
		给student表添加一个类型为varchar的phone字段
alter table student add gender varchar(10) after name;
		在name后面给student表添加一个类型为varchar的gender字段		
alter table student add primary key (id);
		将字段id设置为主键，所设置的字段中的数据应没有空数据		
alter table student add unique (phone);
		将字段phone设置为 unique 唯一键
		
alter table student drop address;
		删除student表中的address字段
alter table student drop primary key;
		删除主键，但不删除字段
alter table student index phone;
		删除唯一键phone

alter table student change phone telephone int(11);
		更改student表中phone字段的名称和类型，改为telephone int(11)
alter table student modify telephone varchar(13);
		更改student表中telephon字段的类型，改为varchar(13)
alter table students rename to student;
		更改表名students为student，注意，表名不能用复数
		
		
```



## 数据的操作

```mysql
insert into teacher (id, name, phone, address) values(1, 'Frank', '100000000', 'ShangHai');
		向表teacher中写入一组数据，
		前后两括号内的数据顺序可以打乱，但是须严格一一对应
		
insert into teacher values(3, 'Tom', '12345566', 'BeiJing');
		如果不写第一个括号里的内容，则数据顺序写入须严格按照表的固有顺序
		
insert into teacher values(NULL, 'Jerry', NULL, default);
		id是auto_increment类型，可以自增，可用NULL代替
		phone和address未定义not null，则也可以用NULL代替
		default 为其填写默认填充内容
		
insert into teacher values(NULL, 'Tom_1', NULL, default),(NULL, 'Tom_2', NULL, default);
		一次插入多条语句，则直接在第一组数据后加逗号和第二组数据即可

insert into teacher values(NULL, '张三', '1111111', '上海');
		也可以使用中文，window使用gbk编码格式，但是工作中需要使用utf8
show variables like 'character_set_%';
		显示各处编码格式
set character_set_client=gbk;
		更改character_set_client的编码格式为gbk

delete from teacher where id=7;
		删除teacher中id=7的数据
delete from teacher where name="Tom";
		若有多个名字相同，都叫Tom，则会将所有Tom全部删掉
		注意：tom和Tom无区别，都会被删除！！！
delete from student where age>30;
		删除student表中age大于30的所有数据
delete from teacher;
		删除teacher中的所有数据（不建议这样写），
		类似for循环一条一条删除，效率低
		并且之后再插入数据其id会按照之前的最大id继续增加

truncate table student;
		直接销毁student表，然后再创建一个和原表相同的框架
		再插入新的数据时，id会从1开始
		
update teacher set name='Frank' where id=1;
		更改数据，将表teacher中id=1的name改为Frank
		id=1，也可为其他字段的指定，但是要特别注意其他字段可能会有重复则更改时会将所有指定字段的都更改
		更改多个值时用逗号隔开就好了

update teacher set address='HangZhou' where phone='1234' or phone='123456';
		可以设置多个控制条件，进行更改
		此句中，会将teacher表中的phone=1234和phone=123456的两组数据的地址均改为 'HangZhou'

select * from teacher;
		查询teacher表中的所有内容（但不建议使用这种方式）
select id,name from teacher;
		查询teacher表中的指定字段，id，name


```





## SQL语言的区分

### DDL 

date definition language  数据库定义语言（对数据库）

create, alter, drop, show 



### DML 

date manipulation language 数据库操纵语言（对数据）

insert, update, delete, select



### DCL 

date control language 数据库控制语言



## MySQL数据类型

| 类型         | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途            |
| :----------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------- |
| TINYINT      | 1 byte                                   | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |



根据实际需求，选用合适的类型。注意**无符号型**的使用。

### 整型

tinyint 	samallint	mediumint	int/integer	bigint

```mysql
create table example(
	id smallint unsigned auto_increment primary key,
	age tinyint unsigned,
	number int(6)
	);
	
	
mysql> desc example;
+--------+----------------------+------+-----+---------+---
| Field  | Type                 | Null | Key | Default |
+--------+----------------------+------+-----+---------+---
| id     | smallint(5) unsigned | NO   | PRI | NULL    |
| age    | tinyint(3) unsigned  | YES  |     | NULL    |     
| number | int(6)               | YES  |     | NULL    |
+--------+----------------------+------+-----+---------+---	

上表中5，3，为该类型的能存储的最大宽度
但是对于int来说，虽然定义6个宽度，但是其最大宽度依然是11，就是说即使超出六个宽度依旧能存储
（（（个人理解：是不是定义int(6),就代表这个int(6)类型,在内存中之占6个宽度，如果是int则占11个宽度）））


```

### 浮点型

float	double	

```mysql
create table t_1(
	number_1 float(3, 1),
	number_2 double(5, 2)
	)
	
	括号里第一个数表示输入数字的总位数，第二个数字表示小数部分的位数
	整数部分必须不能大于设置位数
	小数部分如果大于设置位数，则四舍五入，但是会造成精度丢失
```



### 定点数

decimal

整数和小数部分分开存储，准确

```mysql
create table t_2(
	number decimal(6, 4)
	)
	
如果小数位数超出设置，则依旧四舍五入，但是不会像浮点类型一样丢失精度

```



### 字符串与文本类型

| 类型       | 大小                  | 用途                            |
| :--------- | :-------------------- | :------------------------------ |
| CHAR       | 0-255 bytes           | 定长字符串                      |
| VARCHAR    | 0-65535 bytes         | 变长字符串                      |
| TINYBLOB   | 0-255 bytes           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                    |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535 bytes        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                    |

字符串类型指CHAR、VARCHAR、BINARY、VARBINARY、BLOB、TEXT、ENUM和SET

### 枚举类型

```mysql
create table t_3(
	gender enum('man', 'woman', '?', 'nothing', 'it')
 	);
 	
 	创建t_3表的字段gender为枚举类型
 	则该字段中的数据只能为括号中列举的
 	
insert into t_3 values('man'), ('woman');	
insert into t_3 values(1),(2),(3);
 
 	存储数据时，可以输入规定的字段，如上例'man','woman';也可以输入不超过枚举类型列举总数的数据，如上例
 	枚举类型在存储时，是存储其列举出的类型的编号，而非具体的'man'等
 	节省空间，提高效率
```



### set类型

```mysql
create table t_5(
	class set('c语言','java','离散数学','高等数学','大学物理','mysql')
	);
	
insert into t_5 values('c语言,java,mysql,大学物理');
	
	set数组类型，可以同时取多个
	 注意多个数据存储时是一个字段，即放在一个引号内
	 逗号前后均无空格
```



### 日期和时间类型

| 类型      | 大小 ( bytes) |                             范围                             | 格式                | 用途                     |
| :-------- | :------------ | :----------------------------------------------------------: | :------------------ | :----------------------- |
| DATE      | 3             |                    1000-01-01/9999-12-31                     | YYYY-MM-DD          | 日期值                   |
| TIME      | 3             |                   '-838:59:59'/'838:59:59'                   | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1             |                          1901/2155                           | YYYY                | 年份值                   |
| DATETIME  | 8             |           1000-01-01 00:00:00/9999-12-31 23:59:59            | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4             | 1970-01-01 00:00:00/2038结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYYMMDD HHMMSS     | 混合日期和时间值，时间戳 |

一般使用datetime

```mysql
create table t_6(      
	createTime datetime  
	);
	
insert into t_6 values('2020-07-13 19:01:00');

```



## 列属性完整性

### 数据库完整性

#### 实体完整性

// 同一数据表中不可有多项记录拥有相同识别

表中的字段应当是完整的，比如应当至少要有一个主键

#### 域完整性

// 限制字段中的数据必须乎合预设的数据类型，例如：日期

选择合适的数据类型，比如是否null，是否default

#### 参照完整性

// 如两个数据表是有关联的，父数据表中的记录必须存在，子数据表的记录才有存在

可能需要用到对外部的引用，比如一个表中的主键id拿到另一个表中使用

#### 用户定义完整性





### 外键

通过一个字段将两张表关联起来

但是在实际开发中一般不使用外键，甚至禁止使用外键

#### 严格操作（基本操作）

查看外键的方式

```mysql
show create table + 表名;
```

创建一个主表

```mysql
desc table stu(
    -> stuId int primary key,
    -> money decimal (10,4) 
    -> );
```

在创建从表时创建外键

```mysql
create table eatery(
    -> id int primary key,
    -> money decimal(10,4),
    -> student_id int,
    -> foreign key (student_id) references stu(student_id) 
    -> );
```

在创建从表后，添加外键

```mysql
create table library(
    -> id int primary key,
    -> name varchar(30),
    -> student_id int 
    -> );
    
alter table library add foreign key (student_id) references stu (student_id);
```

删除外键，首先要查看外键，再删除名为   '表名_ibkf_X'  的外键

```mysql
show create table + 表名

alter table eatery drop foreign key eatery_ibfk_1; 
```

```mysql
mysql> desc eatery;  
+------------+---------------+------+-----+---------+-------+
| Field      | Type          | Null | Key | Default | Extra |
+------------+---------------+------+-----+---------+-------+
| id         | int(11)       | NO   | PRI | NULL    |       |
| money      | decimal(10,4) | YES  |     | NULL    |       |
| student_id | int(11)       | YES  | MUL | NULL    |       |
+------------+---------------+------+-----+---------+-------+

其中MUL表示该字段中的数据是可以重复的，即使删除外键，MUL依旧在
```

#### 置空操作

一般用来让外键删除数据

**on delete set null** 			置空操作，删除主表中的某个数据后，从表中对应的外键变为空

#### 级联操作

一般用来让外键更新数据

**on update cascade**		级联操作，更改主表中的数据后，从表中对应外键也跟着改变



#### 演示

```mysql
mysql> create table student(
    -> student_id int primary key,
    -> name varchar(30)
    -> );

mysql> create table eatery(
    -> id int primary key,
    -> money decimal(10,4),
    -> student_id int,
    -> foreign key(student_id) references student(student_id) on delete set null on update cascade
    -> )
    
    
    on delete set null 		置空操作，删除主表中的某个数据后，从表中对应的外键变为空
    on update cascade		级联操作，更改主表中的数据后，从表中对应外键也跟着改变
    
insert into student values(1, 'xuanjin'),(2,'Tom');
insert into eatery values(1, 12.5, 2),(2, 10.0, 1),(3, 8.5, 2);


update student set student_id=4 where name='xuanjin'; # 更改student_id

mysql> select * from student;
+------------+---------+
| student_id | name    |
+------------+---------+
|          2 | Tom     |
|          4 | xuanjin |
+------------+---------+
2 rows in set (0.00 sec)

mysql> select * from eatery;
+----+---------+------------+
| id | money   | student_id |
+----+---------+------------+
|  1 | 12.5000 |          2 |
|  2 | 10.0000 |          4 |
|  3 |  8.5000 |          2 |
+----+---------+------------+
3 rows in set (0.00 sec)

delete from student where student_id=2;  # 删除数据student_id=2\

mysql> select * from student;
+------------+---------+
| student_id | name    |
+------------+---------+
|          4 | xuanjin |
+------------+---------+
1 row in set (0.00 sec)

mysql> select * from eatery;
+----+---------+------------+
| id | money   | student_id |
+----+---------+------------+
|  1 | 12.5000 |       NULL |
|  2 | 10.0000 |          4 |
|  3 |  8.5000 |       NULL |
+----+---------+------------+
3 rows in set (0.00 sec)
```

## 数据库设计思维

### 数据库设计基本概念

#### 1.关系

关系型数据库

通过两张表的共有字段去确定数据的完整性

#### 2.行

一条数据 **实体**

#### 3.列

一个字段 **属性**



#### 数据的冗余

相同的数据存储在不同的地方（一摸一样的数据存储多余一份的情况）

优点：便于查询，提高查询性能

缺点：数据过多，成本高

减少冗余：分表



### 实体和实体之间的关系

一对一

一对多

多对一

多对多

### Codd范式 

#### Codd第一范式  确保字段的原子性

保证每一个字段的内容是不能再分的

#### Codd第二范式  非键字段必须依赖于键字段

这张表中不该有的东西不能出现，说白了就是别tm没事找事

#### Codd第二范式  消除传递依赖

对于多余的字段，要考虑是否要删除



## 单表查询

### select , from.dual, where, in, between...and, null

```mysql
select + '查询内容'			
select + 数据计算式				// 得出结果
select + '查询内容' as + 字段名	// as 起别名

select * from t1,t2;			// 输出t1和t2的笛卡尔积
// example 笛卡尔积
mysql> select * from student_2;
+----+---------+-------+----------+
| id | name    | phone | address  |
+----+---------+-------+----------+
|  1 | xuanjin | 1234  | hangzou  |
|  2 | yip     | 5678  | shanghai |
+----+---------+-------+----------+
mysql> select * from student_3; 
+----+---------+-------+------------+
| id | name    | phone | address    |
+----+---------+-------+------------+
|  5 | frank   | 0000  | shanxi     |
|  6 | frank_2 | 11111 | shanxi_222 |
+----+---------+-------+------------+
mysql> select * from student_2, student_3; 
+----+---------+-------+----------+----+---------+-------+------------+
| id | name    | phone | address  | id | name    | phone | address    |
+----+---------+-------+----------+----+---------+-------+------------+
|  1 | xuanjin | 1234  | hangzou  |  5 | frank   | 0000  | shanxi     |
|  2 | yip     | 5678  | shanghai |  5 | frank   | 0000  | shanxi     |
|  1 | xuanjin | 1234  | hangzou  |  6 | frank_2 | 11111 | shanxi_222 |
|  2 | yip     | 5678  | shanghai |  6 | frank_2 | 11111 | shanxi_222 |
+----+---------+-------+----------+----+---------+-------+------------+

select 2*7 as res;					// 该句后默认带from dual 
select 2*7 as res from dual;		 // 查询来自默认伪表

select * from student where id=2;     
// where后面可以跟上判断的语句，如=,!=.and,or  等来具体查询
// where后面还可跟in，例如where address in ('shanghai','beijing');
// 即可查出shanghai，beijing的数据，类似的，还可以使用 not in

select * from student where age between 15 to 20;
select * from student where age not between 15 to 20;
//　根据数据范围进行查找

select * from student where age is null;
select * from student where age is not null;
// 查找字段中为空的数据

// 聚合函数
select sum(chinese) from score;		// 求表score中chinese字段的和
select avg(chinese) from score;		// 平均值
select max(chinese) from score;		// 最大值
select min(chinese) from score;		// 最小值
select count(chinese) from score;	// 次数，
```



### 模糊查询，排序查询， 分组查询，having，limit，distinct

```mysql
// 模糊查询
select * from student where name like '张%';		// % 表示模糊多个字节
select * from student where name like '高_';		// _ 表示只查询其后带一个字节的

//  排序查询
select * from student order by number asc;		// 对字段number排序查询，升序
select * from student order by number desc;		// 对字段number排序查询，降序

// 分组查询
select avg(age) as '年龄', gender as '性别' from student group by gender;
select avg(age) as '年龄', address as '地区' from student group by address;
select avg(age) as '年龄', address as '地区' from student group by address desc;
select group_concat(id), gender from student_1 group by gender;
// 对于分组查询，语句前半部分必须是聚合函数如avg(age),as+''起别名，
// 逗号后面先是要分组的字段+(as+'')+from+表名+group by+要分组的字段+(排序asc/desc);

// having
select avg(age) as 'age', address as 'address' from student group by address having age > 24;
// 对查询的结果再次进行筛选查询
// as 起别名的好处就在于可以方便对查询结果进行再筛选时使用

// limit
select * from student limit 0, 3;	// 从表中第0号开始，查询3条数据
select * from student limit 3;		// 只有一个数字，则默认从0 开始查x条数据
select 8 from student order by age asc limit 3;	// 结合排序查找年龄最小的三个

// distinct  去重
select distinct address from student;	//  查询所有address，不重复
select count(distinct address) from student; // 计数，共有多少不同的城市
select all address from student;		//  默认情况下自带all，查询该字段的所有

```



## 多表查询

```mysql
// union联合查询
select age, gender from student union select name, phone from teacher;
select age, gender from student union distinct select name, phone from teacher;
// 联合查询可以是两张表中的不同字段，但是前后字段数目必须相同，同时还可加distinct去重

// 内连接 inner join
select name, score from student inner join score on student.id=score.student_id;
// select 字段 from 主表名 inner join 从表名 on 表名.字段=表名.字段;

// 左连接 left join
// 以左表为基准以主表为基准，主表中的每一条数据都使用
select name, score from student left join score on student.id=score.student_id;

// 右连接 right join
// 以右表为基准以从表为基准，从表中的每一条数据都使用
select name, score from student right join score on student.id=score.student_id;

// 笛卡尔积 cross join 
select * from student_5 cross join student_6;

// 自然连接 natural join
// 按照两张表中相同字段名对两张表进行整理
// 如果两张表中没有相同的字段名，则返回笛卡尔积
select * from student_5 natural join student_6;
select * from student_5 natural left join student_6;
select * from student_5 natural right join student_6;

// 如果两个表中有多个字段名相同，则使用 using() 来指定字段
select * from student_5 inner join student_6 using(id);

// 注意：
// 在实际使用中，更多的使用完整的 inner join 内连接来进行关联
// 这样可以更清晰的展示表结构以及减少错误
```



## 子查询

```mysql
select * from student where id in (select studnet_id from score where score>=85);
select * from student where id not in (select studnet_id from score where score>=85);
// 查询score表中分数大于（不大于）85的学生，打印出其对应的studnet表中的信息

select * from studnet where id exists (select studnet_id from score where score>=85);
select * from studnet where id not exists (select studnet_id from score where score>=85);
// 如果score表中有大于（不大于）85的学生，则打印出studnet表中的全部信息


```



## 高级部分

### 视图

隐藏表中的敏感数据和表的结构，降低select语句的复杂程度

```mysql
// 创建视图
create view view_1 as select name, phone from student;
create view view_2 as select name, phone, score from student inner join score on student.id=score.student_id;

// 显示视图。
// 因为视图和表都在一起显示，在命名视图时应加上前缀vw，以进行区分
show tables;
// 查看视图
desc view_1;
show create view_1;
select * from view_1;

// 修改视图（修改此视图的查询内容）
alter view view_1 as select name from student;
// 删除视图
drop view view_1;


```



### 事务

应用于转账，资金等方面

```mysql
start transaction;		// 开始事务
update wallet set balance=balance-50 where id=1;
update wallet set balance=balance+50 where id=2;	// 双方确认
commit;			// 提交

rollback;		// 回滚。在事务未提交之前可以执行此命令以取消之前的操作

savepoint + 回滚点	// 设置回滚点
rollback to 回滚点 // 返回回滚点

四大特性ACID
atomicity	原子性		不能再分了，事务是一个整体，要么一起执行，要么全部不执行
consistency 一致性		事务完成后，数据也要相对应的同步
isolation 	隔离性		每个事务都是相互隔离的
durability	持久性		事务一旦提交，就不能再更改了


```

注意事项：

必须保证数据库的引擎为 innodb ，才能使用事务



### 索引

index

优点：帮助快速查询

缺点：增删改效率降低；占用内存

分类：主键索引，唯一键索引，普通索引，全局索引

```mysql
// 创建索引
create index balance_index on wellet(balance); 	// 普通索引
create unique index score_index on student(score);
```



### 存储过程

```mysql
delimiter //				// 将语句结束符 ; 更改为 // 
create procedure proc()		 // 存储过程
	begin
	update wallet set balance=balance+50;
	update t3 set name='Tom';
	end //
	
delimiter ;					// 将语句结束符 // 更改为 ;

call proc();				// 调用存储过程，执行
drop procedure porc;		 // 删除存储过程

show create procedure proc;	 // 查看存储过程

show procedure status \G	 // 查看所有存储过程
```



### 有趣的函数

#### number

```mysql
select rand();			// 生成一个随机数
select * from student order by rand() limit 3;
	// 从student表中随机取3个人（抽奖）
select * from student order by rand();
	// 随机排序

select ceil(3.1);		// 向上取整
select floor(3.1);		// 向下取整
select round(3.5);    	// 四舍五入
select turncate(3.1415926, 2);	// 截取x位

```

#### string

```mysql
select ucase('frank');		// 转换为大写
select lcase('FRANK');		// 转换为小写
select left('Frank',2);		// 从左截取
select right('frabk',2);	// 从右截取
select substring('frank',2,3);	// 从第二位开始截取3位
select concat('frank','frank');	// 连接字符串

```

#### other

```mysql
select now();			// 获取当前时间
select unix_timestap();
select sha("frank");			// 加密字符串

```



## 企业规范约束

### 库表字段约束规范

1.在某一个字段中，如果要使用是或否（比如这个人是不不是vip），一定要给上 i s_xxx 关键字，其数据类型一定要是 unsigned tinyint ，长度为 1 。

2.如果该字段的数据不能为负数（比如年龄，身高等），则其数据类型一定要设置为unsigned xxxxx。

3.仓库名一般和应用名保持一致。数据库的表名，字段名，必须使用小写字母，不能出现大写字母，不能出现复数，也不能以MySQL关键字命名。不能以数字开头。如果存在分隔单词，必须用下划线隔开，下划线之间也不能只出现数字。字段名一定要谨慎考虑设计，一旦确定下来，再去改动极为麻烦。

4.关于索引名，主键索引名以pk开头即，pk_xxx；唯一键索引名：uk_xxxx；普通键索引名：idx_xxxxx。

6.对于小数类型，禁止使用float和double，全部使用 decimal ，以防止精度丢失给开发带来不必要的损失。

7.如果定义的字符串长度很小，则不必要使用 varchar （动长），应当使用 char （定长）就可以了。如果长度过长，超过5000，直接定义为 text 文本类型就好了。 

8.强制要求，表中必须定义三个字段：

​		1）id  必须设置为主键，并且类型为 unsigned bigint ，如果该表为单表，则必须设为自增

​		2）create_time  强制要求为 datetime 类型

​		3）update_ time  强制要求为 datetime 类型

9.如果某个字段频繁查询，则允许适当的冗余。

10.如果单表行数超过500万行或者容量超过两个G，则需要分库，分表。



### 索引规范

1.如果在业务或流程上具有唯一特性的字段，即使它是多个字段的组合，也应该设置唯一索引。

2.实际开发中两个以上表的关联查询是不允许的。两表 join 两边的数据类型必须一致。

3.多表关联查询时，要保证关联查询的字段也应该要有索引。



### SQL开发约束

1.在查询中，count(xxx,xxx,xxx) 不能替代 count(*) 。

2.判断某字段是否为空，要用 isnull() ，或where xxx is null ,而不能用xxx=null。

3.不要使用外键和级联，特别是在并发的项目中。一切外键和级联的问题统统在应用层解决。

4.实际开发过程中不允许使用存储过程。

5.在数据修改或更新之前，先将数据查询出来再进行更改。

6.子查询中有关 in 的操作，能避免就避免。

7.UTF-8 作为标准格式。



### 其他约束











