---
title: 编码
tags:
  - 乱码
  - 编码
  - http
categories:
  - 412A-语言基础
description: 进入文章
---
 
---

### javase中的编码

```java
public class TestEncoding {  
	public static void main(String[] args) {  
	System.out.println("你好,我是张三");  
	}  
}
```

控制台:
```console
"C:\Program Files\Java\jdk-17.0.3.1\bin\java.exe" ...

你好,我是张三


Process finished with exit code 0
```


以上这段代码从编写到运行中,编码是如何变化的呢?
![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1A1-JavaEE-image-20231115-212529.png)

##### 1.源文件编码
即创建文件时所选用的文件编码,由开发人员指定,通常设置为`UTF-8`

##### 2.编译器编码
- 使用哪种字符编码来读取解析源代码文件
- 在编译java代码时底层使用的是javac命令,此命令存在可选项`-encoding`,用于指定编码时使用的格式,例如`javac -encoding GBK HelloWorld.java`
- 如果在编译过程中未指定编码格式,将采用操作系统默认的编码格式
---
- 在日常开发中我们并不会使用命令去编译程序,而是使用IDEA,在idea中你可以这样设置编码器的编码格式: 
	- 方式一: 在File | Settings | Editor | File Encodings中设置
	- ![412A-A1A1-JavaEE-image-20231115-220448.png](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1A1-JavaEE-image-20231115-220448.png) 
- 方式二: 如果你使用了Maven,可以添加以下代码
```xml
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
```

##### 3.字节码编码
- 源代码中的字符串字面量(string literals)将以<font color="#3271ae">Modified UTF-8</font>的编码格式存储在`.class`文件中
- 字节码中字符串字面量的编码格式是固定的`Modified UTF-8`
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1A1-JavaEE-image-20231115-215903.png" width = 40%/></div>
##### 4.JVM内存编码
![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1A1-JavaEE-image-20231115-215032.png)
- JVM加载`.class`字节码类文件时会把`Modified UTF-8`格式的字符串字面量转换为<font color="#3271ae">UTF-16</font>编码
- JVM中的内存编码为`UTF-16`,也是<font color="#3271ae">固定</font>不变的


##### 5.输出流编码
- 输出到控制台的编码:
	- `System.out`使用的是JVM的默认编码,通常是操作系统的默认编码
	- 可以在JVM<font color="#3271ae">启动时</font>通过JVM参数 `-Dfile.encoding`来指定
- 输出到浏览器
	- `HttpServletResponse`:由开发人员指定

##### 6.显示编码
- 控制台显示的编码:通常是系统的默认编码
- 浏览器显示的编码: 自动检测
	- Http响应的`Content type`头
	- HTML文档中的 `<meta charset>`标签


注: 如果出现了乱码
- 要么是1和2的编码不兼容
- 要么是5和6的编码不兼容



### javaWeb中的编码

以下将从 Chrome发出一个请求 → Tomcat服务器接收 → 运行程序 → 响应数据到浏览器的过程说明

