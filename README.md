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
