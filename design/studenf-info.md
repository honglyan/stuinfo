# 基于关系型数据库的学生信息管理系统

## 系统概述
  学生信息管理系统，可用于学校等机构的学生信息管理，查询，更新与维护，使用方便，易用性强，HTML界面清晰明了。该软件用 C 和 HTML 语言编写，用MySQL数据库作为后台的数据库进行信息的存储，用 SQL 语句完成学生学籍信息的添加， 查询，修改，删除的操作以及成绩的录入，修改，删除等。前端使用 HTML5 页面与用户进行交互, ODBC 使用 CGI 与后台 SQL 数据库的连接。MySQL 数据库高效安全，两者结合可相互利用各自的优势。  
  
  系统主要功能：对学生的信息进行管理，如：插入学生信息、删除学生信息 、修改学生信息、查询学生信息。
## 使用工具
 - [x] ubutun   
 - [x] mysql  
 - [x] c语言  
 - [x] atom   
## 数据库设计  
本学生信息管理系统一共设计了5个表，分别为： 
* 学校表school  
* 课程表class 
* 学生信息表information  
* 成绩表score  
* 教师表teacher

### 1.学校表school的设计。 

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
学校代号 |  sid | int(4） | √ |   |   自动增加|
学校名称 | sname | varchar(10) | |  |不为空 |
系   名 | sdept | varchar(10) |  |  |不为空 |
专   业 | smajor |varchar(10) |  |  |  不为空|
班   级 |sclass | varchar(8) |  |  | 不为空| 

代码如下：
```sql
create table school(
  sid int(4) primary key auto_increment ,
  sname varchar(10) not null,
  sdept varchar(10) not null,
  smajor varchar(10) not null,
  sclass varchar(8) not null
)DEFAULT CHARSET=utf8;
```
 
### 2. 课程表class的设计。  

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
课程号 |  cno | varchar(10) | √ |  ||
课程名称 | cname | varchar(10) | |  |不为空 |
课程成绩 | cirdet | double(2,1) |  | 0.0 | 不能为空，默认值为0.0，只能为0.0-10.0之间的一位小数|

代码如下：
```sql
create table class(
  cno varchar(10) primary key,
  cname varchar(10)not null,
  cirdet double(2,1) not null default 0.0 check(cirdet>=0 and cirdet<10) 
)DEFAULT CHARSET=utf8;
```


### 3.学生信息表information的设计。 

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
学生学号 |  sno | char(12) | √ |   |   大于0|
学生姓名 | name | varchar(8) | |  |不为空 |
性别 | sex | char(4) |  |  |只能是男或女|
出生日期 | birthday |date |  | 默认值为1990-1-1 |  不为空|
学校代号 |sid | int（4） |  |  | 外键，来自school表| 
删除标记|sel | int |  |  | 默认值为'0'| 

代码如下：
```sql
create table information(
  sno char(12) primary key check(sno>0),
  name varchar(8) not null,
  sex char(4)not null check(sex in('男','女')),
  birthday date default '1990-1-1',
  sid int(4),
  sel int default '0',
  foreign key(sid) references school(sid)
)DEFAULT CHARSET=utf8;
```

### 4.成绩表score的设计。 

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
学生 |
学生学号 | sname | char(12) | √|  |不为空，外键，来自information|
课程号 | sdept | varchar(10) | √ |  |不为空 ，外键，来自class|
成绩 | smajor |double(4,1) |  |  |  默认值为0.0，值为0到100之间|

代码如下：
```sql
create table score(
  sno char(12),
  cno varchar(10),
  cgrade double(4,1) default 0 check(cgrade>=0 and cgrade<=100),
  foreign key(sno) references information(sno),
  foreign key(cno) references class(cno),
  primary key(sno,cno)
)DEFAULT CHARSET=utf8;
```


### 5.教师表teacher的设计。 

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
顺序号 | id |int | |  ||
教师号 | tno | char(12) | √|  ||

代码如下：
```sql
create table teacher(
  id int primary key,
  tno char(12)
)DEFAULT CHARSET=utf8;
```

### 6.创建视图。 
在本设计中我创建两个视图用于查询：
1. 一个是stuinfo，用于存储选课了的学生的所有信息.
```sql
create view stuinfo as
select information.sno,name, sex,birthday,school.sid,sname,sdept,smajor,sclass,class.cno,cname,cirdet,cgrade
from information,school,score,class
where information.sno=score.sno and information.sid=school.sid and class.cno=score.cno
```
2. 一个是stuall，用于存储学生的所有信息。
```sql
create view stuall as
select information.sno,name, sex,birthday,school.sid,sname,sdept,smajor,sclass
from information,school
where information.sid=school.sid
```
