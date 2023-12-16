---

title: SpringBoot笔记
tags: [SpringBoot3,笔记,Spring]
categories: [412B-框架工具]
description: 进入文章
sticky: 200
---

---

## 1.SpringBoot 基础
### 什么是Spring Boot
##### 定义:
Spring Boot 是目前流行的微服务框架 倡导 约定优先于配置” 其设 目的是 用来简化新Spring 应用的初始化搭建以及开发过程。 Spring Boot 提供了很多核心的功 能，比如自动化配置 starter（启动器）简化Maven配置、内嵌 Servlet 容器、应用监控等功能， 让我们可以快速构建企业级应用程序

特性：

1. 创建独立的 Spring 应用程序。
2. 嵌入式 Tomcat、 Jetty、 Undertow 容器（jar）
3. 提供的 starters 简化构建配置（简化依赖管理和版本控制）
4. 尽可能自动配置 spring 应用和第三方库
5. 提供生产指标,例如指标、健壮检查和外部化配置
6. 没有代码生成，无需 XML 配置


SpringBoot 同时提供 “开箱即用”，“约定优于配置”的特性。

**开箱即用**：Spring Boot 应用无需从 0 开始，使用脚手架创建项目。基础配置已经完成。集成大部分第三方库对象，无需配置就能使用。例如在 Spring Boot 项目中使用 MyBatis。可以直接使用XXXMapper 对象，调用方法执行 sql 语句。

**约定优于配置**：Spring Boot 定义了常用类，包的位置和结构，默认的设置。代码不需要做调整，项目能够按照预期运行。比如启动类在根包的路径下，使用了@SpringBooApplication 注解。创建了默认的测试类。controller，service，dao 应该放在根包的子包中。application 为默认的配置文件

脚手架（spring 提供的一个 web 应用，帮助开发人员，创建 springboot 项目）

SpringBoot3 最小 jdk17， 支持 17-20. Spring Boot 理念“约定优于配置”，也可称为按约定编程

##### 与 Spring 关系
**Spring 框架:**

&emsp;Spring Boot 创建的是 Spring 应用，对于这点非常重要。也就是使用 Spring 框架创建的应用程序。这里的Spring是指 Spring Framework。 我们常说的 Spring，一般指 Spring 家族，包括 Spring Boot、Spring Framework、SpringData ，Spring Security,Spring Batch , Spring Shell, Spring for Apache Kafka ....


2004 年 3 月，Spring Framework1.0 发布。2006 年 10 月，Spring Framework2.0 发布。

