---

title: Spring笔记
tags: [Spring,笔记]
categories: [412B-框架工具]
description: 进入文章
sticky: 250
---

---

![](http://spring.p2hp.com/images/spring-logo-9146a4d3298760c2e7e49595184e1975.svg)

```java
Spring Xml 文件报红第一时间检查set 、get 、构造方法

```

准备工作
- JDK 最低版本17
- 设置Maven 
	- 见[王鹤老师的笔记]


```
本套Spring教程与其他Spring教程的区别可总结为以下几点： 
第一点：手写Spring框架 
第二点：手写组件扫描器 
第三点：依赖倒置原则DIP 
第四点：CGLIB动态代
```

# §1 Spring启示录

### 当前项目
```java
dao
	UserDao
		impl
			UserDaoImpl_1
service
	UserService
		impl
			UserServiceimpl_1
web
	UserAction 
	
service为了调用dao层方法,有dao层接口的实现类
web为了调用service层方法,有service层接口的实现类

```


### 缺点
若用户提出需求,程序员对项目的功能进行拓展时,就需要更改多层已经运行正常的的代码,不符合软件开发的“开闭原则”[OCP],即对扩展开放,对修改关闭
同时,也违背了“依赖倒置原则”

![700](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-DI2.png)

### 思想与解决方案
```java
违背依赖倒置
	上层依赖下层 : 上层因下层的改动而改动
		[这样不好,违背依赖倒置原则！！！]

符合依赖倒置:
	上不依赖下,"面向接口编程"
	依赖倒置原则的目的,降低程序的耦合度，提高扩展力


解决思想:[控制反转]
只保留接口,把创建对象的的权利、以及对象的维护权利交出
	- 重点:"让出权利"
	- 出现的比较新,没有被纳入GoF23种设计模式中

解决方案:依赖注入[DI]
	何如实现控制反转?
		- 第一种：set注入（执行set方法给属性赋值）
		- 第二种：构造方法注入（执行构造方法给属性赋值）
		
	依赖：A对象和B对象的关系。
	注入：是一种手段，通过这种手段，可以让A对象和B对象产生关系。
	依赖注入：对象A和对象B之间的关系，靠注入的手段来维护。而注入包括：set注入和构造注入
    
控制反转是思想。依赖注入是这种思想的具体实现。
Spring是一个实现了IoC思想的容器。
```


注意术语：

| 术语 | -            | -                          | 全称                           |
| ---- | ------------ | -------------------------- | ------------------------------ |
| OCP  | 开闭原则     | 开发原则                   | Open Close Principle           |
| DIP  | 依赖倒置原则 | 开发原则                   | Dependence Inversion Principle |
| IoC  | 控制反转思想 | 一种新型的设计模式         | Inversion of Control           |
| DI   | 依赖注入     | 控制反转思想的具体实现方式 | Dependency Injection           |



# §2 Spring 简述


![img](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-image.png)

SSM
	Spring 
	SpringMVC
	Mybatis

面向切面编程:[蓉姐]
AOP（Aspect Orient Programming），面向切面编程。
  切面:公共的,通用的,重复的功能称为切面,面向切面编程就是将切面提取出来,单独开发,在需要调用的方法中通过动态代理的方式进行织入
1)切面:就是那些重复的,公共的,通用的功能称为切面,例如:日志,事务,权限.
2)连接点:就是目标方法.因为在目标方法中要实现目标方法的功能和切面功能.
3)切入点(Pointcut):指定切入的位置,多个连接点构成切入点.切入点可以是一个目标方法,可以是一个类中的所有方法,可以是某个包下的所有类中的方法.
4)目标对象:操作谁,谁就是目标对象.
5)通知(Advice):来指定切入的时机.是在目标方法执行前还是执行后还是出错时,还是环绕目标方法切入切面功能.





# §3 Spring 入门程序


### 1、代码编程步骤

##### 基本结构
```xml
	1-创建一个maven项目
		补充项目结构
			resources 并设置为 资源文件夹 
			同理补充测试资源文件夹

	 2-修改pom.xml文件
		 删除build标签
		 添加	spring框架需要的核心依赖 spring-context
		 如果没有jutil 包则添加
		 刷新pom.xml文件


Spring6未正式发布需要添加Spring提供的仓库地址
Add the following to resolve milestone and RC versions – for example, `6.0.0-M2` or `6.0.0-RC1`:
```

```xml
<repository>
    <id>repository.spring.milestone</id>
    <name>Spring Milestone Repository</name>
    <url>https://repo.spring.io/milestone</url>
</repository>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.0.0-M2</version>
</dependency>
```


![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-spring-dep.png)
当加入spring context的依赖之后，会关联引入其他依赖：
spring aop：面向切面编程
spring beans：IoC核心
spring core：spring的核心工具包
spring jcl：spring的日志包
spring expression：spring表达式


```xml
	3-创建项目所需的咖啡豆[无参构造、setXXX方法]
		一定得有无参构造,底层使用的是反射机制通过无参构造创建对象
	
	4-applicationContext.xml文件
	
		- 配置文件放在resources类根路径下,可移植性高
		- IDEA支持spring配置文件,有模板!!
		- 在XML Configuration File → Spring Config
		- xml的文件的名字随意
		
```

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">  

<!--  
    <bean id="userBean" class="com.nfjh.spring6.bean.User">  
    </bean>
    
id是bean的唯一标识,不能重复
class 是 对应bean类的全限定类名
-->
	<bean id="" class="">
		<property name="" value=""/>
		<property name="" ref=""/>
		<!--
			㊟:value 为简单类型赋值
			ref 为引用类型赋值,且要求当前bean工厂中存在该引用类型对象
			ref中填写的是bean的id
		-->
	</bean> 

</beans>
```

```java

		㊟:value 为简单类型赋值
			ref 为引用类型赋值,且要求当前bean工厂中存在该引用类型对象

	5- 创建测试方法
		创建工厂
		
ApplicationContext ac  = new ClassPathXmlApplicationContext("applicationContext.xml路径");
//此处的构造方法是可变长参数,所以如果有多个可以直接加

/*此处有多个重载方法
public ClassPathXmlApplicationContext(String... configLocations) throws BeansException {  
    this(configLocations, true, (ApplicationContext)null);  
}

若项目为普通项目,不是maven的,此处出现了错误
㊟:检查是否将resources 设置为资源文件夹
*/


//返回Object
User user = (User) applicationContext.getBean("userBean");

/*
另一种写法: 直接返回的就是我们需要的类型
在传入id的同时传入类型
User user = applicationContext.getBean("userBean", User.class);
*/
```

![500](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-bean-factory.png)



#### 项目文件的修改与导入
```c
	1、删除target文件夹
	2、删除 .iml 文件
	3、修改pom.xml文件中的坐标
	    <artifactId>MVC_SpringXml</artifactId>
	    修改为项目名
	4、导入
		Project Structure 
		→ Modules 
		→ + 
		→ import Modules 
		→ 选中项目的根路径
		→ import module from external model
		→ maven 
		→ 一直next即可
```



# §4 Spring对IoC的实现

## 实现依赖注入
```java
set注入是在对象创建之后执行

构造注入是在对象实例化的过程中执行的
```


#### set注入

- javaBean中存在符合命名规范的set方法
- applicationContext.xml文件中进行了配置
```xml
<bean id="userDaoBean" class="com.nfjh.spring6.dao.UserDao" />  
  
<bean id="userService" class="com.nfjh.spring6.service.UserService">  
    <property name="userdao" ref="userDaoBean"/>  
</bean>
```
- 启动Spring容器，解析spring.xml文件，并且实例化所有的bean对象，放到spring容器当中。
- 根据bean的id从Spring容器中获取这个对象。

```xml
<!--
		name 是setXxx()方法的xxx
		
	㊟:value 为简单类型赋值
	ref 为引用类型赋值,且要求当前bean工厂中存在该引用类型对象
	ref中填写的是bean的id
-->
	<bean id="" class="">
		<property name="" value=""/>
		<property name="" ref=""/>
	</bean> 
