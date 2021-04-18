---
title: MYSQL入门学习
abbrlink: 36283
date: 2021-04-18 09:49:57
categories: "MYSQL"

tags:
	- MYSQL
	- 学习笔记

---



## 数据库的好处

```mysql
    1.持久存到本地  
    2.可以实现结构化查询，方便管理
```

## 数据库相关概念

```mysql
    1.DB：数据库，保存一组有组织的数据的融通器  
    2.DBMS:数据库管理系统，又称数据库软件(产品),用于管理DB中的数据    
    3.SQL结构化查询语言，用于和DBMS通信的语言
```

## 数据库存储数据的特点

```mysql
    1、将数据放到表中，表再放到库中
	2、一个数据库中可以有多个表，每个表都有一个的名字，用来标识自己。表名具有唯一性。
	3、表具有一些特性，这些特性定义了数据在表中如何存储，类似java中 “类”的设计。
	4、表由列组成，我们也称为字段。所有表都是由一个或多个列组成的，每一列类似java 中的”属性”
	5、表中的数据是按行存储的，每一行类似于java中的“对象”。
```

## MySQL服务的启动和停止

```mysql
    方式一：计算机——右击管理——服务
	方式二：通过管理员身份运行
	net start 服务名（启动服务）
	net stop 服务名（停止服务）
```

## MySQL服务的登录和退出

```mysql
    方式一：通过mysql自带的客户端
	只限于root用户

	方式二：通过windows自带的客户端
	登录：
	mysql 【-h主机名 -P端口号 】-u用户名 -p密码

	退出：
	exit或ctrl+C
```

### MySQL的常见命令

```mysql
    1.查看当前所有的数据库
	show databases;
	
    2.打开指定的库
	use 库名
	
    3.查看当前库的所有表
	show tables;
	
    4.查看其它库的所有表
	show tables from 库名;
	5.创建表
	create table 表名(

		列名 列类型,
		列名 列类型，
		。。。
	);
    6.查看表结构
	desc 表名;


    7.查看服务器的版本
	方式一：登录到mysql服务端
	select version();
	方式二：没有登录到mysql服务端
	mysql --version
	或
	mysql --V
```

### MySQL的语法规范

```mysql
    1.不区分大小写,但建议关键字大写，表名、列名小写
	2.每条命令最好用分号结尾
	3.每条命令根据需要，可以进行缩进 或换行
	4.注释
		单行注释：#注释文字
		单行注释：-- 注释文字
		多行注释：/* 注释文字  */
```

### SQL的语言分类

```mysql
`DQL（Data Query Language）：数据查询语言
		select 
	DML(Data Manipulate Language):数据操作语言
		insert 、update、delete
	DDL（Data Define Languge）：数据定义语言
		create、drop、alter
	TCL（Transaction Control Language）：事务控制语言
		commit、rollback
```

## SQL的常见命令

```mysql
    show databases； 查看所有的数据库
	use 库名； 打开指定 的库
	show tables ; 显示库中的所有表
	show tables from 库名;显示指定库中的所有表
	create table 表名(
		字段名 字段类型,	
		字段名 字段类型
	); 创建表

	desc 表名; 查看指定表的结构
	select * from 表名;显示表中的所有数据
```

## DQL语言的学习

### 进阶1：基础查询

```mysql
语法：
	SELECT 要查询的东西
	【FROM 表名】;

	类似于Java中 :System.out.println(要打印的东西);
	特点：
	①通过select查询完的结果 ，是一个虚拟的表格，不是真实存在
	② 要查询的东西 可以是常量值、可以是表达式、可以是字段、可以是函数
```

### 进阶2：条件查询

```mysql
条件查询：根据条件过滤原始表的数据，查询到想要的数据
	语法：
	select 
		要查询的字段|表达式|常量值|函数
	from 
		表
	where 
		条件 ;

	分类：
	一、条件表达式
		示例：salary>10000
		条件运算符：
		> < >= <= = != <>
	
	二、逻辑表达式
	示例：salary>10000 && salary<20000
	
	逻辑运算符：

		and（&&）:两个条件如果同时成立，结果为true，否则为false
		or(||)：两个条件只要有一个成立，结果为true，否则为false
		not(!)：如果条件成立，则not后为false，否则为true

	三、模糊查询
	示例：last_name like 'a%'
```

### 进阶3：排序查询

```mysql
语法：
	select
		要查询的东西
	from
		表
	where 
		条件
	
	order by 排序的字段|表达式|函数|别名 【asc|desc】
```

### 进阶4：常见函数

```mysql
一、单行函数
	1、字符函数
		concat拼接
		substr截取子串
		upper转换成大写
		lower转换成小写
		trim去前后指定的空格和字符
		ltrim去左边空格
		rtrim去右边空格
		replace替换
		lpad左填充
		rpad右填充
		instr返回子串第一次出现的索引
		length 获取字节个数
		
	2、数学函数
		round 四舍五入
		rand 随机数
		floor向下取整
		ceil向上取整
		mod取余
		truncate截断
	3、日期函数
		now当前系统日期+时间
		curdate当前系统日期
		curtime当前系统时间
		str_to_date 将字符转换成日期
		date_format将日期转换成字符
	4、流程控制函数
		if 处理双分支
		case语句 处理多分支
			情况1：处理等值判断
			情况2：处理条件判断
		
	5、其他函数
		version版本
		database当前库
		user当前连接用户



	


二、分组函数


		sum 求和
		max 最大值
		min 最小值
		avg 平均值
		count 计数
	
		特点：
		1、以上五个分组函数都忽略null值，除了count(*)
		2、sum和avg一般用于处理数值型
			max、min、count可以处理任何数据类型
	    3、都可以搭配distinct使用，用于统计去重后的结果
		4、count的参数可以支持：
			字段、*、常量值，一般放1
	
		   建议使用 count(*)
