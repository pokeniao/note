---
日期: 2024-03-17
tags:
  - 基本语法
  - SQL
  - 快速开始
---
# 基本指令
## 数据库（DDL）
1. 创建数据库：
	Create database `[IF NOT EXISTS]` `<数据库名>` `[[default]character set <字符集名>]` `[[default]collate <校对规则名>]`
>[!tip]- 参数
>**IF NOT EXISTS：**在创建数据库之前进行判断，只有该数据库目前尚不存在时才能执行操作。
>**character set ：**默认utf8
>**collate：** 默认utf8_general_ci[不区分大小写] 常用utf8_bin[区分大小写]

2. 显示数据库：show database
3. 显示数据库创建语句：show create database `<数据库名>`
4. 数据库删除语句： drop database `[IF EXISTS]` `<数据库名>`
5. 备份数据库/备份多个数据库：mysqldump -u `用户名` -p -B `数据库1` `数据库2`  > `路径\文件名.sql`
6. 单个数据库，单表备份：mysqldump -u `用户名` -p -B `数据库` -t `表名 > 路径\文件名.sql`
7. 恢复数据库：Source `文件名.sql`
面试问题：[[mysql面试题#1.表没有主键可以吗？可以不设置主键吗]]
## 表的增删改查（CURD）
1. **创建表**：
```
Create Table table_Name
(
	id bigint primary key,
	name varchar(255) Not Null,
	update_time datetime(3) Default Null
)Engine=Innodb CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
```
>[!tip]- 参数
>**Engine：** [[mysql底层进阶#存储引擎|存储引擎]] 默认[[mysql底层进阶#Innodb|Innodb]]
>**charset：** 字符集，不指定为所在数据库字符集
>**collate：** 校对规则，不指定为所在数据库校验规则
相关字段约束：[[mysql#约束]]
2. **增加表** (DML)
	- insert into `<表名>` values(`插入表的列对应的值`)
	- insert into `<表名>` `(列1,列2)` values(` 插入表的列对应的值 `)
	- insert into `<表名>` values(`插入表的列对应的值`),(`插入表的列对应的值`) 
	- insert into <表> select语法
3. **删除表** (DML) ^8ff1f1
	- 删除表数据： delete from `<表名>` where `条件`
	- 删除表：drop table `<表名>`
4. **修改表** (DML)
	-  修改表行数据：update `<表名>` set `列` = `值` where `条件`
	-  修改表列数据：
		- 给表==添加列==: Alter table `<表>` add `属性名` `属性类型`
		- 给表==删除列==: Alter table `<表>` drop `属性名`
		- 给表==修改列==属性类型或约束: Alter table <表> modify `属性名` `改后属性类型` `[改后约束]`
		- 给表===修改列==属性名: Alter table `<表>` change `属性名` `改后属性名` `改后属性类型`
5. **查询表** (DQL)
	 - select `字段列表` from `表列表` where `查询条件` group by `分组字段列表` having `分组后条件` order by `排序方式` limit `分页参数`
>[!tip]- 关键字
>**distinct:** 去除重复  select distinct `查询` from `表` where `查询条件`
>**聚合函数(count,max,min,avg,sum):** 使用在字段列表
>**条件:** 
>>[!NOTE]- **条件:**
>>  1. `<>` 或 `!=` 不等于
>>  2. `In(...)`  在之后的列表中的值多选一
>>  3. `Like 占位符` 模糊查询==(`_` 匹配单个字符, `% ` 匹配任意字符)==
>>  4. `Is NULL` 为null
>>  5. `NOT` 或 `!` 为非
>>  6. `or ` 或 `and` 或 `&&` 或 `||`
>
>**排序:** `ASC` 升序(默认) `DESC` 降序
>**limit:** limit `起始索引` `展示条数` ^4f65d3

- [[mysql#多表查询]]
# mysql函数
## 字符串函数

| 函数                       | 功能                                |
| ------------------------ | --------------------------------- |
| concat(S1,S2,S3)         | 字符串拼接                             |
| lower(str)               | 字符串变小写                            |
| upper(str)               | 字符串变大写                            |
| lpad(str,n,pad)          | 左填充,用字符串pad对str从左边开始,直到字符串str长度为n |
| rpad(str,n,pad)          | 右填充,用字符串pad对str从左边开始,直到字符串str长度为n |
| trim(str)                | 去掉头尾空格                            |
| substring(str,start,len) | 截取字符串,截取str从start开始长度为len         |
## 数值函数

| 函数         | 功能                            | 举例                                    |
| ---------- | ----------------------------- | ------------------------------------- |
| ceil(X)    | 向上取整                          | ceil(1.1)=2                           |
| FLOOR(x)   | 向下取整                          | floor(1.9)=1                          |
| MOD(X,y)   | 返回（x/y）的模                     | MOD(15,10)=5<br>MOD(3,4)=3            |
| Rand()     | 返回0~1的随机数                     | Rand()\*10是0~10之间的随机数                 |
| ROUND(X,y) | 求参数x的四舍五入，暴留y位小数              | round(2.345,2)=2.35                   |
| TRUNC（X,Y） | 将x截取y位==(当y为正截取小数，当y为负截取整数)== | Trunc(15.01,1)=15.0 Trunc(15.01,-1)=1 |
[[mysql例题#通过数据库来生成，一个六位数的随机验证码]]

## 日期函数

| 函数                                      | 功能                           | 举例                                     |
| --------------------------------------- | ---------------------------- | -------------------------------------- |
| curdate()                               | 返回当前==日期==                   |                                        |
| curtime()                               | 返回当前==时间==                   |                                        |
| NOW()                                   | 返回当期==日期和时间==                |                                        |
| YEAR(date)                              | 获得指定date的==年份==              |                                        |
| Month(date)                             | 获得指定date的==月份==              |                                        |
| DAY(date)                               | 获得指定date的==日期==              |                                        |
| date_add(`date`,interval `expr` `type`) | 返回==日期/时间==加上一个时间间隔expr后的时间值 | date_add(now(),interval 70 day)今天的70天后 |
| DateDIFF(date1,date2)                   | 返回date1和date2之间的天数           | (date1-date2)会得到负数                     |
## 流程函数

| 函数                                                        | 功能                                   |
| --------------------------------------------------------- | ------------------------------------ |
| if(value,t,f)                                             | 如果value为true，返回t，否者返回f               |
| ifnull(value1,value2)                                     | 如果value1不为null,返回value1,否者value2     |
| case when `val` then `res1` `...`else `default` end       | 如果当val为true,返回res1 ...，否者返回default   |
| case `expr`when `val` then `res1` `...`else `default` end | 如果当expr等于val,返回res1 ...，否者返回default2 |
# 约束

| 约束           | 描述                              | 关键字           | 举例                                          |
| ------------ | ------------------------------- | ------------- | ------------------------------------------- |
| 主键约束         | 唯一，非空                           | primary key   |                                             |
| 默认约束         | 没有指定改字段的值，采用默认约束                | default       | sex varchar(6) default 'man'                |
| 唯一约束         | 唯一                              | unique        |                                             |
| 外键约束         | 让两张表建立联系,==外键==对应==其他==表的==主键== | foreign key   | foreign key `(外键字段)` references `主表名(主表列名)` |
| 非空约束         | 非空                              | Not null      |                                             |
| 检查约束（8.0.16） | 检查是否满足条件                        | check         | sex varchar(6) check(sex in('man','woman')) |
| 自动增长         | 自动增长                            | auto_incrment |                                             |
| 注释           | 添加注释                            | comment       | sex varchar(6) comment '性别'                 |


# 多表查询
## 连接
1. 内连接：如果没有设置内连条件 `表1`中的一行对应`表2`的全部行
	- 隐式内连接 select `字段列表` from `表1`，`表2`
	- 显式外连接 select `字段列表` from `表1` \[INNER\] join `表2` on 连接条件；
2. 外连接 : 保存左或右全部数据
	- 左外 select `字段列表` from `表1` left \[outer\] join `表2` on 连接条件；
	- 右外 select `字段列表` from `表1` right \[outer\] join `表2` on 连接条件；
3. 自连接：自己连接自己
	- select `字段列表` from `表1` as`别名1` right join `表2` as `别名2` on 连接条件；
例题：[[mysql例题#update多行数据关联]]
## 查询
1. 联合查询：查询到的结果一同展示出 (all关键字是不去重)
	- select `字段` from `表A` `...` union\[all\]  select `字段` from `表B` `...`
2. 子查询：在语句中嵌套select ，子查询==外部语句==可以是==增删改查任何一个==
	- 语句举例： select * from `表` where column =(select column from `表2`)
	- 子查询位置：` where` 之后 `from`之后 `select` 之后
	1. 标量子查询
		- 符号可以有： `>` `=` `<` 等
	2. 列只查询
		- 符号可以有：`IN` `NOT IN` `Any` `some` `all`

> [!NOTE]- 符号用法介
> **IN:** 范围内选一
> **NOT IN:** 不在范围
> **ANY:** 有一个满足即可 与`some`用法相同
>	例题：select \* from `emp` where `salary` > any(select `salary` from `emp2`)
> **ALL:** 必须全部满足
> 	例题：select \* from `emp` where `salary` > all(select `salary` from `emp2`)


子查询例题：[[mysql例题#子查询和连接]]



# 索引
索引[[mysql底层进阶#索引]]

**索引的分类**

| 分类   | 特点  | 关键字      |
| ---- | --- | -------- |
| 主键索引 | 1个  | primary  |
| 唯一索引 | 多个  | unique   |
| 常规索引 | 多个  |          |
| 全文索引 | 多个  | fulltext |

索引存储形式：（Innodb）
聚集索引:
二级索引:

