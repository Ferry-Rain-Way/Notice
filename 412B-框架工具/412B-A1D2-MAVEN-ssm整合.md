---

title: SSM整合依赖
tags: [Spring,SpringMVC,Mybatis]
categories: [412B-框架工具]
description: 进入文章

---

---




```xml
配置信息:
Tomcat10

```

#### 1.pom.xml


Spring 6.0.4
Tomcat 10.0.20
Mybatis 3.5.1
Mysql-jdbc 8.0.30

##### 高版本(适用于Tomcat10)

```xml

  <!--Spring6仓库地址-->
  <repositories>
    <repository>
      <id>repository.spring.milestone</id>
      <name>Spring Milestone Repository</name>
      <url>https://repo.spring.io/milestone</url>
    </repository>
  </repositories>


  <!-- 集中定义依赖版本号 -->
  <properties>
    <junit.version>4.12</junit.version>
    <spring.version>6.0.4</spring.version>
    <mybatis.version>3.5.1</mybatis.version>
    <!--mybatis-spring 目前测试最低需要用2.1.0版本-->
    <mybatis.spring.version>2.1.0</mybatis.spring.version>
    <mybatis.paginator.version>1.2.15</mybatis.paginator.version>
    <!--mysql需要与自己电脑上的对应-->
    <mysql.version>8.0.30</mysql.version>
    <slf4j.version>1.6.4</slf4j.version>
    <druid.version>1.1.12</druid.version>
    <pagehelper.version>5.1.2</pagehelper.version>
    <!--jstl\servlet-api\jsp-api-->
    <jakarta.jstl.version>2.0.0</jakarta.jstl.version>
    <jakarta.servlet-api.version>5.0.0</jakarta.servlet-api.version>
    <jakarta.jsp-api.version>3.0.0</jakarta.jsp-api.version>

    <jackson.version>2.9.6</jackson.version>

  </properties>


  <dependencies>
    <!-- spring -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aspects</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jms</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- Mybatis -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>${mybatis.version}</version>
    </dependency>
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>${mybatis.spring.version}</version>
    </dependency>
    <dependency>
      <groupId>com.github.miemiedev</groupId>
      <artifactId>mybatis-paginator</artifactId>
      <version>${mybatis.paginator.version}</version>
    </dependency>
    <dependency>
      <groupId>com.github.pagehelper</groupId>
      <artifactId>pagehelper</artifactId>
      <version>${pagehelper.version}</version>
    </dependency>
    <!-- MySql -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>${mysql.version}</version>
    </dependency>
    <!-- 连接池 -->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>${druid.version}</version>
    </dependency>

    <!-- junit -->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>${junit.version}</version>
      <scope>test</scope>
    </dependency>

    <!-- JSP相关 -->

    <dependency>
      <groupId>org.glassfish.web</groupId>
      <artifactId>jakarta.servlet.jsp.jstl</artifactId>
      <version>${jakarta.jstl.version}</version>
    </dependency>

    <dependency>
      <groupId>jakarta.servlet</groupId>
      <artifactId>jakarta.servlet-api</artifactId>
      <version>${jakarta.servlet-api.version}</version>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>jakarta.servlet.jsp</groupId>
      <artifactId>jakarta.servlet.jsp-api</artifactId>
      <version>${jakarta.jsp-api.version}</version>
      <scope>provided</scope>
    </dependency>


    <!-- Jackson Json处理工具包 -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>${jackson.version}</version>
    </dependency>
    <dependency>
      <groupId>org.json</groupId>
      <artifactId>json</artifactId>
      <version>20140107</version>
    </dependency>

    <!--    文件异步上传使用的依赖-->
    <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
      <version>2.4</version>
    </dependency>
    <dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.3.1</version>
    </dependency>
   <!--slf4j日志-->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-simple</artifactId>
      <version>${slf4j.version}</version>
    </dependency>

  </dependencies>

  <!-- 插件配置 -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
          <encoding>UTF-8</encoding>
        </configuration>
      </plugin>
    </plugins>
    <!--识别所有的配置文件-->
    <resources>
      <resource>
        <directory>src/main/java</directory>
        <includes>
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <filtering>false</filtering>
      </resource>
      <resource>
        <directory>src/main/resources</directory>
        <includes>
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <filtering>false</filtering>
      </resource>
    </resources>
  </build>


```



##### 低版本(适用于Tomcat8)

```xml
<dependencies>
    <!--junit单元测试依赖-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
    </dependency>

    <!--Spring相关依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aspects</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <!--Mybatis依赖-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.4.6</version>
    </dependency>
    <!--Mysql驱动依赖-->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.28</version>
    </dependency>

    <!--druid数据源|连接池依赖-->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.2.8</version>
    </dependency>

    <!--Mybatis和Spring框架的整合依赖-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.1</version>
    </dependency>

    <!--SpringMVC所需依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.2.RELEASE</version>
    </dependency>
    <!--servlet-api依赖-->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>
    <!--jsp-api依赖-->
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.1</version>
    </dependency>
    <!--jstl依赖-->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
</dependencies>
```



---



#### 2.jdbc.properties

```properties
jdbc.driverClassName=com.mysql.填空.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/填空?useUnicode=true&characterEncoding=utf8  
jdbc.username=root  
jdbc.password=root
```

