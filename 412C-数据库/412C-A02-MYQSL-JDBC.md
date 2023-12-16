---

title: java连接数据库
tags: [mysql,jdbc,myabtis,springboot,spring,专栏]
categories: [412C-数据库]
description: 进入文章

---

---
#### JDBC
##### 1.导入pom.xml
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

##### 2.编写JDBC代码
工具类:
```java
package cn.tianshi.utils;


import org.apache.commons.dbcp2.BasicDataSource;

import java.io.IOException;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

public class JDBCUtils {
    // 加载驱动，并建立数据库连接
    public static Connection getConnection() throws SQLException,
            ClassNotFoundException, IOException {
        InputStream in = JDBCUtils.class.getClassLoader().getResourceAsStream("jdbc.properties");
        Properties properties = new Properties();
        properties.load(in);
        String driverClassName=properties.getProperty("driverClassName");
        String url = properties.getProperty("url");
        String username = properties.getProperty("username");
        String password = properties.getProperty("password");
        System.out.println(url+"djd"+username);
        Class.forName(driverClassName);
//        Class.forName("com.mysql.cj.jdbc.Driver");
//        String url = "jdbc:mysql://localhost:3306/bookman?serverTimezone=GMT%2B8";
//        String username = "root";
//        String password = "root";

       Connection conn = DriverManager.getConnection(url, username,password);

        /*常见的开源数据库连接池：
        DBCP：速度比C3P0快但有bug
        c3p0:速度慢，但相对稳定
        Proxool：开源连接池，有监控连接池的功能，但稳定性比C3P0差
        BoneCP：速度快，开源
        Druid：阿里提供的连接池，速度快(不及BoneCP)，稳定性好，有监控连接池的功能
        1.DBCP
		BasicDataSource dbs=new BasicDataSource();  
		dbs.setDriverClassName(driverClassName);  
		dbs.setUrl(url);  
		dbs.setUsername(username);  
		dbs.setPassword(password);  
		Connection conn=dbs.getConnection();
        
        */

        return conn;
    }
    // 关闭数据库连接，释放资源
    public static void release(Statement stmt, Connection conn) {
        if (stmt != null) {
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
            stmt = null;
        }
        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
            conn = null;
        }
    }
    public static void release(ResultSet rs, Statement stmt,
                               Connection conn){
        if (rs != null) {
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
            rs = null;
        }
        release(stmt, conn);
    }
}
```


#### Mybatis

> Mybatis + JDBC

##### 1.导入pom文件

```xml

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->  
<dependency>  
  <groupId>org.mybatis</groupId>  
  <artifactId>mybatis</artifactId>  
  <version>3.5.6</version>  
</dependency>

<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.30</version>
</dependency>
```


##### 2.Mapper.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
	"http://mybatis.org/dtd/mybatis-3-mapper.dtd">  
<mapper namespace="">

</mapper>

```

注:*同时编写对应的接口文件*

##### 3.mybatis-config.xml
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
        <!--批量注册 mapper.xml
        name 为所有事的mapper.xml文件所在的包
        在resources文件目录下新建 com/nfjh/mapper
        此时不需要在pom.xml中设置资源文件扫描
        -->
        <package name="_mapper所在的包_"/>
    </mappers>
</configuration>
```



##### 4.jdbc.properties
```properties
jdbc.driverClassName=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:端口/数据库?useUnicode=true&characterEncoding=utf8&useSSL=true&serverTimezone=GMT%2B8
jdbc.username=root
jdbc.password=root
```

##### 5.test.java
```java
SqlSession sqlSession = null;  
Mapper mapper = null;
//日期的格式化刷子
SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd");
  
@Before  
public void openSession() throws IOException {  
    //1、创建资源流,读取核心配置文件  
    InputStream in = Resources.getResourceAsStream("核心配置文件");  
  
    //2、获取sql会话工厂  
    SqlSessionFactory build = new SqlSessionFactoryBuilder().build(in);  
  
    //3、获取sql会话对象  
    sqlSession = build.openSession();  
  
    //4、[取出动态代理对象]  
    mapper = sqlSession.getMapper(Mapper.class);  
  
  
    //5、执行操作  
  
    //6、[事务提交]  
}

@After  
public void  closeSession(){  
    //7、关闭会话  
    sqlSession.close();  
}


    @Test
    public void testUpdate() throws ParseException {
        Users u = new Users(7,"haha66",sf.parse("2000-01-01"),"2","北京大兴亦庄66");
        int num = uMapper.update(u);
        System.out.println(num);
        //切记切记切记:手工提交事务
        sqlSession.commit();
    }
```


#### Mybatis-plus
##### 1.导入pom.xml文件

```xml

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.2.5.RELEASE</version>
	</parent>
<!-- properties 标签位置 -->

	<dependencies>
		<!--Spring Web-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<!--Spring Test-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>

		<!--Mybatis-Plus-->
		<!-- https://mvnrepository.com/artifact/com.baomidou/mybatis-plus-boot-starter -->
		<dependency>
			<groupId>com.baomidou</groupId>
			<artifactId>mybatis-plus-boot-starter</artifactId>
			<version>3.5.3.2</version>
		</dependency>
		<!--JDBC-->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
		</dependency>
		<!--druid数据源|连接池依赖-->
		<dependency>
			<groupId>com.alibaba</groupId>
			<artifactId>druid-spring-boot-starter</artifactId>
			<version>1.1.10</version>
		</dependency>
		<dependency>
			<groupId>com.alibaba</groupId>
			<artifactId>druid</artifactId>
			<version>1.2.8</version>
		</dependency>
	</dependencies>
	
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
		<!--文件夹映射-->
		<resources>
			<resource>
				<directory>src/main/java</directory>
				<includes>
					<include>**/*.properties</include>
					<include>**/*.xml</include>
					<include>**/*.yml</include>
					<include>**/*.yaml</include>
				</includes>
				<filtering>false</filtering>
			</resource>
			<resource>
				<directory>src/main/resources</directory>
				<includes>
					<include>**/*.properties</include>
					<include>**/*.xml</include>
					<include>**/*.yml</include>
					<include>**/*.yaml</include>
				</includes>
				<filtering>false</filtering>
			</resource>
		</resources>
	</build>
<!-- 通过添加文件映射解决yaml文件查找不到,解决驱动查找失败,连接数据库失败的问题-->
```

##### 2.yaml文件(yml文件)
> 要保证添加的文件yaml/yml文件的后缀在pom中已经添加了映射
```yml
```



##### 环境
>如果在非springboot的环境下使用Mybatis


#### Spring

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







```



---

> Citation:
> - []()
> 
> References:
> - []()
