### MySQL常用语法汇总

```
select database();
use mysql_db1;
show tables ;
desc course;
show create table course;
```



#### 函数

##### 字符串函数

- concat(s1, s2, ..., sn) 字符串拼接
- lower(str)  小写转换
- upper(str) 大写转换
- lapd（str, n ,pad)  左填充，用字符串pad对str的左边进行填充，达到n个字符长度
- rpad(str, n, pad)
- trim(str) 去掉字符串头部和尾部的空格
- substring(str, start, len) 返回从字符串str从start位置起的len个长度的字符串



##### 数值函数

- ceil(x) 向上取整
- floor(x) 向下取整
- mod(x, y) 返回x/y的模（取余）
- rand() 返回0-1内的随机数
- round(x, y) 求参数x的四舍五入的值，保留y位小数



##### 日期函数

- curdate() 返回当前日期
- curtime() 返回当前时间
- now() 返回当前日期和时间
- year(date) 获取指定date的年份 ---如year(now())
- month(date) 获取指定date的月份
- day(date)  获取指定date 的日期
- date_add(date, interval expr type) 返回一个日期/时间值加上一个时间间隔expr后的时间值
  - 如 select date_add(now(), interval 70 year);
- datediff(date1, date2) 返回起始时间date1 和 结束时间date2 之间的天数
  - 如 select datediff('2021-10-01', '2021-12-01');



##### 流程函数

- if(value, t, f) 如果value为true，则返回t，否则返回f
  - select if(false, 'ok', 'Error');
- ifnull(value1, value2) 如果value1不为空，返回value1，否则返回value2
  - select ifnull("ok", 'default');
- case when [vall] then [res1] ...else [default] end; 如果vall为true，返回res1，否则返回default默认值
  - select name (case gender when "man" then "男生" when "women" then "女生" else "未知性别" end) from table;
- case [expr] when [vall] then [res1] ... else [default] end; 如果expr的值等于vall,返回res1，否则返回default默认值



### 约束

##### 基础约束

```
not null
# 非空约束

unique
# 唯一约束

primary key
# 主键约束

foreign key
# 外键约束

default
# 默认约束

check
# 检查约束，保证字段值满足某一个条件
```



##### 外键约束

```
# 添加外键
create table 表名(
	字段名		数据类型，
	...
	[constraint] [外键名称] foreign key (外键字段名) references 主表（主表列名)；
	
alter table 表名 add constraint 外键名称 foreign key (外键字段名) references 主表 (主表列名)；

例子：
alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references dept(id);

# 删除外键
alter table 表名 drop foreign key 外键名称；

例子：
alter table emp drop foreign key fk_emp_dept_id;
```



##### 删除/更新行为

| 行为        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| no action   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。与restrict一致，默认行为。 |
| restrict    | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。 (与 NO ACTION 一致) 默认行为 |
| cascade     | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录。 |
| set null    | 当在父表中删除对应记录是，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null |
| set default | 父表有变更时，子表将外键列设置成一个默认的值                 |

```
# cascade
alter table 表名 add constraint 外键名称 foreign key (外键字段) references 主表名 (主表字段名) on update cascade on delete cascade;

例子：
alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references
dept(id) on update cascade on delete cascade ;

# SET NULL

列子：
alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references
dept(id) on update set null on delete set null ;
```



##### 多表查询

- 内连接：相当于查询A、B交集部分数据

```
# 隐式内连接
select 字段列表 from 表1， 表2 where 条件...；
例子：
select emp.name , dept.name from emp , dept where emp.dept_id = dept.id ;

# 显示内连接
select 字段列表 from 表1 [inner] join 表2 on 连接条件 ... ,
on是去除笛卡尔乘积
例子：
select e.name,d.name from emp e , dept d where e.dept_id = d.id;
```



- 左外连接：查询左表所有数据，以及两张表交集部分数据

```
select 字段列表 from 表1 left [outer] join 表2 on 条件...；
```



- 右外连接：查询右表所有数据，以及两张表交集部分数据

```
select 字段列表 from 表1 right [outer] join 表2 on 条件...；
```



- 自连接：当前表与自身的连接查询，自连接必须使用表别名

```
SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件 ... ;
# 对于自连接查询，可以是内连接查询，也可以是外连接查询

例子：
select a.name '员工', b.name '领导' from emp a left join emp b on a.managerid =
b.id;
```



##### 列子查询

| 操作符 | 描述                                   |
| ------ | -------------------------------------- |
| IN     | 在指定的集合范围之内，多选一           |
| NOT IN | 不在指定的集合范围之内                 |
| ANY    | 子查询返回列表中，有任意一个满足即可   |
| SOME   | 与any等同，使用some的地方都可以使用any |
| ALL    | 子查询返回列表的所有制都必须满足       |

```
# IN
select * from emp where dept_id in (select id from dept where name = '销售部' or
name = '市场部');

# ALL
select * from emp where salary > all ( select salary from emp where dept_id =
(select id from dept where name = '财务部') );

# ANY
select * from emp where salary > any ( select salary from emp where dept_id =
(select id from dept where name = '研发部') );
```

