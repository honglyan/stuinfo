# 基于关系型数据库的学生信息管理系统

## 系统概述
  学生信息管理系统，可用于学校等机构的学生信息管理，查询，更新与维护，使用方便，易用性强，HTML界面清晰明了。该软件用 C 和 HTML 语言编写，用MySQL数据库作为后台的数据库进行信息的存储，用 SQL 语句完成学生学籍信息的添加， 查询，修改，删除的操作以及成绩的录入，修改，删除等。前端使用 HTML5 页面与用户进行交互, ODBC 使用 CGI 与后台 SQL 数据库的连接。MySQL 数据库高效安全，两者结合可相互利用各自的优势。
系统主要功能：对学生的信息进行管理，如：插入学生信息、删除学生信息 、修改学生信息、查询学生信息。
## 使用工具
 - [x] ubutun   
 - [x] mysql  
 - [x] c语言  
## 数据库设计  
本学生信息管理系统一共设计了4个表，分别为： 
* 学校表school  
* 课程表class 
* 学生信息表information  
* 成绩表score  

### 1.学校表school的设计。 

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
学校代号 |  sid | int(4) | √ |   |   自动增加|
学校名称 | sname | varchar(10) | |  |不为空 |
系   名 | sdept | varchar(10) |  |  |不为空 |
专   业 | smajor |varchar(10) |  |  |  不为空|
班   级 |sclass | varchar(10) |  |  | 不为空| 

代码如下：
```sql
create table school(
  sid int(4) primary key auto_increment check(sid>0) ,
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
课程成绩 | cirdet | double(1,1) |  | 0.0 | 不能为空，默认值为0.0，只能为0.0-10.0之间的一位小数|

代码如下：
```sql
create table class(
  cno varchar(10) primary key,
  cname varchar(10)not null,
  cirdet double(1,1) not null default 0.0 check(cirdet>=0 and cirdet<10) 
)DEFAULT CHARSET=utf8;
```


### 3.学生信息表information的设计。 

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
学生学号 |  sno | int(4) | √ |   |   大于0|
学生姓名 | name | varchar(8) | |  |不为空 |
性别 | sex | char(1) |  |  |只能是男或女|
出生日期 | birthday |date |  | 默认值为1990-1-1 |  不为空|
学校代号 |sid | int（4） |  |  | 外键，来自school表| 

代码如下：
```sql
create table information(
  sno int(4) primary key check(sno>0),
  name varchar(8) not null,
  sex char(1)not null check(sex in('男','女')),
  birthday date default"1990-1-1",
  sid int(4),
  foreign key(sid) references school(sid)
)DEFAULT CHARSET=utf8;
```

### 4.成绩表score的设计。 

中文名称 | 属性名称 | 字段类型 | 主键 | 默认值 | 其他   
--------|--------|--------|--------|--------|--------|
学生 |
学生学号 | sname | varchar(10) | √|  |不为空，外键，来自information|
课程号 | sdept | varchar(10) | √ |  |不为空 ，外键，来自class|
成绩 | smajor |varchar(10) |  |  |  默认值为0.0|

代码如下：
```sql
create table score(
  sno int(4),
  cno varchar(10),
  cgrade double(3,2) default 0,
  foreign key(sno) references information(sno),
  foreign key(cno) references class(cno),
  primary key(sno,cno)
)DEFAULT CHARSET=utf8;
```
