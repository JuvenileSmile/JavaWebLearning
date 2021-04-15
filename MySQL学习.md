

## MySQL 学习

### 基础部分day01  简介

web页面<-----服务器<-------数据库

**MySQL**是数据库管理系统的一种。 (开源数据库)

数据的存储：数组，集合 （内存） 与  文件(硬盘)。硬盘的存储方式查询困难。

* **使用数据库的优势：**

  1.实现数据的持久化

  2.使用完整的管理系统统一管理，易于查询。

* 数据库的相关概念

  1. DB  数据库(database): 存储数据的仓库。保存了一系列有组织的数据(方便查询)
  2. DBMS 数据库管理系统(Database Management System). 数据库是通过DBMS创建和操作的容器。  MySQL即为其中的一种，其余还有Oracle，DB2，SqlServer  （增删查改四大作用）
  3. SQL  结构化查询语言（Structure Query Language）：专门用来与数据库通信的语言

* SQL 的优点;
  1. 不是特定DBMS的特定语言，具有通用性
  2. 简单易学
  3. 作用强大，可以进行复杂的高级数据库操作

#### 数据库存储数据的特点

1. 将数据放到表中，表再放到库中
2. 一个数据库中可以有多张表，每个表都有一个名字，用于标识，具有**唯一性**
3. 表具有一些特性，定义了数据在表中如何存储，类似于类的特性。
4. 表由列组成，也称为**字段**。所有的表都是由一个或多个列组成的，每一列都类似JAVA中的属性。
5. 表中的数据按行存储，每一行类似JAVA中的**对象**
6. 

#### MySQL 产品特点（属于Oracle公司）

* 优点：1. 开源免费
  			2. 性能高，执行很快

#### DBMS 分类

* 基于共享文件系统的DBMS（Access）
* 基于客户端——服务器(C-S)的DBMS  (MySQL,  Oracle,  SqlServer)

#### MySQL 服务的启动停止(登录与退出)

**方式一：**windows自带的命令行窗口

* 启动: net start mysql

* 停止:  net stop myqsl

* 登录：mysql -h 主机名 -P 端口号 -u 用户名  -p密码（p与密码间不可以用空格）

  mysql (-h localhost -P 3306) -u root  -p     password：root      (括号中的命令可有可无)     

* 退出：exit；

**方式二：**mysql自带的客户端（仅限root用户）



#### MySQL 常见命令介绍

* 查看MySQL版本：

  1. DOS 命令 mysql --version    或  mysql --V
  2. mysql命令：select version()；

* 查看当前所有的数据库:  show databases;

* 打开指定库;    use 库名

* 查看当前库的所有表：  show tables;

* 产看其他库的所有表： show tables form 库名；

* 创建表： 

  creat table 表名(

  列名 	类型，

   列名	类型，

  。。。

  );

* 查看表的结构： desc  表名;

#### MySQL语法规范

1. 不区分大小写，但是建议关键字大写，表名、列名小写

2. 每条命令最好用”  ； “ 结尾

3. 每条命令根据需要可以，缩进或换行     建议关键字大写，独占一行

4. 注释：

   ​		单行注释： # 注释文字

   ​		单行注释:    --  注释文字（注意：--与注释文字间必须要空格）

   ​		多行注释： /* 注释文字 */

#### MySQL图形化用户界面(SQLyog)

#### SQL 语言的细分：DQL语言（Data Query Language）（数据查询）， DML 语言（Data Manpulation Language）（增删改），DDL语言（Data Define Language）（数据定义，库和表定义），TCL语言（Transaction Control Language）（事务控制）



#### DQL语言学习（查询）（学习借助myemployee.sql 库）

##### 进阶1：基础查询
```sql
/*
语法：
selsect 查询列表 from 表名；

类似于System.out.println(打印的东西);

特点：

1. 查询的列表可以是：表中的字段、常量值、表达式、函数
2. 查询的结果是一个虚拟的表格
   */

打开数据库

USE myemployees;

#1. 查询表中单字段

SELECT last_name FROM  employees;

#2. 查询表中多个字段
SELECT last_name, salary, email FROM employees;

#3. 查询表中所有字段
SELECT 
  `first_name`,
  `last_name`,
  `email`,
  `phone_number`,
  `job_id`,
  `salary`,
  `manager_id`,
  `commission_pct`,
  `department_id`,
  `hiredate` 
FROM
  employees ;

  SELECT * FROM employees;

#4. 查询常量值
 SELECT 100;
 SELECT 'john';

#5. 查询表达式,四则运算合法符号
 SELECT 100 * 98;

#6. 查询函数(调用该函数，并获得返回值)

SELECT VERSION();

#7. 起别名
/*

1. 便于理解
2. 如果要查询的字段有重名的情况，使用别名可以区分
   */

#方式一：
SELECT 100%98 AS 结果;
SELECT last_name AS 姓, first_name AS 名 FROM employees;

#方式二：
SELECT last_name 姓, first_name 名 FROM employees;

#案例：查询salary 显示结果为 out put, 防止与关键字重复
SELECT salary AS "out put" FROM employees;


#8.去重
# 去重只能接一个字段，不能加两个，也不能连续使用，否则不规则表不合理
#案例：查询员工表中涉及到的所有部门编号
SELECT DISTINCT department_id FROM employees;

#9. +号的作用
/*
java中的+号

1. 运算符，两个操作数都是数值型
2. 连接符，只要有一个操作数为字符串

mysql中+号
仅仅只有一个功能：运算符

select 100+90; 两方都为数值型，则做加法运算
select '123' + 90; 其中一方为字符型，试图将字符型数值运算转换成数值型
			如果转换成功，则继续做加法运算
select 'john' + 90;	如果转换失败，则将字符型数值转换为0
select null+10; 	只要一方为null，结果肯定为null;
*/
#案例：查询员工名和姓连接成一个字段，并显示为姓名
SELECT 
  CONCAT(last_name, first_name) AS 姓名 
FROM
  employees;


#案例：显示出表employees的全部列，各个列之间用逗号链接，列表头显示out_put
#null 与任何字符链接，结果都是null
SELECT 
  IFNULL(commission_pct, 0) AS 奖金率,
  commission_pct 
FROM
  employees ;

SELECT 
  CONCAT(
    `first_name`,
    `last_name`,
    `job_id`,
    `salary`,
    IFNULL(commission_pct, 0)
  ) AS out_put 
FROM
  employees ;
  
# ISNULL()  判断某字段是否为null，是返回1，否则为0
```

#### 进阶二：条件查询

```sql
#进阶二：条件查询
/*

语法：
	select 
		查询列表
	from
		表明
	where
		筛选条件;
		
分类：
	一、按条件表达式筛选
	条件运算符：< > = != <>(不等于) <= >=
	二、按逻辑表达式筛选
	逻辑运算符：
	作用：链接条件表达式
		&&  ||  !
		and or not(推荐使用)
	三、模糊查询
		like
		between and
		in
		is null
*/
#一、按条件表达式筛选

#案例一、查询工作大于12000的员工信息
SELECT 
  * 
FROM
  employees 
WHERE salary > 12000 ;

#案例二、查询部门编号不等于90的员工名和部门编号
SELECT 
  last_name,
  department_id 
FROM
  employees 
WHERE department_id <> 90 ;


#二、按逻辑表达式筛选

#案例一、查询工资在10000-20000之间的员工名、工资及奖金
SELECT 
	last_name,
	salary,
	commission_pct
FROM
	employees
WHERE
	salary >= 10000 AND salary <= 20000;
	
#案例二：查询部门编号不是90到110之间的，或者工资高于15000的员工信息

SELECT
	*
FROM
	employees
WHERE
	(department_id < 90 OR department_id > 110) OR salary > 15000;
	
# 三、模糊查询
/*
like
特点：
1.一般和通配符搭配使用
	通配符：
	% 任意多个字符，包含0个字符
	_ 任意单个字符
between and
in
is null| is not null
*/
#一、like
#案例一、查询员工中名字包含字符a的员工信息
SELECT 
	* 
FROM
	employees

WHERE
	last_name LIKE '%a%';   # %代表通配符

#案例二、查询员工名字第三个字符为n，第五个字符为l的员工名和工资

SELECT 
	last_name,
	salary
FROM
	employees
WHERE
	last_name LIKE '__n_l%';
	
#案例三、查询员工名字中第二个字符为_的员工名(转义字符\)

SELECT 
	last_name
FROM
	employees
WHERE
	last_name LIKE '_$_%' ESCAPE '$';   #表明$为转义
	
#二、between and
/*
1.使用between and 可以提高语句简洁度
2.包含边界值
3.两个边界值不要调换顺序，小值and大值
*/



#案例一、查询员工编号在100到120之间的员工信息

SELECT 
	*
FROM
	employees
WHERE
	employee_id BETWEEN 100 AND 120;
	
#三、in
/*
含义：判断某字段的值是否属于in列表中的某一项
特点：
	1.使用in提高了语句简洁度
	2.in列表的值类型必须统一或兼容 '123' 123
	3.不支持通配符  
*/
#案例：查询员工的工种编号是 IT_PROG、AD_VP、AD_PRES中的一个的员工名和工种编号
SELECT 
	last_name,
	job_id
FROM
	employees
WHERE
	job_id IN ('IT_PROG','AD_VP','AD_PRES');
	
#4. is null
/*
=或<>不能用于判断null值
is null 或 is not null 可以判断null值
*/
#案例1. 查询没有奖金的员工名和奖金率  
SELECT 
	last_name,
	commission_pct
FROM
	employees
WHERE
	commission_pct IS NULL;


#安全等于 <=>
SELECT 
	last_name,
	commission_pct
FROM
	employees
WHERE
	commission_pct <=> NULL;
	
#案例二、查询工资为12000的员工信息
SELECT 
  * 
FROM
  employees 
WHERE salary <=> 12000 ;


# is null pk <=>
/*
is null 仅仅可以判断null值
<=> 既可以判断null值，也可以判断其他值。可读性低
*/
# 案例：查询员工号为176的员工的姓名和部门号和年薪
SELECT 
  last_name,
  department_id,
  salary * 12 * (1 + IFNULL(commission_pct,0)) AS 年薪 
FROM
  employees 
WHERE employee_id = 176 ;


```

## 基础部分day02 DQL查询操作

#### 排序查询

注意：selcet 查询多个字段 length() 要放在 * 之后

```sql
#进阶三：排序查询
/*
语法：
	select 查询列表
	from 表
	【where 筛选条件】
	order by 排序列表 【asc|desc】
特点：
	1. asc代表升序，desc代表降序
	不写默认是升序
	2. order by 子句支持单个字段，多个字段，表达式，函数，别名
	3. order by 子句一般是放在查询语句的最后面，但limit子句除外
*/

#案例：查询员工信息，按照工资从高到低排序；
SELECT * FROM employees ORDER BY salary DESC;

#案例2： 查询部门编号>=90的员工信息，按入职先后进行排序[添加筛选条件]
SELECT 
  * 
FROM
  employees 
WHERE department_id >= 90 
ORDER BY `hiredate` ASC ;

#案例3： 按年薪的高低显示员工的信息和年薪【按表达式排序】
SELECT 
  * , salary * 12 * (1 + IFNULL(commission_pct,0)) AS 年薪
FROM
  employees 
ORDER BY salary * 12 * (1 + IFNULL(commission_pct,0)) DESC ;


#案例4：按年薪的高低显示员工的信息和年薪【按别名排序】
SELECT 
  * , salary * 12 * (1 + IFNULL(commission_pct,0)) AS 年薪
FROM
  employees 
ORDER BY 年薪 DESC ;

#案例5：按姓名的长度显示员工的姓名和工资【按函数排序】
SELECT 
  LENGTH(last_name) 字节长度, last_name, salary 
FROM
  employees 
ORDER BY 字节长度 ;

#案例6：查询员工信息，先按工资排序，再按编号排序【按多个字段排序】
SELECT 
  * 
FROM
  employees 
ORDER BY salary ASC,
  employee_id DESC ;

# 测试1. 查询员工的姓名，部门号和年薪，按照年薪降序，姓名升序
SELECT 
  last_name,
  department_id,
  salary * 12 * (1 + IFNULL(commission_pct, 0)) AS 年薪 
FROM
  employees 
ORDER BY 年薪 DESC,
  last_name ASC ;

#测试2. 选择工资不在8000-17000的员工姓名和工资，按工资降序
SELECT 
  last_name,
  salary 
FROM
  employees 
WHERE salary NOT BETWEEN 8000 
  AND 17000 
ORDER BY salary DESC ;

#测试3. 查询邮箱包含e的员工信息，并按照邮箱的字节数降序，再按部门号升序
SELECT 
  * , LENGTH(email)
FROM
  employees 
WHERE email LIKE "%e%"
ORDER BY LENGTH(email) DESC,
  `department_id` ASC ;


```