#### 3.mybatis-config

> 注Mybatis的核心配置文件,`sqlMapConfig.xml`也比较常用

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

</configuration>
```

#### 4.applicationContext.xml

> 注:spring的核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd
       http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--1、组件扫描-->
    <context:component-scan base-package="填空_1"/>

    <!--2、引入JDBC属性文件-->
    <!--此处需要加上 classpath: ！！！！！！！！！！！-->
    <context:property-placeholder location="classpath:填空_2"/>

    <!--3、数据源-->
    <!--此处对应的Bean不用我们写,阿里巴巴写好了,我们直接用就行-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
    </bean>

    <!--4、SqlSessionFactoryBean配置-->
    <bean class="org.mybatis.spring.SqlSessionFactoryBean">
        <!--注入mybatis核心配置文件路径-->
        <!--此处需要加上 classpath: ！！！！！！！！！！！-->
        <property name="configLocation" value="classpath:填空_3"/>
        <!--数据源-->
        <property name="dataSource" ref="dataSource"/>
        <!--指定别名-->
        <property name="typeAliasesPackage" value="填空_4"/>
    </bean>
    <!--5、Mapper扫描mapper包,生成代理类-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="填空_5"/>
    </bean>
    <!--6、事务管理器-->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>
    <!--开启事务-->
    <tx:annotation-driven transaction-manager="txManager"/>

    <!--添加事务的切面-->
    <tx:advice id="myAdvice" transaction-manager="txManager">
        <tx:attributes>
            <tx:method name="*select*" read-only="true"/>
            <tx:method name="*find*" read-only="true"/>
            <tx:method name="*get*" read-only="true"/>
            <tx:method name="*search*" read-only="true"/>
            <tx:method name="*insert*" propagation="REQUIRED"/>
            <tx:method name="*save*" propagation="REQUIRED"/>
            <tx:method name="*add*" propagation="REQUIRED"/>
            <tx:method name="*delete*" propagation="REQUIRED"/>
            <tx:method name="*remove*" propagation="REQUIRED"/>
            <tx:method name="*clear*" propagation="REQUIRED"/>
            <tx:method name="*update*" propagation="REQUIRED"/>
            <tx:method name="*modify*" propagation="REQUIRED"/>
            <tx:method name="*change*" propagation="REQUIRED"/>
            <tx:method name="*set*" propagation="REQUIRED"/>
            <tx:method name="*" propagation="SUPPORTS"/>
        </tx:attributes>
    </tx:advice>

    <!--完成切面和切入点的织入-->
    <aop:config>
        <aop:pointcut id="myPointcut" expression="execution(*填空_6.service.*.*(..))"/>
        <!--
<aop:pointcut id="myPointcut" expression="execution(* com.nfjh.ssm.service.*.*(..))"/>
		-->
        <aop:advisor advice-ref="myAdvice" pointcut-ref="myPointcut"/>
    </aop:config>
</beans>
```

#### 5.springmvc.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
<!--添加包扫描-->
    <context:component-scan base-package="包扫描"/>
<!--本项目均为ajax请求,不添加视图解析器-->

<!--注解驱动-->
    <mvc:annotation-driven/>
</beans>
```

#### 6.web.xml
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

#### 7.sql
```sql
CREATE DATABASE /*!32312 IF NOT EXISTS*/`ssm` /*!40100 DEFAULT CHARACTER SET utf8 */;

USE `ssm`;

/*Table structure for table `person` */

DROP TABLE IF EXISTS `person`;

CREATE TABLE `person` (
  `name` char(25) DEFAULT NULL,
  `age` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

/*Data for the table `person` */

insert  into `person`(`name`,`age`) values ('张三',23),('李四',23),('王五',22);
```

#### 8.controller
```java
@Controller  
public class PersonController {  
  
  
    PersonService personService;  
    @Autowired  
    public PersonController(PersonService personService) {  
        this.personService = personService;  
    }  
  
  
    @ResponseBody  
    @RequestMapping("/person/selectAll")  
    public List<Person> selectAll(){  
        System.out.println(personService.selectAll());  
        return personService.selectAll();  
    }  
/**  
 * 使用jackson-databind 需要注意的点:  
 *      如果发送请求,url正常的情况下,仍然404  
 *      检查:是否为方法添加了 @RequestBody注解   
 *   
 */  
}
```

#### 9.service
##### service接口
```java
public interface PersonService {  
    List<Person> selectAll();  
}
```

##### service.impl
```java
@Service  
public class PersonServiceImpl implements PersonService {  
  
    private PersonMapper personMapper;  
    @Autowired  
    public PersonServiceImpl(PersonMapper personMapper) {  
        this.personMapper = personMapper;  
    }  
  
    //查询  
    public List<Person> selectAll(){  
        return personMapper.selectAll();  
    }  
}
```


#### 10.mapper
##### Mapper.java
```java
public interface PersonMapper {  
    /**  
     * 查询所有人的信息(姓名、年龄)  
     * @return  
     */  
    List<Person> selectAll();  
}
```


##### _Mapper.xml
```xml
<!--List<Person> selectAll();-->  
    <select id="selectAll" resultType="person">  
        select name,age from person ;  
    </select>
```



---

> Citation:
> - []()
> 
> References:
> - []()