> 请求url: [http://localhost:8080/encode/编码?name=张三](http://localhost:8080/encode/编码?name=张三)


---
1.浏览器进行uri字符编码
- 浏览器发出请求(此处只说明get请求与post请求)
- 请求uri中存在非ASCII的字符(例如中文,此处还有其他情况需要进行编码,暂不讨论)
- 如果是get请求需要对字符进行百分号编码,Chrome的编码格式为`UTF-8`
- 如果是post请求,`application/x-www-form-urlencoded(需要对字符编码)`和`multipart/form-data(不需要对字符编码)`
- 于是经过uri对字符的"百分号编码"(只讨论字符编码)后以上链接就转变为
> `http://localhost:8080/encode/%E7%BC%96%E7%A0%81/?name=%E5%BC%A0%E4%B8%89`

- 传输: 根据http协议以上的url将会转成字节数组进行传输
---
2.Tomcat进行解码
- 步骤一:接收到字节数组后,会将字节码数组转成"百分号编码"形式的url
- 步骤二:将"百分号编码"形式的url解码成原样


说明1:对于步骤二的解码格式说明:
- 当前版本 <  Tomcat8.0 : 采用`ISO-8859-1`解码
- 当前版本 >= Tomcat8.0 : 采用`UTF-8`解码

[官方原文:](https://tomcat.apache.org/tomcat-8.0-doc/config/http.html)
![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1A1-JavaEE-image-20231116-170610.png)

> 这指定用于解码URI字节的字符编码， 在%xx解码URL之后。如果未指定，将使用UTF-8，除非 `org.apache.catalina.STRICT_SERVLET_COMPLIANCE` [系统属性](https://tomcat.apache.org/tomcat-8.0-doc/config/systemprops.html)设置为`true` 在这种情况下，将使用ISO-8859-1。




---

3.tomcat的JVM(启动Tomcat的jvm的file.encoding)
4.idea输出到控制台(启动Tomcat的jvm的file.encoding)


![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1A1-JavaEE-image-20231117-004607.png)




### 乱码问题的解决

#### 请求乱码

##### post

方式一 (在Spring中):
在web.xml中添加
```xml
<!--中文乱码响应-->
<!--
    private String encoding;//编码格式
    private boolean forceRequestEncoding;//请求编码,默认false,不开启
    private boolean forceResponseEncoding;//响应编码,默认false,不开启
-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceRequestEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
        <init-param>
            <param-name>forceResponseEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

```

方式二: 添加过滤器注解(在SpringMVC中)

```java
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }

    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter filter = new CharacterEncodingFilter();
        filter.setEncoding("UTF-8");
        return new Filter[]{filter};
    }
}
```

```java
@Configuration
@ComponentScan("controller包路径例如com.hello.controller")
@EnableWebMvc
public class SpringMvcConfig {
}

```



##### get
因为自从Tomcat8.0之后URIEncoding就默认设置为UTF-8,所以这是的get请求乱码的问题基本被解决

如果依旧存在:
> <font color="#3271ae">正确的做法是在Tomcat中设置URIEncoding</font>
> 在Tomcat安装包的根路径下找到`conf/server.xml`
> 进入文件中修改`Connector`标签,添加<font color="red">URIEncoding="UTF-8"</font>


<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1A1-JavaEE-image-20231117-005652.png" width = 40%/></div>

注: get请求乱码设置`request.setCharacterEncoding()`是<font color="red">无效</font>的



#### 响应乱码
本质上是为了设置`Content-Type`

方式一:(单个方法有效)
```java
response.setContentType("text/html;charset=UTF-8");
```

方式二:(单个方法有效)
```java
@RequestMapping(value="/路径",produces = "application/json; charset=utf-8")
```
注:虽然是`RequestMapping`中的属性,但produces的作用是指定<font color="#3271ae">返回值</font>类型和设定返回值的字符编码


jsp:(单个页面有效)
```xml
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```


#### @ResponseBody注解返回乱码

- 第一种方法就是以上的方式二

- 第二种是修改SpringMVC的配置文件,进行全局配置
> 使用HttpMessageConverter接口的相关实现类
> **基于spring3.2以后的配置文件。编码配置需要放在<mvc:annotation-driven/>之前，否则无效。**
```xml
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter" >  
    <property name="messageConverters">  
        <list>  
            <bean class="org.springframework.http.converter.json.MappingJacksonHttpMessageConverter" />  
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">  
                <property name="supportedMediaTypes">  
                    <list>  
                        <value>text/plain;charset=utf-8</value>  
                        <value>text/html;charset=UTF-8</value>  
                    </list>  
                </property>  
            </bean>  
        </list>  
    </property>  
</bean>  

```

并且需要在Maven依赖中配置上Jackjson的依赖。
```xml
<dependency>  
    <groupId>org.codehaus.jackson</groupId>  
    <artifactId>jackson-mapper-asl</artifactId>  
    <version>1.9.13</version>  
</dependency>  
<dependency>  
    <groupId>org.codehaus.jackson</groupId>  
    <artifactId>jackson-core-asl</artifactId>  
    <version>1.9.13</version>  
</dependency>  
```

- 方式三: 使用`<mvc:message-converters>`
> 还有一种方式是在SpringMVC的配置文件中的<mvc:annotation-driven>中加入<mvc:message-converters>的配置。具体配置内容如下：

```xml
<!-- SpringMVC注解驱动 -->
<mvc:annotation-driven>  
    <mvc:message-converters>  
        <bean class="org.springframework.http.converter.json.MappingJacksonHttpMessageConverter"/>  
        <bean class="org.springframework.http.converter.StringHttpMessageConverter">  
            <property name="supportedMediaTypes">  
                <list>  
                    <value>text/plain;charset=utf-8</value>  
                    <value>text/html;charset=UTF-8</value>  
                </list>  
            </property>  
        </bean>  
    </mvc:message-converters>  
</mvc:annotation-driven> 
```


注意：始用这种配置的时候，需要去掉RequestMappingHandlerMapping、RequestMappingHandlerAdapter或者DefaultAnnotationHandlerMapping、AnnotationMethodHandlerAdapter的Bean配置，要不然可能会不生效




---

> Citation:
> - []()
> 
> References:
> - [让Java世界中再无乱码！5分钟彻底掌握Java字符编码原理](https://www.bilibili.com/video/BV1Wg411R7Pb?vd_source=3fe14331de51767865a1e0e5e9b9e1c5)
> - [一文让你从此告别HTTP乱码（一）Request篇](https://www.cnblogs.com/brucecloud/p/6601322.html)
> - [Post，Get请求乱码的原因和解决方案](https://blog.csdn.net/a83370892/article/details/82726700)
> - [http请求（GET/POST）时，url/参数编码的过程分析](https://segmentfault.com/a/1190000015800019)
> - [关于 tomcat7 和 tomcat8 服务器编码的解释_tomcat7 编码-CSDN博客](https://blog.csdn.net/LawssssCat/article/details/103522231)
> - [application-x-www-form-urlencoded or multipart-form-data](http://stackoverflow.com/questions/4007969/application-x-www-form-urlencoded-or-multipart-form-data)
> - [tomcat工作原理（基本过程）](https://blog.csdn.net/qq_43677686/article/details/104089426)
> - [HTTP Post请求的四种编码方式](https://zhuanlan.zhihu.com/p/577537832)
> - [【SpringMVC】解决@ResponseBody注解返回中文乱码](https://blog.csdn.net/zsq520520/article/details/68107413)