#### 常见函数

功能：类似于java中的方法，将一组逻辑语句封装在方法体中，对外暴露方法名
好处：1. 隐藏了实现细节 2.提高了代码的重用性
调用：select 函数名(实参列表) 【from 表】;

**特点**： 1. 函数名

       2. 函数的功能

**分类**：
	1.单行函数
	如 concat(), length(), ifnull

 2. 分组函数

    

    功能：做统计使用，又称为统计函数，聚合函数，组函数

**单行函数分类：** 字符函数, 数学函数，日期函数，其他函数，流程控制函数

```sql
#进阶四：常见函数
/*
功能：类似于java中的方法，将一组逻辑语句封装在方法体中，对外暴露方法名
好处：1. 隐藏了实现细节 2.提高了代码的重用性
调用：select 函数名(实参列表) 【from 表】;

特点： 1. 函数名
       2. 函数的功能
       
分类：
	1.单行函数
	如 concat(), length(), ifnull
	2. 分组函数
	
	功能：做统计使用，又称为统计函数，聚合函数，组函数
	
**单行函数分类：** 字符函数, 数学函数，日期函数，其他函数，流程控制函数
常见单行函数
	字符函数：
	length，concat，substr，instr，trim，upper，lower，lpad，rpad，replace
	数学函数：
	round，ceil，floor，truncate，mod
	日期函数
	now，curdat，curtime，year，month，day，hour，minitue，second，str_to_date,date_form
	其他函数：
	version，database，user
	控制函数
	if, case
*/

#一、字符函数

#1.length  获取参数值的字节数
SELECT LENGTH('张三丰');
SHOW VARIABLES LIKE '%char%';

#2.concat() 拼接字符串

SELECT CONCAT(last_name, '_', first_name) FROM employees;

#3.upper、 lower
SELECT UPPER('john');  #大写
SELECT LOWER('joHn');

#示例：将姓大写，名小写，然后拼接
SELECT CONCAT(UPPER(last_name), LOWER(first_name)) FROM employees;

#4. substr、substring  截取字符串  
#注意：索引从开始
#截取从指定索引处后面的所有字符
SELECT SUBSTR('李莫愁爱上了陆展元', 7) out_put;
#截取从指定索引处指定长度字符长度的字符
SELECT SUBSTR('李莫愁爱上了陆展元', 1, 3) out_put;

#案例：姓名中首字母大写，其他字符小写用_拼接，显示
SELECT 
  CONCAT(
    UPPER(SUBSTR(last_name, 1, 1)),
    LOWER(SUBSTR(last_name, 2)),
    '_',
    LOWER(first_name)
  ) 
FROM
  employees ;

#5.instr  返回子串第一次出现的索引，如果没有则返回0
SELECT INSTR('杨不悔爱上了殷六侠', '殷六侠') AS out_put;


#6.trim 去前后空格或指定字符

SELECT LENGTH(TRIM('     张翠山     ')) AS out_put;


SELECT TRIM('a' FROM 'aaaaaaaaaa张翠山aaaaaaa张翠山aaaaaaaa') AS out_put;

#7.lpad 用指定的字符实现左填充指定长度，如果超过，则右截断

SELECT LPAD('殷素素', 10, '*') AS out_put;

#8.rpad 用指定的字符实现右填充指定长度

SELECT RPAD('殷素素', 10, '*') AS out_put;

#9. replace 替换

SELECT REPLACE('张无忌爱上了周芷若', '周芷若', '赵敏');



#二、数学函数

#1.rounf 四舍五入
SELECT ROUND(-1.45);
SELECT ROUND(1.567, 2);

#2.ceil 向上取整  返回>= 该参数的最小整数

SELECT CEIL(1.02);

#3.floor 向下取整  返回<= 该参数的最大整数

SELECT FLOOR(-9.99);

#4. truncate 截断

SELECT TRUNCATE(1.65,1);

#5. mod 取余
# mod(a,b)  a-a/b*b
SELECT MOD(10,3);

#三、日期函数
#now  返回当前系统的日期+时间
SELECT NOW();

#curdate 返回当前系统的日期，不包含时间
SELECT CURDATE();

#curtime 返回当前的时间，不包含日期
SELECT CURTIME();

#可以获得指定的部分，年、月、日day、小时hour、分钟minitue、秒
SELECT YEAR(NOW()) 年; 
SELECT YEAR('1998-1-1') 年 FROM employees;

SELECT YEAR(hiredata) 年 FROM empolyees;

SELECT MONTH(NOW()) 月;
SELECT MONTHNAME(NOW()) 月;

#str_to_date: 将日期格式的字符串转换成指定格式的日期
/*格式：
%Y   四位年份
%y   两位年份
%m   月份01，02，
%c   月份1，2
%d   日(01,02)
%H   小时(24)
%h   小时(12)
%i   分钟(00,01)
%s   秒(00,01)
*/
SELECT STR_TO_DATE('9-13-1999','%m-%d-%Y') AS out_put;

#查询入职日期为1992-4-3的员工信息
SELECT * FROM employees WHERE hiredate = '1992-4-3';

#date_format: 将日期转换成字符

SELECT DATE_FORMAT(NOW(), '%y年%m月%d日') AS out_put; 

#案例：查询有奖金员工的入职日期(XX月/XX日 XX年)
SELECT last_name, DATE_FORMAT(hiredate, '%m月/%d日 %y年') FROM employees;


#四、其他函数

SELECT VERSION();  #版本
SELECT DATABASE(); #查看当前库
SELECT USER();
SELECT PASSWORD('sss');  #返回加密

#五、流程控制函数
#1. if函数：if else 效果

SELECT IF(10>5, '大', '小');

SELECT last_name, commission_pct, IF(commission_pct IS NULL, '没奖金，呵呵', '有奖金，哈哈') 备注 
FROM employees;


#2. cases函数的使用一：switch case 的效果

/*
switch(变量表达式){
	case 常量1：语句1; break;
	...
	default: 语句n; break;
}


mysql 中

case 要判断的字段或表达式
when 常量1 then 要显示值1或语句1;
when 常量2 then 要显示值1或语句2;
...
else 要显示的值n或语句n;
end
*/


/*
案例：查询员工的工资，要求


部门号=30， 显示工资为工资的1.1倍
部门号=40，显示工资为1.2倍
部门号=50，显示工资的1.3倍
其他部门，显示原工资
*/

SELECT salary 原始工资, department_id,

#相当于表达式用
CASE department_id
WHEN 30 THEN salary*1.1
WHEN 40 THEN salary*1.2
WHEN 50 THEN salary*1.3
ELSE salary
END AS 新工资
FROM employees;

#3. case函数的使用二：类似多重if
/*
case
when 条件1 then 要显示的值1 或 语句1;
when 条件2 then 要显示的值2 
。。。
else 要显示的值n
end
*/

#案例：查询员工的工资情况
/*
如果工资>20000 显示A级别
如果工资>15000 显示B级别
如果工资>10000 显示C级别
否则，显示D
*/

SELECT salary,
CASE
WHEN salary > 20000 THEN 'A'
WHEN salary > 15000 THEN 'B'
WHEN salary > 10000 THEN 'C'
ELSE 'D'
END AS 工资等级
FROM employees;

#题目
#1. 显示系统时间(日期+时间)
SELECT NOW();

#2. 查询员工号，姓名，工资，以及工资提高百分之20后的结果(new salary)
SELECT 
  employee_id,
  last_name,
  salary,
  salary * 1.2 AS 'new salary' 
FROM
  employees ;

#3. 将员工的姓名按首字母排序，并写出姓名的长度（length）
SELECT last_name, LENGTH(last_name) AS 姓名长度 FROM employees ORDER BY SUBSTR(last_name,1,1) ASC;

```

#### 分组函数

```sql
#二、分组函数
/*
功能：用作统计使用，又称为聚合函数或哦统计函数或组函数

分类
sum 求和、 avg 平均值、 max最大值、min最小值、 count计算个数

特点：
1.sum、avg一般处理数值型
max，min，cout可以处理任意类型
2.以上分组函数都忽略null
3.可以和distinct搭配实现去重的运算
4.count函数
一般使用count(*)统计行数
5.和分组函数一同查询的字段要求是group by后的字段

*/

#1. 简单 的使用
SELECT SUM(salary) FROM employees;
SELECT AVG(salary) FROM employees;
SELECT MIN(salary) FROM employees;
SELECT MAX(salary) FROM employees;
SELECT COUNT(salary) FROM employees;

SELECT SUM(salary) 和, MAX(salary) 最大, MIN(salary) 最小 FROM employees;

#2. 参数支持哪些类型

#sum avg 一般只支持数值型

#max min 支持数值型，字符型，日期型

#count 计数非空值的个数，null计为0

#3.忽略null
SELECT SUM(commission_pct), AVG(commission_pct) FROM employees;

#4.和distinct搭配

SELECT SUM(DISTINCT salary) FROM employees;   #去重后求和
SELECT COUNT(DISTINCT salary) FROM employees;  #计算几种工资



#5.count函数的详细介绍

SELECT COUNT(salary) FROM employees;

SELECT COUNT(*) FROM employees;  #查询总行数

SELECT COUNT(1) FROM employees;  #统计1的个数，为整个表加一个1 列，然后统计，相当于统计行数

#效率：
/*myisam 存储引擎下  count(*) 效率最高
innodb 存储引擎下  count(*) 和 count(1)效率差不多，比 count(字段)高一些*/


#6. 和分组函数一同查询的字段有限制

SELECT AVG(salary), employee_id FROM employees;


#测试：查询员工表中最大入职日期与最小入职日期相差天数

SELECT DATEDIFF(MAX(hiredate),MIN(hiredate)) DIFFRENCE 
FROM employees;
```

**分组查询**

```sql
#进阶5：分组查询

/*
语法：
	select 分组函数, 列(要求出现在group by的后面)
	from 表
	【where 筛选条件】
	group by 分组的列表
	【order by 子句】
注意：	查询列表必须特殊，要求是分组函数和group by后出现的字段

特点：
	1.分组查询中的筛选条件分为两类
			数据源			位置				关键字
	分组前筛选	原始表			group by 子句的前面		where
	分组后筛选	分组后的结果集		group by 子句的后面		having
	
	分组函数做条件肯定放在having子句中
	能用分组前筛选的，就有限考虑使用分组前筛选
	2.group by 语句支持单个字段分组，多字段分组（多个字段间用逗号隔开没有顺序要求），表达式或函数
	3.排序也可以添加排序（排序放在整个排序的最后面）
*/
#案例1：查询每个工种的最高工资

SELECT MAX(salary), job_id
FROM employees
GROUP BY job_id;

#案例2：查询每个位置上的部门个数
SELECT COUNT(*), location_id
FROM departments
GROUP BY location_id;

#添加分组前筛选条件
#案例1. 查询邮箱中包含a字符的，每个部门的平均工资

SELECT AVG(salary), department_id
FROM employees
WHERE email LIKE '%a%'
GROUP BY department_id;


#案例2: 查询有奖金的每个领导手下员工的最高工资
SELECT MAX(salary), manager_id
FROM employees
WHERE commission_pct IS NOT NULL
GROUP BY manager_id;

#添加分组后的筛选条件(Having)
#案例1：查询那个部门的员工个数>2

#1.查询每个部门的员工个数
SELECT COUNT(*) department_id
FROM employees
GROUP BY department_id;

#2.根据1的结果进行筛选，查询哪个部门的员工个数大于2
SELECT COUNT(*) department_id
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 2;


#案例二：查询每个工种有奖金的员工的最高工资>12000的工种编号和工资

SELECT MAX(salary), job_id
FROM employees
WHERE commission_pct IS NOT NULL
GROUP BY job_id
HAVING MAX(salary) > 12000;

#案例三：查询领导编号>102的每个领导手下的最低工资>5000的领导编号是哪个，以及其最低工资

SELECT MIN(salary), manager_id
FROM employees
WHERE manager_id > 102
GROUP BY manager_id
HAVING MIN(salary) > 5000;

#按表达式或函数分组

#案例：按员工姓名的长度分组，查询每一组的员工个数，筛选员工个数>5的有哪些？

SELECT COUNT(*) AS c,LENGTH(last_name) AS len
FROM employees
GROUP BY len
HAVING c > 5;


#按多个字段分组

#案例：查询每个部门每个工种的员工的平均工资

SELECT AVG(salary), department_id, job_id
FROM employees
GROUP BY department_id, job_id;


#添加排序
#案例：查询每个部门每个工种的员工的平均工资，并按平均工资高低显示
SELECT AVG(salary), department_id, job_id
FROM employees
GROUP BY department_id, job_id
HAVING AVG(salary) > 10000
ORDER BY AVG(salary) DESC;


#作业

#1. 查询各job_id的员工工资的最大值，最小值，平均值，总和，并按job_id升序

SELECT MAX(salary), MIN(salary), AVG(salary), SUM(salary), job_id
FROM employees
GROUP BY job_id
ORDER BY job_id DESC;
```