```

## 代码笔记

### 进阶一：基础查询

```mysql
-- 进阶一：基础查询
/*
语法：select 查询列表 from 表名;
特点：
			1.查询列表可以是： 表中的字段、常量值、表达式、函数
			2.查询的结果是一个虚拟的表格
*/

-- 1.查询表中的单个字段
select email from employees;

-- 2.查询表中的多个字段
select last_name,first_name from employees;

-- 3.查询表中的所有字段
select * from employees;
 
-- 起别名：①便于理解 ②如果查询的字段有重名的情况，起别名可以解决
	-- 方式一：使用AS
	select email AS 邮箱 from employees;

	-- 方式二：使用空格
	select email 邮箱 from employees;
	
-- 去重
-- 案例：查询员工表中涉及到的所有部门编号
select DISTINCT department_id from employees;


-- 加号的作用  : 只有一个功能  运算符
-- 如果两个操作数都为数值，则做加法运算
select 110 + 110;  
-- 只要一方为字符型，试图将字符数值转换成数值型，如果转换成功，则继续加法运算，如果转换失败，则将字符数值转换成0
select '123' + 123; 
select 'Tom' + 123; 
-- 只要其中一方为null ，则结果肯定为null
select null + 10;

-- mysql 中的拼接使用函数 concat
select CONCAT(last_name,first_name) AS 姓名  from employees;

```

### 进阶二：条件查询

```mysql
-- 进阶二：条件查询

/*
语法  SELECT  查询列表  FROM  表名  WHERE  筛选条件

筛选条件分类；
					1、按条件表达式 ： >  <  = {!=  <> 这两个都是不等于}   >=   <=
					2、按逻辑表达式筛选  &&  ||  !   [java中]
															and  or   not  [mysql中]
															作用：用于连接条件表达式
																&& 和 and：两个条件都为true，结果为true，反之为false
																|| 和 or : 只要一个条件为true,结果为true，反之为false
																！和 no		：如果连接的条件本身为false,结果为true,反之为false
					3、模糊查询：like , bweteen and   , in   ,is null 
					like 特点： ①一般和通配符搭配使用  
												通配符： % 任意多个字符，包含0个字符
																 _任意单个字符
*/

-- 按条件表达式查询
 
-- 案例1： 查询工资大于12000的员工信息
select * from employees where salary >12000

-- 案例2：查询部门编号不等于90号的员工名和部门编号
select last_name,department_id from employees where department_id !=90;
select last_name,department_id from employees where department_id <>90;


-- 按逻辑表达式筛选

-- 案例1：查询工资在10000到20000之间的员工名，工资以及奖金
select last_name,salary,commission_pct from employees where salary >=10000  and salary <= 20000;
select last_name,salary,commission_pct from employees where not(salary < 10000 or salary >20000);

-- 案例2：查询部门编号不是在90到110之间或者工资高于15000的员工信息
select * from employees where department_id < 90 or department_id > 110 or salary >15000;
select * from employees where not(department_id >=90 and department_id <=110 and salary <=15000);
select * from employees where  not(department_id >=90 and department_id <=110 ) or salary >15000;


-- 模糊查询
-- 案例1：查询员工名包含字符a的员工信息
select * from employees where last_name like '%a%';

-- 案例2：查询员工名中年第三个字符为n，第五个字符为l的员工名和工资
select last_name,salary from employees where last_name like '__n_l%';

-- 案例3：查询员工名中第二个字符为_的员工名
select * from employees where last_name like '_\_%';  -- 转义字符
select * from employees where last_name like '_@_%' escape '@'; -- 转义关键字  可以是任意字符

-- between and 使用
-- 案例1：插叙员工编号在100 到120之间的员工信息
select * from employees where department_id >=100 and department_id <= 120;
select * from employees where department_id between 100 and 120;

-- in 的使用
-- 案例1：查询员工的工种编号是 IT_PRCG,AD_VP,AD_PRES中的一个员工名和工种编号
select last_name,job_id from employees where job_id ='IT_PRCG' or job_id ='AD_VP' or job_id ='AD_PRES';
select last_name,job_id from employees where job_id in('IT_PRCG','AD_VP','AD_PRES');

-- is null的使用
-- 案例1:查询没有奖金的员工名和奖金率
select last_name,commission_pct from employees where commission_pct is null;

-- 案例2；查询有奖金的员工名和奖金率
select last_name,commission_pct from employees where commission_pct is not null;
```

### 进阶三：排序

```mysql

-- 进阶三：排序----------------------------------------
/*
语法；
select  查询列表  from   表名 
[where 筛选条件]
order by 排序列表[asc/desc]

特点：
1.asc 代表升序，desc代表降序  如果不写默认是asc
2.order by 子句中可以支持单个字段，多个字段，表达式，函数，别名
3.order by 一般是放在查询语句的最后面  limit子句除外

*/

-- 案例1； 查询员工信息，要求工资从高到低排序
select * from employees order by salary desc;

-- 案例2：查询部门编号>=90的员工信息，按入职时间的先后顺序排序【添加筛选条件】
select * from employees where department_id >=90  order by hiredate;

-- 案例3：按年薪的高低显示员工的信息【按表达式排序】
select * from employees order by salary * 12 * (IFNULL(commission_pct,0)+1);

-- 案例4：按年薪的高低显示员工的信息和年薪【按别名排序】
select *,salary * 12 * (IFNULL(commission_pct,0)+1) as  年薪 from employees order by 年薪;

-- 案例5：按姓名的长度显示员工的姓和工资【按函数排序】
select length(last_name),first_name,salary from employees order by length(last_name);

-- 案例6：查询员工信息，要求先按工资升序，再按员工编号降序【按多个字段排序】
select * from employees order by salary,department_id desc;
```

### 进阶四：常见函数

```mysql


-- 进阶四：常见函数----------------------------------------
/*
概念：类似于java方法，将一组逻辑封装在方法体中，对外暴露方法名
好处；1.影藏了实现细节 2.提高代码重用性
调用：select 函数名(实参列表)  【from 表】;
关注： ①叫什么【函数名】  ②干什么【函数功能】

分类：
			1.单行函数 [字符函数、数学函数、日期函数、其它函数、流程控制函数]
			列如：concat 、length  、ifnull等
			2.分组函数
				功能：做统计使用，又称统计函数，聚合函数，组函数
*/


