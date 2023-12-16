---
title: SSL连接
tags:
  - SSL
  - useSSL
  - jdbc
  - Q
categories:
  - 412C-数据库
description: 进入文章
---

---


##### 类型:
###### 1.问题信息
```java
信息: {dataSource-1} inited  
Wed Nov 22 02:36:33 CST 2023 WARN: Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn't set. For compliance with existing applications not using SSL the verifyServerCertificate property is set to 'false'. You need either to explicitly disable SSL by setting useSSL=false, or set useSSL=true and provide truststore for server certificate verification.  
```

翻译:
```java
{dataSource-1} ited Wed Nov 22 02:36:33 CST 2023警告:不建议在没有服务器身份验证的情况下建立SSL连接。

根据MySQL 5.5.45、5.6.26和5.7.6的要求，如果没有设置explicit选项，则默认建立SSL连接。
为了符合不使用SSL的现有应用程序，将verifyServerCertificate属性设置为“false”。

您需要通过设置useSSL=false显式禁用SSL，或者设置useSSL=true并为服务器证书验证提供信任存储。
```

###### 2.问题分析
报这个警告的原因主要是JDBC的版本与MySQL的版本不兼容，而MySQL在高版本需要指明是否进行SSL连接。

###### 3.如何解决

- 在`jdbc.properties`中配置url时加上 <font color="red">&useSSL=false</font>
- 找到安装Mysql的位置,打开`my.ini`文件,在文件的`mysqld`模块添加如下
```
[mysqld]
skip_ssl
```



---
辅助阅读：
1. SSL协议提供服务主要：       
- 认证用户服务器，确保数据发送到正确的服务器
- 加密数据，防止数据传输途中被窃取使用
- 维护数据完整性，验证数据在传输过程中是否丢失；

2. 当前支持SSL协议两层：        
- SSL记录协议（SSL Record Protocol）
>建立靠传输协议（TCP）高层协议提供数据封装、压缩、加密等基本功能支持
- SSL握手协议（SSL Handshake Protocol）：
> 建立SSL记录协议用于实际数据传输始前通讯双进行身份认证、协商加密算法、交换加密密钥等。
---

当配置MySQL端口为SSL，数据通道会加密处理，这样可以避免敏感信息泄漏和被篡改。

但是，启用MySQL的SSL之后，因为每个数据包都需要加密和解密，所以会对MySQL的性能产生不小的影响，大家在使用的时候，可以根据实际情况看是否要开启。


---

> Citation:
> - []()
> 
> References:
> - [useSSL](https://developer.aliyun.com/article/974013)