**连接查询**

```sql
#进阶六：连接查询
/*
含义：又称多表查询，当查询的字段涉及多个表

笛卡尔乘积现象：表1 有m行，表2有n行，结果m*n行

发生原因：没有有效的连接条件


分类：
	按年代分类：
	sql92标准：仅仅支持内连接
	sql99标准【推荐】：支持内连接+外连接（左外和右外）+交叉连接
	
	按功能分类：
		内连接：
			等值连接
			非等值连接
			自连接
		外连接：
			左外连接
			右外连接
			全外连接
		交叉连接
*/

SELECT NAME, boyName FROM boys, beauty
WHERE beauty.`boyfriend_id` = boys.id;

#一、sql92标准
#1.等值连接
/*
1.多表连接的结果为多表的交集部分
2.n表连接，至少需要n-1个连接条件
3.多表的顺序没有要求
4.一般需要为表起别名
5.可以搭配前面介绍的所有子句使用
*/

#案例1：查询对应的女神和男神名
SELECT NAME,boyName 
FROM boys, beauty 
WHERE beauty.`boyfriend_id` = boys.id ;


#案例2：查询员工名和对应的部门名
USE myemployees
SELECT last_name, department_name
FROM employees,departments
WHERE employees.department_id = departments.department_id;


#2. 为表起别名
/*
1.提高语句的简洁度
2.区分多个重名的字段

注意：如果为表起了别名，则查询字段就不能使用原来的表名去限定
*/
#查询员工名、工种号、工种名
SELECT last_name, e.job_id, job_title
FROM employees AS e, jobs AS j
WHERE e.job_id = j.`job_id`;

#3.两个表的顺序可以调换


#4.可以加筛选

#案例：查询有奖金的员工名、部门名
SELECT last_name, department_name,commission_pct

FROM employees e, departments d
WHERE e.`department_id` = d.`department_id`
AND e.commission_pct IS NOT NULL;

#案例二：查询城市名中第二个字符为o的部门名和城市
SELECT department_name, city
FROM departments d, locations l
WHERE d.`location_id` = l.`location_id`
AND city LIKE '_o%';


#5. 加分组

#案例1：查询每个城市的部门个数
SELECT COUNT(*) 个数, city
FROM departments d, locations l
WHERE d.`location_id` = l.`location_id`
GROUP BY city;

#案例2：查询有奖金的每个部门的部门名和部门的领导编号和该部门的最低工资

SELECT `department_name`, d.manager_id, MIN(salary)
FROM employees e, departments d
WHERE d.`department_id` = e.`department_id`
AND commission_pct IS NOT NULL
GROUP BY department_name, d.manager_id;

#6.加排序

#案例：查询每个工种的工种名和员工个数，并按员工个数降序
SELECT job_title, COUNT(*)
FROM jobs j, employees e
WHERE j.`job_id` = e.`job_id`
GROUP BY job_title
ORDER BY COUNT(*) DESC;

#7.三表连接

#案例 查询员工名、部门名、和所在的城市
SELECT last_name,department_name,city
FROM employees e, departments d, locations l
WHERE d.`location_id` = l.`location_id`
AND e.`department_id` = d.`department_id`
AND city LIKE 's%'

ORDER BY department_name;


#2.非等值连接

#案例：查询员工的工资和工资级别
CREATE TABLE job_grades
(grade_level VARCHAR(3),
lowest_sal INT,
highest_sal INT);

INSERT INTO job_grades
VALUE ('A', 1000, 2999);

INSERT INTO job_grades
VALUE ('B', 3000, 5999);

INSERT INTO job_grades
VALUE ('C', 6000, 9999);

INSERT INTO job_grades
VALUE ('D', 10000, 14999);

INSERT INTO job_grades
VALUE ('E', 15000, 24999);

INSERT INTO job_grades
VALUE ('F', 25000, 40000);


SELECT salary, grade_level
FROM employees e, job_grades g
WHERE salary BETWEEN g.`lowest_sal` AND g.`highest_sal`
AND g.`grade_level` = 'A';

#3.自连接

#案例：查询 员工名和上级的名称
SELECT e.employee_id, e.last_name, m.employee_id, m.`last_name`
FROM employees e, employees m
WHERE e.`manager_id` = m.`employee_id`;

```

#### 连接查询（sql99语法）

```sql
#二、sql99语法
/*
语法
	select 查询列表
	from  表1 别名 【连接类型】
	join  表2 别名
	on  连接条件
	【where 筛选条件】
	【group by 分组语句】
	【having 筛选条件】
	【order by 排序列表】
	
内连接：inner
外连接
	左外: left 【outer】
	右外：right 【outer】
	全外：full   【outer】
交叉连接: cross
*/


#一）内连接
/*
语法
select 查询列表
from 表1  别名
inner join 表2 别名
on 连接条件；

分类：
等值
非等值
自连接

特点
1.添加排序、分组、筛选
2.inner可以省略
3.筛选条件放在where后。连接条件放在on后面，提高了分离性，便于阅读
4.inner join 连接和sql92语法中的作用相同，查询多表交集
*/


#1.等值连接

#案例1. 查询员工名，部门名

SELECT last_name, department_name
FROM employees e
INNER JOIN departments d
ON e.`department_id` = d.`department_id`;

#案例2.拆线名字中包含e的员工名和工种名 （添加筛选）
SELECT last_name, job_title
FROM employees e
INNER JOIN jobs j
ON e.`job_id` = j.`job_id`
WHERE last_name LIKE '%e%';

#案例3.查询部门个数 > 3的城市名和部门个数 （添加分组+筛选）
SELECT city, COUNT(*) 部门个数
FROM departments d
INNER JOIN locations l
ON l.`location_id` = d.`location_id`
GROUP BY city
HAVING COUNT(*) > 3;

#案例4.查询部门的员工个数>3 的部门名和员工个数，并按个数降序(添加排序)
SELECT department_name, COUNT(*) 员工个数
FROM departments d
INNER JOIN employees e
ON d.`department_id` = e.`department_id`
GROUP BY department_name
HAVING COUNT(*) > 3
ORDER BY 员工个数;

#案例5.查询员工名、部门名、工种名、并按部门名降序（三表连接）
SELECT last_name, department_name, job_title
FROM employees e
INNER JOIN departments d ON e.`department_id` = d.`department_id`
INNER JOIN jobs j ON e.`job_id` = j.`job_id`
ORDER BY department_name DESC;

#二）非等值连接

#查询员工工资级别
SELECT salary, grade_level
FROM employees e
INNER JOIN job_grades g
ON e.`salary` BETWEEN g.`lowest_sal` AND g.`highest_sal`;

#查询工资级别的个数，并按工资级别降序
SELECT COUNT(*), grade_level
FROM employees e
INNER JOIN job_grades j
ON e.`salary` BETWEEN j.`lowest_sal` AND j.`highest_sal`
GROUP BY grade_level
ORDER BY grade_level DESC;

#三）自连接
#查询员工名字和上级的名字
SELECT e.last_name, m.last_name
FROM employees e
INNER JOIN employees m
ON e.`manager_id` = m.`employee_id`;


#二、外连接
/*
应用场景：查询一个表中有，另一个表中没有的记录

特点：
1.外连接的查询结果为主表中所有记录
	如果从表中有和他匹配的，则显示匹配的值
	如果从表中没有和他匹配的，则显示null
	外连接查询结果 = 内连接结果 + 主表中有而从表没有的记录

2.左外连接，left join左边的是主表
  右外连接，right join右边的是主表
  
3.交换两个表的顺序，可以实现同样的效果
4.全外连接=内连接结果+表1中有但表2没有的+表2有但表1没有的
	
*/


#引入：查询男票不在男神名里的女神名
#左外连接
SELECT b.name, bo.*
FROM beauty b
LEFT OUTER JOIN boys bo
ON b.`boyfriend_id` = bo.`id`
WHERE bo.`id`  IS NULL;  #用带钥匙的主键判断，主键一定不为空


#案例1. 查询哪个部门没有员工
SELECT d.*, e.employee_id
FROM departments d
LEFT OUTER JOIN employees e
ON d.`department_id` = e.`department_id`
WHERE e.`employee_id` IS NULL;


#全外

/*
use girls;
select b.*, bo.*
from beauty b
full outer join boys bo
on b.id is null
*/


#交叉连接,  笛卡尔乘积

SELECT b.*,bo.*
FROM beauty b 
CROSS JOIN boys bo;

#作业
#作业1. 查询哪个城市没有部门
SELECT d.department_name, l.city
FROM departments d
RIGHT JOIN locations l
ON d.`location_id` = l.`location_id`
WHERE department_name IS NULL;
```

#### 子查询

