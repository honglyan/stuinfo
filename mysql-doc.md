# 2017年6月15日 记录
## Ubuntu 安装SQL数据库  
### 步骤如下:
##### 1. 更新源  
用vim打开源列表文件。  
> sudo vim /etc/apt/sources.list  

将下面的源粘贴到源列表里。  
> deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse   
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse    
##测试版源  
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse  
#源码  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse  
##测试版源  
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse  
#Canonical 合作伙伴和附加  
deb http://archive.canonical.com/ubuntu/ xenial partner  
deb http://extras.ubuntu.com/ubuntu/ xenial main  

**注意**:  
如果在vim里面右键不可以黏贴，进行如下操作：  
> vim .vimrc  

然后进入第三行，将第18行mouse=“a”的删除掉，关闭保存后源列表文件。  

##### 2. 安装mysql和Apache  
>sudo apt-get update  
sudo apt-get install tasksel  
sudo tasksel   

在之后会出现一个界面进行选择，向下悬着LAMP Server（Linux Apache Mysql php）,按空格键选择/删除，然后按Tab键回车完成选择。  
然后输入需要设置的密码，我的密码为：123456.  

##### 3. 验证是否安装成功  
>mysql -u root -p  

回车后输入密码即可。  
**到这里数据库就安装完成可以使用了。**  

之后我又安装了一个mysql的图形化界面。  
##### 4. workbench 安装
>sudo apt-get install mysql-workbench

## MySQL数据库的使用
1. 创建数据库  
>注意：创建数据库之前要先连接Mysql服务器  
命令：create database <数据库名>  
例1：建立一个名为xhkdb的数据库 mysql> create database xhkdb;    

2. 显示数据库
>命令：show databases （注意：最后有个s） mysql> show databases;  
注意：为了不再显示的时候乱码，要修改数据库默认编码  

3. 删除数据库
>命令：drop database <数据库名> 例如：删除名为 xhkdb的数据库 mysql> drop database xhkdb;  
例子1：删除一个已经确定存在的数据库 mysql> drop database drop_database; Query OK, 0 rows affected (0.00 sec) 

4. 使用数据库  
>命令： use <数据库名>  
例如：如果xhkdb数据库存在，尝试存取它： mysql> use xhkdb; 屏幕提示：Database changed  

5. 创建数据表  
> 命令：create table <表名> ( <字段名1> <类型1> [,..<字段名n> <类型n>]);

6. 增加字段  
>命令：alter table 表名 add字段 类型 其他;  
例如：在表MyClass中添加了一个字段passtest，类型为int(4)，默认值为0    
mysql> alter table MyClass add passtest int(4) default '0'    

7. 修改字段  
>mysql> ALTER TABLE table_name ADD field_name field_type;  
修改原字段名称及类型： mysql> ALTER TABLE table_name CHANGE old_field_name new_field_name field_type;  
删除字段： MySQL ALTER TABLE table_name DROP field_name; 5.9 修改表名  
命令：rename table 原表名 to 新表名;    
例如：在表MyClass名字更改为YouClass mysql> rename table MyClass to YouClass;  
当你执行 RENAME 时，你不能有任何锁定的表或活动的事务。你同样也必须有对原初表的 ALTER 和 DROP 权限，以及对新表的 CREATE 和 INSERT 权限。  
如果在多表更名中，MySQL 遭遇到任何错误，它将对所有被更名的表进行倒退更名，将每件事物退回到最初状态。  
ENAME TABLE 在 MySQL 3.23.23 中被加入。  