```


```java
public class UserDao {  
        private static final Logger logger = LoggerFactory.getLogger(UserDao.class);  
        public void insert(){  
                logger.debug("保存信息到数据库!\n");  
        }  
}

public class UserService {  
    private UserDao userdao;  
    public void setUserdao(UserDao userdao) {  
        this.userdao = userdao;  
    }  
    public void saveUser(){  
        userdao.insert();  
    }
    
@Test  
public void testInsert(){  
    ApplicationContext applicationContext = (ApplicationContext) new ClassPathXmlApplicationContext("spring-core.xml");  
    UserService userService = applicationContext.getBean("userService", UserService.class);  
    userService.saveUser();  
}



<bean id="userDao" class="com.nfjh.spring6.dao.UserDao" />  
  
<bean id="userService" class="com.nfjh.spring6.service.UserService">  
    <property name="userdao" ref="userDao"/>  
</bean>
```


#### 构造注入
- javaBean中存在构造方法
```xml

<bean id="userDaoBean" class="com.nfjh.spring6.dao.UserDao" />  
 
<bean id="customerServiceBean" class="com.nfjh.spring6.service.CustomerService">  
    <constructor-arg index="0" ref="userDaoBean"/>  
</bean>
```
- applicationContext.xml文件中进行了配置
- 启动Spring容器，解析spring.xml文件，并且实例化所有的bean对象，放到spring容器当中。
- 根据bean的id从Spring容器中获取这个对象。


## set注入的方式
```
使用set方法进行注入,一定得有无参构造,不要因为写了有参数的构造方法,
让无参数的方法被覆盖了,这时需要手动添加无参构造
```



| 注入方式 | 类类型 | 操作记忆  bean[id & class] >                                | 操作对象                                 |
| -------- | ------ | ------------------------------------------------------------ | ---------------------------------------- |
| 外部Bean | 简单   | property[name & value]                    | 简单类型 attrName;                       |
|          | 引用   | property[name & ref]                     | bean[id & class]                         |
| 内部Bean | ---    | property[name] > bean[class]             | bean[id & class]  OR  简单类型 attrName; |
| 级联属性 | 引用   | property[name="注入类的属性名" & ref] +  property[name="注入类的属性名.属性名" & value] | bean[id & class]                         |
| 数组     | 简单   | property[name] > array > value                               | 简单类型[] attrName;                     |
|          | 引用   | property[name] > array > ref[bean]                           | 引用类型[] attrName;                     |
| List/Set | 简单   | property[name] > list/set  > value{值} | List/Set<简单类型> attrName;             |
|          | 引用   | property[name] > list/set  > ref[bean] | List/Set <引用类型> attrName; |
| Map | Map    | property[name] > map > entry[key/key-ref   &value/value-ref] | Map<类型1,类型2> attrName;               |
| Perperties | Perperties | property[name] > props > prop[key]{值}                       | Map<String,String>                       |
| null | ---        | property[name] > null单标签 |bean[id & class]  OR  简单类型 attrName;|
|  | ---        | 对哪个属性注入null值,就啥都不写 |bean[id & class]  OR  简单类型 attrName;|
| 空字符串 | String | property[name & value=""] |String|
| | String | property[name] > value单标签 |String|
| 特殊符号 | | property[name & value="实体符号"] ||
| | | property[name] > value{ `<![CDATA[值]]>`} ||


| 注入方式     | 类类型      | 操作记忆                                             | 操作对象                                 |
| ------------ | ----------- | ---------------------------------------------------- | ---------------------------------------- |
| p 命名空间   | 简单        | bean[id & class & p:属性名="属性值" ]                | 简单类型 attrName;                       |
|              | 引用        | bean[id & class & p:属性名-ref="bean的id"]           | bean[id & class]                         |
|              |             | ` xmlns:p="http://www.springframework.org/schema/p"` |                                          |
| c 命名空间   | 简单_属性名 | bean[id & class c:属性名="属性值"]                   | 简单类型 attrName;                       |
|              | 简单_下标   |` bean[id & class c:_0="属性值"]                 `      | 简单类型 attrName;                       |
|              | 引用_属性名 | bean[id & class c:属性名-ref="bean的id"]             | bean[id & class]  OR  简单类型 attrName; |
|              | 引用_下标   |` bean[id & class c:_0-ref="bean的id"]      `           | bean[id & class]  OR  简单类型 attrName; |
|              |             | `xmlns:c="http://www.springframework.org/schema/c"`  |                                          |
| util命名空间 | List        | bean[id & class] > property[name & ref="util的id"]   | util:list[id]  > value{值}               |
| util命名空间 | Set         | -- 同List --                                         | util:set[id] > value{值}                 |
| util命名空间 | Properties  | -- 同List --                                         | util:properties[id] > prop[key]{值}      |



### 外部Bean
就是使用ref属性来引入。这就是注入外部Bean
```xml
    <!--声明/定义Bean-->
    <bean id="orderDaoBean" class="com.powernode.spring6.dao.OrderDao"></bean>

    <bean id="orderServiceBean" class="com.powernode.spring6.service.OrderService">
        <!--使用ref属性来引入。这就是注入外部Bean-->
        <property name="orderDao" ref="orderDaoBean"/>
    </bean>
```


### 内部bean
```xml
<!--内部bean-->  
    <!--Ctrl + Alt + Shift + C-->    
    <bean id="osBeanIn" class="com.nfjh.spring6.service.OrderService">  
        <property name="orderDao">  
            <bean class="com.nfjh.spring6.dao.OrderDao"/>  
        </property>  
    </bean>

内部bean在定义的时候放在 property标签中
property标签中不加 ref
bean标签中不加 id 
```

### 简单类型注入
```xml
<!--注入简单类型-->  
<bean id="userBean" class="com.nfjh.spring6.bean.User">  
    <property name="username" value="zhangsan"/>  
    <property name="passwd" value="123"/>  
    <property name="age" value="20"/>  
</bean>
```

哪些是简单类型
双击shift → BeanUtils → Ctrl + F12
isSimpleType()
对于Date是简单类型,但是需要严格按照格式写日期,很麻烦
在平常使用时直接当成引用类型,使用ref进行注入
- **基本数据类型**
- **基本数据类型对应的包装类**
- **String或其他的CharSequence子类**
- **Number子类**
- **Date子类**
- **Enum子类**
- **URI**
- **URL**
- **Temporal子类**
- **Locale**
- **Class**
- **另外还包括以上简单值类型对应的数组类型。**

简单类型可以用于对数据源信息的注入


### 级联属性
```java
User 
	private String username;  
	private  String passwd;  
	private int age;
以及对应的get set toString方法

Client
	private User user;  
	private String clientName;
以及对应的get set toString方法

```


```xml
<!--级联属性赋值-->  
<bean id="userBeanCascade" class="com.nfjh.spring6.bean.User"/>  
  
<bean id="clientBean" class="com.nfjh.spring6.bean.Client">  
    <property name="clientName" value="QQ"/>  
    <!--使用级联属性赋值,Client 中要有getUser()方法-->  
    <property name="user" ref="userBeanCascade"/>  
    <!--使用级联属性赋值,user必须要有对应的username、passwd、age get方法-->  
    <property name="user.username" value="张三"/>  
    <property name="user.passwd" value="123456"/>  
    <property name="user.age" value="21"/>  
</bean>
```


### 注入数组
```java'
Lseeon
	private  String [] lessonName ;
	以及对应的set toString方法

Student
	private String name;  
	private Lesson  [] lessons;
	以及对应的set toString方法
```

```xml
<!--  
简答类型数组注入  
property > array > value  
  