```sql
#进阶七：子查询
/*
含义：
出现在其他语句中的select语句，称为子查询或内查询
外部的查询语句，称为主查询或外查询


分类：
按子查询出现的位置：
	select后面：
		仅仅支持标量子查询
	from后面：
		支持表子查询
	where或having后面：
		标量子查询(单行)
		列子查询（多行）
		行子查询
	exists后面(相关子查询)
		表子查询
		
按结果集的行列数不同：
	标量子查询（结果集只有一行一列）
	列子查询（结果集一列多行）
	行子查询（结果集一行多列）
	表子查询（结果集一般为多行多列）
*/

#一、where或者having后
#1.标量子查询（单行子查询）
#2.列子查询（多行子查询）

#3.行子查询（多列多行）

/*
特点：
1.子查询小括号内
2.子查询一般放在条件的右侧
3.标量子查询，一般搭配着单行操作符使用 < > >= <= <>

列子查询，一般搭配多行操作符使用
in,  any/some, all

4.子查询的执行优先于主查询执行，主查询的条件用到了子查询的结果
*/


#1.标量子查询

#案例1. 谁的工资比Abel高

SELECT *
FROM employees
WHERE salary > (
	SELECT salary 
	FROM employees
	WHERE last_name = 'Abel'
);

#案例2：返回job_id与141号员工相同，salary比143号员工多的员工 姓名，job_id和工资
SELECT last_name, job_id, salary
FROM employees
WHERE salary > (
	SELECT salary
	FROM employees
	WHERE employee_id = 143
) AND  job_id = (
	SELECT job_id
	FROM employees
	WHERE employee_id = 141
);

#案例3： 返回公司工资最少的员工的last_name, job_id和salary
SELECT last_name, job_id, salary
FROM employees
WHERE salary = (
	SELECT MIN(salary)
	FROM employees
);


#案例4.查询最低工资大于50号部门最低工资的部门id和其最低工资
SELECT department_id, MIN(salary)
FROM employees
GROUP BY department_id
HAVING MIN(salary) >(
	SELECT MIN(salary)
	FROM employees
	WHERE department_id = 50
);

#非法使用标量子查询
#查询结果不是一行一列



#2.列子查询（多行子查询）
/*
多行操作符
IN/NOT IN  等于列表中的任意一个
ANY|SOME   和子查询返回某一个比较  可替换
ALL 	   和子查询返回所有值比较
*/


#案例1.：返回location_id 是 1400 或 1700 的部门中所有员工的姓名
SELECT last_name
FROM employees
WHERE department_id IN (
	SELECT department_id
	FROM departments
	WHERE location_id IN (1400,1700)
);


#案例2：返回其他部门中比job_id 为 IT_PROG 部门任一工资低的员工的：工号、姓名、job_id、salary
SELECT last_name, job_id, salary
FROM employees
WHERE salary < ANY (
	SELECT DISTINCT salary
	FROM employees
	WHERE job_id = 'IT_PROG'
) AND job_id <> 'IT_PROG';

#案例3.返回其他部门中比job_id 为 IT_PROG 部门所有工资低的员工的：工号、姓名、job_id、salary

SELECT last_name, job_id, salary
FROM employees
WHERE salary < ALL (
	SELECT DISTINCT salary
	FROM employees
	WHERE job_id = 'IT_PROG'
) AND job_id <> 'IT_PROG';


#3. 行子查询（结果一行多列或多行多列）

#案例：查询员工编号最小的员工编号并且工资最高的员工信息
SELECT *
FROM employees
WHERE employee_id = (
	SELECT MIN(employee_id)
	FROM employees
) AND salary = (
	SELECT MAX(salary)
	FROM employees
);

#行子查询
#两个筛选条件都是用相同的符号
SELECT *
FROM employees
WHERE (employee_id, salary) = (
	SELECT MIN(employee_id), MAX(salary)
	FROM employees
)

#二、select后面
/*
仅仅支持标量子查询
*/

#案例：查询每个部门的员工个数
SELECT d.*, (
	SELECT COUNT(*)
	FROM employees e
	WHERE e.department_id = d.department_id
)个数

FROM departments d;

#案例2：查询员工号=102的部门名

SELECT (
	SELECT department_name 
	FROM departments d
	INNER JOIN employees e
	ON d.department_id = e.department_id
	WHERE e.employee_id = 102
) 部门名;


#三、from后面
/*
将子查询结果充当一张表，要求必须起别名
*/

#案例：查询每个部门的平均工资的工资等级

SELECT ag_dep.*, g.grade_level
FROM (
	SELECT AVG(salary) ag, department_id
	FROM employees
	GROUP BY department_id
) ag_dep
INNER JOIN job_grades g
ON ag_dep.ag BETWEEN g.lowest_sal AND g.highest_sal;



#四、exists后面（相关子查询）
/*
语法：
exists（完整的查询语句）
结果：
1或0
*/

SELECT EXISTS(SELECT employee_id FROM employees WHERE salary = 30000)

#案例1.查询有员工名的部门名
SELECT department_name
FROM departments d
WHERE d.department_id IN(
	SELECT department_id
	FROM employees
)



SELECT department_name, 
FROM departments  AS d
WHERE EXISTS(
	SELECT *
	FROM employees  AS e
	WHERE d.department_id = e.department_id
);

#案例2： 查询没有女朋友的男神信息
USE girls;

#in
SELECT bo.*
FROM boys bo
WHERE bo.id NOT IN (
	SELECT boyfriend_id
	FROM beauty
)

#exists
SELECT bo.*
FROM boys bo
WHERE NOT EXISTS(
	SELECT boyfriend_id
	FROM beauty b 
	WHERE bo.`id` = b.`boyfriend_id`
)


```



#### 分页查询

```sql
#进阶8：分页查询

/*
应用场景：当要显示的数，一页显示不全，需要分页提交sql请求

语法：
	select 查询列表
	from 表
	【join type】 join 表2
	on 连接条件
	【where 筛选条件】
	【group by 分组字段】
	【order by 排序字段】
	limit offset, size;
	
	offset 要显示条目的起始索引（起始索引从0开始）
	size（要显示条目个数）

特点：
	1.limit语句放在查询语句的最后
	2.公式
	要显示的页数 page， 每一页条目数size
	
	select 查询列表
	from 表
	limit (page-1)*size, size;
*/

#案例1：查询前五条员工信息

SELECT * FROM employees LIMIT 0, 5;
SELECT * FROM employees LIMIT  5;

#案例2：查询第11到第25条
SELECT * FROM employees LIMIT 10, 15;

#案例3: 有奖金的员工信息，并且工资较高的前10名
SELECT *
FROM employees e
WHERE e.`commission_pct` IS NOT NULL
ORDER BY salary DESC
LIMIT 10;
```

#### 联合查询 uinon

```sql
#进阶9：union联合查询

/*
union 联合 合并：将多条查询语句的结果合并成一个结果

语法：
查询语句1
union
查询语句2
union
...

应用场景：
要查询的结果来自于多个表，且多个表没有直接的连接关系，但查询的信息一致


特点：
1.要求多条查询语句的查询列数一致
2.要求多条查询语句的查询每一列类型和顺序最好一致
3.union关键字默认去重，如果使用union all 可以包含重复项
*/

#引入：查询部门编号大于90或邮箱包含a的员工信息
SELECT * FROM employees WHERE  email LIKE '%a%' OR department_id > 90;

SELECT * FROM employees WHERE  email LIKE '%a%' 
UNION 
SELECT * FROM employees WHERE department_id > 90;
```

#### DML语言（数据操作语言） 增删改

```sql
#DML语言

/*
数据操作语言

插入：insert
修改：update
删除：delete

*/

#一、插入语句
#方式一：经典插入方式
/*
语法：
insert into 表名(列名, ....) values(值1,....);

表名
列名
新值

*/

USE girls;

#1.插入值的类型要与列的类型一致或兼容
INSERT INTO beauty(id,NAME,sex,borndate,phone,photo,boyfriend_id)
VALUES(13,'唐艺昕', '女','1990-4-23','18988888888',NULL,2);

SELECT * FROM beauty;

#2.不可以为null的列必须插入值，可以为null的列如何插入值
#方式一、
INSERT INTO beauty(id,NAME,sex,borndate,phone,photo,boyfriend_id)
VALUES(13,'唐艺昕', '女','1990-4-23','18988888888',NULL,2);
#方式二、不写null，也不写该列
INSERT INTO beauty(id,NAME,sex,borndate,phone,boyfriend_id)
VALUES(14,'金星', '女','1990-4-23','13988888888',9);

SELECT * FROM beauty;

#3.列的顺序是可以调换的
INSERT INTO beauty(NAME,sex,id,phone)
VALUES('蒋欣', '女', 16, '110');


#4.列数和值的个数必须一致

INSERT INTO beauty(NAME,sex,id,phone,boyfriend_id)
VALUES('关晓彤', '女', 16, '110',NULL);

#5.可以省略列表，默认是所有列，而且列的顺序和表的顺序一致
INSERT INTO beauty
VALUES(18, '张飞', '男', NULL, '119', NULL,NULL);


#方式二：
/*
语法：
insert into 表名
set 列名=值，列名=值，.....

*/

INSERT INTO beauty
SET id = 19, NAME = '刘涛', phone = '999'; 


#两种方式对比


# 1.方式一支持插入多行, 但是方式二不支持
INSERT INTO beauty
VALUES()
,VALUES()
,VALUES()


#2.方式一支持子查询，方式二不支持
INSERT INTO beauty(id,NAME,phone)
SELECT 26,'宋茜','11809866';

#二、修改语句

/*
1.修改单表中的记录 【核心】

语法：
update 表名
set 列 = 新值， 列 = 新值....
where 筛选条件;


2.修改多表的记录【补充】

语法：

sql92
update 表1 别名, 表2
set 列 = 值,...
where 筛选条件
and 筛选条件


sql99语法
update 表1 别名
inner|left|right|  join 表2 别名
on 连接条件
set 列 = 值,....
where 筛选条件;
*/


#1.修改单表的记录
#案例1：修改beauty表中姓唐的女神的电话未1389999999

UPDATE beauty SET phone = '13899138'
WHERE NAME LIKE '唐%';

#案例2：修改boys表中的id为2的名称为张飞，魅力值为10
UPDATE boys SET boyName = '张飞', usercp = 10
WHERE id = 2; 


#2.修改多表的记录

#案例1：修改张无忌的女朋友的手机号为114

UPDATE boys bo
INNER JOIN beauty b 
ON bo.id = b.`boyfriend_id`
SET b.`phone` = '114'
WHERE bo.`boyName` = '张无忌';

SELECT * FROM beauty


#案例2：修改没有男朋友的女神的男朋友编号都为2号
UPDATE beauty b
LEFT OUTER JOIN boys bo
ON bo.id = b.boyfriend_id
SET b.boyfriend_id = 2
WHERE bo.id IS NULL;

SELECT *
FROM beauty b
LEFT OUTER JOIN boys bo
ON bo.id = b.boyfriend_id

SELECT * FROM boys
SELECT * FROM beauty

#三、删除语句
/*
方式一、delete

语法：
1.单表的删除【重点】
delete from 表名 where 筛选条件

2.多表的删除【补充】

sql92 
delete 表1别名，表2别名
from 表1 别名，表2 别名
where 连接条件
and 筛选条件

sql99

delete 表1别名，表2别名 
from 表1 别名
inner|left|right join 表2 别名
on 连接条件
where 筛选条件;

方式二：truncate
语法： truncate table 表名;
*/


#方式一;delete
#1.单表的删除
#案例1：删除手机号以9结尾的女神信息

DELETE FROM beauty WHERE phone LIKE '%88';
SELECT * FROM beauty

#2.多表的删除
#案例：删除账务的女友的信息
DELETE b
FROM beauty b 
INNER JOIN boys bo
ON b.boyfriend_id = bo.id
WHERE bo.boyName = '张无忌';



#案例： 删除黄晓明的信息，及它女朋友的信息

DELETE b,bo
FROM beauty b
INNER JOIN boys bo
ON b.`boyfriend_id` = bo.`id`
WHERE bo.`boyName` = '黄晓明';
SELECT * FROM beauty
SELECT * FROM boys


#方式二：truncate语句  清空表
#案例：将魅力值大于100的男神信息删除
TRUNCATE TABLE boys;

#两种删除方法对比

/*
1.delete可以加where条件，truncate不能加
2.truncate删除，效率稍微高一些
3.加入要删除的表中有自增长列，如果用delete删除后，再插入数据，自增长列的值从断点开始
而truncate删除后，再插入数据，自增长列值从1开始
4.truncate删除没有返回值，delete删除有返回值

5.truncate删除不能回滚，delete删除可以回滚。
*/




```

#### DDL语言（库和表的管理）

```sql
#DDL语言

/*
数据定义语言

库和表的管理

一、库的管理
创建、修改、删除

二、表的管理
创建、修改、删除


创建：create
修改：alter
删除：drop
*/



#一、库的管理
#库的建立


/*
语法：

Create dayabase [IF NOT EXISTS] 库名;
*/

#案例：创建库books
CREATE DATABASE IF NOT EXISTS books;


#2.库的修改


#更改库的字符集

ALTER DATABASE books CHARACTER SET gbk;

#3.库的删除

DROP DATABASE IF EXISTS books;


#二、表的管理
#1.表的创建 （重点）

/*
语法：

create table 表名（
	列名 列的类型 【（长度） 约束】，
	列名 列的类型 【（长度） 约束】，
	列名 列的类型 【（长度） 约束】，
	......
	列名 列的类型 【（长度） 约束】

）

*/

#案例：创建表book

CREATE TABLE book(
	id INT, #编号
	bName VARCHAR(20), #图书名
	price DOUBLE, #价格
	authorId INT, #作者
	publishDate DATETIME #出版日期
);

SELECT * FROM book;

DESC book;

#案例：创建表author
CREATE TABLE author(
	id INT,
	au_name VARCHAR(20),
	nation VARCHAR(10)
);


#2.表的修改
/*

alter table 表名 add|drop|modify|change column
*/

#(1) 修改列名

ALTER TABLE book CHANGE COLUMN publishDate pubDate DATETIME;
DESC book

#(2) 修改列的类型或约束

ALTER TABLE book MODIFY COLUMN pubDate TIMESTAMP;

#(3) 添加新列

ALTER TABLE author ADD COLUMN annual DOUBLE;
DESC author

#(4) 删除列

ALTER TABLE author DROP COLUMN annual;


#(5) 修改表名

ALTER TABLE author RENAME TO book_author;


#3.表的删除

DROP TABLE IF EXISTS book_author;

SHOW TABLES;

#通用的写法：

DROP DATABASE IF EXISTS  旧库名;
CREATE DATABASE 新库名;

DROP TABLE IF EXISTS 旧表名;
CREATE TABLE 表名();



#4.表的复制

INSERT INTO author VALUES
(1,'村上春树','日本'),
(1,'莫言','中国'),
(1,'冯唐','中国'),
(1,'金庸','中国');


#1.仅仅复制表的结构

CREATE TABLE copy LIKE author;

#2.复制表的结构+数据
CREATE TABLE copy2
SELECT * FROM author;

#只复制部分数据
CREATE TABLE copy3
SELECT id,au_name
FROM author 
WHERE nation = '中国';

#仅仅复制某些字段

CREATE TABLE copy4
SELECT id,au_name
FROM author
WHERE 1=2;  #写一个不成立的条件，只复制部分字段


```

