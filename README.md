# mysql_study
sql_study 1、抗生/2、微生物检测
<br>sql 语句虽然结果都能出来，但是对于大量数据时时间有很大差别
<br> 在查询之前一定要观察数据，防止重复查询浪费时间，
<hr>
<br>例子：使用mimic数据库，我在已知icustat_id的情况先查询admission里病人的信息时，需要先通过icustat_id来查询charevet表里的subject_id使用inner join但是这样查出来的subjec_id是大量重复的，如果此时再用其查询admission里病人的信息会做大量的重复工作，所以，一定要先用distinct去除重复，然后再查询。
## 创建数据库
- create database python_test charset=utf8
- use python_test 
- select database()
- 创建数据表
   -create table students()
- insert into goods values(0,"a","man","18")
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
   - 平均值 avg（）
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
   - having 是对结果的一个判断
      - select gender,group_concat(name),avg(age) from table group by gender having avg(age)>30
      - select gender,group_concat(name) from table group by gender having count(*)>2
 - 分页
   - limit limit 一定是放在最后的位置
      - select * from table where gender = 1 limit 5 最大选择5
      - select * from table limit 1,5 第一个表示从哪条数据开始，第二个表示条数 limit(n-1)*每页的个数，n代表多少页
 - 连接查询
   - inner join ... on 交集，大家都有的信息关联，交换顺序可改变显示顺序
      - select * from table_a inner join classes on table_b on table_a.cls = classes.id 
      - select table_a.*,table_b.name from table_a inner join  table_b on table_a.cls = table.id
      - select a.*,b.name from table_a as a inner join table_b as b on a.cls = b.id 
   - left join 左连接，以左边的表为基准如果能找到就填写，找不到就填NULL
      - select * from table_a as a left join table_b as b on a.cls = b.id
   - right join 类似于左连接，但是没有，基本上只使用左连接。
   - 查询没有数据的信息 having是对结果的一个操作。
      - select * from table_a as a left join table_b as b on a.cls = b.id having b.id = null
 - 自关联查询 自关联表用一张表表示所有信息
   - 一张表里的一个字段用到同一个表里的另一个字段，查询时将同一张表分别命名为a,b再对a,b操作。 
      - select * from table_a as a inner join table_a as b on a.id = b.pid having a.province = '32011'
 - 子查询 查询里嵌套一个查询
   - select * from table where height = (select max(height) from table)
 - 连接查询和子查询并用。
   - select * from （select cate_name,max(price)）as g_new left join goods as g on g_new,cat_name=g.cate_name and g_new.price = g.price
## 视图
通俗讲视图就是一条select语句执行后返回的结果集，视图是对若干张基本表的引用，相当一张虚拟的表，是查询语句的结果，不存储具体的数据，基本表发生改变，视图也会跟着发生改变。往往用在查数据，而不用来修改数据的。不能进行修改数据。
- 视图作用
   - 提高了重用性
   - 对数据库重构，却不影响程序的运行
   - 提高了安管性能，可对不同的用户
   - 让数据更加清晰
- 创建视图 将select语句的查询内容作为一张视图 v_goods_info
   - create view v_goods_info as select * from ..
- 查看视图
   - show tables
- 使用视图
   - select * from v_table
- 删除视图
   - drop view 视图名
      
