# Mysql

## mysql基础

### SQL

Structured Query Language:结构化查询语言。

### 创建数据库表（重点）

```sql
CREATE DATABASE School;
USE School;
SHOW TABLES;
-- 注意点，使用英文(),表的名称 和 字段 尽量使用 `` 括起来。
-- AUTO_INCREMENT 自增
-- 字符串使用单引号括起来！
-- 所有的语句后面加 ,（英文的）  最后一个字段不用加。
-- PRIMARY KEY  主键 一个表一般只有一个唯一的主键。
CREATE TABLE IF NOT EXISTS `student` (
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
	`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
	`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
	PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

格式

```sql
CREATE TABLE [IF NOT EXISTS] `表名` (
	`字段名` 列类型 [属性] [索引] [注释],
    `字段名` 列类型 [属性] [索引] [注释],
    ...
    `字段名` 列类型 [属性] [索引] [注释],
	PRIMARY KEY (`id`)`school``student`
)[表类型] [字符集设置] [注释]
```

### 数据表的引擎

```sql
-- 关于数据库引擎
/*
INNODB 默认使用
MYISAM早些年使用的
*/
```

|              | MYISAM | INNODB        |
| ------------ | ------ | ------------- |
| 事务支持     | 不支持 | 支持          |
| 数据行锁定   | 不支持 | 支持          |
| 外键约束     | 不支持 | 支持          |
| 全文索引     | 支持   | 不支持        |
| 表空间的大小 | 较小   | 较大，约为2倍 |

常规使用操作：

- MYISAM  节约空间，速度较快
- INNODB 安全性高，事务的处理，多表多用户操作

```
在物理空间内存在的位置
```

所有的数据库文件都存在data目录下，一个文件夹对应一个数据库。

本质还是文件的存储！、

Mysql 引擎在物理文件的区别

- INNODB 在数据库表中只有*.frm文件，以及上一级目录下的ibdata1文件
- MYISAM 对应的文件 ， 生成三个文件。
- *.frm - 表结构的定义文件
- *.MYD - 数据文件（data）
- *.MYI - 索引文件

```
设置数据库表的字符集编码
```

```sql
CHARSET=UTF8
```

不设置，默认的是Latin1，不支持中文。

在my.ini中配置默认编码。(不建议使用该方法)

```sql
character-set-server=utf-8
```

### Mysql数据管理

#### DDL（操作数据库，表）

用来定义数据库对象：数据库，表，列等。关键字：create，drop, alter等

1. 操作数据库：C R（retrieve查询）U D

   ```sql
   #查询所有的数据库
   show databases;
   
   #创建数据库
   create database if not exists 数据库名字;
   
   #使用数据库
   use db1;
   #查看当前正在使用的数据库
   select database();
   
   #查看创建数据库的语句(默认的字符集utf8)
   show create database 数据库名字;
   
   #创建一个字符集为gbk的数据库
   create database if not exists db1 character set gbk;
   
   #修改数据库字符集
   alter database 数据库名字 character set 字符集名字;
   
   #删除数据库(危险)
   drop database 数据库名字;
   drop database if exists db1;
   
   #练习：
   SHOW DATABASES;
   USE test1;
   SELECT DATABASE();
   SHOW CREATE DATABASE test1;
   ALTER DATABASE test1 CHARACTER SET utf8;
   CREATE DATABASE IF NOT EXISTS test2 CHARACTER SET utf8;
   DROP DATABASE IF EXISTS test2;
   ```

2. 操作表

   ```sql
   -- 查询数据库中的表
   SHOW TABLES;
   -- 查询表的结构 desc 表名
   DESC user;
   -- 删除表
   DROP TABLE user2;
   DROP TABLE IF EXISTS user2;
   -- 创建一个和student表相同的stu表(复制表)
   CREATE TABLE stu LIKE student;
   
   -- 注意点，使用英文(),表的名称 和 字段 尽量使用 `` 括起来。
   -- AUTO_INCREMENT 自增
   -- 字符串使用单引号括起来！
   -- 所有的语句后面加 ,（英文的）  最后一个字段不用加。
   -- PRIMARY KEY  主键 一个表一般只有一个唯一的主键。
   CREATE TABLE IF NOT EXISTS `student` (
   	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
   	`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
   	`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
   	`sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
   	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
   	`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
   	`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
   	PRIMARY KEY (`id`)
   )ENGINE=INNODB DEFAULT CHARSET=utf8
   -- 注意点：
   -- `` 字段名，使用这个包裹！
   -- 注释  --   /**/  #注释内容（MySQL特有的）
   -- sql 关键字大小写不明显，建议小写。
   -- 所有的符号全部用英文！
   
   -- 修改表名 alter table 表名 rename to 新名
   ALTER TABLE USER RENAME TO user1;
   -- 查看表的字符集
   SHOW CREATE TABLE USER;
   -- 修改表的字符集
   ALTER TABLE USER CHARACTER SET gbk;
   -- 添加一列 alter table 表名 add 列名 数据类型
   ALTER TABLE USER ADD age INT(5);
   -- 修改列名和类型
   ALTER TABLE USER CHANGE age sex VARCHAR(10);
   -- 只改列的类型
   ALTER TABLE USER MODIFY age VARCHAR(20);
   -- 删除列
   ALTER TABLE USER DROP age;
   ```

常用数据类型：

```sql
double: 小数类型
int:整数类型
date:日期，只包含年月日，yyyy-MM-dd
datetime:包含年月日时分秒，yyyy-MM-dd HH:mm:ss
timestamp:时间戳，yyyy-MM-dd HH:mm:ss  默认使用当前系统时间自动赋值
varchar:字符串
```



#### DML语言（增删改表中的数据）

对数据库中表的数据进行增删改。关键字：insert，delete，update等

#### 添加

```sql
insert into 表(列名1，列名2，列名3..) values(值1，值2，值3..);--向表中插入某些列
insert into 表 values(值1，值2，值3..); --向表中插入所有列

INSERT INTO student(NAME,age,sex,address,math,english) VALUES ('李四',12,'男','河南省商丘市',85,85),('赵五',20,'男','河南省郑州市',90,89),('周七',21,'女','河南省濮阳市',95,96),('小明',25,'男','河南省南阳',97,100);
```

#### 修改

```sql
update 表名 set 字段名=值,字段名=值...; --这个会修改所有的数据，把一列的值都变了
update 表名 set 字段名=值,字段名=值... where 条件;
```

#### 删除

**delete 命令**

```sql
delete from 表名 [where条件]
delete from 表名;
truncate table 表名;
```

**TRUNCATE命令**

作用：完全清空一个数据库表，表的结构和索引约束不会变！

```sql
-- 清空 student表
TRUNCATE `student`
```

**delete和truncate的区别;**

```sql
delete删除表中的数据，是一条一条删除，不清空auto_increment记录数；删除后的数据如果在一个事务中还可以找回。
truncate删除是把表直接drop掉，重新建表，auto_increment将置为零。删除的数据不能找回。执行速度比delete快。
```

（**面试聊天加分项**）了解：`delete删除问题`，重启数据库，现象

- InnoDB 自增列会重1开始（存在内存当中的，断电即失。）
- MyISAM 继续从上一个自增量开始（存在文件中，不会丢失。）

#### DQL查询数据（最重点）  p502

用来查询数据库中表得到数据。关键字：select，where等。

1. 排序查询

   语法：order by 排序字段 排序方式（默认市升序）

   排序方式有两种：desc降序  asc升序

   **如果有多个条件，当前条件值相同时，才会判断第二个条件。**

   ```sql
   -- 排序查询 order by 								
   SELECT * FROM student ORDER BY math ASC;
   -- 当math分数相同时，按照english降序排序
   SELECT math,english FROM student ORDER BY math ASC,english DESC;
   ```

2. 聚合函数

   将一列数据作为一个整体，进行纵向的计算**（排除null值）**。

   - count：计算个数
   - max:计算最大值
   - min:计算最小值
   - avg：计算平均数

   ```sql
   -- 计算学生的人数 一定要是非空列
   SELECT COUNT(NAME) FROM student;
   
   SELECT MAX(math) FROM student;
   SELECT MIN(math) FROM student;
   SELECT AVG(english) FROM student;
   ```

3. 分组查询

   语法：select 字段，函数 from 表名 group by 字段；

   查询的字段必须是`分组字段`或者`聚合函数`

   ```sql
   -- 按照性别分组，分别查询男女学的数学平均分
   SELECT sex,AVG(math) FROM student GROUP BY sex;
   
   -- 按照性别分组，分别查询男女学的数学平均分，要求：分数低于80的不参与分组，分组之后人数要大于2人
   SELECT sex,AVG(math) FROM student WHERE math > 80 GROUP BY sex HAVING COUNT(id) > 2;
   ```

   ```sql
   select [ALL | DISTINCT]
   FROM TABLE_name [as table_name2]
   	[left | right | inner join table_name2]  -- 联合查询
   	[where ...] -- 指定结果徐满足的条件
   	[group by ...] -- 指定结果按照哪几个字段来分组
   	[having] -- 过滤分组的记录必须满足的次要条件
   	[order by ...] -- 指定查询记录按一个或多个条件排序
   	[limit]  -- 指定查询的记录从哪条至哪条。 
   ```

   where和having区别：

   - **where在分组之前进行限定，如果不满足则不参与分组。having在分组之后进行限定，如果不满足结果就不会被查询出来。**
   - **where后面不可以跟聚合函数，having可以。**

4. 分页查询

   语法：limit  开始的索引 ，每页查询的条数；

   开始索引的公式：**开始的索引 = （当前页码 - 1）* 每页条数**

   ```sql
   -- 每页显示3记录
   SELECT * FROM student LIMIT 0,3;  -- 第1页
   
   SELECT * FROM student LIMIT 3,3;  -- 第2页
   
   SELECT * FROM student LIMIT 6,3;  -- 第3页
   ```

#### DQL(Data Query Language:数据查询语言)

- 所有的查询操作都用它  Select
- 简单的查询和复杂的查询他都能做~
- **数据库中最核心的语言，做重要的语句**
- 使用频率最高的语句

语法：`select 字段,... from 表`

```sql
select version()  -- 查询系统版本（函数）
select 1000*3-1 as 计算结果  -- 用来计算（表达式）
select @@auto_increment_increment --查询自增的步长（变量）


--学员考试成绩+1分查看
select `studentNo`,`studentResult` + 1 as '提分后' from result
```

#### 基础查询

```sql
-- 查询姓名和年龄								
SELECT NAME,age FROM student;
-- 去除重复 关键字distinct
SELECT  DISTINCT address FROM student;
-- 计算相加时如果为null值则换成0
SELECT NAME,math,english,math + IFNULL(english,0) FROM student;
```



> 去重 distinct

```sql
select distinct `字段` from 表名
```

#### where条件子句

作用：检索数据中**符合条件**的值

> 运算符    

```sql
 <、>、<=、>=、=、<>
 Between...and
 in(集合)
 is null
 与&&  同时为真则为真。
 或||  同时为假则为假。
 非！  真为假，假为真。
```

```sql
SELECT * FROM student WHERE math > 90;
SELECT * FROM student WHERE age BETWEEN 25 AND 30;

SELECT * FROM student WHERE age IN (23,20,25);
SELECT * FROM student;
-- 模糊查询 查询名字以小开头的名字的信息
-- %是指多个字符  _是指单个字符
SELECT * FROM student WHERE NAME LIKE "小%";
SELECT * FROM student WHERE NAME LIKE "小_";
```

#### 约束：

概念：**对表中的数据进行限定，保证数据的正确性，有效性和完整性。**

分类：

1. 主键约束：primary key
2. 非空约束：not null
3. 唯一约束：unique
4. 外键约束：foreign key

**唯一约束**

```sql
-- 增加唯一约束  注意：可以为多个null值
CREATE TABLE stu(
	id INT(5),
	NAME VARCHAR(5) UNIQUE
);
SELECT * FROM stu;

-- 删除唯一约束  唯一约束也叫唯一索引，
-- 所以删除的时候不能使用alter table stu modify name varchar(5);
ALTER TABLE stu DROP INDEX NAME;

-- 创建表后添加约束
ALTER TABLE stu MODIFY NAME VARCHAR(5) UNIQUE;
```

**主键约束**

**非空且唯一,一张表只能有一个字段为主键，主键是表中记录的唯一标识**

```sql
-- 创建表时添加主键
CREATE TABLE stu1(
	id INT(5) PRIMARY KEY,
	NAME VARCHAR(5)
);

-- 删除主键约束
ALTER TABLE stu1 DROP PRIMARY KEY;

-- 创建表后添加主键约束
ALTER TABLE stu1 MODIFY id INT(5) PRIMARY KEY;
DESC stu1;
```

**外键约束**

语法：CONSTRAINT **外键名字** FOREIGN KEY (**dep_id**) REFERENCES **关联表的主键**

```sql
CREATE TABLE emplyee(
	id INT(5) PRIMARY KEY AUTO_INCREMENT,
	NAME VARCHAR(30),
	age INT(5),
	dep_id INT,
	CONSTRAINT emp_dept_id FOREIGN KEY (dep_id) REFERENCES department(id)
);
INSERT INTO emplyee(NAME,age,dep_id) VALUES ("张三",23,1),
						("李四",24,1),
						("王五",25,1),
						("老王",22,2),
						("大王",21,2),
						("小王",20,2);
CREATE TABLE department(
	id INT PRIMARY KEY AUTO_INCREMENT,
	dep_name VARCHAR(20),
	dep_location VARCHAR(30)
);
INSERT INTO department(dep_name,dep_location) VALUES ("研发部","广州"),("销售部","深圳");

-- 删除外键
ALTER TABLE emplyee DROP FOREIGN KEY emp_dept_id;
-- 添加外键
ALTER TABLE emplyee ADD CONSTRAINT emp_dept_id FOREIGN KEY (dep_id) REFERENCES department(id);
```

![image-20210310165629327](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310165629327.png)

设置级联:需要先删除外键，在设置`ON UPDATE CASCADE``ON DELETE CASCADE`删除时会同时删除关联的表的数据。

```sql
-- 删除外键
ALTER TABLE emplyee DROP FOREIGN KEY emp_dept_id;

-- 添加外键 并设置级联
ALTER TABLE emplyee ADD CONSTRAINT emp_dept_id FOREIGN KEY (dep_id) REFERENCES department(id) ON UPDATE CASCADE;

-- 添加外键 并设置级联更新，设置级联删除 
ALTER TABLE emplyee ADD CONSTRAINT emp_dept_id FOREIGN KEY (dep_id) REFERENCES department(id) ON UPDATE CASCADE ON DELETE CASCADE;

```

### 数据库的设计

1. 多表之间的关系

   - 一对一 

   - 一对多（多对一）

     **在多的一方建立外键，指向一的一方的主键。**

     ![image-20210310200820937](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310200820937.png)

   - 多对多

     ![image-20210310201356184](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310201356184.png)

2. 数据库设计的范式

   **完全函数依赖：**如果A是个属性组，B属性的确定依赖于A属性组中所有的属性值。

   **部分函数依赖：**如果A是个属性组，B属性的确定依赖于A属性组中的某一个。

   **传递依赖：**（A->B，B->C）通过A属性（属性组）的值，可以唯一确定B的值，在通过B属性（属性组）的值可以确定C属性的值。我们C为传递依赖于A。

   **主码：**属性（属性组）可以确定所有的`其他属性`**(非主属性)**。

- **第一范式：每一列都是不可分割的原子项。**

- **第二范式：在第一范式的基础上，非主属性必须完全依赖主码（通过主属性可以确定哪些非主属性，再把非主属性放入到一张表中）。**

- **第三范式：在第二范式的基础上，消除传递依赖（A->B,B->C**

  ​																								**B->D，把C，D放入到一张表）**
  

### 多表查询

准备创建表：

```sql
-- 创建一张部门表
CREATE TABLE dept(
	id INT PRIMARY KEY AUTO_INCREMENT,
	NAME VARCHAR(20)
);
-- 插入数据
INSERT INTO dept(NAME) VALUES ("开发部"),("市场部"),("财务部");
-- 创建一张员工表
CREATE TABLE emp(
	id INT PRIMARY KEY AUTO_INCREMENT,
	NAME VARCHAR(20),
	sex CHAR(1),
	salary DOUBLE,
	jion_date DATE,
	dept_id INT,
	FOREIGN KEY (dept_id) REFERENCES dept(id)
);
-- 插入数据
INSERT INTO emp(NAME,sex,salary,jion_date,dept_id) VALUES ("孙悟空","男",7200,"2013-02-24",1);
INSERT INTO emp(NAME,sex,salary,jion_date,dept_id) VALUES ("猪八戒","男",3600,"2013-12-02",2);
INSERT INTO emp(NAME,sex,salary,jion_date,dept_id) VALUES ("唐僧","男",9000,"2017-08-04",2);
INSERT INTO emp(NAME,sex,salary,jion_date,dept_id) VALUES ("白骨精","女",5000,"2018-03-15",3);
INSERT INTO emp(NAME,sex,salary,jion_date,dept_id) VALUES ("蜘蛛精","女",4500,"2015-03-14",1);
```

多表查询：

```sql
-- 多表查询  笛卡尔积表的所有组合情况
SELECT * FROM emp,dept;
```

多表查询（为了消除无用的数据）分类：

1. 内连接查询：

   - **隐式的内连接：**使用where条件消除无用数据

     ```sql
     -- 查询所有员工信息对应的部门信息
     SELECT * FROM emp,dept WHERE emp.dept_id = dept.`id`;
     -- 标准格式
     SELECT 
     	emp.`id`,emp.`NAME`,emp.`sex`,dept.`name` 
     FROM 
     	emp,dept 
     WHERE 
     	emp.dept_id = dept.`id`;
     ```

   - **显式的内连接**

     语法：`select * from 表名 [inner] jion 另一张表 on 条件`

     ```sql
     -- 查询所有员工信息对应的部门信息	
     SELECT * 
     FROM 
     	emp
     INNER JOIN 
     	dept
     ON emp.`dept_id` = dept.`id`;
     ```

2. 外连接查询：

   - 左外连接：

     语法：`select 字段列表 from 表1 left [outer] jion 表2 on 条件`

     ```sql
     -- 插入一条信息，员工小白龙，但没有部门
     -- 查询所有员工信息，如果员工有部门，则查询部门名称，没有则不显示部门信息。
     SELECT 
     	t1.*,t2.`name`
     FROM 
     	emp t1
     LEFT JOIN
     	dept t2
     ON
     	t1.`dept_id` = t2.`id`;
     ```

     **查询的是左表的所有数据以及交集部分。**

   - 右外连接：

     语法：`select 字段列表 from 表1 right [outer] jion 表2 on 条件`

     ```sql
     SELECT 
     	t1.*,t2.`name`
     FROM 
     	emp t1
     RIGHT JOIN
     	dept t2
     ON
     	t1.`dept_id` = t2.`id`;
     ```

     **查询的是右表的所有数据以及交集部分。**

3. 子查询：

   **概念：查询中嵌套查询，称嵌套的查询为子查询。**

   ```sql
   -- 查询工资最高的员工信息
   -- 1.查询工资最高是多少？
   SELECT MAX(emp.`salary`) FROM emp;
   -- 2.工资最高的员工的信息。
   SELECT * FROM emp WHERE emp.`salary` = 9000;
   
   -- 一条sql就完成操作
   SELECT * FROM emp WHERE emp.`salary` = (SELECT MAX(emp.`salary`) FROM emp);
   ```

   子查询的不同情况：

   1. **子查询的结果是单行单列**

      子查询的结果可以作为条件

      ```sql
      -- 查询员工工资小于平均工资的人
      SELECT *
      FROM
      	emp
      WHERE 
      	emp.`salary` < (SELECT AVG(emp.`salary`) FROM emp);
      ```

   2. **子查询的结果是多行单列**

      ```sql
      -- 查询'财务部'和'市场部'所有的员工信息
      SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部';
      SELECT * FROM emp WHERE dept_id = 3 OR dept_id = 2;
      
      -- 子查询
      SELECT * FROM emp WHERE dept_id IN (SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部');
      ```

   3. **子查询的结果是多行多列**

      ```sql
      -- 查询员工入职日期是2013-12-02日之后的员工信息和部门信息
      SELECT * FROM dept t1,(SELECT * FROM emp WHERE emp.`jion_date` > '2013-12-02') t2
      WHERE t1.`id` = t2.dept_id;
      ```

> JOIN  对比

![点击查看源网页](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg2018.cnblogs.com%2Fcommon%2F842724%2F202002%2F842724-20200228155137649-1462263734.png&refer=http%3A%2F%2Fimg2018.cnblogs.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1615532992&t=2e76526ff7196469c972af0541cb605a)

```sql
-- 我要查询哪些数据 select ...
-- 从哪几个表种查from表 xxx  jion 连接的表  on 交叉条件

--假设存在一种多张表查询，慢慢来，先查询两张再慢慢增加。
```

> 自连接

自己的表和自己的表连接，核心：**一张表拆分为两张一样的表即可。**     

### Mysql常用函数



#### MD5加密（扩展）

什么是MD5？

主要增强算法复杂度和不可逆性。

MD5不可逆，具体值的MD5是一样的。

MD5破解网站的原理：背后有一个字典，ND5加密后的值  加密的前值。

```sql
CREATE TABLE `testmd5`(
	`id` INT(4) NOT NULL,
	`name` VARCHAR(20) NOT NULL,
	`pwd` VARCHAR(50) NOT NULL,
	PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 明文密码
INSERT INTO testmd5 VALUES(1,'zhangsan','123456'),(2,'lisi','123456'),(3,'wangwu','123456');
-- 加密  md5()是个函数
UPDATE testmd5 SET pwd=MD5(pwd) WHERE id = 1;
UPDATE testmd5 SET pwd=MD5(pwd);   -- 加密全部

-- 插入的时候加密
INSERT INTO testmd5 VALUES(4,'haha',MD5('123456'));

-- 如何校验：将用户传递过来的密码进行MD5加密，然后比对加密后的值。
```

### 事务

mysql是**默认开启事务自动提交**的，执行一下命令关闭自动提交（不建议）。

```sql
select @@autocommit  /* 查看当前事务状态*/
set autocommit = 0  /*关闭自动提交 */
set autocommit = 1  /*开启自动提交 （默认的）*/
```

![image-20210311110624011](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311110624011.png)

操作：

1. 开启事务：start transaction
2. 回滚事务：rollback
3. 提交事务：commit

```sql
-- 创建账户表，插入数据
CREATE TABLE account(
	id INT PRIMARY KEY AUTO_INCREMENT,
	NAME VARCHAR(10),
	balance DOUBLE
);
INSERT INTO account(NAME,balance) VALUES("zhansan",1000),("lisi",1000);

SELECT * FROM account;

UPDATE account SET balance = 1000;

-- 张三给李四转账500元
-- 0.开启事务
START TRANSACTION;
-- 1.张三的账户-500
UPDATE account SET balance = balance - 500 WHERE NAME = "zhansan";
-- 出异常了
-- 2.李四的账户+500
UPDATE account SET balance = balance + 500 WHERE NAME = "lisi";
-- 发现没问题，提交事务
COMMIT;
-- 发现出问题了，回滚事务
ROLLBACK;
```

**事务的四大特征（面试题）：**

- **原子性（Atomicity）**
  不可分割的最小操作单位，要么同时成功，要么同时失败。
- **一致性（Consistency）**
  事务前后的数据完整性要保一致。金额总数不变。
- **隔离性（Isolation）**
  事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，多个并发事务之间要相互隔离。**（多个事务之间，相互独立）**
- **持久性（Durability）**----事务提交
  持久性是指一个事务一旦被提交或回滚后，数据库持久化的保存数据。

**要么同时成功，要么同时失败！**



**参考博客连接： ** **https://blog.csdn.net/dengjili/article/details/82468576**

> 隔离导致的一些问题

**脏读：**

指一个事务读取了另外一个事务未提交的数据。

**不可重复读：**

在同一个事务中，读取表中的某一行数据，多次读取结果不同。

**虚读（幻读）：**

是指在一个事务内读取到了别的事务插入的数据，导致前后读取不一致。
 （一般是行影响，多了一行）

#### **四种隔离级别的设置**

**数据库**
set transaction isolation level 设置事务隔离级别set
select @@tx_isolation 查询当前事务隔离级别

| 设置             | 描述                                               |
| ---------------- | -------------------------------------------------- |
| Serializable     | 可避免脏读、不可重复读、虚读情况的发生。（串行化） |
| Repeatable read  | 可避免脏读、不可重复读情况的发生。（可重复读）     |
| Read committed   | 可避免脏读情况发生（读已提交）。                   |
| Read uncommitted | 最低级别，以上情况均无法保证。(读未提交)           |

**隔离级别越高，安全性越高，但效率越来越低。**



### 权限管理(DCL)

> 授权（grant 和 revoke）操作

用户表：mysql.user

本质：是对这张表的增删改查。

```sql
#查询用户 切换mysql->查看user表
use mysql;
select * from user;

#创建用户 create user 用户名 identified by '密码'
create user xaiozhang identified by '123456'

#删除用户
drop user xiaozhang

#修改密码（当前用户）
set password = password('123456')
#修改密码（指定用户密码）
set password for 用户名 = password('123456')

#重命名 rename user 原来名字 to 新名字
rename user 旧名字  to 新名字

#用户授权  all privileges全部权限（不包括grant权限），库.表
grant all privieges on *.* to 用户名

#查询权限(除root权限外)
show grants for 用户
#查看主机的root权限
show grants for root@localhost

#撤销权限  revoke 哪些权限， 在哪个库撤销， 给谁
revoke all privieges on *.* from 用户
```

**root管理员忘记登陆密码怎么办？**

```sql
#停止MySQL服务 以管理员身份运行cmd
cdm--> net stop mysql

#使用无验证方式启动mysql服务
mysqld --skip-grant-tables

#打开新的窗口，直接输入MySQL命令，回车就能登陆成功，再修改密码即可。
```

### 数据库备份

为什么要备份？

- 保证重要的数据不丢失
- 数据转移

mysql备份数据库的方式

1. 直接copy物理文件（data文件）

2. 在sqlyong可视化工具中手动导出

   - 在想要导出的表或者库中，右键，选择备份或者导出

     ![image-20210302104421812](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210302104421812.png)

3. 使用命令行导出 `musqldump`命令行

   ```xml
   #mysqldump -主机名 -用户名 -密码 数据库 表 >导出的地方
   mysqldump -localhost -uroot -p123456 school student >D:/a.sql
   ```




### JDBC（重点）

概念：Java DataBase Connectivity  **Java连接数据库**

本质：官方（sun公司）定义的**一套所有操作数据库的规则，即接口**。各个数据库厂商（mysql、oracle等）去实现这套接口，提供数据库驱动jar包。我们可以使用这套接口（JDBC）编程，真正执行的代码时驱动jar包中的实现类。

**数据库驱动：**

![image-20210311160336433](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311160336433.png)

**第一个JDBC程序**

创建一个数据库

```sql
CREATE DATABASE jdbcStudy CHARACTER SET utf8 COLLATE utf8_general_ci;
USE jdbcStudy;

CREATE TABLE users(
	id INT PRIMARY KEY,
	NAME VARCHAR(40),
	PASSWORD VARCHAR(40),
	email VARCHAR(60),
	birthday DATE
); 

INSERT INTO users (id,NAME,PASSWORD,email,birthday) VALUES (1,"zhangsan","123456","zs@com","2000-01-01"),
							(2,"lisi","123456","lisi@com","2001-02-02"),
							(3,"wangwu","123456","wangwu@com","2003-03-03");
SELECT * FROM users;
```

创建一个项目，添加一个lib目录并把驱动包（mysql-connector-java-5.1.48.jar）放入到lib目录中，

编写测试代码：

```java
package com.xiaozhang.lesson01;

import java.sql.*;

//我的第一个JDBC程序
public class JdbcDemo {
	public static void main(String[] args) throws ClassNotFoundException, SQLException {
		//1.加载驱动  固定写法
		Class.forName("com.mysql.jdbc.Driver");

		//2.用户信息和url  useUnicode=true(中文编码)&characterEncoding=utf8(字符集)&useSSL=true(安全连接)
		String url = "jdbc:mysql://localhost:3306/jdbcStudy?useUnicode=true&characterEncoding=utf8&useSSL=true";
		String username = "root";
		String password = "123456";
		//3.连接成功，数据库对象  connection代表数据库
		Connection connection = DriverManager.getConnection(url,username,password);
		//4.执行SQL的对象 statement
		Statement statement = connection.createStatement();

		//5.对象执行SQL
		String sql = "SELECT * FROM users";
		ResultSet resultSet = statement.executeQuery(sql);	//返回的结果集

		while(resultSet.next()){
			System.out.println("id = " + resultSet.getObject("id"));
			System.out.println("name = " + resultSet.getObject("NAME"));
			System.out.println("pwd = " + resultSet.getObject("PASSWORD"));
			System.out.println("email = " + resultSet.getObject("email"));
			System.out.println("birth = " + resultSet.getObject("birthday"));
			System.out.println("=================================");
		}
		//6.释放连接
		resultSet.close();
		statement.close();
		connection.close();
	}
}
```

步骤总结：

1. **加载驱动**
2. **连接数据库DriverMannager**
3. **获得执行sql的对象 Statement**
4. **获得返回的结果集**
5. **释放连接**



> DriverManager

jdbc 5.几版本后，不用注册数据库驱动，因为默认在INF目录下帮我们自动创建了数据库驱动。（注意：一般还是要手写。`Class.forName("com.mysql.jdbc.Driver")`）。

1.注册驱动：告知我们程序该使用哪一个数据库驱动jar包，源码中

```java
static {
        try {
            DriverManager.registerDriver(new Driver());
        } catch (SQLException var1) {
            throw new RuntimeException("Can't register driver!");
        }
    }
```

2.获取数据库连接：

- url：jdbc:mysql://ip地址（域名）:端口号/数据库名称

- username：

- password：

  ```java
  Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/jdbcStudy?useUnicode=true&characterEncoding=utf8&useSSL=true", "root", "123456");
  ```

  

```java
//1.加载驱动  固定写法
Class.forName("com.mysql.jdbc.Driver");

//3.连接成功，数据库对象  connection代表数据库
Connection connection = DriverManager.getConnection(url,username,password);

//这里connection 代表数据库，可以设置事务提交、事务回滚
connection.rollback();
connection.commit();
connection.setAutoCommit(true);
```



> URL

```java
String url = "jdbc:mysql://localhost:3306/jdbcStudy?useUnicode=true&characterEncoding=utf8&useSSL=true";
```



> Statement 执行SQL的对象  

```java
statement.execute();	//执行任何SQL
statement.executeUpdate();	//更新、插入、删除，返回一个受影响的行数
statement.executeQuery();	//执行查询操作，返回ReaultSet结果集
```



> ResultSet 查询的结果集：封装了所有的查询结果

获得指定的数据类型

```java
resultSet.getObject();	//不知道结果集中的数据类型的情况下使用
resultSet.getString();	//结果集为String
resultSet.getInt();		//结果集为int类型

boolean next();  游标向下移动一行，判断当前行是否是最后一行（是否有数据），如果是返回false不是最后一行则返回true。
```



> 释放资源

```java
//6.释放资源
resultSet.close();
statement.close();
connection.close();	//耗资源，用完后关掉
```



> Statement对象

**用于向数据库中发送SQL语句，想完成对数据库的增删改查，只需要通过这个对象向数据库发送增删查改的语句即可。**



> JDBC工具类

目的：简化书写

分析：

1. 注册驱动抽取
2. 抽取一个方法获取连接对象
   - 通过加载配置文件的形式
3. 抽取一个方法释放资源

第一种：

```java
package com.xiaozhang.lesson01.lesson02.utils;


import java.io.FileReader;
import java.io.IOException;
import java.io.InputStream;
import java.net.URL;
import java.sql.*;
import java.util.Properties;

public class JdbcUtils2 {
	//只有静态的才能访问静态
	private static String driver = null;
	private static  String url;
	private static String username;
	private static String password;
	/*
	* 配置文件的加载只需要加载一次，可以使用静态代码块完成。
	* 静态代码块中只能处理异常，不能抛异常
	* */
	static {
		try {
			//读取配置文件，获取值。

			//创建一个properties集合类对象
			Properties pro = new Properties();
			//加载文件
			ClassLoader classLoader = JdbcUtils.class.getClassLoader();
			URL resource = classLoader.getResource("db.properties");
			String path = resource.getPath();
			pro.load(new FileReader(path));


			driver = pro.getProperty("driver");
			url = pro.getProperty("url");
			username = pro.getProperty("username");
			password = pro.getProperty("password");

			//注册驱动
			Class.forName(driver);

		} catch (IOException e) {
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
	}

	//静态方法方便调用
	//获取连接的方法，返回的是连接的对象
	public static Connection getConnection() throws SQLException {
		return DriverManager.getConnection(url,username,password);
	}

	//释放资源的方法
	public static void close(Statement stmt,Connection conn){
		if (stmt != null){
			try {
				stmt.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		if (conn != null){
			try {
				conn.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}

	//释放资源的重载方法
	public static void close(ResultSet rs,Statement stmt,Connection conn){
		if (rs != null){
			try {
				rs.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}

		if (stmt != null){
			try {
				stmt.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		if (conn != null){
			try {
				conn.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}
}
```

第二种：

```java
package com.xiaozhang.lesson01.lesson02.utils;


import java.io.IOException;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

public class JdbcUtils {
	private static String driver = null;
	private static String url = null;
	private static String username = null;
	private static String password = null;

	static {
		try{
			//读取配置文件
			InputStream in = JdbcUtils.class.getClassLoader().getResourceAsStream("db.properties");

			Properties properties = new Properties();
			properties.load(in);

			driver = properties.getProperty("driver");
			url = properties.getProperty("url");
			username = properties.getProperty("username");
			password = properties.getProperty("password");

			//驱动只要加载一次
			Class.forName(driver);
		     } catch (Exception e) {
					e.printStackTrace();
				}
	}

	//获取链接
	public static Connection getConnection() throws SQLException {
		return DriverManager.getConnection(url,username,password);
	}

	//释放资源
	public static void release(Connection conn, Statement st, ResultSet rs){
		if (rs != null){
			try {
				rs.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		if (st != null){
			try {
				st.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
		if (conn != null){
			try {
				conn.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}
}
```



### SQL注入

sql存在漏洞，会被攻击导致数据泄露，**（SQL会拼接 or 使之成立）**

### PreparedStatedment对象

PreparedStatedment可以防止SQL注入问题，效率更高。

```java
package com.xiaozhang.lesson01.lesson01;

import com.xiaozhang.lesson01.lesson02.utils.JdbcUtils;
import com.xiaozhang.lesson01.lesson02.utils.JdbcUtils_dbcp;

import java.sql.*;
import java.util.*;
import java.util.Date;
/*
* DBCP连接池工具类操作插入数据
*
* */
public class TestInsert2 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;
        try {
            conn = JdbcUtils_dbcp.getConnection();
            String sql = "insert into users(id,`NAME`,`password`,`email`,`birthday`) values(?,?,?,?,?)";
            st = conn.prepareStatement(sql);

            st.setInt(1,5);
            st.setString(2,"haha");
            st.setString(3,"123456");
            st.setString(4,"haha@com");
            st.setDate(5,new java.sql.Date(new Date().getTime()));

            int i = st.executeUpdate();
            if (i > 0){
                System.out.println("插入成功！");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JdbcUtils_dbcp.release(conn,st,rs);
        }
    }
}
```







### 数据库连接池

数据库连接 ---  执行完毕 ---释放

连接  -- 释放  十分浪费系统资源

**池化技术：准备一些预先的资源，过来就连接预先准备好的。**



---- 开门 -- 业务员： 等待i-- 服务 --

最小连接数： 自行设置

最大连接数：自行设置  业务的最高承载上限

等待超时：100ms



编写一个连接池，实现一个接口DataSource

> 开源数据源实现(拿来即用)

1. DBCP

   需要导入jar包 `commons-dbcp-1.4`，`commons-pool-1.6`

   ```java
   package com.xiaozhang.lesson01.lesson02.utils;
   //DBCP工具类
   import org.apache.commons.dbcp.BasicDataSourceFactory;
   
   import javax.sql.DataSource;
   import java.io.InputStream;
   import java.sql.*;
   import java.util.Properties;
   
   public class JdbcUtils_dbcp {
   	private static DataSource dataSource = null;
   
   	static {
   		try{
   			//读取配置文件
   			InputStream in = JdbcUtils_dbcp.class.getClassLoader().getResourceAsStream("dbcpconfig.properties");
   
   			Properties properties = new Properties();
   			properties.load(in);
   
   			//创建数据源  工厂模式 -- > 创建
   			dataSource = BasicDataSourceFactory.createDataSource(properties);
   
   		} catch (Exception e) {
   					e.printStackTrace();
   				}
   	}
   
   	//获取链接
   	public static Connection getConnection() throws SQLException {
   		return dataSource.getConnection();	//从数据源中获取连接
   	}
   
   	//释放资源
   	public static void release(Connection conn, Statement st, ResultSet rs){
   		if (rs != null){
   			try {
   				rs.close();
   			} catch (SQLException e) {
   				e.printStackTrace();
   			}
   		}
   		if (st != null){
   			try {
   				st.close();
   			} catch (SQLException e) {
   				e.printStackTrace();
   			}
   		}
   		if (conn != null){
   			try {
   				conn.close();
   			} catch (SQLException e) {
   				e.printStackTrace();
   			}
   		}
   	}
   }
   
   ------------------------------------------------------------
   
   package com.xiaozhang.lesson01.lesson01;
   
   import com.xiaozhang.lesson01.lesson02.utils.JdbcUtils;
   import com.xiaozhang.lesson01.lesson02.utils.JdbcUtils_dbcp;
   
   import java.sql.*;
   import java.util.*;
   import java.util.Date;
   
   
   /*
   * DBCP连接池工具类操作插入数据
   *
   * */
   public class TestInsert2 {
   	public static void main(String[] args) {
   		Connection conn = null;
   		PreparedStatement st = null;
   		ResultSet rs = null;
   		try {
   			conn = JdbcUtils_dbcp.getConnection();
   
   			String sql = "insert into users(id,`NAME`,`password`,`email`,`birthday`) values(?,?,?,?,?)";
   
   			st = conn.prepareStatement(sql);
   
   			st.setInt(1,5);
   			st.setString(2,"haha");
   			st.setString(3,"123456");
   			st.setString(4,"haha@com");
   			st.setDate(5,new java.sql.Date(new Date().getTime()));
   
   			int i = st.executeUpdate();
   			if (i > 0){
   				System.out.println("插入成功！");
   			}
   
   		} catch (SQLException e) {
   			e.printStackTrace();
   		}finally {
   			JdbcUtils_dbcp.release(conn,st,rs);
   		}
   	}
   }
   ```
   
   
   
1. C3P0

   需要导包`c3p0-0.9.5.5`，`mchange-commons-java-0.2.19`

2. Druid:阿里巴巴

使用了数据库的连接池后，我们在项目中不需要编写数据库的代码了！

**结论：无论使用什么数据源，本质还是一样的，DataSource接口不会变，方法就不会变！**



## MySQL高级

### 索引

定义：帮助MySQL高效获取数据的数据结构。可以简单理解为“**排好序的快速查找数据结构**”

本质：索引是数据结构

目的：提高查询效率，可以类比字典。

优势：**提高数据检索的效率** (数据库的io成本)  **降低数据排序的成本**(cpu的消耗)

劣势：1、索引本身也是一张表，保存了主键与索引字段，并指向实体表的记录。

​			2、提高了查询效率，降低了更新表的速度。

索引分类：（建议一张表最好不要超过5个索引）

​	单值索引：一个索引只包含单个列，一个表可以有多个单列索引。

​	唯一索引：索引列的值必须唯一，但允许有空值。

​	复合索引：一个索引包含多个列

索引的创建

```sql
#创建索引
create [unique] index 索引名 on 表名（字段名 ...）
alter table 表名 add [unique] index 索引名 on 表名（字段名 ...）

#PRIMARY  KEY(主键索引)
ALTER  TABLE  `table_name`  ADD  PRIMARY  KEY (  `column`  )
#UNIQUE(唯一索引)
ALTER  TABLE  `table_name`  ADD  UNIQUE (`column` )
#INDEX(普通索引)
ALTER  TABLE  `table_name`  ADD  INDEX index_name (  `column`  )
#FULLTEXT(全文索引)
ALTER  TABLE  `table_name`  ADD  FULLTEXT ( `column` )
#多列索引
ALTER  TABLE  `table_name`  ADD  INDEX index_name (  `column1`,  `column2`,  `column3`  )


#删除索引
drop index [索引名字] on 表名

#查看
show index from 表名
```



### 索引结构

B+树

### 索引的创建条件

创建：1、主键自动创建唯一索引  2、外键  3、查询中排序的字段  4、频繁作为查询条件的字段 

不创建：1、表的数据比较少 。2、经常更新数据的时候。3、where里用不到的字段  4、数据重复且分布平均的表字段（比如地址、国家）

### 性能分析

![image-20210516112013898](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210516112013898.png)

mysql常见瓶颈：

![image-20210516112326634](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210516112326634.png)

### explain(执行计划)

explain sql语句

![image-20210516113218105](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210516113218105.png)

字段解释：

id:操作表的顺序。

​	id相同时，那么就从上往下依次执行。（多张表的时候）

​	id不相同时，数字越大越先执行。（子查询）

select_type:	主要用于区别普通查询、联合查询、子查询等的复杂查询。

| select_type  | 类型说明                        |
| ------------ | ------------------------------- |
| SIMPLE       | 简单SELECT(不使用UNION或子查询) |
| PRIMARY      | 最外层的SELECT                  |
| UNION        | UNION中第二个或之后的SELECT语句 |
| UNION RESULT | UNION的结果                     |
| SUBQUERY     | 子查询中的第一个SELECT          |
| DERIVED      | 衍生表(FROM子句中的子查询)      |

**type(重要)**:访问类型排列

显示查询使用了何种类型，从最好--->最差:system  >  const  >  eq_ref  >  ref  >  range  >  index  > ALL

- ###### 1、system

表中只有一行数据或者是空表，这是const类型的一个特例。且只能用于myisam和memory表。如果是Innodb引擎表，type列在这个情况通常都是all或者index

- ###### 2、const（常量）

通过索引一次就能找到，最多只有一行记录匹配。当联合主键或唯一索引的所有字段跟常量值比较时，

- ###### 3、eq_ref

唯一性索引扫描，对于每个索引键，表中只有一条记录与之匹配。常见于主键或唯一索引扫描。

**相对于下面的ref区别就是它使用的唯一索引，即主键或唯一索引，而ref使用的是非唯一索引或者普通索引。eq_ref只能找到一行，而ref能找到多行。**

- ###### 4、ref

对于来自前面表的每一行，在此表的索引中可以匹配到多行。若联接只用到索引的最左前缀或索引不是主键或唯一索引时，使用ref类型（也就是说，此联接能够匹配多行记录）。

- ###### 5、range

索引范围查询，常见于使用 =, <>, >, >=, <, <=, IS NULL, <=>, BETWEEN, IN()或者like等运算符的查询中。

```sql
SELECT * FROM tbl_name
  WHERE key_column BETWEEN 10 and 20;

SELECT * FROM tbl_name
  WHERE key_column IN (10,20,30);
```

- ###### 6、index

索引全表扫描，把索引从头到尾扫一遍。这里包含两种情况：
 一种是查询使用了覆盖索引，那么它只需要扫描索引就可以获得数据，这个效率要比全表扫描要快，因为索引通常比数据表小，而且还能避免二次查询。在extra中显示Using index，反之，如果在索引上进行全表扫描，没有Using index的提示。

- ###### 7、all

全表扫描，性能最差。



possible_keys

查询可能使用到的索引都会在这里列出来。（不一定被查询实际使用）

key

查询真正使用到的索引。如果为null，则没有使用索引。

覆盖索引：查询的字段和索引的字段一致。



key_len

查询用到的索引长度（字节数）。(结果相同的情况下，长度越短越好)
 如果是单列索引，那就整个索引长度算进去，如果是多列索引，那么查询不一定都能使用到所有的列，用多少算多少。留意下这个列的值，算一下你的多列索引总长度就知道有没有使用到所有的列了。

**key_len只计算where条件用到的索引长度，而排序和分组就算用到了索引，也不会计算到key_len中。**

![image-20210516154408231](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210516154408231.png)

 ref

显示索引的哪一列被使用了，如果可能的话是个常数。

如果是使用的常数等值查询，这里会显示const，如果是连接查询，被驱动表的执行计划这里会显示驱动表的关联字段，如果是条件使用了表达式或者函数，或者条件列发生了内部隐式转换，这里可能显示为func

**rows（重要）**

**rows 也是一个重要的字段**。 这是mysql估算的需要扫描的行数（不是精确值）。
这个值非常直观显示 SQL 的效率好坏, 原则上 rows 越少越好.



**Extra(重要)**

EXplain 中的很多额外的信息会在 Extra 字段显示

- **distinct**：在select部分使用了distinc关键字
- **Using filesort**：当 Extra 中有 Using filesort 时, 表示 MySQL 需额外的排序操作, 不能通过索引顺序达到排序效果. 一般有 Using filesort, 都建议优化去掉, 因为这样的查询 CPU 资源消耗大.

```sql
# 例如下面的例子:

mysql> EXPLAIN SELECT * FROM order_info ORDER BY product_name \G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: order_info
   partitions: NULL
         type: index
possible_keys: NULL
          key: user_product_detail_index
      key_len: 253
          ref: NULL
         rows: 9
     filtered: 100.00
        Extra: Using index; Using filesort
1 row in set, 1 warning (0.00 sec)
我们的索引是

KEY `user_product_detail_index` (`user_id`, `product_name`, `productor`)
但是上面的查询中根据 product_name 来排序, 因此不能使用索引进行优化, 进而会产生 Using filesort.
如果我们将排序依据改为 ORDER BY user_id, product_name, 那么就不会出现 Using filesort 了. 例如:

mysql> EXPLAIN SELECT * FROM order_info ORDER BY user_id, product_name \G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: order_info
   partitions: NULL
         type: index
possible_keys: NULL
          key: user_product_detail_index
      key_len: 253
          ref: NULL
         rows: 9
     filtered: 100.00
        Extra: Using index
1 row in set, 1 warning (0.00 sec)
```

- **Using index**
   "覆盖索引扫描", 表示查询在索引树中就可查找所需数据, 不用扫描表数据文件, 往往说明**性能不错**

- **Using temporary**
   查询有使用临时表, 一般出现于排序, 分组和多表 join 的情况, 查询效率不高, 建议优化.

  

作用：

![image-20210516112903148](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210516112903148.png)

### 索引优化

1、jion语句的优化

尽可能减少jion语句中的nestedloop的循环总次数；“永远用小结果集驱动大结果集”。

优先优化nestedloop的内层循环；

保证jion语句中被驱动表上jion条件字段已经被索引；

当无法保证被驱动表的jion条件字段被索引且内存资源充足的前提下，不要太吝啬jionBuffer的设置；

### 索引失效

![image-20210517090425489](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517090425489.png)

**最佳左前缀法则**：如果引用了多列，要遵循最左前缀法则，指的是查询从索引的最左前列开始，不跳过索引中的列。

group by 基本上都需要进行，会有临时表产生。分组之前必排序。



### 小表驱动大表

![image-20210517110357200](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517110357200.png)

![image-20210517110330757](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517110330757.png)

![image-20210517110710003](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517110710003.png)



### 慢查询日志



### Show Profile

是什么：是MySQL提供可以用来分析当前会话中语句执行的资源消耗情况。  可以用于SQL的调优的测量。

```sql
#查看profile状态
show variables like 'profiling';
```

![image-20210611214057879](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210611214057879.png)

默认是关闭的，并保存最近15次的运行结果。

分析步骤：

1. 查看是否支持

2. 开启功能，默认是关闭的，使用前需要打开

   ```sql
   #开启profile
   set profiling = on
   ```

3. 运行sql

4. 查看结果

   ```sql
   #查看结果
   show profiles
   ```

5. 诊断SQL  ，show profile cpu,block io for query上一步前面的问题SQL的数字号码。

   ```sql
   #id为show profiles结果里面的sql的id。
   show profile cpu,block io for query id;
   ```

6. 日常开发需要注意的结论 。

   ![image-20210611215851971](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210611215851971.png)

### 全局查询日志

```sql
#命令
set global general_log = 1;
set global log_output = 'table';

#编写的sql语句，将会记录到mysql库里的general_log。可以使用命令查看：
select * from mysql.general_log;

```

![image-20210611220431266](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210611220431266.png)

**不要再生产环境开启这个功能**



### Mysql锁机制

mysql锁分类：

1. 对数据的操作类型分类（读/写锁）：

   读锁（共享锁）：针对同一份数据，多个操作可以同时进行而不会互相影响。

   写锁（排它锁）：当前写操作没有完成之前，他会阻断其他的写锁和读锁。

2. 从对数据操作的粒度：

   - 表锁（偏度）：

     ```sql
     #手动添加表锁
     lock table 表名1 read(write),表名2 read(write),....;
     
     #查看表是否添加锁
     show open tables
     
     #释放锁
     unlock tables;
     
     #查看表锁的状态
     show status like 'table%';
     ```

     ![image-20210612093608762](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612093608762.png)

     ![image-20210612093756002](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612093756002.png)

     ![image-20210612093921921](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612093921921.png)

     **如果加了read锁，一个会话只能进行查询加锁的表，无法查询其他的为加锁的表，也不能修改表数据，另一个会话如果要执行修改操作，此时会被阻塞，直到锁被释放。**

     **如果加了write锁，可以查询和修改自己表的数据，但是不能读或修改其他未加锁的表。**

     注意：**写锁只能加在一张表中**。

     ![image-20210612092543263](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612092543263.png)

     ​			**读锁会阻塞写，但不会堵塞读，而写锁则会把读和写都阻塞。**

     ​			**一个数据中只能给一个表加锁（读/写）！**

   - 行锁（偏写）：

     ```sql
     #查看档当前事务的隔离级别
     show variables like 'tx_isolation';
     
     #关闭自动提交事务
     set autocommit = 0;
     ```

     varchar类型不写''，会导致索引失效，行锁变表锁。

     **间隙锁**：

     ![image-20210612103221794](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612103221794.png)

     ![image-20210612103313530](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612103313530.png)

   - 页锁：

3. 如何锁定一行？

   ```sql
   begin;
   select *from emp where id = 1 for update;
   commit
   
   #查看行锁的状态信息
   show status like 'innodb_row_lock';
   ```

   ![image-20210612103859454](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612103859454.png)

   ![image-20210612104404402](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612104404402.png)



### 主从复制



**每个slave只有一个master，每个slave只能有一个唯一的服务器id，每个master可以有多个slave。**

注意：主机和从机的版本要一致。

主机配置：

```bash
#设置主机唯一id  *
server-id = 1

#启用二进制日志  例如：D:/Mysql/data/mysqlbin    *
log-bin = 自己本地路径/mysqlbin

#启用错误日志  例如：D:/Mysql/data/mysqlerr
log-err = D:/Mysql/data/mysqlerr

#根目录
bashdir = "D:/Mysql"
#临时目录
temdir = "D:/Mysql"

#数据目录
datadir = "D:/Mysql/data"
```

从机配置

```bash
#服务器唯一id   *
server-id = 2

#启用二进制日志
log-bin = 自己本地路径/mysqlbin
```

注意：**主机和从机都配置好之后，需要重启服务器。  关闭防火墙**



主机执行:

```bash
grant replication(复制) slave  on *.* to 'zhangsan'@'从机ip' identify by "密码"

#沙刷新权限
flush peivileges;

#查看master状态
show master status;
```

![image-20210612111530988](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612111530988.png)

从机执行：

```bash
change master to master_host = '主机ip',
master_user = 'zhangsan',
master_password = '密码',
master_log_file = 'mysqlbin.具体数字',
master_log_pos = '具体位置';


#启动从机
start slave;

#查看状态
show slave status\G; 

#停止复制功能
stop slave;
```



![image-20210612104708941](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612104708941.png)