#### 常见的数据类型

```sql
#常见的数据类型
/*
数值型：
	整形
	小数：
		定点数
		浮点数
字符型：
	较短的文本：char，varchar
	较长的文本：text、blob（较长的二进制数据）

日期型: 
	
*/

#一、整形：
/*
分类：
Tinyint(1)、 Smallint(2)、 Mediumint(3)、Int(4)、Bigint(8); 括号内表示类型所占字节

特点：
(1)如果不设置无符号还是有符号，默认无符号，如果想设置无符号，需要添加unsigned关键字
(2)如果超出了整型的范围，会报一场，并且插入临界值
(3)如果不设置长度，会有默认的长度

长度代表了显示的最大宽度，如果不够会用0左边填充，但必须搭配zerofill关键字
*/

#1.如何设置无符号和有符号
DROP TABLE IF EXISTS tab_int;
CREATE TABLE tab_int(
	t1 INT,
	t2 INT UNSIGNED
);

DESC tab_int;

INSERT INTO tab_int VALUES(-123,0);
SELECT * FROM tab_int;

#二、小数
/*
分类：
1. 浮点型：float(M,D)  double(M,D)
2. 定点型：DEC(M,D) decimal(M,D)

特点：
(1) M代表整数部位外加小数部位，D代表小数部位，如果超出范围，则插入临界值
(2)M和D都可以省略 如果是decimal，则M默认10，D默认0，double和float会根据插入数据的大小变化

(3)定点型的精度较高，如果要求插入数值的精度较高如果货币运算，优先使用
*/

CREATE TABLE tab_float(
	f1 FLOAT(5,2),
	f2 DOUBLE(5,2),
	f3 DECIMAL(5,2)

);

INSERT INTO tab_float VALUES(123.45,123.45,123.45);
INSERT INTO tab_float VALUES(123.456,123.456,123.456);
INSERT INTO tab_float VALUES(123.4,123.4,123.4);

#原则：
/*
所选择的类型越简单越好
*/

#三、字符型
/*
较短的文本：
char
carchar
其他： binary和varbinary 保存较短的二进制
enum 保存枚举
set保存集合

特点：
	写法	  	  M的意思			   特点		   空间的耗费      效率
char	char(M)	    最大字符数可以省略，默认1    	固定长度的字符      比较耗费       高   
	
varchar varchar(M)   最大的字符数 ，不可省略  		可变长的字符	    比较节省       低


较长的文本：
text
blob（较大的二进制）

*/

#枚举类型
CREATE TABLE tab_char(
	c1 ENUM('a','b','c')
);

INSERT INTO tab_char VALUES('a');
INSERT INTO tab_char VALUES('b');
INSERT INTO tab_char VALUES('m');  #插入失败
INSERT INTO tab_char VALUES('A');

SELECT * FROM tab_char;


#集合类型Set
CREATE TABLE tab_set(
	s1 SET('a','b','c','d')
);

INSERT INTO tab_set VALUES('a');
INSERT INTO tab_set VALUES('a,b');

SELECT * FROM tab_set;


#日期型
/*
分类：
date 只保存日期
time 只保存时间
year 只保存年
datetime 保存日期+时间
timestamp 保存日期+时间

特点		字节		范围		   时区等的影响
	
datetime	  8		1000-9999		不受

timestamp	  4		1970-2038		受
*/

CREATE TABLE tab_date(
	t1 DATETIME,
	t2 TIMESTAMP
);

INSERT INTO tab_date VALUES(NOW(),NOW());

SELECT * FROM tab_date;

SHOW VARIABLES LIKE 'time_zone'

set time_zone = '+9:00';  #更改时区
```

#### 常见约束

```sql
#常见约束

/*

含义：一种限制，用于限制表中的数据，为了保证表中数据的准确和可靠性

分类：六大约束
	NOT NULL: 非空，用于保证该字段值不能非空
	比如：姓名，学号
	DEFAULT: 默认约束，用于保证该字段有默认值
	比如性别
	PRIMARY KEY: 主键约束，保证该字段的值具有唯一性，并且非空
	比如学号、员工编号
	UNIQUE:唯一余数，用于保证该字段的值具有唯一性，可以为空
	比如座位号
	CHECK: 检查约束【mysql中不支持】
	比如年龄，性别
	FOREIGN KEY: 外键，用于限制两个表的关系，用于保证该字段的值必须来自于主表的关联列的值
		在从表添加外键约束，用于引用主表中某列的值
	比如学生表的专业编号，员工表的部门编号、员工表的工种编号
	
	
添加约束的实际：
	1.创建表时
	2.修改表时
	
约束的添加分类：
	列级约束：
		六大约束语法上都支持，但外键约束没有效果
	表级约束
		除了非空，默认，其他都支持
		
主键和唯一的对比：
		唯一性		是否允许为null		一个表中可以有多少个	是否允许组合
	主键	是			不允许			至多有一个	允许，但不推荐
	唯一	是			允许			可以多个	允许，但不推荐
	
外键：
	1.要求在从表设置外键关系
	2.从表的外键列的类型和主表的关联列的类型要求一致或兼容，名称无要求
	3.主表的关联列必须是一个key（一般是主键或唯一键）
	4.插入数据时，先插入主表，再插入从表
	删除数据时，先删除主表，再删除从表

*/
CREATE TABLE 表名(
	字段名 字段类型 列级约束，
	字段名 字段类型 列级约束，
	表级约束
	
)

#一、创建表时，添加约束
#1.添加列级约束
/*
语法：

直接在字段名和类型后面追加约束类型即可
支持添加多个列级约束

只支持： 默认、非空、主键、唯一
*/

CREATE DATABASE students;

CREATE TABLE stuinfo(
	id INT PRIMARY KEY, #主键
	stuName VARCHAR(20) NOT NULL, #非空
	gender CHAR(1), CHECK(gender = '男' OR gender = '女'),  #检查
	seat INT UNIQUE, #唯一
	age INT DEFAULT 18, #默认约束
	majorId INT REFERENCES major(id) #外键，无效，仅仅不报错

)

CREATE TABLE major(
	id INT PRIMARY KEY,
	majorName VARCHAR(20)

)
#查看stuinfo表中所有的索引，包含主键，外键，唯一
SHOW INDEX FROM stuinfo;


#2.添加表级约束
/*

语法：在各个字段的最下面
【constraint 约束名】 约束类型(字段名)

*/
DROP TABLE IF EXISTS stuinfo;
CREATE TABLE stuinfo(
	id INT,
	stuName VARCHAR(20),
	gender CHAR(1),
	seat INT,
	age INT,
	majorid INT,
	
	CONSTRAINT pk PRIMARY KEY(id),  #主键
	CONSTRAINT uq UNIQUE(seat), #唯一键
	CONSTRAINT ck CHECK(gender = '男' OR gender = '女'),  #检查 不支持
	CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERENCES major(id) #外键

)

SHOW INDEX FROM stuinfo;


#通用写法：

CREATE TABLE IF NOT EXISTS stuinfo(
	id INT PRIMARY KEY,
	stuname VARCHAR(20) NOT NULL,
	sex CHAR(1),
	age INT DEFAULT 18,
	majorid INT,
	CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERENCES major(id)
);


#二、修改表时添加约束
/*
1.添加列级约束
alter table 表名 modify column 字段名 字段类型 新约束;

2.添加表级约束
alter table 表名 add 【constraint 约束名】约束类型(字段名) 【外键的引用】
*/
DROP TABLE IF EXISTS stuinfo;
CREATE TABLE IF NOT EXISTS stuinfo(
	id INT,
	stuname VARCHAR(20),
	gender CHAR(1),
	seat INT,
	age INT,
	majorid INT
);


#1.添加非空约束
ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20) NOT NULL;

#2.添加默认约束
ALTER TABLE stuinfo MODIFY COLUMN age INT DEFAULT 18;

#3.添加主键
#(1)列级约束
ALTER TABLE stuinfo MODIFY COLUMN id INT PRIMARY KEY;
#(2)表级约束
ALTER TABLE stuinfo ADD PRIMARY KEY(id);


#4.添加唯一键
#(1)列级约束
ALTER TABLE stuinfo MODIFY COLUMN seat INT UNIQUE;
#(2)表级约束
ALTER TABLE stuinfo ADD UNIQUE(id);


#5.添加外键
ALTER TABLE stuinfo ADD CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERENCES major(id);


#三、修改表时删除约束

#1.删除非空约束
ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20) NULL;

#2.删除默认约束
ALTER TABLE stuinfo MODIFY COLUMN age INT;

#3.删除主键
ALTER TABLE stuinfo DROP PRIMARY KEY;

#4.删除唯一键
ALTER TABLE stuinfo DROP INDEX id;

SHOW INDEX FROM stuinfo;

#5.删除外键约束
ALTER TABLE stuinfo DROP FOREIGN KEY fk_stuinfo_major;
```

#### 标识列

```sql
#标识列

/*
又称为自增长列
含义：可以不用手动的插入值，系统提供默认的序列值

特点：
1.标识列必须和主键搭配吗？ 不一定，但是要求是一个key
2.一个表中可以有几个标识列？ 只能有一个
3.标识列的类型 只能是数值型
4.标识列可以通过SET auto_increment_increment = 1 设置步长
可以通过手动插入值设置起始值


*/

#一、创建表时，设置标识列 
DROP TABLE IF EXISTS tab_identify
TRUNCATE TABLE tab_identify;
CREATE TABLE IF NOT EXISTS tab_identify(
	id INT PRIMARY KEY,
	NAME VARCHAR(20)

);

INSERT INTO tab_idetify VALUES(10,'john');
INSERT INTO tab_idetify(NAME) VALUES('lucy');

SELECT * FROM tab_idetify

SET auto_increment_increment = 1;

#二、修改表时设置表示列

ALTER TABLE tab_identify MODIFY COLUMN id  INT AUTO_INCREMENT;


#三、修改表时删除表示列

ALTER TABLE tab_identify MODIFY COLUMN id INT;
```

#### 事务

```sql
#TCL 

/*
Transaction Control Language 事务控制语言

事务：
一个或一组SQL语句组成的一个执行单元，这个执行单元要么全部执行，要么全部不执行
如果其中有部分执行失败，那么会回滚，回到事务执行前的状态

案例：转账

张三丰 1000
郭襄   1000

update 表 set 张三丰的余额 = 500 where name = ’张三丰‘
update 表 set 郭襄的余额 = 1500 where name = ’郭襄‘

存储引擎： 在mysql中数据用各种不同的技术存储在文件中
通过show engines 来看支持的存储引擎

innodb引擎是支事务的

事务(ACID)的属性：
1.原子性(Atomicity)
事务中的操作要么全部执行，要么什么都不发生
2.一致性(Consistency)
事务必须使数据库从一个一致性状态变换到另一个一致性状态
3.隔离性(Isolation)
并发执行的各个事务之间不能互相干扰
4.持久性(Durability)
一个事务一旦提交，对数据库的改变是永久性的



事务的创建
隐式的事务：事务没有明显的开启和结束的标记
比如insert、update、delete语句

显式事务：事务具有明显开启和结束的标记
前提：必须先设置自动提交功能为禁用

set autocommit = 0;  仅针对当前会话有效

步骤1：开启事务
set autocommit = 0;
satrt transaction; 可选
步骤2：编写事务中的SQL语句（select insert update delete）

步骤3：结束事务
commit; 提交事务
rollback; 回滚事务


savepoint 结点名； 设置保存点


事务的隔离级别
read uncommitted：出现脏读，幻读，不可重复读
read comiitted： 出现幻读，不可重复读
repeatable read： 幻读
serializable：均不出现

mysql中默认的是第三个隔离级别 repeatable read
oracle 中默认 第二个隔离级别 read committed
查看隔离级别
select @@tx_isolation;

设置隔离级别
set session|global transaction isolation level 隔离级别;


*/

SHOW ENGINES;


CREATE DATABASE test;

DROP TABLE IF EXISTS account;

CREATE TABLE account(
	id INT PRIMARY KEY AUTO_INCREMENT,
	username VARCHAR(20),
	balance DOUBLE

);

INSERT INTO account(username,balance)
VALUES('张无忌', 1000),('赵敏',1000);

SELECT * FROM account

#1.演示事务的使用步骤
#开启事务
SET autocommit = 0;
START TRANSACTION;
#编写事务语句
UPDATE account SET balance = 1000 WHERE username = '张无忌';
UPDATE account SET balance = 1000 WHERE username = '赵敏';
#结束事务
#commit;
ROLLBACK;


#2.演示事务对delete和truncate的处理区别

SET autocommit = 0;
START tansaction;

DELETE FROM account;
#truncate from account
ROLLBACK;

SELECT * FROM account;

#3.演示savepoint的使用
SET autocommit = 0;
START TRANSACTION;


DELETE FROM account WHERE id = 1;
SAVEPOINT a;  #设置保存点
DELETE FROM account WHERE id = 3;
ROLLBACK TO a;  #回滚到保存点 删了1号，回滚了3号


```

