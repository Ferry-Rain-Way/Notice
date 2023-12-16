---
title: 一台电脑安装多个mysql
tags:
  - mysql
  - 配置
categories:
  - 412C-数据库
description: 进入文章
---

---


##### 0.重点说明
【0.1】操作:
如果电脑以前安装过Mysql,且<font color=red>配置了Mysql的环境变量,就先把Mysql的环境变量给删除了(可以先用记事本临时保存一下)</font>,不确定是否配置过,就检查一下环境变量中的Path里面

重复:如果配置了环境变量一定要删除了!!!
	最后是可以配置回来的,但安装过程中一定不要存在

【0.2】说明:(<font color="#3271ae">不想看可跳过</font>)
在同时配置多个mysql时,需要去执行mysql的一些安装命令,这些命令会在对应的要安装的Mysql的`Mysql安装根目录\bin\`文件夹下执行,以保证X版本执行的安装命令是作用于X,Y版本执行的安装命令是作用于Y。

如果在之前配置过了环境变量,环境变量中配置的是A版本的`Mysql安装根目录\bin\`,而我们都知道,环境变量一旦配置好,就是作用于全局的,也就是说如果配置了环境变量,<font color="#3271ae">即使在X版本的`Mysql安装根目录\bin\`下,执行安装命令,所配置的路径也不会是X的,而是A的,这样就会出问题。</font>


##### 1.下载地址
[MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/)

##### 2.版本选择

- 选择需要的版本号与操作系统(本文以Windows为例)

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412C-A1A-MYSQL-download_url.png" style="zoom: 80%;" />

- 跳转到新页面,找到下面的"链接",点击即可下载
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412C-A1A-MYSQL-download_url2.png" style="zoom: 50%;" />



#####  3.文件夹准备

- 原则上只要路径上没有中文即可,但比较推荐只更换盘符其余不变
- 选择一个盘(此处选择D盘) 创建`D:/Program Files/MySQL/`文件夹
- 将下载的压缩包解压到`MYSQL`下
 <img src="https://gitcode.net/qq_50848214/image/-/raw/master/412C-A1A-MYSQL-%E6%96%87%E4%BB%B6%E5%A4%B9%E7%94%A8%E9%80%94.png" style="zoom:50%;" />
- <font color="#3271ae">手动创建my.ini文件和data文件夹</font>

- 文件用途介绍(可跳过不看)
```bash
  bin：该文件夹包含了MySQL的可执行文件，
  	如mysql.exe和mysqld.exe。
  	mysql.exe是MySQL客户端程序，用于连接和操作MySQL服务器；
  	mysqld.exe是MySQL服务器程序，用于启动和管理MySQL数据库服务。
  
  data: 解压完不存在的手动创建一个
  	该文件夹是MySQL数据库的默认存储路径，其中包含了所有数据库的数据文件和日志文件
  	每个数据库都有一个对应的文件夹，其中包含了该数据库的表和数据文件
  
  etc: 没有的话不用创建(一会直接把my.ini配置在根目录下)
  	该文件夹包含了MySQL的配置文件，如my.ini（Windows）或my.cnf（Linux）
  	在配置文件中，可以设置MySQL服务器的参数，如端口号、字符集、缓存大小
  	
  lib：该文件夹包含了MySQL的动态链接库文件，
  	如libmysql.dll（Windows）或libmysqlclient.so（Linux）
  	这些库文件提供了MySQL的API接口，可以用于开发MySQL的客户端程序
  	
  share: 该文件夹包含了一些共享文件，如字符集文件和错误消息文件。
  	字符集文件定义了MySQL支持的字符集，错误消息文件包含了MySQL的错误码和错误信息
  	
  ```




---

##### 4.my.ini文件配置

- 文件如下:
- 需要更改端口号`两处`,多个数据库之间的端口不能相同
- 文件之间的路径只用`/`或者`\\`分割
- 修改`basedir`
- 修改`datadir`
- <font color="red">如果MySQL版本为5.7.X,在最后一行添加免登录检查</font>
```ini
[mysqld]
# 这里设置3306端口
port=3306
# 设置mysql的安装目录
basedir=D:/Program Files/MySQL/mysql-5.7.43-winx64
# 设置mysql数据库的数据的存放目录
datadir=D:/Program Files/MySQL/mysql-5.7.43-winx64/data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用"mysql_native_password"插件认证
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
#免登陆检查
skip-grant-tables 
```



##### 5.安装

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412C-A1A-MYSQL-cmd.png" style="zoom:50%;" />

- 以<font color="red">管理员</font>身份打开命令提示符,<font color="red">并进入要配置的Mysql的bin文件夹下</font>
  ![](https://gitcode.net/qq_50848214/image/-/raw/master/412C-A1A-MYSQL-cd.png)
> 如果还用的是Windows PowerShell 在切换目录时,"Program Files"要加上双引号
> 例如 : `cd D:/"Program Files"/MySQL/mysql-5.7.43-winx64/bin`

<font color="#3271ae">注: 以下所有的命令都是在对应Mysql安装文件夹bin下执行的,如果你可以在bin以外的文件夹下执行mysqld命令,说明你配置了环境变量,先删了,再继续</font>


- <font color="#3271ae">安装:</font> 输入命令 `mysqld install 服务名 --defaults-file="路径"`
  > 例如: `mysqld install MYSQL57 --defaults-file="D:\Program Files\MySQL\mysql-5.7.43-winx64\bin"`


- <font color="#3271ae">初始化:</font> 输入命令` mysqld --initialize` 


- <font color="#3271ae">启动服务: </font>输入命令`net start 服务名`，服务名要与上面设置的相同
  > 例如: `net start MYSQL57

