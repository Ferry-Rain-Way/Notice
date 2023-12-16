---
title: 在Linux中卸载Mysql
tags:
  - Linux
  - 卸载
  - mysql
categories:
  - 412C-数据库
description: 进入文章
---

---

[【转载】](https://blog.csdn.net/Turniper/article/details/130397482)

## Linux彻底删除MySQL 
 >**注意**：在安装另一个MySQL版本之前一定要把之前MySQL版本给卸载干净。 


#### 详细步骤如下：
 >**1、检查云服务器是否已经安装了MySQL：** 

```bash
rpm -qa | grep mysql
```


 >如下所示：

```bash
mysql-community-release-el7-5.noarch
mysql-community-libs-5.6.51-2.el7.x86_64
mysql-community-client-5.6.51-2.el7.x86_64
mysql-community-server-5.6.51-2.el7.x86_64
mysql-community-common-5.6.51-2.el7.x86_64
```


 >**2、查看MySQL服务是否开启：** 

```bash
systemctl status mysqld
```


 >如开启则须关闭，关闭MySQL服务： 

```bash
systemctl stop mysqld
```


 >**3、查找含有MySQL的目录：** 

```bash
find / -name mysql
```


 >如下所示： 

```bash
/var/lib/mysql
/var/lib/mysql/mysql
/usr/local/mysql
/usr/lib64/mysql
/usr/share/mysql
/usr/bin/mysql
/etc/logrotate.d/mysql
/etc/selinux/targeted/active/modules/100/mysql
```


 >**4、删除含有MySQL的目录，依次删除目录（根据自己查找出来的目录进行依次删除）：** 

```bash
rm -rf /var/lib/mysql
rm -rf /var/lib/mysql/mysql
rm -rf /usr/local/mysql
rm -rf /usr/lib64/mysql
rm -rf /usr/share/mysql
rm -rf /usr/bin/mysql
rm -rf /etc/logrotate.d/mysql
rm -rf /etc/selinux/targeted/active/modules/100/mysql
```


 >注意：上面执行完后/etc/my.cnf不会删除掉，需要手动单独删除。 

```bash
rm -rf /etc/my.cnf
```


 >**5、查找MySQL安装的组件服务：** 

```bash
rpm -qa|grep -i mysql
```


 >如下所示： 

```bash
mysql-community-release-el7-5.noarch
mysql-community-libs-5.6.51-2.el7.x86_64
mysql-community-client-5.6.51-2.el7.x86_64
mysql-community-server-5.6.51-2.el7.x86_64
mysql-community-common-5.6.51-2.el7.x86_64
```

 >**6、卸载并删除查找出来的组件服务，依次删除目录（根据自己查找出来的目录进行依次删除）：** 

```bash
rpm -ev mysql-community-release-el7-5.noarch
rpm -ev mysql-community-server-5.6.51-2.el7.x86_64
rpm -ev mysql-community-client-5.6.51-2.el7.x86_64
rpm -ev mysql-community-libs-5.6.51-2.el7.x86_64
rpm -ev mysql-community-common-5.6.51-2.el7.x86_64
```

```bash
如果删除不了则加上--nodeps。例如：rpm -ev --nodeps mysql-community-libs-5.6.51-2.el7.x86_64
```


 >**7、卸载完成后检查是否卸载成功：** 

```bash
rpm -qa | grep -i mysql
```


```bash
systemctl start mysql
```


 >如提示`Failed to start mysql.service: Unit not found.`则说明此时已尽卸载干净了。 



---

> Citation:
> - []()
> 
> References:
> - [Linux操作系统彻底删除MySQL——详细步骤](https://blog.csdn.net/Turniper/article/details/130397482)