#### 视图

```sql
#视图
/*
含义：虚拟表，和普通的表一样使用
mysql5.1出现的新特性，是通过表动态生成的数据

比如：舞蹈班和普通班的对比

好处：
1.重用sql语句
2.简化复杂的sql操作，不必知道细节
3.保护数据，提高安全性


视图和表的对比
	创建的语法		是否占用实际物理空间		使用

视图	create view		只保存了逻辑			增删改查；一般不能删改

表	create table 		保存了数据			增删改查

*/



#一、创建视图
/*
语法：
create view 视图名
as
查询语句;
*/
USE myemployees;

#1.查询邮箱中包含字符a的员工名、部门名和工种信息
#(1) 创建视图
CREATE VIEW myv1
AS 
SELECT last_name, department_name, job_title
FROM employees e
INNER JOIN departments d 
ON e.department_id = d.department_id
INNER JOIN jobs j 
ON e.job_id = j.job_id;

#(2)使用
SELECT *
FROM myv1
WHERE last_name LIKE '%a%';


#2.查询各部门的平均工资级别

#创建视图查各部门的平均工资
CREATE VIEW myv2
AS
SELECT AVG(salary), department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id
GROUP BY e.department_id;

SELECT * FROM myv2;


SELECT department_name, myv2.`avg(salary)` 部门平均工资, j.`grade_level` 工资等级
FROM myv2
INNER JOIN job_grades j
WHERE myv2.`avg(salary)` BETWEEN j.`lowest_sal` AND j.`highest_sal`;


#二、视图的修改

#方式一：
/*
create or replace view 视图名
as
查询语句;
*/

#方式二：

/*
语法：
alter view 视图名 
as
查询语句;

*/


#三、删除视图

/*
drop view 视图名，视图名，。。。

*/


DROP VIEW myv1, myv2;


#四：查看视图

DESC myv1;

SHOW CREATE VIEW myv1;


#创建视图emp_v1, 查询电话号码为'011'开头的员工姓名，工资和邮箱

CREATE OR REPLACE VIEW emp_v1
AS 
SELECT last_name, salary, email
FROM employees 
WHERE phone_number LIKE '011%';


SELECT * FROM emp_v1;


#创建视图emp_v2，查询部门最高工资高于12000的部门信息

CREATE OR REPLACE VIEW emp_v2
AS
SELECT MAX(salary) ms, department_id
FROM employees
GROUP BY department_id
HAVING MAX(salary) > 12000

SELECT emp.ms 最高工资, d.*
FROM emp_v2 emp
INNER JOIN departments d
ON d.department_id = emp.department_id;



#五、视图的更新(基本不使用)
DROP VIEW emp_v1,emp_v2,myv1;

CREATE OR REPLACE VIEW myv1
AS
SELECT last_name, email
FROM employees


#1.插入数据  对原始表也生成更新
SELECT * FROM myv1;
INSERT INTO myv1 VALUES('张飞','zf@qq.com');

#2.修改
UPDATE myv1 SET last_name = '刘备' WHERE last_name = '张飞';

#3.删除
DELETE FROM myv1 WHERE last_name = '刘备';


#具备以下特点的视图不更新的

#(1) 包含一下关键字的sql语句：分组函数，distinct， group by，having，union或者union all

#(2)常量视图

CREATE OR REPLACE VIEW myv2
AS
SELECT 'john' NAME;

UPDATE myv2 SET NAME = 'lili';

#(3)select中包含子查询

#(4)join
#(5)from一个不能更新的视图
CREATE OR REPLACE VIEW myv3
AS 
SELECT * FROM myv2;

UPDATE myv3 SET NAME = 'ssss';

#(6)where子句中的子查询引用了from子句的表
CREATE OR REPLACE VIEW myv4
AS

SELECT last_name, email, salary
FROM employees
WHERE employee_id IN (
	SELECT manager_id
	FROM employees
	WHERE manager_id IS NOT NULL
)


```

#### 变量

```sql
#变量

/*
系统变量：
	全局变量
	会话变量

自定义变量：
	用户变量
	局部变量

*/


#一、系统变量
/*
说明：变量由系统提供，不是用户定义，属于服务器层面

注意：如果是全局级别，需要加global，如果是绘画界别，则需要加session，如果不写则默认session

使用语法：
1.查看所有的系统变量
show global|【session】 variables;

2.查看满足条件的部分系统变量

show global|【session】 variables like '%char%';

3.查看指定的某个系统变量

select @@global|【session】.系统变量名;

4.为某个具体的系统变量赋值
方式一、

set global|【session】系统变量名 = 值; 

方式二、

set @@global|【session】.系统变量名 = 值

*/

#1》全局变量
/*
作用域：服务器每次启动将所有的全局变量赋初始值，针对所有的会话链接有效，但是不能跨重启
*/

#(1)查看所有的全局变量
SHOW GLOBAL VARIABLES;


#(2)查看部分全局变量
SHOW GLOBAL VARIABLES LIKE '%character%';

#(3)查看指定的全局变量
SELECT @@global.autocommit;
SELECT @@tx_isolation;

#(4)为某个指定的全局变量赋值 全局有效
SET @@global.autocommit = 0;

#2》会话变量
/*
作用域：仅仅针对于当前的会话（连接）有效
*/

#(1)查看所有的会话变量
SHOW SESSION VARIABLES;

SHOW VARIABLES;

#(2)查看部分会话变量
SHOW SESSION VARIABLES LIKE '%character%';
SHOW VARIABLES LIKE '%character%';


#(3)查看指定的全局变量
SELECT @@tx_isolation;
SELECT @@session.tx_isolation;

#(4)为某个指定的全局变量赋值 全局有效
#方式一、
SET @@session.tx_isolation = 'read-uncommitted';

#方式二、
SET SESSION tx_isolation = 'read-uncommitted';


#二、自定义变量
/*

说明：变量是用户自定的，不是由系统提供的
使用步骤
声明
赋值
使用（查看，比较，运算）
*/

#1.用户变量
/*
作用域：针对当前会话（连接）有效，同于会话变量的作用域
应用在任何地方， 也就是begin end里面或begin end 外面

*/

#(1)声明并初始化
SET @用户变量名  = 值;

SET @用户变量名:=值;

SELECT @用户变量名:=值;

#(2)赋值（更新用户变量的值）
#方式一、通过set或select

SET @用户变量名  = 值;

SET @用户变量名:=值;

SELECT @用户变量名:=值;

#方式二、通过select into

SELECT 字段 INTO 变量名
FROM 表;


#(3)使用（查看用户变量的值）
SELECT @用户变量名;




#案例：
#声明并初始化
SET @name = 'john';
SET @name='100';
SET @count = 1;

SELECT COUNT(*) INTO @count
FROM employees;


#2.局部变量
/*
作用域：仅仅在定义它的begin end 中有效
应用在begin end中的第一句话

*/

#(1)声明
DECLARE 变量名 类型;
DECLARE 变量名 类型 DEFAULT 值;

#赋值
SET 局部变量名  = 值;

SET 局部变量名:=值;

SELECT @局部变量名:=值;

#方式二、通过select into

SELECT 字段 INTO 局部变量名
FROM 表;

#(3)使用
SELECT 局部变量名;


对比用户变量 和 局部变量

		作用域 		定义和使用的位置		语法

用户变量	当前会话	会话中的任何地方		必须加@


局部变量	BEGIN END 中	只能在begin end中，且为第一句 	一般不用加@，除非需要限定类型


#案例：声明两个变量并赋初值，求和，并打印

#1.用户变量
SET @m=1;
SET @n=2;
SET @sum = @n+@m;
SELECT @sum;

#2.局部变量  报错
DECLARE m INT DEFAULT 1;
DECLARE n INT DEFAULT 2;
DECLARE SUM INT;
SET SUM = m +n;
SELECT SUM;
```

#### 存储过程

```sql
#存储过程和函数

/*
存储过程和函数：类似于java中的方法

好处：
1.提高代码的重用性
2.简化操作
*/


#存储过程
/*
含义：一组预先定义好的SQL语句的集合，理解成批处理语句
1.提高代码的重用性
2.简化操作
3.减少了编译次数并减少了和数据库连接次数，提高了效率

*/

#一、创建语法
CREATE PROCEDURE 存储过程名(参数列表)
BEGIN
	存储过程体(一组合法的SQL语句)
END

注意：
1.参数列表包含三部分
参数模式 参数名 参数类型

举例
IN sryname VARCHAR(20)

参数模式：
IN:该参数可以作为输入,即该参数需要调用方传入值
OUT:该参数可以作为输出，即为该参数可以作为返回值
INOUT:该参数既可以作为输入，也可以作为输出

2.如果存储过程体仅仅一句话, BEGIN END 可以省略
存储过程过程体中的每条SQL语句, 必须加分号
存储过程的结尾可以使用 DELIMITER 重新设置

语法:
DELIMITER 结束标记
案例：
DELIMITER $

#二、调用语法

CALL 存储过程名(实参列表);

#1.空参列表

#案例：插入到admin表中五条记录
SELECT * FROM admin;

DELIMITER $  #设置终止符号为 $
CREATE PROCEDURE myp1()
BEGIN 
	INSERT INTO admin(username, `password`) 
	VALUES('john1','0000'),('lily','0000'),('rose','0000'),('jack','0000'),('tom','0000');
END $

#调用
CALL myp1()$

#2.创建带in模式的参数的存储过程

#案例：创建存储过程实现 根据女神名，查询对应的男神信息

CREATE PROCEDURE myp2(IN beauty_name VARCHAR(20))
BEGIN
	SELECT bo.*
	FROM boys bo
	RIGHT JOIN beauty b ON bo.id = b.`boyfriend_id`
	WHERE b.name=beauty_name;

END $

#调用
CALL myp2('柳岩')$

#案例：创建存储过程实现，用户是否登陆成功

CREATE PROCEDURE myp5(IN username VARCHAR(20), IN PASSWORD VARCHAR(20))
BEGIN
	DECLARE result INT DEFAULT 0; #声明并初始化
	SELECT COUNT(*) INTO result #赋值
	FROM admin
	WHERE admin.username = username
	AND admin.password = PASSWORD;
	
	SELECT IF(result>0, '成功','失败');  #使用
END $

#调用
CALL myp5('张飞','888')$


#3.创建带out模式的存储过程

#案例1：根据女神名，返回对应的男神名
CREATE PROCEDURE myp6(IN beautyName VARCHAR(20), OUT boyName VARCHAR(20))
BEGIN
	SELECT bo.boyName INTO boyName
	FROM boys bo
	INNER JOIN beauty b ON bo.id = b.boyfriend_id
	WHERE b.name = beautyName;


END $

#调用
SET @bName$
CALL myp6('小昭',@bName)$
SELECT @bName$


#案例2：根据女神名。返回对应的男神名和男神魅力值

CREATE PROCEDURE myp7(IN beautyName VARCHAR(20), OUT boyName VARCHAR(20), OUT userCp INT)
BEGIN
	SELECT bo.boyName, bo.userCP INTO boyName,userCP
	FROM boys bo
	INNER JOIN beauty b ON bo.id = b.boyfriend_id
	WHERE b.name = beautyName;

END $

CALL myp7('柳岩',@bName, @usercp)$

#4.创建带inout模式参数的存储过程

#案例1：传入a和b两个值，最终要求a和b都翻倍并返回

CREATE PROCEDURE myp8(INOUT a INT, INOUT b INT)
BEGIN
	SET a = a*2;
	SET b = b*2;

END $


#调用

SET @m = 10$
SET @n = 20$
CALL myp8(@m,@n)$


#作业；

#1.创建存储过程或函数实现传入用户名和密码，插入到admin表中

CREATE PROCEDURE myp9(IN username VARCHAR(20), IN loginPwd VARCHAR(20))
BEGIN
	INSERT INTO admin(admin.`username`,admin.`password`) VALUES(username, loginPwd);

END $


#2、创建存储过程或函数实现传入女神号，返回女神名称和女神电话

CREATE PROCEDURE test_pro2(IN beautyid INT, OUT beautyName VARCHAR(20), OUT phoneNum VARCHAR(20))
BEGIN
	SELECT b.name, b.phone INTO beautyName, phoneNum
	FROM beauty b
	WHERE b.id = beautyid;
	
END $


#二、删除存储过程
#语法： drop procedure 存储过程的名称(一次只能删除一个)

DROP PROCEDURE myp1;

#三、查看存储过程的信息

SHOW CREATE PROCEDURE myp2;

#四、创建存储过程或函数，传入一个日期，格式化为xx年xx月xx日并返回
CREATE PROCEDURE test_pro4(IN mydate DATETIME, OUT strDate VARCHAR(20))
BEGIN
	SELECT DATE_FORMAT(mydate, '%y年%m月%d日') INTO strDate;

END $

CALL test_pro4(NOW(),@str)$
SELECT @str$
```

