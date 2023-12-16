---

title: 配置数据源失败
tags: [Maven,yaml,yml,Q,SpringBoot]
categories: [412B-框架工具]
description: 进入文章

---


---


##### 类型:
###### 1.问题信息
![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I1-S-BOOT-sshot-2.png)

```java
Description:

Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured.

Reason: Failed to determine a suitable driver class
```
###### 2.问题分析
配置数据源失败：未指定"url"属性，无法配置嵌入式数据源。原因：未能确定合适的驱动程序类

###### 3.如何解决

在检查完成所有的数据源配置都是正确的情况下,造成此异常的原因为`application.yaml`或`application.yml`文件没有被Spring扫描到,需要在pom.xml文件的build中添加扫描的相关配置

```xml
<resources>
	<resource>
	<directory>src/main/java</directory><!--所在的目录-->
	<includes><!--包括目录下的.properties,.xml 文件都会扫描到-->
	<include>**/*.properties</include>
	<include>**/*.xml</include>
	<include>**/*.yml</include>
	<include>**/*.yaml</include>
	</includes>
	</resource>
	<resource>
	<directory>src/main/resources</directory><!--所在的目录-->
	<includes><!--包括目录下的.properties,.xml 文件都会扫描到-->
	<include>**/*.properties</include>
	<include>**/*.xml</include>
	<include>**/*.yml</include>
	<include>**/*.yaml</include>
	</includes>
	</resource>
</resources>
```


---

> Citation:
> - [412B-A1D1-MAVEN-maven依赖](412B-A1D1-MAVEN-maven依赖.md)
> 
> References:
> - []()
