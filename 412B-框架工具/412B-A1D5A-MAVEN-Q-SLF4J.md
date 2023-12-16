---

title: No SLF4J providers were found.
tags: [问题,SLF4J,依赖问题]
categories: [412B-框架工具]
description: 进入文章

---

---

#### 问题描述:
在控制台中出现:
SLF4J: No SLF4J providers were found.  
SLF4J: Defaulting to no-operation (NOP) logger implementation  
SLF4J: See https://www.slf4j.org/codes.html#noProviders for further details.  


#### 错误分析:

报错原因是SLF4J本身是一个接口，并不是真的日志实现库，需要依赖具体的实现才能正常运行，因此其必须和其他日志配合才可正常运行。  
如果没有实现层，SLF4J会使用一个空类（no-operation (NOP) logger）来完成，就不会记录log信息，  
需要将例如slf4j-api-xx.jar）+中间层（例如slf4j-log4j12）+实现层（例如log4j）这三层都配置好才能保证SLF4J正常运行。  
本配置文件使用的是SLF4J 与他的简单实现slf4j-simple  


#### 解决:
在pom.xml文件中:
1.添加SLF4J的依赖:(如果已存在,则不必再次添加)
```xml
<!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-api -->  
<dependency>  
<groupId>org.slf4j</groupId>  
<artifactId>slf4j-api</artifactId>  
<version>1.8.0-beta0</version>  
</dependency>
```

2.为其添加一个具体的实现
```xml
<dependency>  
<groupId>org.slf4j</groupId>  
<artifactId>slf4j-simple</artifactId>  
<version>1.8.0-beta0</version>  
</dependency>
```



---

> Citation:
> - []()
> 
> References:
> - []()