-- 单行函数
-- 1.length  获取字节长度
select length('张三123');

-- 2.concat  字符串拼接
select CONCAT(last_name,'_',first_name) 姓名 from employees;

-- 3.upper、lower 大小写转换
select UPPER('tom');
select LOWER('TOM');
-- 实例：将姓变大写，名变小写，然后拼接
select concat(upper(last_name),'_',lower(first_name)) from employees

-- 4.substr[或substring] 字符串截取
-- 截取从指定索引开始处后面所有字符
select substr('张三爱上了李四',3) out_pu; 

-- 截取从指定所有开始指定字符长度的字符
select substr('张三爱上了李四',1,4);

-- 案例：姓名中首字母大写，其它字符小写
select concat(CONCAT(upper(substr(last_name,1,1)),lower(substr(last_name,2))),'_'   ,CONCAT(UPPER(substr(first_name,1,1)),LOWER(substr(first_name,2)))) 姓名 from employees;


-- 5.instr 返回子串第一次出现的索引，如果找不到返回0
 select instr('张三爱上李四','李四');
 

-- 6.trim 去除两边空格
select trim('  aa   张三  aa  ');\
select trim('a' from 'aaaaaa张aaaaa三aaaaa');

-- 7.lpad 用指定的字符实现左填充指定长度
select lpad('张三',4,'*');
 
 -- 8.rpad 用指定的字符实现右填充指定长度
select rpad('张三',4,'*');
 
--  9.replace 替换
select replace('张三张三爱上了李四','张三','小红');
 
 
-- 数学函数
-- 1.round 四舍五入
select round(1.61);
select round(1.41);

-- 2.ceil 向上取整，返回>=该参数的最小整数
select ceil(1.01);
select ceil(1.0);

-- 3.floor 向下取整，返回<=该参数的最大整数
select floor(1.1);
select floor(2.0);

--  4.truncate 截断
select truncate(1.222,2);

-- 5.mod  取余
select mod(10,3);


-- 日期函数
-- 1.now 返回当前系统日期+时间
select now();
 
--  2.curdate 返回当前系统日期，不包含时间
select curdate();

-- 3.curtime 返回当前时间，不包含日期
select curtime();

-- 4.可以获取指定的不分:年、月、日、小时、分钟、秒
select year(now())  年; 
select month(now()) 月;
select date(now()) 日;
select hour(now())  小时;
select minute(now()) 分钟;
select second(now()) 秒;


-- 5.str_to_date 将字符通过指定的格式转换成日期
select STR_TO_DATE('1998-3-2','%Y-%c-%d') oup_put;


-- 6.date_fomart 将指定日期转换成字符串
select date_format(now(),'%y年%m月%d日');


-- 其它函数
select version();
select database();
select user();




-- 流程控制函数
-- 1.if函数
select if(10>5,'大','小');

-- 案例:
select last_name,commission_pct,if(commission_pct is null ,'没奖金','有奖金') 备注 from employees;


-- 2.case函数的使用一
/*
语法：
case 要判断的字段或表达式
when 常量1  then 要显示的值1或语句
when  常量2 then 要显示的值2或语句
...
else  要显示的值n或语句n
end
*/

-- 案例：查询员工的工资要求 
-- 部门号= 30，显示的工资为1.1倍
-- 部门号= 40，显示的工资为1.2倍
-- 部门号= 50，显示的工资为1.3倍
-- 其它部门，显示的工资为元工资

select salary 原工资,department_id, 
case department_id
when 30 then salary * 1.1
when 40 then salary * 1.2
when 50 then salary * 1.3
else salary  
end 新工资
from employees;



-- 2.case函数的使用二
/*
语法：
case 
when 条件1  then 要显示的值1或语句
when  条件2 then 要显示的值2或语句
...
else  要显示的值n或语句n
end
-- */
-- 案例：查询员工的工资情况
-- 如果工资>20000，显示A级别
-- 如果工资>15000，显示B级别
-- 如果工资>10000，显示C级别
-- 否则显示D级别
select salary,
case
when salary >20000 then 'A'
when salary >15000 then 'B'
when salary >10000 then 'C'
else 'D'
end 工资等级
from employees;



-- 分组函数
-- 分类： sun求和、  avg平均值、   max最大值、  min 最小值 count计算个数
-- 1.简单实用
select sum(salary) from employees;
select avg(salary) from employees;
select max(salary) from employees;
select min(salary) from employees;
select count(salary) from employees;
```

### 进阶五：分组查询

```mysql
-- 进阶五：分组查询----------------------------------------
/*
语法：
select 分组函数，列（要求出现在group by的后面）
from 表
【where 筛选条件】
group by 分组的列表
【order by 子句】

注意： 查询列表必须特殊，要求是分组函数和gruop by后面出现的字段
*/

-- 简单的分组查询
-- 案例1：查询每个工种的最高工资
select MAX(salary),job_id from employees
group by job_id;

-- 案例2：查询每个位置上的部门个数
select count(*), location_id from departments
group by location_id;

-- 案例3：查询邮箱中包含a字符的，每个部门的平均工资
select  avg(salary),department_id from employees
where email like '%a%'
group by department_id;


-- 案例4：查询有奖金的每个领导手下员工的最高工资
select max(salary),manager_id from employees
where commission_pct is not null
group by manager_id;

-- 案例5：哪个部门的员工个数>2
select count(*),department_id from employees
group by department_id
having count(*)>2;

-- 案例6：查询每个工种有奖金的员工最高工资>12000的工种编号和最高工资
select max(salary),job_id from  employees
where commission_pct is not null
group by job_id
having max(salary) >12000;

-- 案例7：查询领导编号>102的每个领导手下的最低工资>5000的领导编号是哪个，以及其最低工资
 select manager_id ,min(salary) from employees
 where manager_id >102
 group by manager_id
 having min(salary) > 5000;