注:如果以上命令出现了问题,可以看看本文的第9点有没有符合的

##### 6.密码的修改

- 进入对应版本的`bin`文件夹中
- 关闭服务 `net stop 服务名`
- 按照Mysql的版本执行下面对应的操作

###### 5.7.5以及更低版本
- 确保上面的my.ini配置文件中已经配置了免登录检查
- 或者使用`sudo mysqld --skip-grant-tables  --skip-networking`

```sql
-- 登录
mysql -uroot -p
-- 提示输入密码时直接回车

-- 刷新权限
flush privileges; 

-- MySQL 5.7.5以及之前的版本使用SET PASSWORD语法修改密码
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('此处填密码');
```


###### 5.7.6以及高低版本
- 确保上面的my.ini配置文件中已经配置了免登录检查
- 或者使用`sudo mysqld --skip-grant-tables  --skip-networking`
```sql
输入 mysql -uroot -p
-- 提示输入密码时直接回车
-- 刷新权限
flush privileges; 

-- MySQL 5.7.6以及之后的版本，使用ALTER USER语法来修改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY '此处填密码';

```

如果上面的方法修改密码有错，可以直接修改mysql.user表：
```sql
UPDATE mysql.user SET authentication_string = PASSWORD('此处填密码')WHERE User = 'root' AND Host = 'localhost';FLUSH PRIVILEGES;
```
mysql5.7 user表里已经去掉了password字段，改为了authentication_string


---

<font color="red">注意</font>

--skip-grant-tables：此选项会让MySQL服务器跳过验证步骤，允许所有用户以匿名的方式，无需做密码验证直接登陆MySQL服务器，并且拥有所有的操作权限
因此在配置完成密码后,删除上面Mysql5.7.X中配置的`my.ini`中的免登录检查`skip-grant-tables `

```bash
-- 启动数据库,改成自己的服务名!!!
net start 服务名
```


---


