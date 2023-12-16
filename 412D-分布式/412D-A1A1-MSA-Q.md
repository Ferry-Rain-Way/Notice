---
title: Springcloud连接eureka异常
tags:
  - Q
  - 连接异常
  - eureka
  - ConnectException
categories:
  - 412D-分布式
description: 进入文章
---

---

##### 类型:Springcloud连接eureka异常
###### 1.问题信息
```java
at com.sun.jersey.client.apache4.ApacheHttpClient4Handler.handle(ApacheHttpClient4Handler.java:187)
Caused by: java.net.ConnectException: Connection refused: no further information
com.netflix.discovery.shared.transport.TransportException:Cannot execute request on any known server

```
###### 2.问题分析
- 翻译
```java
网址：com.sun.jersy.client.apache4.ApacheHttpClient4Handler.handle（ApacheHttpClient4 Handler.java:187）

引起原因：java.net.ConnectException：连接被拒绝：无进一步信息

com.netflix.discovery.shared.transport.TransportException：无法在任何已知服务器上执行请求
```


*2.1 服务端报错:*
- 1) 因为eureka默认会去检索服务，当我们只写了这么一个注册中心（eureka）而没有其他服务的时候，它去检索服务就会出现上述错误,需要添加配置 
- 2) 配置文件中idea提示会出现default-zone这种形式,也会报错改为defaultZone


*2.2 客户端报错*
- 1) 可能是服务端没有跑起来
- 2) defaultZone: 配置的URL有问题
- 3) 可能是服务端的端口被占用

###### 3.如何解决

- 1) 需要添加配置 fetch-registry: false
```yaml
# 端口
server:
  port: 10089
# 微服务名
spring:
  application:
    name: eureka-server
# eureka的服务配置
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:10089/eureka
    fetch-registry: false
    register-with-eureka: false
```




---

> Citation:
> - []()
> 
> References:
> - [com.netflix.discovery.shared.transport.TransportException: Cannot execute request on any known serve-CSDN博客](https://blog.csdn.net/luansha0/article/details/88789742)