```



### 进阶六：连接查询

```mysql
-- 进阶六：连接查询----------------------------------------
 /*
 含义：又称多表查询，当查询的字段来自于多个表示，就会用到连接查询
 笛卡尔积现象：表1  有m行，表2有n行  结果=m*n行
 
 发送原有：没有有效的连接条件
 如何避免：添加有效的连接条件
 
 分类；
				按年代分类：
								sql92标准；仅仅支持内连接
								sql99标准【推荐使用】：支持内连接+外连接（左外右外） + 交叉连接
								
					按功能分；
									内连接：
													等值连接
													非等值连接
													自连接
									外连接；
													左外连接
													右外连接：
													全外连接
													
									交叉连接
 */
 
--  一、sql92标准--------------
--  1、等值连接

 
--  案例1：查询员工名和对应的部门名
 
 select last_name,department_name from employees ,departments 
 where employees.employee_id = departments.department_id;
 
 
--  为表起别名： ①提高了语句的简介度 ②区分多个重名字段
-- 		注意：如果为表起了别名，则查询的字段就补鞥呢使用原来的表名去限定
--  案例2：查询员工名、工种号、工种名
select last_name,e.job_id,job_title from employees e,jobs j
where e.job_id = j.job_id;

 
--  案例3：查询有奖金的员工名，部门名【加筛选】
select last_name ,e.commission_pct,d.department_name from  employees e,departments d
where e.department_id = e.department_id  
and e.commission_pct is not null;

-- 案例4：查询城市名中第二个字符为o的部门名称和城市名【加筛选】

select d.department_name,l.city from departments d, locations l
where d.location_id = l.location_id
and l.city like '_o%';

-- 案例5：查询每个城市的部门个数【加分组】
select count(*),city from departments d,locations l
where d.location_id = l.location_id
GROUP BY city;

-- 案例6：查询有奖金的每个部门的部门名和部门的领导编号和该部门的低工资
select d.department_name,d.manager_id,min(salary) from employees e,departments d
where e.department_id = d.department_id
and commission_pct is not null
GROUP BY d.department_name,d.manager_id;
 
-- 案例7：查询每个工种的工种名和员工的个数，并按员工个数降序
select count(*),j.job_title from employees e,jobs j
where e.job_id = j.job_id
group by j.job_title
order by count(*) desc;


-- 三表联查
-- 案例：查询员工名、部门名和所在的城市
select e.last_name,d.department_name,l.city from employees e,departments d,locations l
where e.employee_id = d.department_id and d.location_id =l.location_id;



-- 二、非等值连接
-- 案例1：查询员工的工资和工资级别
select salary,grade_level from employees e,job_grades j
where salary between j.lowest_sal and j.highest_sal;


-- 三、自连接
-- 案例：查询员工名和上级的名称																																								-- as 员工表			-- as 领导表
select e.last_name as 员工名,e.manager_id as 上级编号,d.employee_id as 上级员工编号,d.last_name  as 上级名称 from employees e ,employees d 
where e.manager_id = d.employee_id;



-- 二、sql99语法
/*
语法：	
					select 查询列表
					from 表1  as 别名
					join 表2	as 别名
					on  连接条件
					[wehre 筛选条件]
					[gruop by 分组]
					[having 筛选条件]
					[order by 排序列表]
					
分类：
					内连接★：	inner
					外连接:  
					
										左外★：left [outer]
										右外★：right[outer]
										全外：full[outer]
					交叉连接； cross
					
*/

-- 等值连接
-- 案例1；查询员工名、部门名（调换位置）
select last_name,department_name from employees e
inner join departments d
on e.department_id = d.department_id;

-- 案例2：查询名字包含e的员工名和工种名(筛选)
select last_name ,job_title from employees e
inner join jobs j
on e.job_id = j.job_id;
where e.last_name like '%e%';

-- 案例3：查询部门个数>3的城市名和部门个数(分组+筛选)
select count(*),city from departments d
inner join locations l
on d.location_id = l.location_id
group by city
having count(*) >3;

-- 案例4：查询那个部门的部门员工个数>3的部门名和员工个数，并按个数降序(排序)
select count(*) ,department_name from employees e
inner join departments d
on e.department_id = d.department_id
GROUP BY d.department_name
having count(*) >3
order by count(*) desc;

-- 案例5：查询员工名、部门名、工种名，并按部门名降序

select last_name,department_name,job_title from employees e
inner join departments d on e.department_id = d.department_id
inner join jobs j on e.job_id = j.job_id
order by d.department_name desc;


-- 二、非等值连接
-- 案例1：查询员工的工资级别
select salary,grade_level from employees e
inner join job_grades j
on e.salary between j.lowest_sal and j.highest_sal;

-- 案例2：查询工资级别的个数>20的个数，并按工资级别降序
select count(*),salary,grade_level from  employees e
inner join job_grades j
on e.salary between j.lowest_sal and j.highest_sal
group by grade_level
having count(*) >20
order by grade_level desc;


-- 三、自连接
-- 案例：查询员工的名字、上级的名字
select e.last_name 员工名字,e.manager_id as 上级编号,m.employee_id as 上级员工编号,m.last_name as 上级名字 from employees e
inner join employees m
on e.manager_id =m.employee_id;



-- 四、外连接

/*
应用场景: 用于查询一个表中有，另一个表中没有的记录


特点：
	1.外连接的查询结果为主表中的所有记录
			如果从表中有和它匹配的，则显示匹配的值
			如果从表中没有和它匹配的，则显示null
			外连接查询结果=内连接结果 + 主表中有而从表中没有的记录
	2.左外连接 	left join 左边的是主表
		右外连接 right join	右边的是主表
	3.左外和右外交换两个表中的顺序，可以实现同样的效果
		
*/


-- 案例：查询哪个部门没有员工