###### 8.X
- 配置:
```sql
-- 跳过权限验证登录mysql
mysqld --shared-memory --skip-grant-tables
-- 注:打开新的窗口(管理员)!!!
输入 mysql -uroot -p
-- 提示输入密码时直接回车


-- 切换到mysql库
use mysql;

-- 密码置空
update user set authentication_string='' where user='root';

-- 刷新权限
flush privileges; 

-- 设置加密规则并更新新密码，授权
ALTER USER 'root'@'localhost' IDENTIFIED BY '此处填密码' PASSWORD EXPIRE NEVER; 
alter user 'root'@'localhost' identified by '此处填密码';
grant all privileges  on *.*  to "root"@'localhost';


-- 刷新权限
flush privileges;

-- 启动数据库,改成自己的服务名!!!
net start 服务名
```


- 注意
```bash
注:由于mysql 8.0不在支持password函数
因此如下命令无法执行
update mysql.user set authentication_string=password('123456') where user='root';
```

- 重启服务`net start 服务名`

##### 7.环境变量配置

在配置的多个版本的Mysql中选择一个你常用的配置环境变量,同时配置多个<font color="#3271ae">只有第一个有效</font>

在Windows底部的菜单中搜索`编辑系统环境变量` 
![](https://gitcode.net/qq_50848214/image/-/raw/master/412C-A1A-MYSQL-image-20231110-025720.png)

- `环境变量(N)...` 
- `系统环境变量(S)`
- 双击`Path` 
- `新建(N)`
- 添加`Mysql的解压路径\bin`例如`D:\Program Files\MySQL\MySQL Server 5.5\bin`


##### 8.登录

使用 `mysql -u用户名 -p密码 -P端口`登录 ,注意字母的大小写



#### 9.可能遇到的问题

---

- MySQL服务正在启动或停止中，请稍候片刻后再试一次
  - 首先以管理员身份打开命令行窗口，注意是管理员身份，不然无权限访问
  -  输入命令	`tasklist| findstr "mysql"`  查找所有Mysql的进程
  -  输入命令	`taskkill /f /t /im mysqld.exe`  杀死所有Mysql进程
  -  输入命令	`tasklist| findstr "mysql"`   查看是否还留有有其他的mysql残留进程 直到完全杀死进程为止
  - 执行以上命令后,就可以对MYSQL服务重新启动或者停止


---
**错误:**
- 请键入 NET HELPMSG 3523 以获得更多的帮助。
- net start 服务启动失败
- 修复Windows下安装MySQL服务(安装 Windows服务时指定了错误的 `mysqld`)


- 可能是配置了Mysql的环境变量导致的

```bash
  # 重复执行安装MySQL服务
  mysqld --install
  The service already exists!
  The current server installed: "C:\Program Files\MySQL\MySQL Server 8.0\mysqld" MySQL
```



**解决:**
- 方式1.修改注册表 : `win+r` 打开运行，输入 `regedit`，然后参照如下方式修改

```bash
# 找到注册路径
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MySQL

# 修改右边窗口里的 ImagePath 字段
"C:\Program Files\MySQL\MySQL Server 8.0\mysqld" MySQL
# 改为
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysqld" MySQL

# 再次执行安装服务命令
mysqld --install
The service already exists!
The current server installed: "C:\Program Files\MySQL\MySQL Server 8.0\bin\mysqld" MySQL

# 看起来安装服务路径正确，让我们试试通过服务命令启动
net start mysql
MySQL 服务正在启动 .
MySQL 服务已经启动成功。
```

方式2. 删除服务,删除环境变量,重新安装
`sc delete 服务名`


---

> Citation:
>
> - []()
>
> References:
>
> - [MySQL安装完整教程--5.7和8.0版本](https://blog.csdn.net/qq_45929019/article/details/129380445)
> - [MySQL修改root用户密码](https://blog.csdn.net/qq_40757240/article/details/118068317)
> - [# MySQL 5.7 忘记root密码](https://blog.csdn.net/diavid/article/details/93192588)
> - [修复Windows下安装MySQL服务](https://www.jianshu.com/p/47d049e975b9)
> - [深入分析MySQL ERROR 1045 (28000)](https://www.linuxidc.com/Linux/2014-07/104244.htm)