    private  String [] lessonName ;-->  
<bean id="lessonBean" class="com.nfjh.spring6.bean.Lesson">  
    <property name="lessonName">  
        <array>  
            <value>JAVA</value>  
            <value>MYBATIS</value>  
            <value>SPRING</value>  
        </array>  
    </property>  
</bean>  
  
<bean id="lessonBean2" class="com.nfjh.spring6.bean.Lesson">  
    <property name="lessonName">  
        <array>  
            <value>MYSQL</value>  
            <value>JDBC</value>  
            <value>AJAX</value>  
        </array>  
    </property>  
</bean>  
  
<!--
......
Lesson lessonBean = applicationContext.getBean("lessonBean", Lesson.class);
System.out.println(lessonBean);  
//Lesson{lessonName=[JAVA, MYBATIS, SPRING]}
-->



<!--引用类型数组注入  
private String name;  
private Lesson  [] lessons;  
  
property > array > ref[bean]  
-->  
<bean id="studentBean" class="com.nfjh.spring6.bean.Student">  
    <property name="name" value="张三"/>  
    <property name="lessons">  
        <array>  
           <ref bean="lessonBean"/>  
            <ref bean="lessonBean2"/>  
        </array>  
    </property>  
</bean>

<!--
......
Student studentBean = applicationContext.getBean("studentBean", Student.class);  
System.out.println(studentBean);  
//Student{name='张三', lessons=[Lesson{lessonName=[JAVA, MYBATIS, SPRING]}, Lesson{lessonName=[MYSQL, JDBC, AJAX]}]}

-->

```


### List 和Set集合注入
```java
Person
	private List<User> userList;  
	private Set<User> userSet;
	以及对应的set toString方法
```

```xml
<!--
㊟:List中的元素可以重复
	Set中的元素如果重复写,不报错,但是相同元素只算1个
-->

<!--List注入  
简单类型  
    property > list > value
引用类型  
    property > list > ref[bean]
-->  

<!-- set注入
简单类型  
    property > list > value
引用类型  
    property > list > ref[bean]
-->
  
    <bean id="personBean" class="com.nfjh.spring6.bean.Person">  
        <property name="userList">  
            <list>  
                <ref bean="userBean"/>  
                <ref bean="userBeanCascade"/>  
            </list>  
        </property>  
    </bean>  

<!--
//Person{userList=[User{username='zhangsan', passwd='123', age=20}, User{username='张三', passwd='123456', age=21}], userSet=null}  
//通过此程序可以得知  
//通过级联属性赋值的bean可以通过 id 实例化,拿到其中的值
-->
  
    <bean id="personBean2" class="com.nfjh.spring6.bean.Person">  
        <property name="userList">  
            <list>  
                <ref bean="userBean"/>  
                <ref bean="userBeanCascade"/>  
            </list>  
        </property>  
        <property name="userSet">  
            <set  >  
                <ref bean="userBean"/>  
                <ref bean="userBeanCascade"/>  
            </set>  
        </property>  
    </bean>
<!--
Person{userList=[User{username='zhangsan', passwd='123', age=20}, User{username='张三', passwd='123456', age=21}], userSet=[User{username='zhangsan', passwd='123', age=20}, User{username='张三', passwd='123456', age=21}]}

-->

```


### Map 注入
```java
还是person
再加上一个属性
	private Map<Integer,User> userMap;
	以及对应的set toString方法
```

```xml
<!--Map注入  
简单类型  
    property > map > entry[key &  value]  
引用类型  
    property > map >  enter[key-ref & value-ref]
    
-->  
    <bean id="personMapBean" class="com.nfjh.spring6.bean.Person">  
        <property name="userMap">  
            <map>  
                <entry key="1" value-ref="userBean"/>  
                <entry key="2" value-ref="userBeanCascade"/>  
            </map>  
        </property>  
    </bean>
<!--
......
Person personMapBean = applicationContext.getBean("personMapBean", Person.class);  
System.out.println(personMapBean);  
//Person{userList=null, userSet=null, userMap={1=User{username='zhangsan', passwd='123', age=20}, 2=User{username='张三', passwd='123456', age=21}}}
-->
```


### Perperties类型注入
```java
/*虽然properties也是Map但是他的注入方式与Map不同*/ 
还是person
再加上一个属性
    Properties properties ;
	以及对应的set toString方法
```

```xml
    <!--特殊Map类型Properties类型注入
    property > props > prop[key](内容)
    -->  
    
    <bean id="personProBean" class="com.nfjh.spring6.bean.Person">  
        <property name="properties" >  
            <props>  
                <!--注意 prop的key 与值都是String类型-->  
                <prop key="driver">com.nfjh.hello</prop>  
                <prop key="url">www.baidu.com</prop>  
            </props>  
        </property>  
    </bean>

<!--
......
Person personProBean = applicationContext.getBean("personProBean", Person.class);  
System.out.println(personProBean);  
//Person{userList=null, userSet=null, userMap=null, properties={driver=com.nfjh.hello, url=www.baidu.com}}
-->
```


### 注入null
```java
User 
	private String username;  
	private  String passwd;  
	private int age;
以及对应的get set toString方法
```

```xml
<!--null值的注入-->  
<bean id="userNullBean" class="com.nfjh.spring6.bean.User">  
    <!--第一种注入方式,不注入自动注入null-->  
   <!--此处不给age 注入值-->  
    <!--第二中注入方式,手动注入null-->    
    <property name="username">  
        <null/>  
    </property>  
  
    <!--错误的注入,这种是注入了"null"字符串,不是注入正真的null-->  
    <property name="passwd" value="null"/>  
</bean>

<!--
......
User userNullBean = applicationContext.getBean("userNullBean", User.class);  
System.out.println(userNullBean);  
System.out.println(userNullBean.getPasswd().toUpperCase());  
/*  
User{username='null', passwd='null', age=0}  
NULL

对于第三种错的注入的解释:
如果 真的注入的是null的话,此处应该报空指针异常
但运行结果确实"null"字符串被转化成了大写的字母
所以未注入成功null


另外对于age属性,我的却没有注入值
但结果却是0 ,这点需要注意
 */
-->
```



### 注入空字符串
```java
还是User
```

```xml
<!--  
空字符串的注入  
-->  
<!--null值的注入-->  
<bean id="userStrNullBean" class="com.nfjh.spring6.bean.User">  
    <!--第一种注入方式 value中不给值即可-->  
    <property name="username" value=""/>  
  
    <!--第二中注入方式,手动标签注入""-->  
    <property name="passwd">  
        <value/>  
    </property>  
</bean>

<!--
......
User userStrNullBean = applicationContext.getBean("userStrNullBean", User.class);  
System.out.println(userStrNullBean);  
//User{username='', passwd='', age=0}
-->

```

### < " ' &  >   5个特殊符号的注入
```xml
    <!--特殊符号的注入-->
    <bean id="specialSymbolsBean" class="com.nfjh.spring6.bean.User">
        <!--第一种:只用实体符号
        这里就之列出一种
        >   &gt;
         <property name="username" value="2 < 3"/>
        -->
        <property name="username" value="2 &gt; 3"/>

        <!--第二种:使用value标签 + <![CDATA[2<3]]>-->
        <property name="passwd">
            <value> <![CDATA[2<3]]> </value>
        </property>
        <!--
        注意点1：
        要使用value标签直接放在value中是不对的!!!!
        <property name="passwd" value="<![CDATA[2<3]]>"/>