-- 左外
select d.department_name,e.employee_id from departments d
left outer join employees e
on d.department_id =e.department_id
where e.employee_id is null;

-- 右外
select d.department_name,e.employee_id from  employees e
right outer join departments d
on e.department_id =d.department_id
where e.employee_id is null;
```



### 进阶7：子查询

```mysql
-- 进阶7：子查询------------------------------------------
/*
含义：
出现在其它语句的select语句，称为子查询或内查询
外部语句的查询语句，称为主查询或外查询

分类：
按子查询初夏你的位置：
						select后面：
												仅仅支持标量子查询
						from后面：
												支持表子查询
							where或having后面★：
														标量子查询(单行)√
														列子查询	（多行）√
														
														行子查询
								exists后面(相关子查询)
													表子查询
按结果集的行里书不同：
						标量子查询（结果集只有一行一列）
						列子查询（结果集只有一行多列）
						行子查询（结果集只有一行多列）
						表子查询（结果集一般为多行多列）
*/


-- 一、where或having后面
/*
1.标量子查询(单行子查询)
2.列子查询(多行子查询)
3.行子查询(多列多行)

特点：
①子查询放在小括号右侧
②子查询一般放在条件的右侧
③标量子查询，一般搭配着单行操作符使用
< 、>、<=、  >=、 = 、 <>

列子查询，一般搭配着多行操作符使用
in 、 any/some 、 all
*/


-- 案例1：谁的工资比Abel高？

-- ①查询Abel的工资
select salary from employees
where last_name ='Abel';

-- ②查询员工的工资，满足salary①结果
select * from employees
where salary >(select salary from employees
where last_name ='Abel');

-- 案例2：返回job_id与141号员工相同，salary比143号员工多的员工 姓名，job_id 和工资

-- ①查询job_id与141号员工相同
select job_id from employees where employee_id=141;

-- ②查询salary比143号员工多的员工
select salary from employees where employee_id =143;

-- ③查询员工的 姓名，job_id 和工资 要求job_id = ① 并且salary>②
select last_name,job_id,salary from employees
where job_id =(select job_id from employees where employee_id=141) and salary >(select salary from employees where employee_id =143);



-- 案例三：返回公司工资最少的员工的last_name,job_id和salary

-- ①查询公司的最低工资
select min(salary) from employees;

-- ②查询工资=①的员工的last_name,job_id和salary
select last_name,job_id,salary from employees
where salary = (
select min(salary) from employees);



-- 案例4：查询最低工资大于50号部门最低工资的部门id和其最低工资

-- ①查询50号部门最低工资
select min(salary) from employees 
where department_id = 50;

-- ②查询每个部门的最低工资
select min(salary),department_id from employees
group by department_id

-- ③筛选② 最低salary >①50号部门最低salary
select min(salary),department_id from employees
group by department_id
having min(salary) >(select min(salary) from employees 
where department_id = 50);

-- 列子查询(多行子查询)
-- 案例1；返回location_id是1400或1700的部门中的所有员工姓名

-- ①查询location_id是1400或1700的部门编号
select distinct department_id from departments
where location_id in(1400,1700);

-- ②查询员工姓名 要是部门编号是①列表中的某一个
select last_name from employees
where department_id in(select distinct department_id from departments
where location_id in(1400,1700));


-- 案列2：返回其它工种中比job_id为‘IT_PROG’部门任意工资低的员工的；工号、姓名、job_id、salary

-- ①查询job_id为‘IT_PROG’部门任意工资
select distinct salary from employees
where job_id ='IT_PROG';

-- ②查询员工的；工号、姓名、job_id、salary, salary<①的任意一个
select last_name,job_id,salary from employees
where salary < any(select distinct salary from employees
where job_id ='IT_PROG')   and  job_id <> 'IT_PROG';

-- 案例3：返回其它工种中比job_id为‘IT_PROG’部门所有工资低的员工的；工号、姓名、job_id、salary

select last_name,job_id,salary from employees
where salary < all(select distinct salary from employees
where job_id ='IT_PROG')   and  job_id <> 'IT_PROG';


-- 二、select后面
-- 案例1；查询每个部门的员工个数
select d.* ,(
select count(*) from employees e
where e.department_id = d.department_id)
from departments d;


-- 案例2；查询员工号=102的部门
select (select department_name from departments d
inner join employees e
on d.department_id =e.department_id
where e.employee_id =102) as 部门名;


-- 三、from后面

-- 案例：查询每个部门的平均工资的工资等级
select em.*,j.grade_level 
from (
			select avg(salary) as ag,department_id 
			from employees
				group by department_id) as em
inner join  job_grades j
on em.ag between j.lowest_sal and j.highest_sal;


-- 四、exists后面(相关子查询)
/*
语法；
exists(完整的查询语句)
结果：
1或0

*/

select exists(select employee_id from employees);


-- 子查询经典测试题
-- 查询工资最低的员工信息：last_name,salary
-- ①查询最低工资
select min(salary) from employees;
-- ②查询员工的信息：last_name,salary，并且salary=①
select last_name ,salary from employees
where salary =(select min(salary) from employees);


-- 查询平均工资最低的部门信息

#方式一
-- ①查询各部门的平均工资
 select avg(salary),department_id from employees
 group by department_id;

-- ②查询①结果上的最低平均工资
select min(ag) from 
( select avg(salary) as ag,department_id from employees 
 group by department_id) as emps;
 
--  ③查询各部门的平均工资，并且salary =②  得到department_id
 select avg(salary),department_id from employees
 group by department_id
 having avg(salary) = (select min(ag) from 
( select avg(salary) as ag,department_id from employees 
 group by department_id) as emps);
 
--  ④根据③得到的部门最低平均工资和id  关联表查询部门信息
 select * from departments
 where department_id = ( select department_id from employees
 group by department_id
 having avg(salary) = (select min(ag) from 
( select avg(salary) as ag,department_id from employees 
 group by department_id) as emps));
 
 
 
 #方式二
 -- ①查询各部门的平均工资并对salary进行升序,然后用limit查询第一条
 select avg(salary),department_id from employees
 group by department_id
 order by avg(salary)
 limit 1;
 