#### 函数

```sql
#函数
/*
含义：一组预先定义好的SQL语句的集合，理解成批处理语句
1.提高代码的重用性
2.简化操作
3.减少了编译次数并减少了和数据库连接次数，提高了效率

区别

存储过程：可以由0个返回，也可以有多个返回，适合做批量插入，批量更新
函数：只能有一个返回，适合做处理数据后返回一个结果

*/

#一、创建语法
CREATE FUNCTION 函数名(参数列表) RETURNS 返回类型
BEGIN
	函数体
END

/*
注意：
1.参数列表 包含两部分： 参数名 参数类型

2.函数体：肯定会return语句，如果没有会报错
如果return语句没有放在函数体最后也不会报错，但不建议

return 值;

3.当函数体中仅有一句话，则可以省略begin end
4.使用delimiter语句设置结束标记
*/

#二、调用语法
SELECT 函数名(参数列表)

#---------------------------------------案例演示-----------------------------------------

#1.无参有返回
#案例：返回公司员工个数

CREATE FUNCTION myf1() RETURNS INT
BEGIN
	DECLARE c INT DEFAULT 0; #定义一个变量
	SELECT COUNT(*) INTO c  #赋值
	FROM employees;
	RETURN c;

END $

SELECT myf1()$

#2.有参返回
#案例：更具员工名，返回他的工资
CREATE FUNCTION myf2(empName VARCHAR(20)) RETURNS DOUBLE
BEGIN
	DECLARE s INT DEFAULT 0;  #定义一个局部变量
	SELECT salary INTO s
	FROM employees
	WHERE last_name = empName;
	
	RETURN s;

END$


SELECT myf2('Kochhar')$

#案例：根部部门名，返回该部门的平均工资

CREATE FUNCTION myf3(deptName VARCHAR(20)) RETURNS DOUBLE
BEGIN
	DECLARE sal DOUBLE;
	SELECT AVG(salary) INTO sal
	FROM employees e
	JOIN departments d ON e.department_id = d.department_id
	WHERE d.department_name = deptName;
	RETURN sal;
END $

SELECT myf3('IT')$

#三、查看函数

DELIMITER ;
SHOW CREATE FUNCTION myf3;

#删除函数

DROP FUNCTION myf3;

#案例：
#一、创建函数，传入两个float， 返回二者之和
DELIMITER $
CREATE FUNCTION test_fun1(a FLOAT, b FLOAT) RETURNS DOUBLE
BEGIN
	DECLARE result DOUBLE;
	SET result = a + b;
	RETURN result;
END $

SELECT test_fun1(2.1,13.2)$
```

#### 流程控制结构

```sql
#流程控制结构
/*
顺序结构：程序从上往下顺序执行
分支结构：程序从两条或多条路径中选择一条去执行
循环结构：程序在满足一定条件的基础上，重复执行一段代码

*/

#一、分支结构

#1.if函数
/*
功能：实现简单的双分支

语法：

select if(表达式1，表达式2，表达式3)
执行顺序，如果表达式1成立，返回表达式2，否则返回表达式3

*/


#2.case结构

情况1：类似java中的switch语句 一般用于实现等值判断
语法：
	CASE 变量|表达式|字段
	WHEN 要判断的值 THEN 返回值1或语句1;
	WHEN 要判断的值 THEN 返回值2或语句2;
	...
	ELSE 要返回的值n或语句n;
	END CASE;


情况2: 类似于java中多重if语句，一般用于区间判断
语法：
	CASE
	WHEN 要判断的条件1 THEN 返回值1或语句1;
	WHEN 要判断的条件2 THEN 返回值2或语句2;
	...
	ELSE 要返回的值n或语句n;
	END CASE;

特点：
(1)
可以作为表达式，嵌套在其他语句中使用，可以放在任何地方， BEGIN END 中或者 BEGIN END 外
可以作为独立语句去使用，只能放在 BEGIN END 中
(2)
如果 WHEN 中的值或条件成立，则执行对应的 THEN 后面的语句，并且结束 CASE
如果都不满足，则执行 ELSE 中的语句或值

(3)
ELSE 可以省略，如果 ELSE 省略了，并且所有的 WHEN 条件都不满足，则返回 NULL


#案例：创建存储过程，根据传入的成绩，显示等级，比如传入成绩90-100，显示A， 80-90 显示B， 60-80显示C，否则显示D
DELIMITER $

CREATE PROCEDURE test_case(IN score INT)
BEGIN 
	CASE
	WHEN score BETWEEN 90 AND 100 THEN SELECT 'A';
	WHEN score BETWEEN 80 AND 90 THEN SELECT 'B';
	WHEN score BETWEEN 60 AND 80 THEN SELECT 'C';
	ELSE SELECT 'D';
	END CASE;
END $

CALL test_case(88)$


#3.if结构

/*
功能：实现多重分支

语法：
if 条件1 then 语句1;
elseif 条件2 then 语句2;
...
【else 语句n;】
end if;


应用在begin end中

*/


#案例：创建存储过程，根据传入的成绩，显示等级，比如传入成绩90-100，返回A， 80-90 返回B， 60-80返回C，否则返回D
CREATE FUNCTION test_if(score INT) RETURNS CHAR(1)
BEGIN
	IF score BETWEEN 90 AND 100 THEN  RETURN 'A';
	ELSEIF score BETWEEN 80 AND 90 THEN RETURN 'B';
	ELSEIF score BETWEEN 60 AND 80 THEN RETURN 'C';
	ELSE RETURN 'D';
	END IF;
END $


#二、循环结构
/*
分类：
while、loop、repeat、

循环控制：
iterate 类似于continue 结束本次循环，继续下次
leave 类似于 break 结束当前所在循环


*/


#1.while
/*
语法：
【标签:】 while 循环条件 do
	循环体;
end while 【标签】;

*/

#2.loop
/*
语法：
【标签：】loop
	循环体
end loop 【标签】;

可以用来模拟简单的死循环
*/


#3.repeat
/*
语法：
【标签：】repeat
	循环体;
until 结束循环的条件
end repeat【标间】;

*/


#案例：批量插入，根据设置次数插入到admin表中多条记录

CREATE PROCEDURE pro_while1(IN insertCount INT)
BEGIN
	DECLARE i INT DEFAULT 1;
	WHILE i <= insertCount DO
		INSERT INTO admin(username, PASSWORD) VALUES(CONCAT('Rose', i), '666');
		SET i = i +1;
	END WHILE;
END $

CALL pro_while1(100)$



#2.添加leave语句

#案例：批量插入，根据设置次数插入到admin表中多条记录，如果次数大于20停止
DELIMITER $
TRUNCATE TABLE admin$

DROP PROCEDURE test_while1$

CREATE PROCEDURE test_while1(IN insertCount INT)
BEGIN
	DECLARE i INT DEFAULT 1;
	a:WHILE i < insertCount DO
		INSERT INTO admin(username, `password`) VALUES(CONCAT('xiaohu',i),'0000');
		IF i >=20  THEN LEAVE a;
		END IF;
		SET i = i +1;
	END WHILE a;
	
END $

#3.添加iterate

#案例：批量插入，根据设置次数插入到admin表中多条记录，只插入偶数次
DELIMITER $
TRUNCATE TABLE admin$

DROP PROCEDURE test_while1$

CREATE PROCEDURE test_while1(IN insertCount INT)
BEGIN
	DECLARE i INT DEFAULT 0;
	a:WHILE i < insertCount DO
		SET i = i +1;
		IF MOD(i,2) !=0  THEN ITERATE a;
		END IF;
		INSERT INTO admin(username, `password`) VALUES(CONCAT('xiaohu',i),'0000');
	END WHILE a;
	
END $


#练习

/*
已知表stringcontent
其中字段
id 自增长
content varchar(20)

向该表插入指定个数的 随机字符串

*/

DELIMITER ;
CREATE TABLE stringcontent(
	id INT PRIMARY KEY AUTO_INCREMENT,
	content VARCHAR(20)
);


DELIMITER $
CREATE PROCEDURE test_randstr_insert(IN insertCount INT)
BEGIN
	DECLARE i INT DEFAULT 1; #定义一个变量，表示插入次数
	DECLARE str  VARCHAR(26) DEFAULT 'abcdefghijklmnopqrstuvwxyz';
	DECLARE startIndex INT DEFAULT 1; #代表起始索引
	DECLARE len INT DEFAULT 1; #代表截取字符串长度
	WHILE i <= insertCount DO
		SET len = FLOOR(RAND()*(20-startIndex+1)+1);
		#产生一个随机整数，代表起始索引1-26
		SET startIndex = FLOOR(RAND()*26+1);
		INSERT INTO stringcontent(content) VALUES(SUBSTR(str,startIndex,len));
		SET i = i +1;
	END WHILE;

END $

```

#### DCL语言 : 管理用户，授权(了解)

**DCL**: 管理用户，授权

1. 管理用户
   1. 添加用户

      ​	CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';

     2. 删除用户

        ​	DROP USER '用户名'@'主机名';

     3. 修改用户密码：

        ​	UPDATE USER SET PASSWORD = PASSWORD('新密码') WHERE USER = '用户名';

        ​	UPDATE USER SET PASSWORD = PASSWORD('root') WHERE USER = 'MEWT';

        ​	SET PASSWORD FOR '用户名'@'主机名' = PASSWORD('新密码');

        ​	SET PASSWORD FOR 'MRWT'@'%' = PASSWORD('root');

        	* 忘记mysql中root的密码
         * 1. cmd -- >  net stop mysql  停止mysql服务(需要管理员权限)
           2. 启动无验证方式启动mysql服务： mysqld  -- skip-grant-tables
           3. 打开新的cmd窗口，直接输入mysql命令，回车，直接登录
           4. use mysql
           5. update user set password = password(‘新密码’ )  where user = 'root';
           6. 打开任务管理器 手动结束mysqld.exe 进程

        4.查询用户：

   ​	-- 1. 切换到mysql数据库
   ​	USE mysql;
   ​	-- 2. 查询user表
   ​	SELECT * FROM USER;

   * 通配符： %表示可以在任意主机登录数据库

2. 授权： 权限管理

   1. 查询权限

      ​	SHOW GRANTS FOR '用户名'@'主机名';

      ​	SHOW GRANTS FOR 'MRWT'@'%';

   2. 授予权限

      ​	GRANT 权限列表 ON 数据库.表 TO '用户名'@'主机名';

      ​	GRANT SELECT, DELETE, UPDATE ON myemployees.employees TO 'MRWT'@'%';


      ​	-- 给MRwt授予所有权限，在任意数据库任意表上
    
      ​	GRANT ALL ON *.* TO 'MRwt'@'localhost';

   3. 撤销权限

      ​	--撤销权限：

      ​	revoke 权限列表 on 数据库名. 表名 from '用户名'@'主机名'

#### JDBC 学习

**概念：**  Java DataBase Connectivity     java 数据库连接， java语言操作数据库

**JDBC本质**：官方定义的一套操作所有关系型数据库接口的规则，即接口，各个数据库厂商去实现这套接口，提供数据库驱动 jar 包。我们可以使用这套接口          （ JDBC）编程 ，真正的执行代码是驱动 jar 包中的实现类。