        注意点2：
        <value></value>中的内容为注入的内容
        所以如果这么写结果为
        <property name="passwd">
            <value>
                <![CDATA[2<3]]>
            </value>
        </property>
        User{username='2 > 3', passwd='
                2<3
            ', age=0}

            注意点3:
            <![CDATA[]]> 中的字符全部要大写
            注意点:
            不管是使用实体符还是!<[CDATA[]]>这都是XML的语法
        -->

    </bean>


<!--
User specialSymbolsBean = applicationContext.getBean("specialSymbolsBean", User.class);  
System.out.println(specialSymbolsBean);
//User{username='2 > 3', passwd=' 2<3 ', age=0}
-->
```




## 小结
```java
外部bean
	
<property name="orderDao" ref="orderDaoBean"/>
```




## p命名空间注入
```xml
p命名空间注入的底层还是"set"注入
所以仍然需要提供set方法
只不过这种注入方式会让spring配置更加简单
```

![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-p-namespace.png)

```xml
xmlns:p="http://www.springframework.org/schema/p"
```

```java
User 
	private String username;  
	private  String passwd;  
	private int age;
以及对应的get set toString方法

Client
	private User user;  
	private String clientName;
以及对应的get set toString方法
```


```xml

<!--
p命名空间
1、修改头部
    添加   xmlns:p="http://www.springframework.org/schema/p"

2、直接使用
           简单类型
                p:属性名="属性值"
          引用类型
                p:属性名-ref="bean的id"
-->

    <bean id="userBean" class="com.nfjh.spring6.bean.User" p:age="0" p:passwd="haha" p:username="zhangsan"/>
    <bean id="clientBean" class="com.nfjh.spring6.bean.Client" p:clientName="QQ" p:user-ref="userBean"/>

<!--
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("p-namespace.xml");  
Client clientBean = applicationContext.getBean("clientBean", Client.class);  
System.out.println(clientBean);  
//Client{user=User{username='zhangsan', passwd='haha', age=0}, clientName='QQ'}
-->

```


## c 命名空间注入

```xml
c命名空间注入的底层还是"构造"注入
所以仍然需要提供构造方法
只不过这种注入方式会让spring配置更加简单
```

修改就不说了,上面改p的这里改成 c 就行了
```xml
xmlns:c="http://www.springframework.org/schema/c"
```

```java
Shop
	private  String address;  
	private String name;  
	private Date businessHours;
	以及对应的三个参数构造方法
```

```xml
    <bean id="date" class="java.util.Date"/>  
  
<!--    
<bean id="shopBean" class="com.nfjh.spring6.bean.Shop" c:_0="天津市" c:_1="小张水果" c:_2-ref="date"/>
-->  
        <bean id="shopBean" class="com.nfjh.spring6.bean.Shop" c:address="天津市" c:name="小张水果" c:businessHours-ref="date"/>  

<!--
对于c命名空间
可以使用参数下标对参数赋值,也可以使用属性名对参数赋值
Shop shopBean = applicationContext.getBean("shopBean", Shop.class);  
System.out.println(shopBean);  
//Shop{address='天津市', name='小张水果', businessHours=Fri Oct 28 06:35:03 CST 2022}
-->

```



## util命名空间
```xml
简化集合 Map ,提高代码复用率


第一步:和p一样修改
第二步:在第三行的引号中追加 
```


![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-util_namespace.png)

```xml
使用
<util:TYPE  id="">
	.....
	
</util:TYPE>
```

![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-util.png)


```java
Book
	private List<String> name;  
	private Set<String> ISBN;  
	private Properties type;
	以及对应的set toString方法
```

```xml
<util:list id="bookList">  
    <value>三体</value>  
    <value>活着</value>  
</util:list>  
  
<util:set id="bookSet">  
        <value>1211121</value>  
        <value>22332232</value>  
</util:set>  
  
<util:properties id="bookProp">  
    <prop key="1">科幻</prop>  
    <prop key="2">文学</prop>  
</util:properties>  
  
  
<bean id="bookBean" class="com.nfjh.spring6.bean.Book">  
    <property name="name" ref="bookList"/>  
    <property name="ISBN" ref="bookSet"/>  
    <property name="type" ref="bookProp"/>  
 </bean>  
  
<util:list id="bookList2">  
    <value>流浪地球</value>  
    <value>诗经</value>  
</util:list>  
  
<bean id="bookBean2" class="com.nfjh.spring6.bean.Book">  
    <property name="name" ref="bookList2"/>  
    <property name="ISBN" ref="bookSet"/>  
    <property name="type" ref="bookProp"/>  
</bean>
```



## 基于XML的自动装配
```java
不管是使用 autowire="byName" 
还是autowire="byType"
底层都是使用set方法
```
```java
User 
	private String username;  
	private  String passwd;  
	private int age;
以及对应的get set toString方法

Client
	private User user;  
	private String clientName;
以及对应的get set toString方法

```

### autowire="byName"
```xml
    <!--根据名称自动装配
    1、添加 autowire属性
    2、被装配的bean的id必须是setXxx()方法的xxx
    -->
    <bean id="clientBean" class="com.nfjh.spring6.bean.Client" autowire="byName">
        <property name="clientName" value="QQ"/>
        <!--
        这里没有了
         <property name="user" ref="..."/>
		-->
    </bean>

<!--这里的id不能随便写了-->
    <bean id="user" class="com.nfjh.spring6.bean.User">
        <property name="age" value="20"/>
        <property name="passwd" value="1221"/>
        <property name="username" value="zhangsan"/>
     </bean>

```

### autowire="byType"
```java
User 中添加该方法
public void testAutoWire(){  
    System.out.println("user对象已经实例化");  
}
```
```xml
    <!--
    根据类型进行自动进行装配
    1、添加 autowire属性 值为 byType
    2、被装配的bean可以没有id,且只能有一个实例,如果有多个就会出现错误
	3、如果xml文件中只有一个bean,但是爆红了,不用管,因为Spring扫描的是全部的xml文件
			可以降低xml文件的报红的级别,让他不报红,或者直接不管
    -->
<!--
<bean class="java.util.Date"/>
Date类型注入失败,为null
怀疑是普通类型,不走byType进行注入
-->

<bean id="user" class="com.nfjh.spring6.bean.User">  
    <property name="age" value="20"/>  
    <property name="passwd" value="1221"/>  
    <property name="username" value="zhangsan"/>  
 </bean>

<bean id="clientBean2" class="com.nfjh.spring6.bean.Client" autowire="byType">  
    <property name="clientName" value="QQ"/>  
</bean>
<!--

ApplicationContext applicationContext = new ClassPathXmlApplicationContext("autowire.xml");  
Client clientBean = applicationContext.getBean("clientBean2", Client.class);  
clientBean.getUser().testAutoWire();;  
System.out.println(clientBean);  
//user对象已经实例化  
//Client{user=User{username='zhangsan', passwd='1221', age=20}, clientName='QQ'}
-->

```


## spring引入外部属性配置文件

### 步骤
1、准备jdbc.properties文件
```properties
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:2022/spring6
username=root
password=root
initialSize=5
maxIdle=10

```


2、在xml文件中添加context命名空间以及约束文件
```xml
修改与util命名空间的修改时一样的
只不过把该util的地方该成context即可
```

3、准备好接收数据的几个属性
这里我创建了一个普通的类,用来接收数据
```java
JDBC
	private String driver;  
	private String url;  
	private String passwd;  
	private String initialSize;  
	private String maxIdle;
	以及对应的set和toString方法
```


3、引入配置文件
```xml
<context:property-placeholder location="jdbc.properties"/>

<!--
注意这样写jdbc.properties 文件是放在resources类的根路径下的
-->
```

4、注入数据
```xml
<bean id="jdbcBean" class="com.nfjh.spring6.bean.JDBC" >  
    <property name="driver" value="${driverClassName}"/>  
    <property name="url" value="${url}"/>  
    <property name="username" value="${username}"/>  
    <property name="passwd" value="${password}"/>  
    <property name="initialSize" value="${initialSize}"/>  
    <property name="maxIdle" value="${maxIdle}"/>  
</bean>

<!--
JDBC jdbcBean = applicationContext.getBean("jdbcBean", JDBC.class);  
System.out.println(jdbcBean);  
//JDBC{driver='com.mysql.jdbc.Driver', url='jdbc:mysql://localhost:2022/spring6', username='34838', passwd='root', initialSize='5', maxIdle='10'}
-->
```

### ${username}加载错误

```xml
需要注意的是Spring 的配置文件中有一个坑!!!
Spring 在加载配置文件的时候,会先加载系统的环境变量

此时如果jdbc.properties文件中存在username就会被加载为电脑的用户名
而不是我们的配置

解决的方式有三种

1、直接更换名字
	把username换成 user_name 或者 name 或者其他的
	但注意,spring在加载时不区分大小写,所以改成 userName是没用滴
	还有当使用数据源时,存在无法更改配置文件中的名称,否则无法成功创
	建连接的情况,此时建议使用其他的解决方案
	

2、添加配置信息local-override="true"
<context:property-placeholder local-override="true"  location="jdbc.properties"/>

3、[已过时,但能用]使用另一个标签,并添加p命名空间

<bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer" p:localOverride="true">  
    <property name="locations" value="classpath:jdbc.properties"></property>  
</bean>

```





# §5 Bean的作用域

```java
public class ScopeBean {  
    public ScopeBean() {  
        System.out.println("无参构造执行了!");  
    }  
}


    @Test
    public void testScopeBean(){
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("bean-scope.xml");
        System.out.println("-------------");
        ScopeBean scopeBean = applicationContext.getBean("scopeBean", ScopeBean.class);
        System.out.println(scopeBean);
        ScopeBean scopeBean2 = applicationContext.getBean("scopeBean", ScopeBean.class);
        System.out.println(scopeBean2);
        ScopeBean scopeBean3 = applicationContext.getBean("scopeBean", ScopeBean.class);
        System.out.println(scopeBean3);
```

```xml
    <!--spring默认bean的构建使用单例模式
    单例模式对象给的创建在
    new ClassPathXmlApplicationContext()的执行中
    -->
    <bean id="scopeBean" class="com.nfjh.spring6.bean.ScopeBean" scope="singleton"/>
<!--
        /* 单例模式下:
                    无参构造执行了!
                    -------------
                    com.nfjh.spring6.bean.ScopeBean@75f95314
                    com.nfjh.spring6.bean.ScopeBean@75f95314
                    com.nfjh.spring6.bean.ScopeBean@75f95314
        * */
-->
```


```xml
    <!--可以更改为原型模式(每次获取的都是新的实例对象)
     此时执行new ClassPathXmlApplicationContext()时不在创建对象
     在执行 getBean()方法时创建对象
    -->
    <bean id="scopeBean" class="com.nfjh.spring6.bean.ScopeBean" scope="prototype"/>

<!--㊟: 
prototype ['prәutәtaip]
n. 原型
[计] 样机; 原型
-->

<!--
        /*
                    -------------
                    无参构造执行了!
                    com.nfjh.spring6.bean.ScopeBean@15dcfae7
                    无参构造执行了!
                    com.nfjh.spring6.bean.ScopeBean@3da05287
                    无参构造执行了!
                    com.nfjh.spring6.bean.ScopeBean@1e636ea3
         */
-->
```


# §6 bean的获取方式
## 构造方法获取bean

## 简单工厂获取bean
```java
public class Sweet {  
    public Sweet(){}  
    public void getType(){  
        System.out.println("这是一个水果糖");  
    }  
}
```

```java
public class SweetFactory {  
  //注意这个方法是静态的
    public static Sweet get(){  
        return new Sweet();  
    }  
}
```

```xml
<!--  
1、简单工厂模式给"工厂类"注入  
2、简单工厂模式的get方法是静态方法  
使用1个bean 标签即可获取

Spring提供的实例化方式，第二种：通过简单工厂模式。你需要在Spring配置文件中告诉Spring框架，调用哪个类的哪个方法获取Bean
factory-method 属性指定的是工厂类当中的静态方法。也就是告诉Spring框架，调用这个方法可以获取Bean。
-->  

<bean id="sweetFactory" class="com.nfjh.spring6.factory.SweetFactory" factory-method="get"/>
```

```java
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("factory.xml");  
Sweet sweet = applicationContext.getBean("sweetFactory", Sweet.class);  
sweet.getType();  
//这是一个水果糖
```


## Factory-bean获取bean
```java
Sweet还是使用上面的那个,原封不动

public class SweetFactor_Bean {  
    //此方法不在是静态的了  
    public  Sweet get(){  
        return new Sweet();  
    }  
}
```

```xml
<!--  
factory-bean的方式获取对象  
需要两个bean标签
Spring提供的实例化方式，第三种：通过工厂方法模式。通过 factory-bean属性 + factory-method属性来共同完成
告诉Spring框架，调用哪个对象的哪个方法来获取Bean。
-->  
    <bean id="sweetFactoryBean" class="com.nfjh.spring6.factory.SweetFactor_Bean"/>  
    <bean id="sweetBean" factory-bean="sweetFactoryBean" factory-method="get"/>

<!--
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("factory.xml");  
Sweet sweetBean = applicationContext.getBean("sweetBean", Sweet.class);  
sweetBean.getType();  
//这是一个水果糖
-->
```


## 实现FactoryBean接口重写方法获取

```java
/*
对于实现FactoryBean接口重写getObject()的方式
其实就是对第三中方式的简化
*/


还是Sweet不动


FactoryBeanImpl
import org.springframework.beans.factory.FactoryBean;  
  
//该类实现了FactoryBean 所以不需要在配置factory-bean  
public class FactroyBeanImpl implements FactoryBean<Sweet> {  
  
    //该类重写了getObject ,所以不在需要配置 factory-method  
    @Override  
    public Sweet getObject() throws Exception {  
        return new Sweet();  
    }  
  
    @Override  
    public Class<?> getObjectType() {  
        return null;  
    }  
  
    //返回的对象是否为单例对象,TRUE为单例,FALSE为多例  
    @Override  
    public boolean isSingleton() {  
        return FactoryBean.super.isSingleton();  
    }  
}

```

```xml
<!--FactoryBeanImpl是一个工厂bean  
是实现了FactoryBean接口的特殊bean  
而辅助spring实例化其它Bean对象的特殊bean  
-->  
<bean id="sweetFactoryBeanImpl" class="com.nfjh.spring6.factory.FactroyBeanImpl"/>

<!--
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("factory.xml");  
Sweet sweetBean = applicationContext.getBean("sweetFactoryBeanImpl", Sweet.class);  
sweetBean.getType();  
//这是一个水果糖
-->
```


## 
```java
Con 
	private Date date;  
	private String clientLog;  
	private  String clientType;
	以及对应的set和toSring方法
	
```

```java
import java.text.SimpleDateFormat;  
import java.util.Date;  
  
public class DateFactoryBeanImpl implements FactoryBean<Date> {  
    private String strDate;  
  
    public DateFactoryBeanImpl(String strDate) {  
        this.strDate = strDate;  
    }  
  
    @Override  
    public Date getObject() throws Exception {  
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");  
        return sdf.parse(strDate);  
    }  
  
    @Override  
    public Class<?> getObjectType() {  
        return null;  
    }  
}
```

```xml
<!--通过factoryBean的方式创建Date对象-->  
<bean id="date" class="com.nfjh.spring6.factory.DateFactoryBeanImpl">  
    <constructor-arg value="2001-09-20"/>  
</bean>  
  
<bean id="conBean" class="com.nfjh.spring6.factory.Con">  
    <property name="date" ref="date"/>  
    <property name="clientType" value="QQ"/>  
    <property name="clientLog" value="QQ_Log"/>  
</bean>



<!--
Con conBean = applicationContext.getBean("conBean", Con.class);  
System.out.println(conBean);  
//Condate=Thu Sep 20 00:00:00 CST 2001, clientLog='QQ_Log', clientType='QQ'}
-->


<!--

当然也可以使用其他方式对Con中的date进行注入
比如内部bean等
-->
<bean id="conBean2" class="com.nfjh.spring6.factory.Con">  
    <property name="date">  
        <bean class="com.nfjh.spring6.factory.DateFactoryBeanImpl">  
            <constructor-arg value="2001-09-20"/>  
        </bean>  
    </property>  
    <property name="clientType" value="WeChat"/>  
    <property name="clientLog" value="WeChat_Log"/>  
</bean>
<!-- Con{date=Thu Sep 20 00:00:00 CST 2001, clientLog='WeChat_Log', clientType='WeChat'} -->
```


## bean的生命周期
```java
Student 

public class Student {  
    private  int age;  
  
    public Student() {  
        System.out.println("无参构造执行了!!!");  
    }  
  
    public void setAge(int age) {  
        System.out.println("赋值执行了");  
        this.age = age;  
    }  
  
  
    public void init(){  
        System.out.println("init初始化执行了!!!");  
    }  
  
    public void sleep(){  
        System.out.println("bean对象正在使用中!!!");  
    }  
  
    public  void destroy(){  
        System.out.println("destroy方法执行了!!!");  
    }  
}
```

```java
@Test  
public  void testLifeCycle(){  
    ApplicationContext applicationContext = new ClassPathXmlApplicationContext("lifecycle.xml");  
    Student student = applicationContext.getBean("lifecycleBean", Student.class);  
    student.sleep();  
  
    //销毁  [ApplicationContext没有close这个方法,需要向下转型]  
    ClassPathXmlApplicationContext context = (ClassPathXmlApplicationContext) applicationContext;  
    context.close();  //如果不加上这个关闭,destroy方法不会执行
}
```

### 5步

```xml
<bean id="lifecycleBean" class="com.nfjh.spring6.life_cycle.Student" init-method="init" destroy-method="destroy">  
    <property name="age" value="21"/>  
</bean>

<!--
无参构造执行了!!!
赋值执行了
init初始化执行了!!!
bean对象正在使用中!!!
destroy方法执行了!!!
-->
```

### 7步
```java
添加一个类实现BeanPostProcessor接口
重写其中的两个方法


import org.springframework.beans.BeansException;  
import org.springframework.beans.factory.config.BeanPostProcessor;  
  
public class LifeCycleAllBeanPost  implements BeanPostProcessor {  
    @Override  
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {  
        //初始化之前执行  
        System.out.println("初始化之前执行");  
        return BeanPostProcessor.super.postProcessBeforeInitialization(bean, beanName);  
    }  
  
    @Override  
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {  
        //初始化之后执行  
        System.out.println("初始化之后执行");  
        return BeanPostProcessor.super.postProcessAfterInitialization(bean, beanName);  
    }  
}
```

```xml
<!--这个配置针对当前XML中所有的bean有效-->  
<bean id="postProcessor" class="com.nfjh.spring6.life_cycle.LifeCycleAllBeanPost"/>  
  
<bean id="lifecycleBean" class="com.nfjh.spring6.life_cycle.Student" init-method="init" destroy-method="destroy">  
    <property name="age" value="21"/>  
</bean>

<!--对于相同的测试程序 7 步的结果为
无参构造执行了!!!
赋值执行了
初始化之前执行
init初始化执行了!!!
初始化之后执行
bean对象正在使用中!!!
destroy方法执行了!!!
-->
```


### 10步

![img](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-ten-step.png)

5步
无参构造执行了
赋值执行了
initBean初始化执行了
bean对象正在使用中
destroyBean方法执行了

7步 在init的前后添加bean后处理器(BeanPostProcessor) 
		的postProcessBeforeInitialization
		和postProcessAfterInitialization


10步是在
	bean后处理器的Before方法前后添加   
		Aware的相关接口的检查,设置依赖
		和InitializingBean接口的检查,调用接口方法
	
	在使用bean之后添加
		DisposableBean接口的检查,调用接口方法



Spring容器只对<font color="#9ebc19">单例(singleton)</font>的Bean进行完整的生命周期管理。
     如果是<font color="#9ebc19">prototype(多例)</font>作用域的Bean，Spring容器只负责将该Bean初始化完毕。等客户端程序一旦<font color="#9ebc19">获取到该Bean之后</font>，Spring容器就不再管理该对象的生命周期了。

### DefaultListableBeanFactory
```java
@Test  
public void registerBean(){  
    //让自己创建完毕的类纳入Spring容器的管理  
    Student student = new Student();  
    student.setAge(33);  
  
    DefaultListableBeanFactory factory = new DefaultListableBeanFactory();  
    factory.registerSingleton("studentBean",student);  
  
    Object studentBean = factory.getBean("studentBean");  
    System.out.println(student);  
    }
```





# §7 IoC 注解式开发

## Spring注解使用
```java
- 第一步：加入aop的依赖
- 第二步：在配置文件中添加context命名空间
- 第三步：在配置文件中指定扫描的包
- 第四步：在Bean类上使用注解

```


## 声明Bean

```java
@Component  声明所有类型 Bean

以下三个注解是@Component 注解的别名,可以使用@Component代替
但是代码的可读性会下降

@Controller  声明界面层的bean
@Service        声明业务逻辑层的bean
@Repository 声明数据访问层的bean
```

```java
User.java
@Component(value="userBean")
如果注解的属性名是value，那么value是可以省略的@Component("userBean")
如果把value属性彻底去掉，spring会给Bean自动取名吗？会的。并且默认名字的规律是：Bean类名首字母小写即可@Component  ==> getBean("user");


如果是多个包怎么办？有两种解决方案：

第一种：在配置文件中指定多个包，用逗号隔开
第二种：指定多个包的共同父包
```



我的疑问与测试
如果一个类中添加了注解,同时又在XML文件中进行了bean的配置
会不会报错,是两个都能用,还是两个都不能用
如果能用获得的对象是同一个吗[我只测试了单例模式下]

```java
@Component  
public class User {  
}
```

```xml
<context:component-scan base-package="com.nfjh.bean"/>  
<bean id="userBean" class="com.nfjh.bean.User"/>
```

```java
@Test
    @Test  
    public void testBean(){  
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("Annotation-test.xml");  
        Object userBean = applicationContext.getBean("userBean");  
        Object userBean2 = applicationContext.getBean("user");  
        System.out.println(userBean);  
        System.out.println(userBean2);  
        }
/*
结果为两个都可以用,且获得的对象不是同一个
com.nfjh.bean.User@7756c3cd
com.nfjh.bean.User@2313052e
*/
```

## 指定注解类型生效[过滤]
```xml
    <!--

先设置过滤所有  再确定只扫描的类型
context:component-scan[base-package & use-default-filters="false"] > context:include-filter[type expression]

    先所有的都扫描,再设置不扫描的类型
		context:component-scan[base-package & use-default-filters="true"] >  context:exclude-filter [type expression]


    base-package 需要扫描的包
    use-default-filters
         false表示全过滤      context:include-filter  需要添加的扫描
         true表示全扫描        context:exclude-filter  需要过滤的类型  若为true   use-default-filters="true" 可以不写

    type annotation
    expression
                    org.springframework.stereotype.Repository
                    org.springframework.stereotype.Service
                    org.springframework.stereotype.Controller
                    org.springframework.stereotype.Component
    -->
```



## 注入数据
### @Value

以前这样注入
```xml
<!--注入简单类型-->  
<bean id="userBean" class="com.nfjh.spring6.bean.User">  
    <property name="username" value="zhangsan"/>  
    <property name="passwd" value="123"/>  
    <property name="age" value="20"/>  
</bean>
```

使用注解这样注入
1、在属性上注入
```java
@Component("userAnnotation")  
public class User {  
    @Value("张三")  
    private String username;  
    @Value("123456")  
    private  String passwd;  
    @Value("21")  
    private int age;

	@Override  
	public String toString() {  
	    return "User{" +  
	            "username='" + username + '\'' +  
	            ", passwd='" + passwd + '\'' +  
	            ", age=" + age +  
	            '}';  
	}
}
/*

㊟:使用@Value的注解方式,可以不用写构造方法和set以及get方法
	toString方法只是用做输出看比较方便,也可以省略

User{username='张三', passwd='123456', age=21}
*/
```

2、在set方法上注入
```java
@Component("userAnnotation")  
public class User {  
    private String username;  
    private  String passwd;  
    private int age;  
  
    @Value("张三")  
    public void setUsername(String username) {  
        this.username = username;  
    }  
    @Value("123456")  
    public void setPasswd(String passwd) {  
        this.passwd = passwd;  
    }  
    @Value("23")  
    public void setAge(int age) {  
        this.age = age;  
    }

/*
User{username='张三', passwd='123456', age=23}
*/
```


3、在构造方法的参数上进行注入
```java
@Component("userAnnotation")  
public class User {  
    private String username;  
    private  String passwd;  
    private int age;  
  
  
    public User(@Value("李四") String username,  @Value("3012") String passwd, @Value("23") int age) {  
        this.username = username;  
        this.passwd = passwd;  
        this.age = age;  
    }

/*
User{username='李四', passwd='3012', age=23}
*/
```


## 自动装配

### @Bean
 #Bean 
```
@Bean明确地指示了一种方法，什么方法呢——产生一个bean的方法，并且交给Spring容器管理；从这我们就明白了为啥@Bean是放在方法的注释上了，因为它很明确地告诉被注释的方法，你给我产生一个Bean，然后交给Spring容器，剩下的你就别管了

记住，@Bean就放在方法上，就是产生一个Bean
```


```
一类是注册Bean,@Component , @Repository , @ Controller , @Service , @Configration这些注解都是把你要实例化的对象转化成一个Bean，放在IoC容器中，等你要用的时候，它会和上面的@Autowired , @Resource配合到一起，把对象、属性、方法完美组装。

 一类是使用Bean，即是把配置好的Bean拿来用，完成属性、方法的组装；比如@Autowired , @Resource，可以通过byTYPE（@Autowired）、byNAME（@Resource）的方式获取Bean；
```

> [113A-WithNotNID-@Configuration与@Bean](../../../113-引文盒/113A-博客-引文/文档类/113A-WithNotNID-@Configuration与@Bean.md)


###  @AutoWired  类型自动装配

AutoWired根据类型自动装配时,类型需要唯一

```java
autowireTest
	dao
		UserDao
							@Repository  
							public interface UserDao {  
							     void insert();  
							}
							
		impl
							@Repository  
							public class UserDaoForJK implements UserDao{  
							    @Override  
							    public void insert() {  
							        System.out.println("计科学生信息插入中");  
							    }  
							}

	
	
	service
		UserService
							@Service  
							public class UserService {  
							    @Autowired  
							    private UserDao userDao;  
							    public void generate(){  
							        userDao.insert();  
							    }  
							  
							}
```

```xml
<!--添加包扫描-->  
<context:component-scan base-package="com.nfjh.autowireTest"/>
```

```java
@Test  
public void testAnnotationAutoWiredInjection(){  
    ApplicationContext applicationContext = new ClassPathXmlApplicationContext("Annotation-test.xml");  
    Object userService = applicationContext.getBean("userService");  
    UserService service = (UserService) userService;  
    service.generate();  
}
//计科学生信息插入中
```


缺点
```java
如何解决同一接口有多个实现类,无法通过类型注入? 

如果在impl包下添加实现类
@Repository  
public class UserDaoForTX implements UserDao {  
    @Override  
    public void insert() {  
        System.out.println("通信学生信息插入中");  
    }  
}
```


```
如果同一个类型有多个实现类,则Spring无法通过AutoWired直接进行装配
例如下面如果UserDao 的实现类除了UserDaoForJK之外还有一个userDaoForTX的话
在运行测试程序时会报错
org.springframework.beans.factory.UnsatisfiedDependencyException: 

Error creating bean with name 'userService': Unsatisfied dependency expressed through field 'userDao'; nested exception is org.springframework.beans.factory.NoUniqueBeanDefinitionException: No qualifying bean of type 'com.nfjh.autowireTest.dao.UserDao' available: expected single matching bean but found 2: userDaoForJK,userDaoForTX

注意:如果UserDao 有多页实现类,但是只有一个实现类添加了@Component以及他的别名,且
其他实现类也没有在XML文件中进行<bean>的配置
这种只算一个,也是可以正常装配的
```


### @AutoWired + Qualifer名称自动装配
对与以上使用类型无法自动装载的问题,可以使用名称自动装载进行解决
在UserService中这样写
```java
@AutoWired
@Qualifer("userDaoForTX")
private UserDao userDao;  
注意@Qualifer括号中的内容是bean的id

即可指定UserService中装载的对象为userDaoForTX
```


### @AutoWired出现的位置

以下举例以使用@AutoWired类型装配有多个实现类无法解决
为例,但是注意,当可以单独使用@AutoWired解决时,@AutoWired也是可以出现在这些位置上的

属性上,set方法上,构造方法上,构造方法的参数上,省略

1、属性上上面已经出现了,不再举例

2、set方法上
```java
@Autowired  
@Qualifier("userDaoForJK")  
public void setUserDao(UserDao userDao) {  
    this.userDao = userDao;  
}
```


3、构造方法上
```java  
    @Autowired  
    public UserService(UserDao userDao) {  
        this.userDao = userDao;  
    }

需要注意的是,@Qualifier限定符不适用于构造函数
" @Qualifier is not applicable for constructor"
所以在测试时,我把userDaoForJK类上的@Repository  给注释了
但是虽然@Qualifier无法在构造方法上使用,但是@Autowired可以

```

4、构造方法的参数上
```java
public UserService(@Autowired  @Qualifier("userDaoForJK") UserDao userDao) {  
    this.userDao = userDao;  
}
```

5、不使用@Autowired
```java
当且仅当有参数的构造方法只有一个,@Autowired注解可以省略

当然如果有多个构造方法,@Autowired不能省略,即使是无参的构造和有参构造,也不能省

public UserService(UserDao userDao) {  
    this.userDao = userDao;  
}

[OS]最好不要省略,会降低代码的可读性!!
```



### @Resource
使用使用这个注解是需要引入jar包的
Spring6支持的javaEE9 所以需要引入的是
```xml
<dependency>
  <groupId>jakarta.annotation</groupId>
  <artifactId>jakarta.annotation-api</artifactId>
  <version>2.1.1</version>
</dependency>
```

```java
dao
			public interface StudentDao {  
			    void delete();  
			}
			
	impl
		@Repository
		public class StudentDaoImpl  implements StudentDao {  
		    @Override  
		    public void delete() {  
		        System.out.println("学生信息删除....");  
		    }  
		}

service
@Service  
public class StudentService {  
  
    @Resource(name="studentDaoImpl")
    private StudentDao studentDaoProp;  

    public void delStu(){  
        studentDaoProp.delete();  
    }
```


1、@Resource 默认使用名称进行装配
```java
当StudentDaoImpl的注解中value是空的
和上面使用@AutoWired结合@Qualifier一样名称默认是类名的首字母小写
 @Resource(name="studentDaoImpl")

当value不为空时填写的
在使用@Resource时name="名称"
```

2、当名称为空时,属性名做为名称进行查找
```java
impl
	@Repository("studentDaoProp")
			public class StudentDaoImpl  implements StudentDao 

service
	@Resource
	    private StudentDao studentDaoProp;  
```


3、当名称为空,且根据属性名无法查找到类时,根据类型进行查找
注意此时根据类型查找时,如果类型有多个,和@Autowired一样是不行的
```java
impl
	@Repository
			public class StudentDaoImpl  implements StudentDao 

service
	@Resource
	    private StudentDao studentDaoProp;  
```

如果条件符合以上可以查询出结果


总结一下

| 注解类型   | 属性上 | set | 构造方法 | 构造方法的参数上 | 来源      |
| ---------- | ------ | --- | -------- | ---------------- | --------- |
| @Autowired | ✓      | ✓   | ✓        | ✓                | Spring    |
| @Qualifier | ✓      | ✓   | ×        | ✓                | Spring    |
| @Resource  | ✓      | ✓   | ×        | ×                | JDK扩展包 |

同时,如果只是用@Autowired说明使用类型注入,被注入的类型是唯一的
@Autowired结合 @Qualifer 说明使用名称注入




## 全注解式开发
```xml
通过使用以上的注解,目前我们的配置文件中只有一个包扫描
<context:component-scan base-package="com.nfjh.bean"/>  

现在编写一个类,用于代替这个配置文件
```

```java
  
@Configuration  
@ComponentScan({"com.nfjh.Resource.dao","com.nfjh.Resource.service"})  
public class Spring6Config {  
}


注意这里的注解 @Configuration   以及 @ComponentScan ,
看清楚不是@ComponentScans,不是s结尾！！！

```

```java
注意此时已经没有了xml文件,所以这里的测试程序需要修改
使用"AnnotationConfigApplicationContext",传入“配置类”的类名,类名随意起,在这里传入即可

AnnotationConfigApplicationContext annotationConfigApplicationContext 
= new AnnotationConfigApplicationContext(Spring6Config.class);  

StudentService studentService = annotationConfigApplicationContext.getBean("studentService", StudentService.class);  
studentService.delStu();
```






# AOP 面向切面编程


## AOP七大术语
```java
关于面向切面编程我的理解:

将与核心业务逻辑无关的代码进行抽离,形成以横向交叉应用于多个项目的"万金油"代码

例如事务管理,日志,安全等,提高代码的复用率

AOP面向切面编程是一种编程思想,而JDK动态代理和GBLIB动态代理就是AOP的实现

```


![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1H-SPRING-aop.png)

连接点[Joinpoint]
	可以织入切面的位置

切点[Pointcut]
	核心业务逻辑方法,真正织入切面的的方法
     一个切点对应多个连接点
     

通知[Advice] 
	我们将要织入的增强代码   
	[前置通知、后置通知、环绕通知、异常通知、最终通知]

切面[Aspect]
	切点 + 通知(在什么位置放什么代码)

织入 [Weaving]
	把通知应用到目标对象上的过程。

代理对象[Proxy]
	 一个目标对象被织入通知后产生的新对象。

目标对象[Target]
	被织入通知的对象。




## 切点表达式

execution([访问控制权限修饰符] 返回值类型 [全限定类名]方法名(形式参数列表) [异常])


## AspectJ

1、使用Spring+AspectJ的AOP需要引入的依赖如下：

```xml
<!--spring context依赖-->
<!--spring aop依赖-->
<!--spring aspects依赖-->
```

2、<font color="#9ebc19">Spring配置文件中添加context和aop的命名空间和约束文件
</font>


### AspectJ框架__注解
#### 5个通知类型
```xml
    <!--组件扫描-->
    <context:component-scan base-package="com.ndjh.spring6.service"/>

	<!--交给spring管理,可用注解代替-->
    <bean id="logAspect" class="com.ndjh.spring6.service.LogAspect"/>
    <bean id="userService" class="com.ndjh.spring6.service.UserService"/>

<!--    开启自动代理-->
<!-- proxy-target-class="true" 强制使用CGLIB动态代理
          proxy-target-class="false" 默认值 ,依情况而定使用哪种代理
                    有接口使用JDK代理,其他使用CGLIB代理
-->
    <aop:aspectj-autoproxy proxy-target-class="true"/>
```

```java
service

UserService
		//Target目标对象,待增强  
		public class UserService {  
		    public void  login(){  
		        System.out.println("系统正在进行身份验证");  
		    }  
		}

LogAspect


//@Aspect注解给spring检查
@Aspect
public class LogAspect {
    //通知+切点
    /*
    通知就是增强代码
     */

    //括号里是切点表达式
    //execution([访问控制权限修饰符] 返回值类型 [全限定类名]方法名(形式参数列表) [异常])
    //注意在全限定类名与方法名之间没有空格

    //Before注解标注的是前置通知
    @Before("execution(* com.ndjh.spring6.service..*(..))")
    public void testBefore(){
        System.out.println("前置通知");
    }

    @AfterReturning("execution(* com.ndjh.spring6.service..*(..))")
    public void testAfterReturning(){
        System.out.println("后置通知");
    }

    //注意环绕通知方法有参数,且有调用方法
    @Around("execution(* com.ndjh.spring6.service..*(..))")
    public void testAround(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("前环绕通知");
        joinPoint.proceed();
        System.out.println("后环绕通知");
    }


    //若异常环绕通知执行,则后环绕通知不会执行,而最终环绕通知执行
    @AfterThrowing("execution(* com.ndjh.spring6.service..*(..))")
    public void testAfterThrowing(){
        System.out.println("异常通知");
    }

    @After("execution(* com.ndjh.spring6.service..*(..))")
    public void testAfter(){
        System.out.println("最终通知");
    }

}

/*----在IDEDA2021.3中运行结果------
前环绕通知
前置通知
系统正在进行身份验证
后置通知
最终通知
后环绕通知
-------------------------------*/

现在修改代码UserService
增加异常
//Target目标对象,待增强  
public class UserService {  
    public void  login(){  
        System.out.println("系统正在进行身份验证");  
        throw  new RuntimeException();  
    }  
}



/*----在IDEDA2021.3中运行结果------
前环绕通知
前置通知
系统正在进行身份验证
异常通知
最终通知

java.lang.RuntimeException
	at com.ndjh.spring6.service.UserService.login(UserService.java:8)
	at com.ndjh.spring6.service.UserService$$FastClassBySpringCGLIB$$93098a3f.invoke(<generated>)
.........异常信息.............

观察可知,最终通知会执行,但是后环绕通知不在执行
-------------------------------*/
```



#### 切面的顺序

对于"切面类"可以使用注解@Order进行排序
@Order(整型数字) 
数字越小越先执行

```java
@Retention(RetentionPolicy.RUNTIME)  
@Target({ElementType.TYPE, ElementType.METHOD, ElementType.FIELD})  
@Documented  
public @interface Order {  
    int value() default 2147483647;  
}
```



#### 通用切点表达式

```java
@Pointcut("execution(* com.ndjh.spring6.service..*(..))")  
public void generalExpression(){}


使用@Pointcut进行标注

当前类进行标注
@Before("generalExpression()")  
public void testBefore(){  
    System.out.println("前置通知");  
}


//跨类使用要写全限定类名+方法名()  
@Before("com.ndjh.spring6.service.LogAspect.generalExpression()")  
public void safetyBefore(){  
    System.out.println("安全前置通知");  
}
```



## Spring事务


spring事务失效的12种场景：
访问权限问题
方法用final修饰
方法内部调用
末被spring管理
多线程调用
表不支持事务
未开启事务
错误的传播特性
自己吞了异常
手动抛了别的异常
自定义了回滚异常
嵌套事务回滚多了



## spring集成Mybatis

pom文件
- 仓库地址
- spring-context
- spring-jdbc
- mybatis
- mybatis-spring
- jdbc
- druid
- junit


```java
mapper :  接口
pojo  : 普通类

service
	接口
	接口的实现类 
		归入Spring管理加上注解 @Service  @Transactional
		添加Mapper中的属性,加上注解 @Autowired,需要时再加上 @Qualifer


resources:
	mapper
		Mapper.xml 编写SQL语句
	jdbc.properties
	mybatis-config.xml
			<settings>  
			    <setting name="logImpl" value="STDOUT_LOGGING"/>  
			    <setting name="mapUnderscoreToCamelCase" value="true"/>  
			</settings>
	spring-config.xml
			1、组件扫描
			2、引入JDBC配置文件
			3、数据源
			4、sqlSessionFactoryBean配置
					mybatis核心配置文件路径
					数据源
					指定别名 [sql中的resultType]
			5、Mapper扫描mapper包
			6、事务管理器
			7、开启事务
```



```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context"  
       xmlns:tx="http://www.springframework.org/schema/tx"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">  
  
<!--1、组件扫描-->  
    <context:component-scan base-package="com.nfjh.bank"/>  
  
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
        <property name="configLocation" value="mybatis-config.xml"/>  
        <!--数据源-->  
        <property name="dataSource" ref="dataSource"/>  
        <!--指定别名-->  
        <property name="typeAliasesPackage" value="com.nfjh.bank"/>  
    </bean>  
<!--5、Mapper扫描mapper包,生成代理类-->  
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">  
        <property name="basePackage" value="com.nfjh.bank.mapper"/>  
    </bean>  
<!--6、事务管理器-->  
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">  
        <property name="dataSource" ref="dataSource"/>  
    </bean>  
<!--开启事务-->  
    <tx:annotation-driven transaction-manager="txManager"/>  
</beans>

```



---

> Citation:
> - []()
> 
> References:
> - []()