&emsp;2006 年后开始，国内项目渐渐的开始应用 Spring 框架，2009 年 12 月，Spring3.0 发布。这时国内已经比较注重Spring 使用了。项目多数转移到 Spring 框架了。 我是在 2007 开始知道渐渐了解 Spring 框架。那个时候用Struts或者就是 jsp+servlet+jdbc 比较多。当时研发项目也没什么烦恼， 就一，两个技术可以用。没什么可选择的。现在的框架，技术太多了。2017 年 09 月，Spring Framework5.0 发布。 2022 年 11 月Spring Framework6.0发布。<br>
[第一个版本 1.0 的 blog](https://spring.io/blog/2004/03/24/spring-framework-1-0-final-released)

&emsp;Spring 的核心功能：IoC , AOP , 事务管理，JDBC，SpringMVC ， Spring WebFlux,集成第三方框架MyBatis,Hibernate, Kafka , 消息队列... 

&emsp;Spring 包含 SpringMVC， SpringMVC 作为 web 开发的强有力框架，是 Spring 中的一个模块。首先明确一点，Spring Boot 和 Spring Framework 都是创建的 Spring 应用程序。Spring Boot 是一个新的框架，看做是 Spring 框架的扩展，它消除了设置 Spring 应用程序所需的 XML 配置，为更快，更高效的创建Spring应用提供了基础平台。Spring Boot 能够快速创建基于 Spring ，SpringMVC 的普通应用以及Web 项目

&emsp;SpringBoot 是包含了 Spring 、SpringMVC 的高级的框架，提供了自动功能，短平快。能够更快的创建Spring应用。消除了 Spring 的 XML 配置文件，提供了开发效率，消除 Spring 应用的臃肿。避免了大量的样板代码。所以学习 Spring Boot 的建议：了解 Spring + SpringMVC 核心功能，基本应用是最好的，能够更快的上手SpringBoot。一般的 Spring Boot 课程中默认听众是会 Spring ，SpringMVC 


<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot0.png" width = 80%/> </div>
> 注: Spring Boot 在现在 Java 开发人员必须掌握的框架。Spring Boot 是掌握 Spring Cloud 的基础


##### 与 SpringCloud 关系
&emsp;微服务：微服务(Microservices Architecture)是一种架构和组织方法，微服务是指单个小型的但有业务功能的服务，每个服务都有自己的处理和轻量通讯机制，可以部署在单个或多个服务器上。

&emsp;将一个大型应用的功能，依据业务功能类型，抽象出相对独立的功能，称为服务。每个服务就上一个应用程序，有自己的业务功能，通过轻量级的通信机制与其他服务通信（通常是基于 HTTP 的RESTful API），协调其他服务完成业务请求的处理。 这样的服务是独立的，与其他服务是隔离的，可以独立部署，运行。与其他服务解耦合。

&emsp;微服务看做是模块化的应用，将一个大型应用，分成多个独立的服务，通过http 或rpc 将多个部分联系起来。请求沿着一定的请求路径，完成服务处理。

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot1.png" width = 80%/> </div>

&emsp;项目规模大，服务多。要构建大型的分布式应用，保证应用的稳定，高效，不间断的提供服务。SpringCloud是对分布式项目提供了，有力的支持。


&emsp;Spring Cloud 是一系列框架的有序的组合，为开发人员提供了快速构建分布式系统中常用工具(例如，配置管理、服务发现、断路器、智能路由、微代理、控制总线、一次性令牌、全局锁、领导选举、分布式会话、集群状态)。开发人员使用使用 Spring Cloud 这套框架和工具的集合可以快速建立实现分布式服务。这些框架需要使用Spring Boot 作为基础开发平台。

&emsp;学好了 Spring Boot，才能使用这些框架，创建良好的 Spring Cloud 应用。分布式应用。

&emsp;访问：https://spring.io/projects/spring-cloud

Spring Cloud 包含的这些框架和工具各负其职，例如 Spring Cloud Config 提供配置中心的能力，给分布式多个服务提供动态的数据配置，像数据库的 url，用户名和密码等，第三方接口数据等。Spring Cloud Gateway网关，提供服务统一入口，鉴权，路由等功能。

学习 Spring Colud 难度比较大，里面框架，工具比较多。有多个框架需要学习，在把框架组合起来又是一个难度。

##### Spring Boot3 新特性
&emsp;2022 年 11 月 24 日。Spring Boot3 发布，里程碑的重大发布。这个版本应该是未来5 年的使用主力。Spring官网支持 Spring Boot3.0.X 版本到 2025 年。

SpringBoot3 中的重大变化：

1. JDK 最小 Java 17,能够支持 17-20.
2. Spring Boot 3.0 已将所有底层依赖项从 Java EE 迁移到了 Jakarta EE API。原来javax 开头的包名，修改为 jakarta<br>
> 例如 jakarta.servlet.http.HttpServlet 原来 javax.servlet.http.HttpServlet
3. 支持 GraalVM 原生镜像。将 Java 应用编译为本机代码，提供显著的内存和启动性能改进。
4. 对第三方库，更新了版本支持。
5. 自动配置文件的修改。
6. 提供新的声明式 Http 服务，在接口方法上声明@HttpExchange 获取 http 远程访问的能力。代替OpenFeign
7. Spring HTTP 客户端提供基于 Micrometer 的可观察性. 跟踪服务，记录服务运行状态等
8. AOT（预先编译） 支持 Ahead Of Time，指运行前编译
9. Servlet6.0 规范
10. 支持 Jackson 2.14。
11 .Spring MVC :默认情况下使用的 PathPatternParser。删除过时的文件和 FreeMarker 、JSP 支持

伴随着 Spring Boot3 的发布，还有 Spring Framework 6.0 的发布(2022-11-16),先于Spring Boot 发布。

###  脚手架

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot2.png" width = 40%/> </div>

&emsp;脚手架是一种用在建筑领域的辅助工具，是为了保证建筑施工过程顺利进行而搭设的工作平台。软件工程中的脚手架是用来快速搭建一个小的可用的应用程序的骨架，将开发过程中要用到的工具、环境都配置好，同时生成必要的模板代码。

&emsp;脚手架辅助创建程序的工具，Spring Initializr 是创建 Spring Boot 项目的脚手架。快速建立Spring Boot 项目的最好方式。他是一个 web 应用，能够在浏览器中使用。IDEA 中继承了此工具，用来快速创建Spring Boot 项目以及 Spring Cloud 项目。



##### 在线脚手架
[阿里云脚手架](https://start.aliyun.com/)<br>
[Spring Initializr](https://start.spring.io/)  

以Spring Initializr举例:

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot3.png" width = 80%/> </div>
在存放项目的地方解压缩
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot4.png" width = 40%/> </div>
打开idea,project struct → import module
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot5.png" width = 40%/> </div>
选择上面的选择的构建方式
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot6.png" width = 40%/> </div>
文件结构
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot7.png" width = 100%/> 

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot8.png" width = 40%/> </div>

- .gitignore: 该文件指定哪些文件或文件夹不需要纳入到 Git 版本库中
- HELP.md: 该文件提供项目的帮助信息
- mvnw、mvnw.cmd: 这是 Maven Wrapper 的可执行文件，用于在不安装 Maven 的情况下构建项目。
- pom.xml: 该文件是 Maven 的配置文件，定义了工程的基本信息、依赖关系等。
- .mvn/wrapper: 该目录包含 Maven Wrapper 相关的文件。
- src/main/java: 该目录包含主要的 Java 代码文件，用来实现项目的业务逻辑和功能。
- src/main/resources: 该目录包含主要的配置文件和资源文件，比如数据库连接、日志配置等。
- src/main/resources/static: 该目录一般存放静态资源文件，比如图片、CSS 文件等。
- src/main/resources/templates: 该目录一般存放 HTML 模板文件，用于后台将数据渲染成最终的 HTML 页面。
- src/test/java: 该目录包含测试用例 Java 代码文件，用于测试项目的正确性和稳定性等

阿里的脚手架同理


##### idea脚手架
idea → 菜单 → File → new → module
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot9.png" width = 80%/> </div>

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot10.png" width = 80%/> </div>

**可能遇到的问题**

- 只出现了项目,但是没有显示文件结构,右击项目,找到`↺Reload from Disk`刷新就行<br>
- pom.xml的图标没有变蓝,在pom.xml上右键 `+ Add as Maven Project`<br>
- pom.xml中`<artifactId>spring-boot-maven-plugin</artifactId>`爆红<br>
> 添加上版本`<version>2.2.1.RELEASE</version>`然后刷新

### 代码结构
##### 单一模块
一个工程一个模块的完整功实现
```
com.example.模块名称
    +----Application.java 启动类
    +----controller 控制器包
        ---StudentController.java
        ---ScoreController.java
    +----service 业务层包
        ---inter 业务层接口
        ---impl 接口实现包
    +----repository 持久层包
    +----model 模型包
        ---entity 实体类包
        ---dto 数据传输包
        ---vo 视图数据包
```

##### 多个模块
一个 Spring Boot 中多个模块。在根包下创建每个模块的子包， 子包中可以按“单一模块”包结构定义。创建包含多个功能的单体 Spring Boot。

##### 包和主类
&emsp;我们通常建议您将主应用程序类定位在其他类之上的根包中。@SpringBootApplication 注释通常放在主类上，它隐式地为某些项定义了一个基本的“搜索包”。例如，如果您正在编写一个 JPA 应用程序，则使用@SpringBootApplication 注释类的包来搜索@Entity 项。使用根包还允许组件扫描只应用于您的项目。

&emsp;Spring Boot 支持基于 java 的配置。尽管可以将 SpringApplication 与 XML 源一起使用，但我们通常建议您的主源是单个@Configuration 类。通常，定义主方法的类可以作为主@Configuration 类。


##### `<parent>`
&emsp;pom.xml 中的<parent>指定 spring-boot-starter-parent 作为坐标，表示继承 Spring Boot 提供的父项目。从spring-boot-starter-parent 继承以获得合理的默认值和完整的依赖树，以便快速建立一个Spring Boot 项目。父项目提供以下功能:

- JDK 的基准版本，比如`<java.version>17</java.version>`
- 源码使用 UTF-8 格式编码
- 公共依赖的版本
- 自动化的资源过滤：默认把 src/main/resources 目录下的文件进行资源打包
- maven 的占位符为`@`
- 对多个 Maven 插件做了默认配置，如 maven-compile-plugin，maven-jar-plugin


快速创建 Spring Boot 项目，同时能够使用父项目带来的便利性，可以采用如下两种方式：

1. 在项目中，继承 spring-boot-starter-parent
```xml
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.0.5</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

```
2. pom.xml 不继承，单独加入 spring-boot-dependencies 依赖<br>
在`<properties>`标签的下面,与`<dependencies>`同级

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>3.0.1</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

##### starter
starter 是一组依赖描述，应用中包含 starter，可以获取 spring 相关技术的一站式的依赖和版本
不必复制、粘粘代码。通过 starter 能够快速启动并运行项目

starter 包含：

- 依赖坐标、版本
- 传递依赖的坐标、版本
- 配置类，配置项

##### @SpringBootApplication
```java
/**
 * 核心注解功能
 *    @SpringBootConfiguration： 包含@Configuration注解的功能
 *      @Configuration： JavaConfig的功能，配置类，结合@Bean能够将对象注入到spring的IOC容器。
 *      有@SpringBootConfiguration标注的类是配置类，Lession06PackageApplication是配置类
 *
 * @EnableAutoConfiguration ： 开启自动配置。 将spring和第三方库中的对象创建好，注入到spring容器
 *                             避免写xml，去掉样例代码。 需要使用的对象，由框架提供。
 *
 * @ComponentScan ： 组件扫描器，<context:component-scan base-package="xxx包"/>
 *        扫描@Controller, @Service, @Repository ,@Component注解， 创建他们的对象注入到容器
 *        springboot约定:启动类，作为扫描包的根（起点）， @ComponentScan扫描com.bjpowernode.pk
 *        和它的子包中所有的类。
 */
@SpringBootApplication
public class Lession06PackageApplication {

  @Bean
  public Date myDate(){
    return new Date();
  }

  public static void main(String[] args) {
    //run方法的第一个参数是 源（配置类），从这里加载bean，找到bean注入到spring的容器
    //run方法返回值是容器对象
    ApplicationContext ctx  = SpringApplication.run(Lession06PackageApplication.class, args);

    //可以从容器获取对象
    Date bean = ctx.getBean(Date.class);
  }

}

```

###   配置文件
##### 配置文件格式
&emsp;配置文件有两种格式分别：properies 和 yaml（yml）。properties 是 Java 中的常用的一种配置文件格式，key=value。key 是唯一的，文件扩展名为 properties。

&emsp;yaml（YAML Ain't Markup Language）也看做是 yml，是一种做配置文件的数据格式，基本的语法key:[空格]值。yml 文件文件扩展名是 yaml 或 yml（常用）


**[YAML 基本语法规则:](https://zhuanlan.zhihu.com/p/145173920)**

- 大小写敏感
- 使用缩进表示层级关系
- 缩进只可以使用空格，*不允许使用 Tab 键*
- 缩进的空格数目不重要，相同层级的元素左侧对齐即可
- `#`字符表示注释，只支持单行注释。#放在注释行的第一个字符

> YAML 缩进必须使用空格，而且区分大小写，建议编写 YAML 文件只用小写和空格


**YAML 支持三种数据结构**

- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
- 标量（scalars）：单个的、不可再分的值，例如数字、字符串、true|false 等

需要掌握数据结构完整内容，可从 https://yaml.org/type/index.html 获取详细介绍。

##### application文件
application文件了解:

- Spring Boot3 的核心配置文件,有 application.properties 与 application.yml两种形式
- 默认情况下自动加载properties文件,即:若两种同时存在,加载properties文件
- 虽然Spring Boot 同时支持两种文件,但是建议使用一种格式的配置文件(风格统一,编写时思路更清晰)
- 由于yaml文件的格式清晰,且可以避免写相同的前缀,所以开发时通常使用yml文件
- application 配置文件的名称和位置都可以修改。约定名称为 application，位置为 resources 目录




##### 组织多文件
1.为什么存在组织多文件:<br>
&emsp;整个项目会涉及到多个中间件,多个配置,若使用单个文件表述,会导致内容复杂,结构不清晰,可读性下降<br>
&emsp;其实这种拆分思想在日场开发中经常使用,最常见的就是分包,分模块,在SpringMVC中我们已经学过了类似的操作,对配置文件拆分,在核心文件中导入,使文件结构更清晰

2.application文件的使用
> 不管是yaml文件还是properties文件,其本质上都是为了数据的存储<br>
> 所以以下以数据的存与储进行展开

实际操作:<br>
1> 在resource文件夹下自定义一个文件夹,此处我写做config<br>
2> 在config下创建需要配置的文件,例如Redis.yml 和 db.yml (当然此处的文件也可以是properties文件)<br>
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot13.png" width = 40%/> </div>
3> 在application文件中导入<br>

- .properties 
```properties
spring.config.import =  config/db.yml ,config/redis.yml
```

- .yml文件
```yaml
spring :
    config :
      import :
       config/db.yml ,config/redis.yml
```

4> 存储数据(以db.yml为例,Redis.yml同理)<br>

- .properties 
```properties
spring.db.url = jdbc:mysql://localhost:3306/boot_db
spring.db.name = root
spring.password = root
```

- .yml文件
```yaml
spring :
     db :
        url : jdbc:mysql://localhost:3306/boot_db
        name : root
        password : root
```

5> 数据注入<br>

> 创建config包(在main/java/项目/config)<br>
> 创建MultiConfigService.java

```java
//添加注解
@Service
public class MultiConfigService{
    //使用@Value关联配置文件,进行数据注入
    //若password不存在,设置默认值为"root"
    @Value("${spring.db.password:root}")
    private String dbPassword;
    
    public void printMultiConfig(){
        System.out.println(dbPassword)
    }

}
```

6> 数据读取<br>
> 在测试类中读取数据

```java
	@Autowired
	private MultiConfigService multiConfig;

	@Test
	void testMultiConfig() {
		multiConfig.printMultiConfig();
	}
```




##### Environment
Environment 是外部化的抽象，是多种数据来源的集合。从中可以读取 **application 配置文件，环境变量，系统属性**。使用方式在 Bean 中注入 Environment。调用它的 getProperty(key)方法。

数据
```yaml
app :
  name : hello
  owner : true
  port : 8080
```
1> 创建ReadConfigService类,注入Environment<br>
```java
@Service
public class ReadConfig {

    private Environment environment;

    public void print(){
    String name = environment.getProperty("app.name");
    //key 是否存在
    if (environment.containsProperty("app.owner")) {
    System.out.println("有 app.owner 配置项");
    }
    //读取 key 转为需要的类型，提供默认值 8000
    Integer port = environment.getProperty("app.port", Integer.class, 8000);String result = String.format("读取的 name：%s，端口port：%d", name,port);System.out.println("result = " + result);
    }
}
```

2> 在测试类中注入ReadConfig,调用print方法
```
有 app.owner 配置项
result = 读取的 name：Lession07-yml，端口 port：8002
```



##### 多环境配置
1.为什么需要多配置环境<br>
```
Spring Profiles 表示环境，Profiles 有助于隔离应用程序配置，并使它们仅在某些环境中可用。
常说开发环境，测试环境，生产环境等等。一个环境就是一组相关的配置数据， 支撑我们的应用在这些配置下运行。
应用启动时指定适合的环境
```

2.名称 application-{profile}.properties(yml)<br>
```
 profile 为自定义的环境名称，推荐使用 
    dev 表示开发 ，
    test 表示测试。
    prod 表示生产，
    feature 表示特性。总之 profile 名称是自定义的。
    SpringBoot会加载 application 以及 application-{profile}两类文件，
    不是只单独加载 application-{profile}
```

3.创建与使用<br>
1> 在resource下创建文件<br>
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot14.png" width = 40%/> </div>

2> 配置环境<br>

- application-dev.yml

```yaml
app :
  name : 开发环境
spring:
  config:
    activate:
      on-profile: dev # 当前文件其作用时的环境名称
```

- application-test.yml
```yaml
app :
  name : 测试环境
spring:
  config:
    activate:
      on-profile: test # 当前文件其作用时的环境名称
```

3> 激活指定环境
application.yml
```yaml
spring :
    config :
      import :
       config/db.yml ,config/redis.yml

    profiles :
      active : dev # 需要激活的文件的环境名称
```

4> 测试
```java
@Service
public class MultiConfig {
        @Value("${app.name}")
        private String appName;
        public void printAppName(){
        System.out.println(appName);
    }
}
/*在测试类中调用方法
Console :
    ????
明显出现编码问题,在IDEA的右下角更改编码格式为UTF-8
重新写"开发环境"四个字,再次运行
Console: 
    开发环境
*/
```

> 看了上面的yaml文件与properties文件的开发实例,不难发现<br>
> 如果以上的环境配置为properties文件时,只需要将yaml结构中的 ':'<br>
> 换成 '.' 并写出完整的结构即可<br>
> `spring.config.import =  config/db.yml ,config/redis.yml`


### 绑定Bean 
#####  绑定Bean

- @Value绑定单个属性,但属性多时不方便
- @ConfigurationProperties 注解配合JavaBean可以进行多配置项绑定
- Bean的属性若为static则该属性无效
- @ConfigurationProperties 能够配置多个简单类型属性，同时支持 Map，List，数组类型。对属性还能验证基本格式


##### 简单的绑定
1. 数据准备<br>
```yaml
student : 
 name : jack
 age : 12
 address : 北京大兴区
```

2. 创建Bean,定义属性,属性名同yaml文件中的key<br>
```java
/**
@ConfigurationProperties 声明在类上，表示绑定属性到此类。
prefix 表示前缀，是配置文件中多个key 的公共前缀。
这些 key 以“.”作为分隔符。例如 app.name, app: name 等。 
prefix=”app”, 将文件中app 开始的key都找到，调用与 key 相同名称的 setXXX 方法。如果有给属性赋值成功。没有的忽略。
 */


@Configuration//使用@Component也可以
@ConfigurationProperties(prefix = "student")
public class Student {
    private String name;
    private Integer age;
    private String address;
   
    //无参构造,get,set,toString
}

/**
@Configuration的proxyBeanMethods = true,默认使用代理
如果希望是一个普通的类,不设置代理的话,改为false即可

**/
```

3. 测试
```java
	@Autowired
	private Student student;

	@Test
	void testBean(){
		System.out.println(student);
        System.out.println(student.getClass());
        //proxyBeanMethods = true (默认不写) → class com.power.pojo.Student$$SpringCGLIB$$0
        //proxyBeanMethods = false → class com.power.pojo.Student
	}
/**
Console:
Student{name='jack', age=12, address='北京大兴区'}

 */
```


##### 嵌套Bean
Bean 中包含其他 Bean 作为属性，将配置文件中的配置项绑定到 Bean 以及引用类型的成员


1> 数据准备<br>
```yaml
app:
 name: Lession07-yml
 owner: bjpowernode
 port: 8002
 security:
 #  注意缩进
  username: root
  password: 123456
```

2> 创建Bean<br>
```java
public class Security {
    private String username;
    private String password;
    //....
}
@Configuration(proxyBeanMethods = false)
@ConfigurationProperties(prefix = "app")
public class NestAppBean {
    private String name;
    private String owner;
    private Integer port;
    private Security security;
    // ... 
}

```

3> 测试<br>
```java
	@Autowired
	private NestAppBean nestAppBean;

	@Test
	void testNestAppBean(){
		System.out.println(nestAppBean);
	}
/**
Console:
NestAppBean{name='dev', owner='bjpowernode', port=8002, security=Security{username='root', password='123456'}}
 */
```

##### 扫描注解
启动配置的方式<br>

1.@Configuration + @ConfigurationProperties <br>

2.@ConfigurationProperties + @EnableConfigurationProperties<br>
```java
@ConfigurationProperties(prefix = "app")
public class NestAppBean {...}

//属性是配置类的名字
@EnableConfigurationProperties({NestAppBean.class })
@SpringBootApplication
public class Lession07ConfigApplication {...}
```

3.@ConfigurationProperties +@ConfigurationPropertiesScan
```java
@ConfigurationProperties(prefix = "app")
public class NestAppBean {...}

//属性是配置类所在的包
@ConfigurationPropertiesScan({"com.power.pojo"})
@SpringBootApplication
public class Lession07ConfigApplication {...}
```

##### 处理第三方库对象
1.什么时候使用
- 如果某个类需要在配置文件中提供数据，但是**没有源代码**
- @ConfigurationProperties 结合@Bean 一起在方法上面使用<br>
比如现在有一个 Security 类是第三方库中的类，现在要提供它的 username，password 属性值。

2.操作<br>
1> 数据准备<br>
```yaml
security:
 username: common
 password: abc123
```

2> 创建配置类<br>
```java
@Configuration
public class ApplicationConfig {
    @ConfigurationProperties(prefix = "security")
    @Bean
    public Security createSecurity(){
    return new Security();
    }
}
```


3> 单元测试<br>
```java
@SpringBootTest
public class BeanMethodTest {
    @Autowired
    private Security security;
    @Test
    void test01() {
    System.out.println("security = " + security);
    }
}
/**
Console :
    security = Security{username='common', password='abc123'}
 */
```


##### 集合 Map List  Array
使用方法参考嵌套Bean

1> 数据准备<br>
```yaml
#集合以及数组
#List<String> names
names:
  - lisi
  - zhangsan

#List<MyServer> servers
servers:
  - title: 华北服务器
    ip: 202.12.39.1
  - title: 西南服务器
    ip: 106.90.23.229
  - title: 南方服务器
    ip: 100.21.56.23

#Map<String,User> users
users:
  user1:
    name: 张三
    sex: 男
    age: 22
  user2:
    name: 李四
    sex: 男
    age: 26
```

2> javaBean创建<br>
```java
public class User {
    private String name;
    private String sex;
    private Integer age;
    //set | get ,toString
}
public class MyServer {
    private String title;
    private String ip;
    //set | get ,toString
}
@ConfigurationProperties
public class CollectionConfig {
    private List<MyServer> servers;
    private Map<String,User> users;
    private String [] names;
    //set | get ,toString
}
```


3> 添加包扫描
```java
@ConfigurationPropertiesScan({"其他包","com.bjpowernode.config.pk5"})
@SpringBootApplication
public class Lession07ConfigApplication {...}
```

4> 单元测试
```java
    @Autowired
    private CollectionConfig collectionConfig;
    @Test
    void test01() {
    String str = collectionConfig.toString();
    System.out.println("str = " + str);
    }
/**
Console:
str = CollectionConfig{servers=[MyServer{title='华北服务器', ip='202.12.39.1'}, MyServer{title='西南服务器', ip='106.90.23.229'}, MyServer{title='南方服务器', ip='100.21.56.23'}], users={user1=User{name='张三', sex='男', age=22}, user2=User{name='李四', sex='男', age=26}}, names=[lisi, 
 */
```

```
“-”表示集合一个成员，因为成员是对象，需要属性名称指定属性值。
List 与数组前面加入“-”表示一个成员。
Map 直接指定 key 和 value，无需“-”。
```


##### 指定数据源文件
指定某个文件作为数据来源。@PropertySource 是注解，用以加载指定的 **properties** 文件<br>
@PropertySource 与@Configuration一同使用，其他注解还有@Value，@ConfigurationProperties


1> 数据准备
```yaml
group.name = 中文
group.leader = 无名
group.members = 500
```
2> javaBean创建
```java
@Configuration
@ConfigurationProperties(prefix = "group")
@PropertySource(value = "classpath:/group-info.properties")
public class Group {
    private String name;
    private String leader;
    private Integer members;
    //set | get ,toString
}
```

3> 单元测试
```java
@Autowired
private Group group;
@Test
void test01() {
System.out.println("group = " + group.toString());
}
/**
Console:
group = Group{name='IT 学习专栏', leader='无名', members=500}
 */
```


##### 创建对象三种方式

- 传统的 XML 配置文件
- Java Config 技术， @Configuration 与@Bean
- 创建对象的注解，@Controller ，@Service ， @Repository ，@Component

Spring Boot 不建议使用 xml 文件的方式， 自动配置已经解决了大部分 xml 中的工作了<br>
如果需要xml 提供bean的声明，@ImportResource 加载 xml 注册 Bean。

1> 创建 Person 类，对象由容器管理
```java
public class Person {
    private String name;
    private Integer age;
    //set | get ,toString
}
```

2> 数据准备resources 目录下创建 XML 配置文件<br>
applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myPerson" class="com.bjpowernode.config.pk7.Person">
    <property name="name" value="李四" />
    <property name="age" value="20" />
    </bean>

</beans>
```

3> : 启动类，从容器中获取 Person 对象
```java
@ImportResource(locations = "classpath:/applicationContext.xml")
@ConfigurationPropertiesScan({"com.bjpowernode.config.pk4",
"com.bjpowernode.config.pk5"})
@SpringBootApplication
public class Lession07ConfigApplication {
public static void main(String[] args) {
    ApplicationContext ctx =
    SpringApplication.run(Lession07ConfigApplication.class, args);Person myPerson = (Person) ctx.getBean("myPerson");
    System.out.println("myPerson = " + myPerson);
    }
}

/**
Console:
myPerson = Person{name='李四', age=20}
 */

```


##### AOP
Spring中怎么用,这里就怎么用<br>
SpringBoot中的aop依赖<br>
```xml
    <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
    </dependency>
```


## 2.自动配置

什么是自动配置:<br>

- Springboot 框架提供快速创建spring与第三方库对象的一种方式
- 原理是:从类路径中查找xxx.jar,创建这个jar中的某些Bean <br>
> 例如:mybatis.jar, 进一步创建SqlSessionFactory, 还需要 DataSource 数据源对象,尝试连接数据<br>
- 以上这些工作由XXXAutoConfiguration类(自动配置类)完成<br>
-在 spring-boot-autoconfigure-3.0.2.jar 定义了很多的 XXXAutoConfiguration 类
- 第三方框架的starter 里面包含了自己 XXXAutoConfiguration
> 第三方框架 MyBatis，mybatis-spring-boot-starter 的 MyBatisAutoConfiguration 自动配置类


<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot15.png" width = 80%/> </div>


## 3.JDBCTemplate
㊟:使用方法同spring中的JDBCTemplate,不在赘述


##### 配置JDBCTemplate
1.pom.xml

- MySQL Driver
- JDBC API
- Lombok(非必要)

2.配置文件(resource下)
1>application.properties

```properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/blog?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf8&autoReconnect=true&useSSL=false
spring.datasource.username=root
spring.datasource.password=root

#总是执行数据库脚本,创建成功后设置为 never,不然会报错
spring.sql.init.mode=always
```

2> 创建schema.sql文件<br>
> DDL (Data Define Languge:数据定义语言)<br>

```sql
-- 正常编写建库建表语句即可
CREATE TABLE `article`
(
    `id`          int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
    `user_id`     int(11) NOT NULL COMMENT '作者 ID',
    `title`       varchar(100) NOT NULL COMMENT '文章标题',
    `summary` varchar(200) DEFAULT NULL COMMENT '文章概要',
    `read_count`  int(11) unsigned zerofill NOT NULL COMMENT '阅读读数',
    `create_time` datetime     NOT NULL COMMENT '创建时间',
    `update_time` datetime     NOT NULL COMMENT '最后修改时间',
    PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4;

```

3> 创建data.sql

> DML (Data Manipulate Language:数据操作语言)<br>
```sql
-- 正常编写增删改查语句即可
INSERT INTO `article`
VALUES ('1', '2101', 'SpringBoot 核心注解','核心注解的主要作用', '00000008976', '2023-01-16 12:11:12', '2023-01-16 12:11:19');
INSERT INTO `article`
VALUES ('2', '356752', 'JVM 调优','HotSpot 虚拟机详解', '00000000026', '2023-01-16 12:15:27', '2023-01-16 12:15:30');
```


3.JavaBean准备
```java
//Lombok的注解,不使用的话就手动补全javaBean的其他方法
@Data//数据
@NoArgsConstructor//无参构造
@AllArgsConstructor//全参构造


public class Article {
    private Integer id;
    private Integer userId;
    private String title;
    private String summary;
    private Integer readCount;
    private LocalDateTime createTime;
    private LocalDateTime updateTime;
}
```

4. 测试
```java
//注意此处使用的是@Resource注入
    @Resource
    JdbcTemplate jdbcTemplate;
    @Test
    void testJdbcTemplate(){
        String sql = "select count(*) as ct from article ";
        Long count = jdbcTemplate.queryForObject(sql,Long.class);
        System.out.println(count);
    }

    @Test
    void testQuery() {
// ？作为占位符
        String sql = "select * from article where id= ? ";
    //BeanPropertyRowMapper 将查询结果集，列名与属性名称匹配，名称完全匹配或驼峰
    // 此处没办法使用Record,此处是需要无参构造的,而Record不提供无参构造
    Article article = jdbcTemplate.queryForObject(sql,new BeanPropertyRowMapper<>(Article.class), 1 );
        System.out.println("查询到的文章 = " + article);
    }
```
> 其他的不在测试,详细见Spring的JdbcTemplate

## 4.Mybatis

依赖:

- mysql驱动
- mybatis依赖
- Lombok (可选)

##### 单表的CRUD
&emsp;相较于直接使用Mybatis,在Springboot中省去了大量的配置,非必要可以不写`mapper/*.xml`文件
,在mapper包中的接口中通过为方法添加注解的方式完成sql的编写,常用注解为`@Select`、`@Insert`、`@Delete` 、`@Update`<br>

所以需要准备的文件为:

- javaBean
- mapper/XxxMapper (接口,编写抽象方法和sql)
- application.properties(添加数据源)(必要时配置别名、导入其他XxxMapper.xml等)
- pom.xml依赖


例如:<br>
1、javaBean 
```java
//使用了Lombok
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Article {
    private Integer id;
    private Integer userId;
    private String title;
    private String summary;
    private Integer readCount;
    private LocalDateTime createTime;
    private LocalDateTime updateTime;
}
```


2、接口
```java
@Insert("""
insert into
article(user_id,title,summary,read_count,create_time,update_time) \
values(#{userId},#{title},#{summary},#{readCount},#{createTime},#{updateTime})""")
int insertArticle(ArticlePO article);
```
以上产生了个问题:user_id与userId 无法对应,即列名与属性无法映射?<br>
解决的方法有四种:

- 直接在sql语句中为下划线的列名起别名
- 在application.properties文件中添加驼峰转换<br>
> `mybatis.configuration.map-underscore-to-camel-case=true`<br>
- 在XxxMapper.xml中进行映射,在application.properties文件中导入<br>
> `mybatis.mapper-locations=classpath:/mapper/**/*.xml`<br>
- 使用@Results注解进行映射<br>

例如以上的sql在使用Xml映射的语句如下<br>
```xml
    <resultMap id="ArticleMapper" type="com.power.pojo.Article">
        <id column="id" property="id"/>
        <result column="user_id" property="userId" />
        <result column="read_count" property="readCount" />
        <result column="create_time" property="createTime" />
        <result column="update_time" property="updateTime" />
    </resultMap>
```



例如以上的sql在使用@Results映射的语句如下<br>
```java
  @Results(id = "BaseMapper", value = {
  @Result(id = true, column = "id", property = "id"),
  @Result(column = "user_id", property = "userId"),
  @Result(column = "read_count", property = "readCount"),
  @Result(column = "create_time", property = "createTime"),
  @Result(column = "update_time", property = "updateTime"),
  })
  Article articleMapper();
```

**@ResultMap 指定使用哪个结果映射**


##### SQL 提供者
不在XxxMapper接口中写方法,创建一个只用来写sql的java类,其中的方法为:<br>
```java
public static String 方法名(){
  return """
  sql语句
  """;
}
```

在XxxMapper中通过注解使用需要的sql,(`@SelectProvider`，`@InsertProvider`，`@UpdateProvider`，@DeleteProvider`)
例如:
```java
@SelectProvider(type = sql提供者类名.class,method = "方法名")
ArticlePO selectById(Integer id);
```

@One与@Many比较简单,直接看文档

##### 常用配置
- 在application文件中进行配置
```properties
#驼峰命名
mybatis.configuration.map-underscore-to-camel-case=true
#mapper xml 文件位置
mybatis.mapper-locations=classpath:/mappers/**/*.xml
#启用缓存
mybatis.configuration.cache-enabled=true
#延迟加载
mybatis.configuration.lazy-loading-enabled=true
#mybatis 主配置文件，按需使用
mybatis.config-location=classpath:/sql-config.xml
```

- 在mybatis的主配置文件中配置
如果配置较多,可以放在mybatis的主配置文件中(resource/),然后再application文件中通过`mybatis.config-location`进行加载
具体的配置内容还是Mybatis的老一套<br>

mybatis-config.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
    <setting name="cacheEnabled" value="true"/>
    <setting name="lazyLoadingEnabled" value="true"/>
    <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
    <typeAliases>
    <package name="com.bjpowernode.po"/>
    </typeAliases>
</configuration>
```

引用:`mybatis.config-location=classpath:/mybatis-config.xml`

[Mybatis的配置](https://mybatis.org/mybatis-3/zh/configuration.html#settings)

##### 合适的连接池

- [HikariCP 连接池](https://github.com/brettwooldridge/HikariCP/wiki)
- [连接池配置](https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing)
- [MySQL 连接池配置建议](https://github.com/brettwooldridge/HikariCP/wiki/MySQL-Configuration)

application.yaml
```yaml
spring:
 datasource:
 type: com.zaxxer.hikari.HikariDataSource
  driver-class-name: com.mysql.cj.jdbc.Driver
  url: jdbc:mysql://localhost:3306/blog?serverTimezone=Asia/Shanghai
  username: root
  password: 123456
  hikari:
    auto-commit: true
    # # connections = ((cpu 核心数 * 2) + 磁盘数量) 近似值。默认10
    maximum-pool-size: 10
    #最小连接数，默认 10，不建议设置。默认与 maximum-pool-size 一样大小。推荐使用固定大小的连接池
    minimum-idle: 10
    #获取连接时，检测语句
    connection-test-query: select 1
    ###
    # 连接超时，默认 30 秒。
    # 控制客户端在获取池中 Connection 的等待时间，
    # 如果没有连接可用的情况下超过该时间，则抛出 SQLException 异常，###
    connection-timeout: 20000
    #其他属性
    data-source-properties:
      cachePrepStmts: true
      dataSource.cachePrepStmtst: true
      dataSource.prepStmtCacheSize: 250
      dataSource.prepStmtCacheSqlLimit: 2048
      dataSource.useServerPrepStmts: true
```

##### 事务
这里做简单的概括:

- 事务的处理在Service层
- 可以使用Xml配置事务
- SpringBoot处理的`public`方法,私有、受保护的、或者包可见的不会报错,但事务也不会生效<br>
> 如果需要受保护的、私有的方法具有事务考虑使用 AspectJ。而不是基于代理的机制<br>
- 使用的注解是`@Transactional`,Spring团队建议您只使用@Transactional 注释具体类(以及具体类的方法)，而不是注释接口<br>
> 当然，可以将@Transactional 注解放在接口(或接口方法)上，但这只有在使用基于接口的代理时才能正常工作<br>


如何开启事务:

- service层中为需要使用事务的类或`public`的方法
- 在启动类上添加注解`@EnableTransactionManagement`

什么时候事务无效

- A方法使用了注解,B调用了A方法(B没有添加注解) ,此时A的事务无效<br>
> 只有通过代理对象调用具有事务的方法才能生效<br>
- 方法在线程中运行的，在同一线程中方法具有事务功能， 新的线程中的代码事务无效



## 5.Web

### Web项目构建
##### 初始化一个Web
- Lombok
- Spring Web
- Thymeleaf

打包方式:jar


##### 构架Web应用
1.在template中存放的文件,在@RequestMapping方法中返回"文件名"可访问
2.如果Controller需要发出JSON数据,使用@ResponseBody注解
3.使用响应流返回json字符串时,添加响应头
4.添加favicon图标,通过[网站](https://quanxin.org/favicon )生成图标,放在resources或resources/static文件夹下,在视图文件中<head>添加`<link rel="icon" href="../favicon.ico" type="image/x-icon"/>` 如果没有出现检查href路径,清除浏览器缓存


### Spring MVC 
##### 控制器Controller
使用同Spring,说一下需要注意的点

&emsp;SpringMVC 支持多种策略，匹配请求路径到控制器方法。AntPathMatcher 、PathPatternParser,
从 SpringBoot3 推荐使用 PathPatternParser 策略。比之前 AntPathMatcher 提示 6-8 倍吞吐量。

通配符：

-`?` : 一个字符
- `*` ： 0 或多个字符。在一个路径段中匹配字符
-`**`：匹配 0 个或多个路径段，相当于是所有
- 正则表达式： 支持正则表达式

RESTFul 的支持路径变量:

- `{变量名}`
- `{myname:[a-z]+}`: 正则皮 a-z 的多个字面，路径变量名称“myname”。@PathVariable(“myname”)
- `{*myname}`: 匹配多个路径一直到 uri 的结尾


#####  @RequestMapping
@RequestMapping的使用方法同Spring<br>
以下为@RequestMapping的常见接收参数的方式:

- 请求参数与形参一一对应，适用简单类型。形参可以有合适的数据类型，比如String，Integer ，int 等。 
- 对象类型，控制器方法形参是对象，请求的多个参数名与属性名相对应。
- @RequestParam 注解，将查询参数，form 表单数据解析到方法参数，解析 multipart 文件上传。 
- @RequestBody，接受前端传递的 json 格式参数。
- HttpServletRequest 使用 request 对象接受参数， request.getParameter(“...”)
- @RequestHeader ,从请求 header 中获取某项值

##### 验证参数
在javaBean中为需要验证的属性添加相应的注解,需要注意的是在不同情况下对同一个属性需要的验证要求可能不同,此时需要“分组验证”<br>

如何使用分组验证:

- 在需要使用分组验证的javaBean中添加组(接口)<br>
```java 
public static interface EditArticleGroup { };
```
- 在需要分组的属性的注解中添加
```java
@NotNull(message = "文章 ID 不能为空", groups = { EditArticleGroup.class})private Integer id;
/*
以上注解表示的是
@NotNull注解为“编辑修改组”服务
 */
```
- 在需要使用验证的位置对javaBean添加`@Validated`注解开启指定组的验证<br>
> 例如: `@Validated(ArticleVO.EditArticleGroup.class)`

##### 模型 Model
Model 模型的意思，Spring MVC 中的“M”，用来传输数据。从控制层直接返回数据给前端，配置jsp，模板技术能够展现 M 中存储的数据。
Model 简单理解就是给前端浏览器的数据，放在 Model 中，ModelAndView 里的任意值，还有json 格式的字符串等都是 Model。


##### 视图 View
Spring MVC 中的 View（视图）用于展示数据的，视图技术的使用是可插拔的。无论您决定使用thymleaf、jsp 还是其他技术，classpath 有 jar 就能使用视图了


### SpringMvc请求流程
##### DispatcherServlet
&emsp;DispatcherServlet 是核心对象，称为中央调度器（前端控制器 Front Controller）。负责接收所有对Controller的请求，调用开发者的 Controller 处理业务逻辑，将 Controller 方法的返回值经过视图处理响应给浏览器。DispatcherServlet 作为 SpringMVC 中的 C,职责:<br>

1. 是一个门面，接收请求，控制请求的处理过程。所有请求都必须有 DispatcherServlet 控制。SpringMVC对外的入口。可以看做门面设计模式。
2. 访问其他的控制器。 这些控制器处理业务逻辑
3. 创建合适的视图，将 2 中得到业务结果放到视图，响应给用户。
4. 解耦了其他组件，所有组件只与 DispatcherServlet 交互。彼此之间没有关联
5. 实现 ApplictionContextAware, 每个 DispatcherServlet 都拥自己的 WebApplicationContext，它继承了ApplicationContext。WebApplicationContext 包含了 Web 相关的 Bean 对象，比如开发人员注释@Controller的类，视图解析器，视图对象等等。 DispatcherServlet 访问容器中 Bean 对象。
6. Servlet + Spring IoC 组合
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot16.png" width = 80%/> </div>

##### Spring MVC 的完整请求流程
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1I-S-BOOT-SpringBoot17.png" width = 80%/> </div>

1. 红色 DispatherServlet 是框架创建的核心对象（可配置它的属性 contextPath）
2. 蓝色的部分框架已经提供多个对象。开发人员可自定义，替换默认的对象。
3. 绿色的部分是开发人员自己创建的对象，控制器 Conroller 和视图对象。

**流程说明**


1. DispatcherServlet 接收到客户端发送的请求。判断是普通请求，上传文件的请求。
2.DispatcherServlet 收到请求调用 HandlerMapping 处理器映射器。
3. HandleMapping 根据请求 URI 找到对应的控制器以及拦截器，组装成 HandlerExecutionChain 读写。将此对象返回给 DispatcherServlet，做下一步处理。
4. DispatcherServlet 调用 HanderAdapter 处理器适配器。这里是适配器设计模式，进行接口转换，将对一个接口调用转换为其他方法。
5. HandlerAdapter 根据执行控制器方法，也就是开发人员写的 Controller 类中的方法，并返回一个ModeAndView
6. HandlerAdapter 返回 ModeAndView 给 DispatcherServlet
7. DispatcherServlet 调用 HandlerExceptionResolver 处理异常，有异常返回包含异常的ModelAndView
8. DispatcherServlet 调用 ViewResolver 视图解析器来 来解析 ModeAndView
9. ViewResolver 解析 ModeAndView 并返回真正的 View 给 DispatcherServlet
10. DispatcherServlet 将得到的视图进行渲染，填充 Model 中数据到 request 域
11. 返回给客户端响应结果


##### 自动配置类
- DispatcherServletAutoConfiguration.class <br>
> 代替SpringMVC在Xml中配置的置 DispatcherServlet<br>
- WebMvcConfigurationSupport<br>
> 自动配置Web服务器


Servlet、Filter、Listeners等的使用直接查阅文档




---

> Citation:
> - []()
> 
> References:
> - [HikariCP 连接池](https://github.com/brettwooldridge/HikariCP/wiki)
> - [连接池配置](https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing)
> - [MySQL 连接池配置建议](https://github.com/brettwooldridge/HikariCP/wiki/MySQL-Configuration)
> - [Mybatis的配置](https://mybatis.org/mybatis-3/zh/configuration.html#settings)