**JDBC** 定义了操作所有关系型数据库的规则(接口)， 不同的数据库管理系统写了不同的  JDBC 实现类，  称为数据库驱动



**快速入门**：

  		1. 导入驱动 jar 包
  	     		1. 复制mysql-connertor 到 libs 目录下
  	     		2. 右键-->add as library
  		2. 注册驱动
  		3. 获取数据库连接对象 Connection
  		4. 定义sql
  		5. 获取执行sql语句的对象 Statement
  		6. 执行sql，接收返回的结果
  		7. 处理结果
  		8. 释放资源

* 代码实现

```java
//1.导入驱动架包
//2.注册驱动
Class.forName("com.mysql.cj.jdbc.Driver");
//3.获取数据库连接对象
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test?serverTimezone=UTC","root","root");
//4.定义sql语句
String sql = "update account set balance = 500 where id = 2";
//5.获取执行sql的对象
Statement stmt = conn.createStatement();
//6.执行sql
int count = stmt.executeUpdate(sql);
//7.处理结果
System.out.println(count);
//8.释放资源
stmt.close();
conn.close();
```

3. 详解各个对象：	

    1. DriverManager：驱动管理对象

         * 功能

           1. 注册驱动 :  告诉程序该使用哪一个数据库驱动  jar

              ​	 static void registerDriver(Driver driver) :   注册与给定的驱动程序 DriverManager

              ​	写代码使用： Class.forName("com.mysql.cj.jdbc.Driver");  将类字节码文件加载进内存

              ​	查看源码发现，在Driver类中，存在静态代码块

              ```java
              static {
                  try {
                      java.sql.DriverManager.registerDriver(new Driver);
                  }catch{
                      throw new RuntimeException("can't register driver!");
                  }
              }
              ```

              注意 ： mysql5之后的驱动jar包，可以省略注册驱动

           2. 获取数据库连接

                * 方法：static Connection getConnection(String url, String user, String password)
                * 参数：
                    * url:  指定连接路径
                      	* 语法：jdbc:mysql://ip地址(地址): 端口号/数据库名称 ? 时区设置
                      	* 例子 :  jdbc:mysql://localhost:3306/test?serverTimezone=UTC
                      	* 细节：如果连接本机的mysql服务器，并且mysql默认端口3306，则url可以简写为： jdbc:mysql:///数据库名称 ? 时区设置
                  * user：用户名
                  * password： 密码

    2. Connection：数据库连接对象

          			1. 功能：
            	   			1. 获取执行sql 的对象
            	         	* Statment  createSatement()
            	         	* PrepareSattement prepareSatatement(String sql)
            				2. 管理事务：
            	      * 开启事务：void setAutoCommit(boolean autoCommit) :  调用该方法设置参数为false，即开启事务
            	      * 提交事务： commit()
            	      * 回滚事务：rollback()

    3. Statement：执行sql的对象

         		1. 执行sql
          	 	1. boolean execute(String sql): 可以执行任意sql    了解
          	 	2. int excuteUpdate(String sql1)：执行DML（inset update delete）语句、DDL（create，alter，drop）语句
          	     		* 返回值：影响的行数，可以通过影响行数判断DML语句是否执行成功 返回值>0则执行成功，反之，执行失败
          		3. ResultSet excuteQuery（String sql）:执行DQL（select）语句
       		2. 练习
         	1. 添加account表中一条记录
         		2. account 表 修改记录
         		3. account 表删除一条记录

    4. ResultSet：结果集对象，封装查询结果的对象

          * boolean next() 方法 ：游标向下移动一行，判断当前行是否有数据，如果是末尾，返回 false， 如果不是返回true

          * getXxx(参数): 获取数据

            			* Xxx代表数据类型  如 int getInt()    String getString()
               * 参数：
                 1. int：列的编号，从1开始  如：getString（1）
                 2. String：代表列的名称 如： getDouble("balance")

       * 注意：

          * 使用步骤

            	1. 游标向下移动一行
            	2. 判断是否有数据
            	3. 获取数据

            ```java
            while(result.next())   //判断是否有数据，打印所有数据
            System.out.println("------" + result.getInt("id") +"-----" + result.getString("username") + "-----"+result.getDouble(3));
            ```

       * 联系：
          *  定义一个方法，查询beauty表的数据将其封装为对象，然后装载集合，返回。
             	1.  定义个beauty类
              	2.  定义方法 public List<beauty> findAll(){}
              	3.  实现方法 select * from beauty;

    5. PreparedStatement：执行sql对象

        	1.  SQL注入问题：在拼接sql的时候，有一些特殊的关键字参与字符串拼接，会造成安全问题
        	 	1. 输入用户随便，输入密码  a' or 'a' = 'a'
        	  	2. sql: select * from user where username = 'dwdwa' and pawword = 'a'  or 'a' = 'a'
       	2.  解决sql注入问题：使用PrepareStatement对象来解决
       	3.  **预编译sql：参数使用  ？ 作为占位符**
       	4.  步骤
        	 	1. 导入驱动 jar 包
        	 	2. 注册驱动
        	 	3. 获取数据库连接对象 Connection
        	 	4. 定义sql
        	     * 注意： sql 参数使用 ？ 作为占位符。 如： select * from user where user name = ? and password = ?;
        	 	5. 获取执行sql语句的对象 PreparedStatement  Connection.preparedStatement(String sql)
        	 	6. 给？赋值
        	      * 方法; setXxx(参数1，参数2)
        	        	* 参数1： ？的位置 从1 开始
        	        	* 参数2： ？的值
        	 	7. 执行sql，接收返回的结果，不需要传递sql语句
        	 	8. 处理结果
        	 	9. 释放资源
       	5.  注意：后期都会使用PreparedStatement，完成增删改查所有操作
        		1. 防止SQL注入
        	 	2. 效率更高



### 抽取JDBC工具类： JDBCUtils

 * 目的：简化书写

 * 分析：

     1. 注册驱动也抽取

     2. 抽取一个方法获取连接对象

          * 需求：不想传递参数，还得保证工具类的通用性

          * 解决：通过配置文件

            ​		jdbc.properties

            ​		url=

            ​		user = 

            ​		password = 

            ```java
                /**
                 * 文件的读取只需要读取以此即可拿到这些值。使用静态代码块，指挥随着类的加载而加载，只执行以此
                 */
                static{
                    try {
                        //读取资源，获得值
                        //1.创建Properties集合类
                        Properties pro = new Properties();
            
                        //获取src路径下的文件的方式------>ClassLoader 类加载器
                        ClassLoader classloader = JDBCUtils.class.getClassLoader();
                        URL res = classloader.getResource("jdbc.properties");
                        String path = res.getPath();
                        //2.加载文件
                        pro.load(new FileReader(path));
            
                        //3.获取数据，赋值
                        url = pro.getProperty("url");
                        user = pro.getProperty("user");
                        password = pro.getProperty("password");
                        driver = pro.getProperty("driver");
                        //4.注册驱动
                        Class.forName(driver);
                    } catch (IOException e) {
                        e.printStackTrace();
                    } catch (ClassNotFoundException e) {
                        e.printStackTrace();
                    }
                }
            ```

            

     3. 抽取一个方法释放资源

        ```java
            /**
             * 释放资源
             * @param stmt
             * @param conn
             */
            public static void close(Statement stmt, Connection conn){
                if(stmt != null){
                    try {
                        stmt.close();
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
                if(conn != null){
                    try {
                        conn.close();
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
            }
        
        
            /**
             * 释放资源
             * @param result
             * @param stmt
             * @param conn
             */
            public static void close(ResultSet result, Statement stmt, Connection conn){
                if(result != null){
                    try {
                        result.close();
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
                if(stmt != null){
                    try {
                        stmt.close();
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
                if(conn != null){
                    try {
                        conn.close();
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
            }
        ```

* 练习：

   * 需求

      1. 通过键盘录入用户名和密码

      2. 判断用户是否登录成功

         ```sql
         select * from user where username = '' and password = '';
         ```

         如果该语句有返回值则执行成功

  * 步骤

     1. 创建一个数据库表

        ```sql
        CREATE TABLE USER(
        	id INT PRIMARY KEY AUTO_INCREMENT,
        	username VARCHAR(32),
        	pasword VARCHAR(32)
        	
        )
        SELECT * FROM USER;
        
        INSERT INTO USER VALUES(NULL,'zhangsan','123'),(NULL,'lisi','234')
        ```

#### JDBC 控制事务

1. 事务： 一个包含多个步骤的业务操作。要么同时执行，要么都不执

2. 操作

   	1. 开启事务
   	2. 提交事务
   	3. 回滚事务

3. 使用Connection对象来管理事务

    * 开启事务：setAutoCommit(boolean autoCommit) : 调用该方法设置参数为false 开启事务

      ​	* 在执行sql之前开启事务

    * 提交事务： commit()

      ​	* 当所有sql都执行完提交事务

    * 回滚事务：rollback()

      ​	* 在cathch中回滚事务

#### 数据库连接池

* 概念：其实是一个容器（集合），存放数据库连接的容器。

  ​			放系统初始化好后，容器被创建，容器中申请了一些连接对象，用户访问数据时，从容器中获取链接对象，用户访问完后，会将连接对象归还容器。

* 好处：

  	1. 节约资源
   	2. 用户访问高效

* 实现：

   	1. 标准接口 DataSource  java/sql包下的
        	1. 方法：
            	*  获取连接 getConnection()
            	*  归还连接：Connection.close() 如果连接对象Connection是从连接池中获取的，那么调用Connection.close()的方法，不会是关闭连接，而是归还连接
  	2. 一般我们不去实现，由数据库厂商实现
      	1. C3P0: 数据库连接池技术
       	2. Druid：数据库连接池实现技术，由阿里巴巴提供 

* C3P0： 数据库连接池

   * 步骤：

      1. 导入jar包 两个， 

         ​	* 不要忘记导入数据库驱动jar包

      2. 定义配置文件 ：

         		* 名称：c3p0.properties 或者 c3p0-config.xml
         		* 路径:  直接将文件放在src目录下即可

     	3. 创建核心对象  数据库连接池对象   ComboPooledDataSource

     	4. 获取链接： getConnection()

* Druid：数据库连接池，由阿里巴巴提供

   * 步骤：
     1. 导入jar 包
     2. 定义配置文件：
        	* 是properties形式文件
        	* 可以叫任意名称，可以放任意目录下
     3. 加载配置文件。 Properties
     4. 获取数据库连接池对象：通过工厂类来获取  DruidDatsSourceFactory
     5. 获取链接：getConnection
  * 定义工具类
    	1. 定义一个类 JDBCUtils
     	2. 提供静态代码块，加载配置文件，初始化连接池对象
     	3. 提供方法
         	1. 获取连接方法：通过数据库连接池获取链接
          	2. 释放资源
          	3. 获取连接池的方法

#### Spring JDBC

   * Spring框架对JDBC的简单封装。提供了JDBCTemplate对象简化JDBC的开发

   * 步骤：

      1. 导入jar包

      2. 创建JdbcTemplate对象。依赖于数据源DataSource

         	* JdbcTmeplate template = new JdbcTemplate(ds)

     	3. 调用JdbcTemplate方法来完成CRUD操作

          * update()  : 执行DML语句。 增删改

          * queryForMap()：查询结果，将结果集封装为map集合

            ​	* 注意：查询的结果集长度只能为1，将列名作为key，值作为value

          *  queryForList()：查询结果，将结果集封装为List集合

             * 注意：将每一条记录封装为一个map集合，再将多个map集合装载到list集合中

          * query(): 查询结果，将结果封装为JavaBean对象

             * 注意：基本数据类型无法存储null，定义为引用数据类型即可
             * query参数： RowMapper
               	* 一般我们使用BeanPropertyRowMapper()实现类。可以完成数据到JavaBean的自动封装
               	* new BeanPropertyRowMapper<类型>(类型.class)

          * queryForObject：查询结果，将结果封装为对象

            	*  一般用于聚合函数的查询

     	4. 练习：

          * 需求
            	1. 修改1号数据的salary的工资为10000
             	2. 添加一条记录
             	3. 删除更高添加的记录
             	4. 查询id为1的记录，将其封装为Map集合
             	5. 查询所有记录，将其封装为List
             	6. 查询所有记录，将其封装为Beauty对象List集合
             	7. 查询总记录数





