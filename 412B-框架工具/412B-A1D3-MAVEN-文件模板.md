---

title: 常用模板文件
tags: [模板,整合]
categories: [412B-框架工具]
description: 进入文章

---

---

### Web

#### index.jsp
```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>  
<html>  
<head>  
    <title>Title</title>  
</head>  
<body>  
  
</body>  
</html>
```

#### jdbc.properties
```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:端口/数据库?useUnicode=true&characterEncoding=utf8&useSSL=true&serverTimezone=GMT%2B8
jdbc.username=root
jdbc.password=root
```

#### web.xml(servlet版)

```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
						https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
	version="5.0"
	metadata-complete="true">
  
  
</web-app>
```



#### Web.xml(Spring整合版)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
						https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
         version="5.0"
         metadata-complete="true">
<!--中文乱码
    private String encoding;
    private boolean forceRequestEncoding;
    private boolean forceResponseEncoding;
-->
<!--  <filter>-->
<!--    <filter-name>encoding</filter-name>-->
<!--    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>-->
<!--    <init-param>-->
<!--      <param-name>encoding</param-name>-->
<!--      <param-value>UTF-8</param-value>-->
<!--    </init-param>-->
<!--    <init-param>-->
<!--      <param-name>forceRequestEncoding</param-name>-->
<!--      <param-value>true</param-value>-->
<!--    </init-param>-->
<!--    <init-param>-->
<!--      <param-name>forceResponseEncoding</param-name>-->
<!--      <param-value>true</param-value>-->
<!--    </init-param>-->
<!--  </filter>-->
<!--  <filter-mapping>-->
<!--    <filter-name>encoding</filter-name>-->
<!--    <url-pattern>/*</url-pattern>-->
<!--  </filter-mapping>-->


<!--注册springmvc框架-->
  <servlet>
    <servlet-name>springmvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!--引入springmvc-config.xml配置-->
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:填空_1</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>springmvc</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>

<!--注册spring框架-->
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
<!--引入spring-config.xml配置-->
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:填空_2</param-value>
  </context-param>
</web-app>
```



### mybatis

#### mybatis-config.xml(简单配置)
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<!--或者SqlMapConfig.xml-->
<configuration>
    <settings>
        <!-- 设置查看 mybatis 生成的 sql 语句的日志配置-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
        <!--
        是否开启驼峰命名自动映射，即从经典数据库列名 A_COLUMN 映射到经典 Java 属性名 aColumn。
        -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>


        <!--
        <mappers>  
            <package name=""></package>  
        </mappers>  
        -->  

</configuration>
```

#### mybatis-config.xml(更全点)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--读取jdbc.properties属性-->
    <properties resource="jdbc.properties"/>

    <settings>
            <!--设置日志输出-->
        <!-- 设置查看 mybatis 生成的 sql 语句的日志配置-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
        <!--
        是否开启驼峰命名自动映射，即从经典数据库列名 A_COLUMN 映射到经典 Java 属性名 aColumn。
        -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>


    <!--注册实体类的别名-->
    <typeAliases>
        <package name="_实体类所在的包_"/>
    </typeAliases>
    <!--配置环境变量-->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driverClassName}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.username}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <!--注册方式1.批量注册 mapper.xml
        name 为所有事的mapper.xml文件所在的包
        在resources文件目录下新建 com/nfjh/mapper
        此时不需要在pom.xml中设置资源文件扫描
        -->
        <package name="_mapper所在的包_"/>
        <!--
     	注册方法2:
		执行XxxMapper.xml文件的路径
        resource属性自动会从类的根路径下开始查找资源
        <mapper resource=""/>
		-->
    </mappers>
</configuration>
```



#### _Mapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="">
    
</mapper>
```

### spring

### spring-config.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">  
  
</beans>
```


#### spring集成mybatis

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context"  
       xmlns:tx="http://www.springframework.org/schema/tx"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">  
  
	<!--1、组件扫描-->  
    <context:component-scan base-package="填空"/>  
  
	<!--2、引入JDBC属性文件-->  
    <context:property-placeholder location="jdbc.properties"/>  
  
	<!--3、数据源-->  
	<!--此处对应的Bean不用我们写,阿里巴巴写好了,我们直接用就行-->  
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">  
        <property name="username" value="${jdbc.username}"/>  
        <property name="password" value="${jdbc.password}"/>  
        <property name="url" value="${jdbc.url}"/>  
        <property name="driverClassName" value="${jdbc.driver}"/>  
    </bean>  
  
	<!--4、SqlSessionFactoryBean配置-->  
    <bean class="org.mybatis.spring.SqlSessionFactoryBean">  
        <!--注入mybatis核心配置文件路径-->  
        <property name="configLocation" value="填空"/>  
        <!--数据源-->  
        <property name="dataSource" ref="dataSource"/>  
        <!--指定别名-->  
        <property name="typeAliasesPackage" value="填空"/>  
    </bean>  
	<!--5、Mapper扫描mapper包,生成代理类-->  
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">  
        <property name="basePackage" value="填空"/>  
    </bean>  
	<!--6、事务管理器-->  
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">  
        <property name="dataSource" ref="dataSource"/>  
    </bean>  
	<!--开启事务-->  
    <tx:annotation-driven transaction-manager="txManager"/>  
</beans>

```


### springboot
#### application.properties
```properties
## 配置前缀prefix和后缀.jsp
spring.mvc.view.prefix=/
spring.mvc.view.suffix=.jsp

## 修改内嵌服务器端口号，默认8080，可以不修改
server.port=8989

## 启用jsp页面热部署
server.servlet.jsp.init-parameters.development=true

#数据源配置
#连接池
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
#驱动类
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/dd?CharacterEncoding=UFT-8
spring.datasource.username=root
spring.datasource.password=

#mybatis配置
#mapper文件位置
mybatis.mapper-locations=classpath:
#这个包里的类会自动成为别名
mybatis.type-aliases-package=

```

#### application.yaml
```yaml
# mysql config
spring:
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:端口/数据库?useUnicode=true&characterEncoding=utf8&useSSL=true&serverTimezone=GMT%2B8
    username: root
    password: root
#mybatis config
mybatis:
  mapper-locations: classpath:
  type-aliases-package: 
```


### Log日志

#### logback.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>

<configuration debug="false">
    <!-- 控制台输出 -->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <!--格式化输出：%d表示日期，%thread表示线程名，%-5level：级别从左显示5个字符宽度%msg：日志消息，%n是换行符-->
            <pattern>[%thread] %-5level %logger{50} - %msg%n</pattern>
        </encoder>
    </appender>

    <!--mybatis log configure-->
    <logger name="com.apache.ibatis" level="TRACE"/>
    <logger name="java.sql.Connection" level="DEBUG"/>
    <logger name="java.sql.Statement" level="DEBUG"/>
    <logger name="java.sql.PreparedStatement" level="DEBUG"/>

    <!-- 日志输出级别,logback日志级别包括五个：TRACE < DEBUG < INFO < WARN < ERROR -->
    <root level="DEBUG">
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="FILE"/>
    </root>

</configuration>
<!--
在resources下添加logback.xml文件
    注:文件名必须叫做logback.xml或logback-test.xml
这种不是标准的配置,所以不用在核心配置文件中配置
但是需要在pom.xml文件中添加依赖
-->
```




---

> Citation:
> - []()
> 
> References:
> - []()