--  ②根据①查询部门信息
 select * from departments
 where department_id =(select department_id from employees
 group by department_id
 order by avg(salary)
 limit 1);

-- 查询平均工资最低的部门信息和该部门的平均工资
 -- ①查询各部门的平均工资并对salary进行升序,然后用limit查询第一条
 select avg(salary),department_id from employees
 group by department_id
 order by avg(salary)
 limit 1;
 
 
 --  ②根据①查询部门信息
 select * from departments
 where department_id =(select department_id from employees
 group by department_id
 order by avg(salary)
 limit 1);
 
--  ③在②的基础上把①当做一个字段查询
 select d.*,( select avg(salary)from employees
 group by department_id
 order by avg(salary)
 limit 1) as 平均工资  from departments d
 where department_id =(select department_id from employees
 group by department_id
 order by avg(salary)
 limit 1);

-- 查询平均工资最高的job信息
-- ①查询最高的平均工资
 select avg(salary),job_id from employees
 group by job_id
 order by avg(salary) desc
 limit 1;
 
--  ②查询job信息  job_id = ①的job_id
select * from jobs j
where j.job_id =( select job_id from employees
 group by job_id
 order by avg(salary) desc
 limit 1);
-- 查询平均工资高于公司平均的部门有哪些
-- ①查询部门的平均工资
 select avg(salary),department_id from employees
 group by department_id;
 
--  ②查询公司的平均工资
select avg(salary) from employees;

-- ③筛选①的结果集，满足平局工资>②
 select avg(salary),department_id from employees
 group by department_id
 having avg(salary) > (select avg(salary) from employees);

-- 查询出公司所有manager的详细信息
-- ①查询所有的manager_id
select distinct manager_id  from employees;

-- ②查询详细信息，满足manager_id=①
select * from employees
where manager_id =any(select distinct manager_id  from employees);

-- 各个部门中 最高工资中最低的那个部门的最低工资是多少 
-- 方式一
select MAX(salary),department_id from employees e
group by department_id
order by  MAX(salary) 
limit 1;

-- 查询平均工资最高的部门的manager的详细信息：last_name,department_id,email,salary
-- 方式一；
select  avg(salary),e.* from  employees e
group by department_id
order by avg(salary) desc
limit 1;
```

### 进阶8：分页查询

```mysql

-- 进阶8:分页查询----------------------------------
/* 应用场景:当腰显示的数据，一页显示不全，需要分页提交sql请求
语法；
					select 查询列表
					from 表1
					【inner type  join 表2
						on 连接条件
						where 筛选条件
						group by 分组字段
						having 分组后的筛选
						order by 排序的字段
						limit offset,size;】
						offset ：要显示条目的起始索引（起始索引从0开始）
						size 要显示的条目个数	
特点：

	1.起始条目索引从0开始
	
	2.limit子句放在查询语句的最后
	
	3.公式：select * from  表 limit （page-1）*sizePerPage,sizePerPage
	假如:
	每页显示条目数sizePerPage
	要显示的页数 page
	
	
*/

-- 案例1：查询前五条员工信息
select * from employees
limit 0,5;

select * from employees
limit 5;


-- 案例2:查询第11条---第25条
select * from employees
limit 10,15;


-- 案例3：有奖金的员工信息，并且工资较高的前10名显示出来
select * from employees
where commission_pct is not null
limit 10;

```



### 进阶9：联合查询

```mysql
-- 进阶9：联合查询--------------------------------------
/*
union 联合 合并：将多条查询语句的结果合并成一个结果
语法：
查询语句1
union
查询语句2
union
......

应用场景：
要查询的结果来自于多个表，且多个表没有直接的连接关系，但查询的信息一致时

特点:
1.要求多条查询语句的查询列数是一致的！
2.要求多条查询语句的查询的每一列的类型和顺序最好一致
3.nuion关键字默认去重，如果使用union all可以包含重复项
*/


-- 引入案例：查询部门编号>90或邮箱包含a的员工信息
select * from employees
where department_id >90 or email like '%a%';


select * from employees where department_id >90
union
select * from employees where  email like '%a%';
```



### 进阶10：DML语言

```mysql
/*
数据操作语言
插入：insert
修改：update
删除：delete
*/



-- 一、插入语句
/*
语法；
insert into 表名(列名.......)  values(值1,......);
*/

-- 1.插入的值类型要与列的类型一致或兼容
desc beauty;
select * from beauty;
insert into beauty(id,`name`,sex,borndate,phone,photo,boyfriend_id)
values(13,'张三','男','1992-12-12','11111111',null,1);

-- 2.不可以为null的列必须插入值，可以为null的列如何插入值？
desc beauty;
-- 方式一；
insert into beauty(id,`name`,sex,borndate,phone,photo,boyfriend_id)
values(15,'王五','男','1992-12-12','11111111',null,1);


-- 方式二：语序为空的字段可以不加
select * from beauty;
insert into beauty(id,`name`,sex,borndate,phone,boyfriend_id)
values(14,'李四','女','1997-12-12','11111111',2);

-- 3.列的顺序是否可以调换? 可以
insert into beauty(`name`,sex,id,phone) values('赵六','男',16,'120');

-- 4.列数和个数必须一致
insert into beauty(`name`,sex,id,phone) values('李七','男',17);
-- 5.可以省略列名，默认所有列，而且列的顺序和表的顺序一致
insert into beauty values(18,'张三','男','1992-12-12','11111111',null,1);


-- 方式二；
/*
语法；
insert into 表名
set 列名=值,列名=值,......
*/
insert into beauty
set id =19,`name` ='小红',phone='119';

-- 两种方式比较：

-- 1.方式一支持插入多行，方式二不支持
insert into beauty 
values(21,'张三','男','1992-12-12','11111111',null,1),
(22,'张三','男','1992-12-12','11111111',null,1),
(23,'张三','男','1992-12-12','11111111',null,1);


