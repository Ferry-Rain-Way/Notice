---

title: Maven的常用依赖
tags: [Maven,常用依赖 ,maven仓库,中央仓库]
categories: [412B-框架工具]
description: 进入文章
sticky: 200

---

---


<a href="https://mvnrepository.com/" style=" padding: 10px 10px 10px 10px;margin-bottom: 5px; border-radius: 10px;border: 1px solid #b8b8b8;border-right: 2px solid #fff;border-bottom: 2px solid #fff;box-shadow: 0px 0px 5px #000;">Maven 依赖搜索</a>

#### 打包&资源文件
##### webapp资源扫描
```xml
  <build>
    <resources>
      <resource>
        <directory>src/main/webapp</directory>
        <targetPath>META-INF/resources</targetPath>
        <includes>
          <include>**/**</include>
        </includes>
      </resource>
    </resources>
  </build>
```


##### 配置文件扫描

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


##### 局部配置JDK
全局配置参考 [412B-A1D4-MAVEN-maven配置](412B-A1D4-MAVEN-maven配置.md) #maven配置jdk
```xml
<build>  
    <plugins>  
        <plugin>  
            <groupId>org.apache.maven.plugins</groupId>  
            <artifactId>maven-compiler-plugin</artifactId>  
            <configuration>  
                <source>17</source>  
                <target>17</target>  
            </configuration>  
        </plugin>  
    </plugins>  
</build>  
```


#### 测试

##### junit
```xml
<!-- https://mvnrepository.com/artifact/junit/junit -->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
<!--
junit从4.12开始(含4.12)被Spring接管
-->
```

```
@BeforeClass – 表示在类中的任意public static void方法执行之前执行
@AfterClass – 表示在类中的任意public static void方法执行之后执行
@Before – 表示在任意使用@Test注解标注的public void方法执行之前执行
@After – 表示在任意使用@Test注解标注的public void方法执行之后执行
@Test – 使用该注解标注的public void方法会表示为一个测试方法
```



##### Servlet 、jsp <=9
```xml
	<dependency>
		 <groupId>javax.servlet</groupId>
		 <artifactId>javax.servlet-api</artifactId>
		 <version>3.1.0</version>
		 <scope>provided</scope>
	</dependency>
	<dependency>
		 <groupId>javax.servlet.jsp</groupId>
		 <artifactId>jsp-api</artifactId>
		 <version>2.1</version>
		 <scope>provided</scope>
	</dependency>
```

##### Servlet 、jsp >=10
```xml

<!-- https://mvnrepository.com/artifact/jakarta.servlet/jakarta.servlet-api -->  
<dependency>  
  <groupId>jakarta.servlet</groupId>  
  <artifactId>jakarta.servlet-api</artifactId>  
  <version>5.0.0</version>  
  <scope>provided</scope>  
</dependency>
	
<!-- https://mvnrepository.com/artifact/jakarta.servlet.jsp/jakarta.servlet.jsp-api -->
<dependency>
    <groupId>jakarta.servlet.jsp</groupId>
    <artifactId>jakarta.servlet.jsp-api</artifactId>
    <version>3.0.0</version>
    <scope>provided</scope>
</dependency>

```

##### JSTL [javax]
```xml
<!-- https://mvnrepository.com/artifact/jstl/jstl -->
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>

```

##### JSTL [jakarta]
```xml
<!-- https://mvnrepository.com/artifact/org.glassfish.web/jakarta.servlet.jsp.jstl -->
<dependency>
    <groupId>org.glassfish.web</groupId>
    <artifactId>jakarta.servlet.jsp.jstl</artifactId>
    <version>2.0.0</version>
</dependency>

<!--  
org.glassfish.web的jakarta.servlet.jsp.jstl  
在使用时就用2.0.0的版本,在此基础上时可以使用 core核心库的  
如果使用3.0.1的版本就会抛出异常  
-->
```


##### JDBC
```xml
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.32</version>
</dependency>

```


```xml
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.30</version>
</dependency>

```


#### 框架
##### MyBatis

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->  
<dependency>  
  <groupId>org.mybatis</groupId>  
  <artifactId>mybatis</artifactId>  
  <version>3.5.6</version>  
</dependency>
```


```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>

```




##### spring context 6.0.0-M2
```xml
<!--Spring6的正式版发布之前，这个仓库地址是需要的-->
<repositories>
  <repository>
    <id>repository.spring.milestone</id>
    <name>Spring Milestone Repository</name>
    <url>https://repo.spring.io/milestone</url>
  </repository>
</repositories>

<dependencies>
  <!--spring context依赖：使用的是6.0.0-M2里程碑版-->
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.0.0-M2</version>
  </dependency>
</dependencies>
```


##### spring-context 5.318

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.18</version>
</dependency>

```


##### spring-aspects 
```xml
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>6.0.0-M2</version>
  </dependency>

```


##### annotation-api
使用@Resource需要引入
Spring6+版本
```xml
<dependency>
  <groupId>jakarta.annotation</groupId>
  <artifactId>jakarta.annotation-api</artifactId>
  <version>2.1.1</version>
</dependency>
```

Spring其他版本
```xml
<dependency>
  <groupId>javax.annotation</groupId>
  <artifactId>javax.annotation-api</artifactId>
  <version>1.3.2</version>
</dependency>
```


##### spring-webmvc
```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->  
<dependency>  
  <groupId>org.springframework</groupId>  
  <artifactId>spring-webmvc</artifactId>  
  <version>6.0.4</version>  
</dependency>
```


#### 工具
##### jackson-databind
> JSON解析
```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.14.1</version>
</dependency>

```

##### Jsoup
```xml
	<!-- https://mvnrepository.com/artifact/org.jsoup/jsoup -->  
	<dependency>  
	  <groupId>org.jsoup</groupId>  
	  <artifactId>jsoup</artifactId>  
	  <version>1.14.3</version>  
	</dependency>
```

##### dom4j
```xml
<!-- https://mvnrepository.com/artifact/org.dom4j/dom4j -->
<dependency>
    <groupId>org.dom4j</groupId>
    <artifactId>dom4j</artifactId>
    <version>2.1.3</version>
</dependency>

<!-- https://mvnrepository.com/artifact/jaxen/jaxen -->
<dependency>
    <groupId>jaxen</groupId>
    <artifactId>jaxen</artifactId>
    <version>1.2.0</version>
</dependency>

```

##### javassist
```xml
<!-- https://mvnrepository.com/artifact/org.javassist/javassist -->
<dependency>
    <groupId>org.javassist</groupId>
    <artifactId>javassist</artifactId>
    <version>3.29.0-GA</version>
</dependency>

```

#### 日志
##### logback
```xml
<!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.11</version>
    <scope>test</scope>
</dependency>

```

##### SLF4J
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



