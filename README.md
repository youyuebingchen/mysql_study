# mysql_study
sql_study 1、抗生/2、微生物检测
## 创建数据库
- create database python_test charset=utf8
- use python_test 
- select database()
- 创建数据表
   create table students(
    )

## 查询
- 查询所有字段
  - select * from table
-查询指定字段
  - select name,age from table
  - select table.name,table.age from table
- 使用as 给字段起别名
   - select name as 姓名,age as 年龄 from table
- 使用as 给表起名
  - select t.name,t.age from table as t :用t 代替table后必须用t.name不能用table.name
- 消除重复行
  - select distinct gender from table
## 条件查询
- 比较查询
  - select * from table where age > 18
  - select * from table where age < 18
  - select * from table where age = 18
- 逻辑运算符
  - and ：select * from table where age > 18 and age<28
  - or : select * from table where age >18 or gender =女
  - not : select * from table where not (age >18 or gender =女) :注意not 在哪里表示否定哪个条件，比如不加括号只否定第一个条件年龄。
- 模糊查询
   - like 
      - select name from table where name like '%小%'  % 号替换一个或者多个
      - select name from table where name like '__'    _号代表替换一个 
      - select name from table where name like '__%' 找出包含两个以上的
   - rlike 正则查询
      - select name from table where name rlike '^周.*伦$'
- 范围查询
   - 不连续查询
      - select name,age from table where age in (12,18,34) 不连续查询。
      - select name,age from table where age not in (12,18,34) 不在。
   - 连续查询
      - select name,age from table where age between 18 and 34
      - select name,age from table where age not between 18 and 34; not betwee 是一个整体
      - select name,age from table where not age between 18 and 34
 - 空判断
   - a = None表示a没有指向任何空间而a = ''表示数据为空但是有空间a指向该空间
   - select * from table where height is null ; 提取为空的
   - select * from table height is not null
 - 排序
   - order by 字段
      - select * from stable where (age between 18 and 34) and gender = 1 order by age;
      - select * from stable where (age between 18 and 34) and gender = 1 order by age asc; asc升序
      - select * from stable where (age between 18 and 34) and gender = 1 order by age desc; desc降序
   - oder by 多个字段 先按age age相同按height age和heigt都相同按id
      - select * from stable where (age between 18 and 34) and gender = 1 order by age desc，height desc,id desc
      - select * from stable order by age desc，height desc,id desc
 - 聚合函数
   - 总数 count()
      - select count(*) from table where gender = 1
      - select count(*) as 男性人数 from table where gender = 1
   - 最大值 max()
      - select max(age) from table where gender = 1
   - 最小值 min()
      - select min(age) from table where gender = 1
   - 求和 sum()
      - select sum(age) from table
   - 平均值
      - select ave(age) from table where gender = 1
      - select sum(age)/count(*) from table where gender = 1
   - 四舍五入保留一位小数点 round(12.34,1) c语言在底层小数点的时候都是约等于很多解释器都是用c，银行的里一定不会用约等于，而是直接扩大多少倍取时在除以倍数
      - select round(sum(age)/count(*),2) from table where gender = 1
 - 分组 
   - group by 要分组后每一组都一样的，分组一定要和聚合函数一块用材有意义
      - select gender,avg(age) from student group by gender
      - select gender ,count(*) from table where gender = 1 group by gender
   - group_concat(name) 将分组的成员加到一块显示
      - select gender,group_concat(name) from student group by gender
      - select gender,group_concat(name,"-",age,' ',id) from student group by gender 将name age id 加到一块显示
 
      
      
      
      
      
      
      