-- 2.方式一支持子查询，方式二不支持
inser into beauty(id,`name`,phone)
select id,boyName,'110' from boys
where id <3;  -- 执行不成功原有 两张表有id重复


-- 二、修改语句
/*
1.修改单标的记录★
语法：
update 表明
set 列=值,列=值,......
where 筛选条件；

2.修改多表的记录[补充]
语法:
sql92：
update 表1 别名,表2 别名
set 列=值......
wehre 连接条件
and 筛选条件;

sql99语法：
update 表1 别名
inner |left|right join 表2 别名
on 连接条件
set 列=值......
wehre 筛选条件;


*/

-- 案例1：修改beauty表中姓张的电话为'123';
select * from beauty;
update beauty
set phone='119'
where  `name` like '张%';
-- 案例2：修改boys表中的id号为2的名称为张飞，魅力值10;
update boys
set boyName ='张飞',userCP=10
where id =2;


-- 修改多表记录
-- 案例1：修改张无忌的女朋友的手机号为114
update boys bo
inner join beauty be
on bo.id=be.boyfriend_id
set phone='114'
where bo.boyName='张无忌';

-- 案例2：修改没有男朋友的女神的男朋友编号都为2
select * from beauty;

update beauty be
left join boys bo
on be.boyfriend_id =bo.id
set be.boyfriend_id=2
where be.id is null;



-- 三、删除语句
/*

方式一：delte
语法：
		1.单表的删除★
		delete from 表名  wehre 筛选条件;
		
		2.多表的删除[补充]
		sql92语法：
		delete 表1的别名,表2的别名
		from 表1  别名,表2 别名
		where 连接条件
		and 筛选条件;
		
		sql99语法：
		delete 表1的别名,表2的别名
		from 表1  别名
		inner |left|right join 表2 别名
			on 	 连接条件
		where  筛选条件;

方式二：truncate
语法：truncate table 表明；
*/

-- 单表的删除
-- 案例：删除手机号以9结尾的女神信息
delete from beauty
where phone like '%9';



-- 多表的删除
-- 案例：删除张无忌的女朋友的信息
delete be from beauty be
inner join boys bo
on be.boyfriend_id =bo.id




-- delete 和 truncate比较
/*
1.delete 可以加where 条件，truncate不能加
2.truncate删除，效率高一些
3.加入要删除的表中有自增列。如果用delete删除，在插入数据，自增列从断点开始
如果用truncate删除，在插入数据，自增列从1开始
4.truncate删除没有返回值，delete删除有返回值

5.truncate删除不能回滚，delete删除可以回滚
*/

```

### 进阶11：DDL语言

```mysql
-- DDL  
/*
数据库定义语言

一、库和表的管理
创建、修改、删除

二、表的管理
创建、修改、删除

创建：create 
修改：alter
删除：drop

*/

-- 一、库的管理
-- 1.库的创建
/*
语法：
create database [if  [not ] exist] 库名 [character 字符集];
*/
-- 案例：创建库books;
create database if not exists books ;

-- 库的修改
alter database books character set gbk;


-- 库的删除
drop database if exists books;


-- 
-- 二、表的管理
-- 1、表的创建★
/*
语法：
create table 表名（
				列名 列的类型 (长度) 约束,
				列名 列的类型 (长度) 约束,
				列名 列的类型 (长度) 约束,
				列名 列的类型 (长度) 约束,
				...
				列名 列的类型 (长度) 约束,
）
*/


-- 案例：创建book表
create table book(
				id int,  #编号
				bName varchar(20), #书名
				price double,  #价格
				anthorId int,  #作者id
				publiishDate datetime #出版日期
);
desc bool;

-- 案例：创建表author
create table author(
				it int,
				au_name varchar(20),
				nation varchar(20)
);



-- 2.表的修改
/*
alter table 表名 add|drop|modify|change  colum 列名【列类型 约束】;


*/

-- ①修改列名
alter table book change column publiishDate pubDate  datetime;

-- ②修改列的类型或约束
alter table book modify column pubDate  double;

-- ③添加新列
alter table book add column annual double;

-- ④删除列
alter table book drop column annual;

-- ⑤修改表名
alter table author rename to book_another;


-- 3.表的删除
drop table book_another;
show tables;



-- 4.表的复制

-- 1.只复制表的结构
create table copy1 like employees;

-- 2.复制表的结构和数据
create table copy2
select * from employees;

select * from copy2;


-- 3.只复制部分数据
create table copy3
select * from employees
 limit 3;
 
 
 
```

### 常见的数据类型

```mysql
-- 常见的数据类型
/*
数值型：
				整型
				小数：
								定点数
								浮点数

字符型：
					较短的文本：char 、varchar
					较长的文本：text、blob(较长的二进制数)
					
日期型：
*/

-- 一、整型
/*
分类：
		tinyint、  smallint 、  mediumint  、int/integer 、bigint
字节		1					2								3						4						8




*/

```

### 创建约束

```mysql

-- 常见约束
/*
not null  用于保证该字段的值不能为空
default   默认，用于保证该字段值有默认值
primary key   主键。用于保证该字段的值具有唯一性，并且非空
unique  唯一，用于保证该字段值具有唯一性，可以为空
check 检查约束{mysql中不支持}
FOREIGN KEY 外键

*/
```



### TCL（事务控制语言）

```mysql

-- TCL
/*
Transaction  Control  Language 事务控制语言

含义：通过一组逻辑操作单元（一组DML——sql语句），将数据从一种状态切换到另外一种状态

特点：
ACID）
原子性：要么都执行，要么都回滚
一致性：保证数据的状态操作前和操作后保持一致
隔离性：多个事务同时操作相同数据库的同一个数据时，一个事务的执行不受另外一个事务的干扰
持久性：一个事务一旦提交，则数据将持久化到本地，除非其他事务对其进行修改

事务的分类：
			隐式事务：没有明显的开启和结束事务的标志
						比如：insert、update、delete语句本身就是一个事务
			显示事务：具有明显的开启和结束事务的标志
					1、开启事务
						取消自动提交事务的功能

					2、编写事务的一组逻辑操作单元（多条sql语句）
							insert
							update
							delete

					3、提交事务或回滚事务

*/


drop table if exists account;

create table account(
				id int primary key auto_increment,
				username varchar(20),
				balance double
);

insert into account(username,balance)
values('张三',1000),('李四',1000);


-- 简单演示事务的使用步骤
-- 开启事务
set autocommit=0;
start transaction; -- 可选

-- 编写一组事务的语句
update account set balance='100' where username='张三';
update account set balance='1100' where username='李四';

-- 结束事务
rollback; -- 回滚

commit; -- 提交


select * from account;


/*事务的隔离级别:

事务并发问题如何发生？

	当多个事务同时操作同一个数据库的相同数据时
事务的并发问题有哪些？

	脏读：一个事务读取到了另外一个事务未提交的数据
	不可重复读：同一个事务中，多次读取到的数据不一致
	幻读：一个事务读取数据时，另外一个事务进行更新，导致第一个事务读取到了没有更新的数据
	
如何避免事务的并发问题？

	通过设置事务的隔离级别
	1、READ UNCOMMITTED
	2、READ COMMITTED 可以避免脏读
	3、REPEATABLE READ 可以避免脏读、不可重复读和一部分幻读
	4、SERIALIZABLE可以避免脏读、不可重复读和幻读
	
设置隔离级别：

	set session|global  transaction isolation level 隔离级别名;
查看隔离级别：

	select @@tx_isolation;
	*/
	
	
```



### 视图

```mysql
	
	
-- 视图
/*
含义：虚拟表，和普通表一样使用
mysql5.1出现的新特性，是通过表动态生成的数据
*/
-- 一、创建视图
/*
语法：
create view  视图名
as
查询语句;
*/


-- 1.查询姓名中包含a字符的员工姓名、部门名和工种信息
-- ①创建
create view myv1
as
select last_name,department_name,job_title from employees e
inner join departments d on e.department_id=d.department_id
inner join jobs j on e.job_id=j.job_id;

-- ②使用
select * from myv1 where last_name like '%a%';



-- 2.查询各部门的平均工资级别
-- ①创建视图查看每个部门的平均工资
create view myv2
as
select avg(salary) ag ,department_id from employees
group by department_id;

-- ②使用
select myv2.ag,g.grade_level from myv2
inner join job_grades g
on ag between g.lowest_sal and g.highest_sal;



-- 二、视图的修改
-- 方式一
/*
语法；
create or replace view 视图名
as 
查询语句；
*/

create or replace view myv3
as
select avg(salary),job_id from employees
group by job_id;



-- 方式二；
/*
语法；
alter view 视图名
as
查询语句;

*/
alter view myv3
as
select * from employees;

select * from myv3;


-- 三、删除视图
/*
yfja : drop view  视图名,视图名,......
*/
drop view myv1,myv2;


-- 四、查看视图
desc myv3;
show create view myv3;
```

### 存储过程

```mysql
-- 存储过程
/*
含义：一组经过预先编译的sql语句的集合
好处：
			1、提高了sql语句的重用性，减少了开发程序员的压力
			2、提高了效率
			3、减少了传输次数


创建语法：
create procedure  存储过程名(参数列表)
begin 

			存储过程体(一组合法的sql语句)

end

参数列表包含三部分：参数模式   参数名  参数类型


参数模式；
in:该参数只能作为输入 （该参数不能做返回值）
out：该参数只能作为输出（该参数只能做返回值）
inout：既能做输入又能做输出


如果存储过程只有一句话 begin  and  可以省略
存储过程体中的每条sql语句的结尾都必须加分号
存储过程的结尾可以使用delimiter 重新设置
语法：
delimiter 结束标记
案例：
delimiter $



调用语法；
call  存储过程名(实参列表)
*/


-- 1.空参列表
-- 案例:插入到 admin 表中五条记录
DELIMITER $
create procedure myp1()
begin 
insert into jobs values('1111','11111',1111,1111),
('2222','2222',222,112211),
('3333','333',333,333);
end $


-- 调用
call myp1() $





-- 2.创建带in模式参数的存储过程


create procedure myp2(in beautyName  varchar(20))
begin 
				select bo.* from boys bo
				right join beauty b on bo.id=b.boyfriend_id
				where b.`name`=beautyName;
end $


-- 调用
call myp2('柳岩')

```



### 函数

```mysql
-- 函数
/*
含义：一组预先编译好的sql语句的集合，理解成批处理语句
1.提高代码的重用性
2.简化操作
3.减少了编译次数并减少了和数据库服务器的连接次数，提高了效率


区别：
存储过程：可以有0个返回值，也可以有多个返回值，适合做批量插入，批量更新
函数：有且仅有一个返回，适合做批量数据后返回一个结果
*/


/*
创建语法：
create function 函数名(函数列表) returns  返回类型
begin

函数体
end


注意：参数列表包含两部分：
参数名  参数类型

函数体：肯定有return语句，如果没有回报错
如果return语句没有放在函数体的最后也不会报错，但不建议

return 值；
3.函数体仅有一句话 可以省略 begin end
4.使用delimiter语句设置结束标记





二
调用语法；
select  函数名(参数列表)
*/

-- 1、无参有返回
-- 案例：返回公司的员工个数
CREATE FUNCTION myf1() returns int
BEGIN
    declare c int default 0;  -- 定义局部变量
		select count(*) into c  -- 赋值
		from employees;
		return c;

END

-- 调用函数
select myf1()



-- 2.有参返回
-- 案例：根据员工名，返回他的工资

create function myf2(emoName varchar(20)) returns double 
begin
			set @sal=0; -- 定义用户变量
			select salary into  @sal  -- 赋值
			from employees
			where last_name =emoName;
			
			return @sal;
			
end


-- 调用函数
select myf2('kochhar')
```