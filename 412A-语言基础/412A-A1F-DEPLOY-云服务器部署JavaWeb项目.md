---

title: 云服务器部署JavaWeb项目
tags: [javaWeb,部署,Tomcat]
categories: [412A-语言基础]
description: 进入文章

---

---



# 云服务器部署JavaWeb项目
[进入bilibili观看](https://www.bilibili.com/video/BV1yP411N7pK/?spm_id_from=333.788&vd_source=0623423bf320a03e4028ac01936b80a6)

## 零、服务器、域名购买
[进入Bilibili观看](https://www.bilibili.com/video/BV1cf4y1d75U/?spm_id_from=333.788&vd_source=0623423bf320a03e4028ac01936b80a6)

### 0.1 服务器购买
进入[腾讯云](https://cloud.tencent.com/)<br>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-f-01.png" alt="f-01.png" style="zoom: 20%;" /><br>

找到"云 + 校园"  模块(在校学生,第一次购买) 不是的话去活动中心看看有没有优惠的服务器购买<br>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-f-02.png" alt="f-02.png" style="zoom: 50%;" /><br>

选择够用的服务器就行,我这里选的是最便宜的,够用了<br>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-f-03.png" alt="f-03.png" style="zoom: 30%;" /><br>

服务器的类型建议选择Linux系统,这里选择Centos7.6
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-f-04.png" alt="f-04.png" style="zoom: 30%;" />

### 02.域名购买 
进入腾讯的产品,搜索"域名注册"<br>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-y-01.png" alt="y-01.png" style="zoom: 30%;" /><br>

输入自己想要注册的域名<br>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-y-02.png" alt="y-02.png" style="zoom: 30%;" /><br>

购买想要的域名,建议一次性购买多年的比较划算<br>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-y-03.png" alt="y-03.png" style="zoom: 20%;" /><br>


<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-y-04.png" alt="y-04.png" style="zoom: 30%;" /><br>

下单购买后即可,点击导航栏的备案即可进行备案,按照引导进行备案即可,注意:<br>

- 备案个人域名时,网站的名称有要求,查看腾讯的建议
- 填写的应急联系方式(电话)一定是知情"你在备案"这件事的,腾讯会打电话进行核对
- 网站的功能信息描述要尽可能的详细
- 备案期间不能对"正在备案的域名"进行解析,如果解析过了,需要对解析记录进行删除
- 腾讯云会打电话进行信息核对,注意电话接听
- 工信部会发送短信,需要在24小时内进行验证,注意查看






## 一、准备工作

本教程使用的是腾讯云服务器（其他云服务器也行，原理一样），需要提前购买哟，此处不做演示。

### 1.1 所需工具软件环境

| 项目       | 说明                                        |
| ---------- | ------------------------------------------- |
| CentOS7.6  | 系统环境版本                                |
| finalshell | 远程连接linux并传输文件的工具，其他软件也行 |
| navicat    | 远程连接访问数据库的工具，其他软件也行      |
| jdk1.8     | `jdk-8u251-linux-x64.tar.gz`                |
| tomcat8.5  | `apache-tomcat-8.5.66.tar.gz`               |
| MySQL5.7   | 在线下载安装                                |

==对于初学者，建议跟本教程一样的软件版本，成功率会比较高哦！==



### 1.2 finalshell远程连接云服务器

点击finalshell软件，点击SSH连接（Linux），输入名称、主机名、用户名、密码。

![image-20221018230208984](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018230208984.png)

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018225924105.png" alt="image-20221018225924105" style="zoom: 50%;" />

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018230050566.png" alt="image-20221018230050566" style="zoom:50%;" />

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018230355217.png" alt="image-20221018230355217" style="zoom:50%;" />

出现如下所示界面，证明连接成功！

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018230411222.png" alt="image-20221018230411222" style="zoom:50%;" />



### 1.3 新建目录结构及说明

**准备在根目录下的usr下，新建一个专门的目录myapp来存放环境所需的软件。**

```java
/usr/myapp
		  /java
		  /tomcat
		  /mysql
```

==具体步骤如下：==

进入根目录下的`usr`，新建myapp目录（用于存放本教程使用的软件）

```shell
cd /
cd usr
mk myapp
```

之后，在`myapp`内新建三个目录分别是java、tomcat、mysql

```
cd /usr/myapp
mk java
mk tomcat
mk mysql
```

**当然，上述操作也可以直接在finalshell内==可视化==完成，如下：**

进入`/usr`

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018205804693.png" alt="image-20221018205804693" style="zoom:50%;" />

在`usr`下新建myapp目录

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018205858144.png" alt="image-20221018205858144" style="zoom:50%;" />

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018210004023.png" alt="image-20221018210004023" style="zoom:50%;" />

在`myapp`目录下新建java、tomcat、mysql

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018210644448.png" alt="image-20221018210644448" style="zoom:50%;" />



### 1.4 上传tomcat及jdk解压包到对应目录

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018210510230.png" alt="image-20221018210510230" style="zoom: 50%;" />![image-20221018211038655](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018211038655.png)

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018211811674.png" alt="image-20221018211811674" style="zoom:50%;" />

至此，准备工作完毕！



## 二、jdk安装及环境配置

### 2.1 安装

进入  `/usr/myapp/java`   目录，并安装jdk解压包（一定要解压到当前文件夹）

```
cd /usr/myapp/java
tar -zxvf /usr/myapp/java/jdk-8u251-linux-x64.tar.gz
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018212816910.png" alt="image-20221018212816910" style="zoom:50%;" />

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018212938500.png" alt="image-20221018212938500" style="zoom:50%;" />

解压即安装。

### 2.2 配置环境变量

**接下来，配置环境变量。**

进入根目录下的etc目录，找到profile文件（在这里，直接可视化操作），并打开。

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018213310464.png" alt="image-20221018213310464" style="zoom:67%;" />

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018213403527.png" alt="image-20221018213403527" style="zoom:50%;" />

将以下代码粘贴到profile文件的最后。

```
JAVA_HOME=/usr/myapp/java/jdk1.8.0_251
CLASSPATH=.:$JAVA_HOME/lib.tools.jar
PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME CLASSPATH PATH
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018213519887.png" alt="image-20221018213519887" style="zoom:67%;" />

让配置文件生效

```
source /etc/profile
```

### 2.3 检查是否成功

```
java
javac
java -version
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018213731198.png" alt="image-20221018213731198" style="zoom:50%;" />



## 三、tomcat安装及环境配置

### 3.1 安装

进入  `/usr/myapp/tomcat`   目录，并安装tomcat解压包

```
cd /usr/myapp/tomcat
tar -zxvf /usr/myapp/tomcat/apache-tomcat-8.5.66.tar.gz
```

进入  `/usr/myapp/tomcat/apache-tomcat-8.5.66`，可以发现，该目录结构与windows电脑下安装的tomcat一致。

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018215955194.png" alt="image-20221018215955194" style="zoom:50%;" />

### 3.2 腾讯云开放8080端口

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018234719608.png" alt="image-20221018234719608" style="zoom:50%;" />

有可能是到【安全组】的位置开放端口。



### 3.3 系统开放8080端口

**① 先检查防火墙的状态**

```
firewall-cmd --state
```

==runing 表示开启，not runing 表示关闭==

如果防火墙关闭的状态，则执行以下命令开启防火墙

```
systemctl start firewalld.service
```

补充：`systemctl stop firewalld.service`  就是关闭防火墙

**② 开启8080端口**

```
firewall-cmd --zone=public --add-port=8080/tcp --permanent
```

**③ 重启防火墙**

```
systemctl restart firewalld.service
```

**④ 重新加载配置**

```
firewall-cmd --reload
```



### 3.4 开启tomcat服务器

进入tomcat的安装目录下的bin目录

```
cd /usr/myapp/tomcat/apache-tomcat-8.5.66/bin
```

开启tomcat服务器

```
./startup.sh
```



### 3.5 测试

在本地电脑，浏览器地址栏输入  ip:8080测试，我的就是 http://121.4.53.226:8080/

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018215823893.png" alt="image-20221018215823893" style="zoom:50%;" />



## 四、MySQL下载安装配置

### 4.1 下载

进入 `/usr/myapp/mysql`,并通过`wget`下载数据库。

```
cd /usr/myapp/mysql

wget http://repo.mysql.com/mysql57-community-release-el7-8.noarch.rpm
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018230955815.png" alt="image-20221018230955815" style="zoom:40%;" />

### 4.2 安装数据库

```
rpm -ivh mysql57-community-release-el7-8.noarch.rpm
```





### 4.3 安装服务

```
yum -y install mysql-server
```

（这里需要花费一段时间，耐心等待……）

==在安装的过程中，有可能会报错。==

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018231833809.png" alt="image-20221018231833809" style="zoom:50%;" />

原因：MySQL GPG [密钥](https://so.csdn.net/so/search?q=密钥&spm=1001.2101.3001.7020)已过期导致

解决办法：执行以下命令

`rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022`

之后，再运行安装服务的命令

`yum -y install mysql-server`

出现 ==Complete!== 则代表安装成功！如下图。

![image-20221018232327141](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018232327141.png)



### 4.4 检查是否安装成功

```
rpm -qa | grep mysql
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018232718889.png" alt="image-20221018232718889" style="zoom:50%;" />



### 4.5 初始化mysql

```
mysqld --initialize
```



### 4.6 授权防火墙

```
chown mysql:mysql /var/lib/mysql -R;
systemctl start mysqld.service;
systemctl enable mysqld;
```



### 4.7 启动服务

```
service mysqld restart
```



### 4.8 查看数据库默认密码

```
grep "password" /var/log/mysqld.log
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018233836838.png" alt="image-20221018233836838" style="zoom:50%;" />

==注意：如果密码为空，则直接进入。==



### 4.9 进入数据库并修改数据库的密码

进入数据库

```
mysql -uroot -p
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018234233072.png" alt="image-20221018234233072" style="zoom:50%;" />

修改数据库密码，这里修改为123456

```
alter user 'root'@'localhost' identified by '123456';
```

之后，退出，用新密码进入。

```
exit

mysql -uroot -p
```



### 4.10 设置对外连接的数据库名及密码

此处设置的是外部访问时的名称及密码，这个密码可以与本身数据库的密码相同，也可以不同。

```
create user 'root'@'%' identified with mysql_native_password by 'root';
grant all privileges on *.* to 'root'@'%' with grant option;
flush privileges;
```

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019000314479.png" alt="image-20221019000314479" style="zoom:67%;" />

之后，退出mysql

```
exit
```



### 4.11 腾讯云开放3306端口

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018234912585.png" alt="image-20221018234912585" style="zoom:50%;" />

### 4.12 系统开放3306端口

```
firewall-cmd --zone=public --add-port=3306/tcp --permanent
systemctl restart firewalld.service
firewall-cmd --reload
```



## 五、navicat连接云服务器的数据库，并转储数据

本地电脑打开navicat，点击连接------MySQL

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018235631069.png" alt="image-20221018235631069" style="zoom:50%;" />![image-20221019001034596](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019001034596.png)

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221018235631069.png" alt="image-20221018235631069" style="zoom:50%;" />![image-20221019001034596](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019001034596.png)

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019001056381.png" alt="image-20221019001056381" style="zoom:50%;" />

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019001226476.png" alt="image-20221019001226476" style="zoom:50%;" />

接下来，我们只需要将本地的数据，转储迁移到云服务器的数据库，即可。

具体教程可参考视频教程。

[05-2 6分钟学会navicat常用操作，轻松搞定数据转储](https://www.bilibili.com/video/BV1Lt4y1A79N/)



## 六、打包项目并上云

### 6.1 修改localhost为公网ip

将`localhost`或 `127.0.0.1` 改为`公网ip`

![image-20221019104348023](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019104348023.png)

==注意：若是前后端分离的项目，那么，则需要修改所有前端url路径为服务器公网ip。==

本演示项目仅仅需只需修改连接数据库的地址、用户名、密码，即可。

### 6.2 将项目打成war包

可以利用IDEA的Maven工具快速将项目打成包

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019104540919.png" alt="image-20221019104540919" style="zoom:50%;" />

之后，在项目结构的生成了一个target目录，里面包含了一个war包，如图。

<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1F-DEPLOY-image-20221019104605952.png" alt="image-20221019104605952" style="zoom:67%;" />

### 6.3 将war包上传至云服务器的tomcat的webapps中



### 6.4 测试项目云上运行情况



## 七、总结与注意事项

1. 为了保证最后整体项目能“跑”得通，本地的环境版本与云端的一定要一致
2. 如果是前后端分离的项目，前端的url路径要改为公网ip




---

> Citation:
> - []()
> 
> References:
> - []()
