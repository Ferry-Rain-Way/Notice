---

title: SpringMCV 笔记
tags: [SpringMVC,笔记]
categories: [412B-框架工具]
description: 进入文章
sticky: 200
---

---

### springmvc项目创建
1、使用maven创建web项目结构
2、补充更改结构
![700](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1J-SM-index.png)

3、springmvc-config.xml
	1)添加包扫描(context命名空间)
	2)添加视图解析器
		前缀后缀
```xml
    <!--包扫描-->  
    <context:component-scan base-package="com.nfjh.springmvc.controller"/>  
    <!--视图解析器-->  
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
        <property name="prefix" value="/admin/"/>  
        <property name="suffix" value=".jsp"/>  
    </bean><!--  
/admin/main.jsp  
-->
```

4、更换新的web.xml文件
	设置前置控制器DispatcherServlet
	并在控制器中引入spring.xml的配置
```xml
<!--前置控制器DispatcherServlet-->  
    <servlet>  
        <servlet-name>springmvc</servlet-name>  
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
        <!--引入springmvc-config.xml配置-->  
        <init-param>  
            <param-name>contextConfigLocation</param-name>  
            <param-value>classpath:springmvc-config.xml</param-value>  
        </init-param>    
     </servlet>
     
    <servlet-mapping>        
        <servlet-name>springmvc</servlet-name>  
        <url-pattern>*.action</url-pattern>  
    </servlet-mapping>
```


5、index.jsp
	`<a href="${pageContext.request.contextPath}/hello.action">访问服务器</a>`
6、在controller包下创建控制器类
```java
@Controller  
public class UserController {  
    @RequestMapping("/hello.action")  
    public String sayHello(){  
        return "main";  
    }  
}
```

### @RequestMapping
 此注解就是来映射服务器访问的路径.
  1)此注解可加在方法上,是为此方法注册一个可以访问的名称(路径)
```java
@RequestMapping("/demo.action")
    public String demo(){
        System.out.println("服务器被访问到了.......");
        return "main";  //可以直接跳到/admin/main.jsp页面上
    }
```
`  <a href="${pageContext.request.contextPath}/demo.action">访问服务器</a>`

 2)此注解可以加在类上,相当于是包名(虚拟路径),区分不同类中相同的action的名称
 ```java
@RequestMapping("/user.action")
  public class DemoAction1 {..}
 ```
`  <a href="${pageContext.request.contextPath}/user/demo.action">访问服务器</a>`

 3)此注解可区分get请求和post请求

  ```java
 
@Controller
public class ReqAction {
	@RequestMapping(value = "/req.action",method = RequestMethod.GET)
	public String doGetTest(){
		System.out.println("我是处理get请求的........");
		return "main";
	}
	@RequestMapping(value = "/req.action" ,method = RequestMethod.POST)
	public String doPostTest(){
		System.out.println("我是处理post请求的........");
		return "main";
	}
}
/**
	通过此案例可以发现,对于相同的请求路径,使用RequestMethod.POST/RequestMethod.GET
	可以进入不同的方法
*/
  ```


### 5中数据提交方式的优化
![500](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1J-SM-to.png)

#### 总结
```java
1、表单name对应action方法形参
2、表单name对应实体类属性,action 形参类实体类
3、 仅限于超链接或地址拦提交数据,链接中的数据值以'/'分割
	  action方法上的@RequestMapping(value="/{占位字符串1}/{占位字符串2}/submit.action")
	  占位字符串对应action形参名,且需要使用@PathVariable解析
4、表单name与action方法形参名不对应时,在形参名前添加@RequestParam("表单name")
5、action方法形参类型使用 (HttpServletRequest request),方法内部和以前一样 
```


#### 1)方法形参名
```html
<%--1、表单中name对应方法形参名--%>  
<form action="${pageContext.request.contextPath}/submit1.action" method="post">  
    <input type="text" name="student_name"/>  
    <input type="text" name="studentNo"/> <!--测试是否区分大小写-->  
    <input type="submit" value="submit"/>  
</form>
```

```java
//接收数据  
@RequestMapping(value={"/submit1.action"})  
public String  getData1(String student_name, int studentNo){//㊟:此处的形参名区分大小写,所以要和表单中的完全一致  
    System.out.println(student_name + studentNo);  
    return "main";  
}
```

#### 2)封装实体类
```html
<%--  
    中文乱码问题:  
        当前使用的是Tomcat10
实体类:
    private String name;    
    private int age;    
--%>  
  
<form action="${pageContext.request.contextPath}/submit2.action" method="post">  
    <input type="text" name="name"/>  
    <input type="text" name="age"/>  
    <input type="submit" value="submit2"/>  
</form>
```

```java
@RequestMapping(value="/submit2.action")  
public String  getDataByPojo(Student student){//此处的Student类并不在包扫描中,可正常运行  
    System.out.println(student);  
    return "main";  
}
```

#### 3)动态占位符提交
```html
<a href="${pageContext.request.contextPath}/郭洪宇/20111022/submit3.action">submit3</a>
```

```java
@RequestMapping(value = "/{name}/{no}/submit3.action")  
public String getDataByPlaceholder(  
        //测试后发现 如果占位的字符串与形参不对应,会报500错误  
        @PathVariable  
                String name,  
        @PathVariable  
                int no){  
    System.out.println(name + no);  
  
    return "main";  
}
```

#### 4) 映射名称不一致 
```html
<form action="${pageContext.request.contextPath}/submit4.action" method="post">  
    <input type="text" name="uname"/>  
    <input type="text" name="uage"/>  
    <input type="submit" value="submit4"/>  
</form>
```

```java
@RequestMapping(value = "/submit4.action")  
public String getDataAndInconsistentMapping(  
        @RequestParam("uname")  
        String name,  
        @RequestParam("uage")  
        int age){  
    System.out.println(name + age);  
    return "main";  
}
```


#### 5) HttpServletRequest
```html
<form action="${pageContext.request.contextPath}/submit5.action" method="post">  
    <input type="text" name="name"/>  
    <input type="text" name="age"/>  
    <input type="submit" value="submit5"/>  
</form>
```

```java
@RequestMapping(value = "/submit5.action")  
public String getDataByHttpServletRequest(HttpServletRequest request){  
    String name = request.getParameter("name");  
    int age = Integer.parseInt(request.getParameter("age"));  
    System.out.println(name + age);  
    return "main";  
}
```

### 乱码问题
在web.xml文件中添加类CharacterEncoding类
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

### ajax请求

pom.xml
```xml
spring-webmvc
junit
jakarta.servlet-api
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->  
<dependency>  
  <groupId>com.fasterxml.jackson.core</groupId>  
  <artifactId>jackson-databind</artifactId>  
  <version>2.14.1</version>  
</dependency>
```

index.jsp
```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>  
<html>  
<head>  
    <title>Title</title>  
    <%--导入jQuery--%>  
    <script src="js/jquery-3.3.1.js"></script>  
</head>  
<body>  
<a href="javascript:show()">点击显示学生信息</a>  
<div id="mydiv">  
等待响应.....  
</div>  
<script type="text/javascript">  
    function show() {  
        $.ajax({  
            url :"${pageContext.request.contextPath}/list.action",  
            type :"get",  
            dataType : "json",  
            success:function(responseList){  
                let s = "";  
                $.each(responseList,function (i,stuInfo){  
                    s+= stuInfo.name +"------"+ stuInfo.age +"</br>";  
                });  
                $("#mydiv").html(s);  
            }  
        });  
    }  
</script>  
</body>  
</html>

```

pojo
```java
private String name;
private int age;
...
```

action
```java
/**  
 * @Auther: 34838  
 * @Date: 2023/2/2 18:41  
 * @Description:  
 *      生成Student对象封装入List返回  
 *      jackson-databind自动转化实体对象成JSON并响应给前端  
 */  
@Controller  
public class StudentListAction {  
  
    @ResponseBody  
    @RequestMapping("/list.action")  
    public List<Student> classToJson(){  
        List<Student> list = new ArrayList<>();  
        list.add(new Student("小郭",22));  
        list.add(new Student("小张",21));  
        list.add(new Student("小刘",22));  
        return list;//jackson-databind自动转化实体对象成JSON并响应给前端  
    }  
}
```

web.xml → CharacterEncodingFilter 、DispatcherServlet

springmvc-config.xml 
```xml
<!--  
添加context & mvc 命名空间  
-->
<context:component-scan base-package="com.springmvc.controller"/>
<mvc:annotation-driven/>
```


### 跳转方式
前提回顾:
	转发:携带的数据依旧存在,转发的过程发生在"服务器",由服务器转发到新的界面
	重定向:全新的请求,重定向的过程发生在"客户端"

 按照我的归类跳转方式为
 - springmvc  默认返回值拼接转发
 - forward:    转发action/转发页面
 - redirect:  重定向action/重定向页面
 - HttpServletRequest HttpServletResponse  转发
 - HttpServletRequest HttpServletResponse  重定向
 - 举例:
```java
    @RequestMapping("/forward/test.action")
    public String requestForwarding(){
        System.out.println("forward:转发开始");
//        return "forward:/admin/main.jsp"
        return "forward:/ghy/other.action";\
        //注意此处的/ghy是路径的一部分,不是项目名
//        return "forward:/temp/test.jsp";
    }

@RequestMapping("/redirect/HttpServlet.action")  
public void redirectHttpServlet(HttpServletRequest request, HttpServletResponse response)  
        throws ServletException, IOException {  
        System.out.println("HttpServlet重定向开始");  
        response.sendRedirect(request.getContextPath() + "/admin/main.jsp");  
        //在使用HttpServletResponse 进行页面的重定向时需要加上项目名  
}
```

```java
/*
总结:
    springmvc-config.xml文件中 前缀 /admin/  后缀 .jsp
    
    1、不使用forward: & redirect: 时,返回值自动拼接前后缀
    2、forward: & redirect: 都是以webapp为起始点,最前面加'/' 开始
    3、使用 forward: & redirect: 跳转文件夹前后缀无用,
		 都需要加上文件夹名,admin文件夹也要加
    4、使用HttpServletResponse 进行重定向需要加上项目名
```




### 常用默认参数[可传递数据]
```java
HttpServletRequest
HttpServletResponse
Model
Map
ModelMap
```

index.jsp
```html
<a href="${pageContext.request.contextPath}/data.action?haha=22">springmvc param</a>
```

action:
```java
@Controller  
public class DataParamAction {  
    @RequestMapping("/data.action")  
    public String forwardDataTest(  
            HttpServletRequest request,  
            HttpSession session,  
            Model model,  
            Map map,  
            ModelMap modelMap){  
  
        //待转发的数据  
        Student stu = new Student("张三", 45);  
        request.setAttribute("requestStu",stu);  
        session.setAttribute("sessionStu",stu);  
        model.addAttribute("modelStu",stu);  
        map.put("map_stu",stu);  
        modelMap.addAttribute("modelMapStu",stu);  
  
        return "forward:/data/data.jsp";  
    }  
}
```

webapp/data/data.jsp
```html
HttpServletRequest ${requestStu}<br>  
HttpSession session${sessionStu}<br>  
Model model${modelStu}<br>  
Map map${map_stu}<br>  
ModelMap modelMap${modelMapStu}<br>  

错误写法:\${haha} ${haha}<br>  
正确写法:\${param.haha}${param.haha}<br>
```




### 日期

#### 单个日期
总结:@DateTimeFormat 加 <mvc:annotation-driven/>

springmvc-config.xml
```xml
添加mvc命名空间  
开启注释解析器
<mvc:annotation-driven/>
```

index.jsp
```html
<form action="${pageContext.request.contextPath}/date.action" method="post">  
    <input type="date" name="datePlaceholder1"/>  
    <input type="date" name="datePlaceholder2"/>  
    <input type="submit"/>  
</form>
```

```java
//简单日期格式刷:  
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");  
  
@RequestMapping("/date.action")  
public String  testDateParam(  
                @DateTimeFormat(pattern = "yyyy-MM-dd")Date datePlaceholder1,  
                @DateTimeFormat(pattern = "yyyy-MM-dd")Date datePlaceholder2){  
  
    //注意此处形参与表单name保持一致  
    System.out.println("原始值:" + datePlaceholder1);  
    System.out.println("SimpleDateFormat: "  + sdf.format(datePlaceholder1)); //注意此处形参与表单name保持一致  
    System.out.println("原始值:" + datePlaceholder2);  
    System.out.println("SimpleDateFormat: "  + sdf.format(datePlaceholder2));  
  
    return "main";  
}
/*
原始值:Wed Feb 08 00:00:00 CST 2023
SimpleDateFormat: 2023-02-08
原始值:Mon Feb 20 00:00:00 CST 2023
SimpleDateFormat: 2023-02-20
*/

```


#### 多个日期,全局注解
使用@InitBinder注解,不需要添加<mvc:annotation-driven/>
```html
<form action="${pageContext.request.contextPath}/date2.action" method="post">  
    <input type="date" name="datePlaceholder1"/>  
    <input type="date" name="datePlaceholder2"/>  
    <input type="submit"/>  
</form>
```

```java
@InitBinder  
public void initBinderForDate(WebDataBinder webDataBinder){  
    webDataBinder.registerCustomEditor(  
            Date.class,new  CustomDateEditor(new SimpleDateFormat("yyyy-MM-dd"),true)  
    );  
}

@RequestMapping("/date2.action")  
public String  testDateParams(Date datePlaceholder1,Date datePlaceholder2){  
  
    //注意此处形参与表单name保持一致  
    System.out.println("原始值:" + datePlaceholder1);  
    System.out.println("SimpleDateFormat: "  + sdf.format(datePlaceholder1)); //注意此处形参与表单name保持一致  
    System.out.println("原始值:" + datePlaceholder2);  
    System.out.println("SimpleDateFormat: "  + sdf.format(datePlaceholder2));  
  
    return "main";  
}
```


#### 在jsp界面处理日期

1、添加依赖:[Tomcat 10版]
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
如果使用3.0.1的版本,使用core就会抛出异常  
-->  
```

[Tomcat 低版本]
```xml
<!--理论上可行,未经过测试
出现问题看看
https://www.jianshu.com/p/e8b35b8ad9ab
文件在 V:\02-工具环境\JAR\JavaWeb\JSTL
https://blog.csdn.net/Ruiskey/article/details/115363117
-->

<!-- https://mvnrepository.com/artifact/jstl/jstl -->
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>

<!--如果不行的话试试下面的-->
<dependency>
	<groupId>javax.servlet</groupId> 
	<artifactId>jstl</artifactId> 
	<version>1.2</version> 
</dependency>
```

2、index.jsp
```html
<a href="${pageContext.request.contextPath}/date3.action">date数据在前端处理</a>
```

3、模拟数据传给前端
```java
//Date数据在前端转化并展示  
@RequestMapping("/date3.action")  
public String showDate(HttpServletRequest request) throws ParseException {  
    //模拟一个数据传输给前端
    /*Person
	private String name;  
	private Date birthday;
    */
    Person jack = new Person("Jack", sdf.parse("2001-11-02"));  
    request.setAttribute("person",jack);  
    return "forward:/date/date.jsp";  
}
```

4、数据处理 date.jsp
```html
1- 导入格式化标签库
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
2- 使用
<fmt:formatDate value="${person.birthday}" pattern="yyyy-MM-dd"/>

```



#### get、set方法上使用
```java
可以在
Person 中的birthday属性上添加 @DateTimeFormat(patter="yyyy-MM-dd")注解
或者在set方法上添加

如果返回的是JSON格式数据在get方法上添加
[具体内容看文档.doc]
```

### WEB-INF资源访问受限问题
 举例:
	 webapp文件结构:
	 webapp
		 WEB-INF
			 jsp
				 hello.jsp
			 web.xml
		 index.jsp

```xml
 spring-config.xml:
	<!--包扫描-->  
	<context:component-scan base-package="com.nfjh.springmvc.controller"/>

web.xml
<!--前置控制器DispatcherServlet 不在赘述-->
```

```java
@Controller  
public class UserController {  
    //此处的.action  
    @RequestMapping("/hello.action")  
    public String sayHello(){  
        return "/WEB-INF/jsp/hello.jsp";  
        //如果spring-config.xml中添加了前缀 /WEB-INF/jsp/  和后缀.jsp
        //则此处可以直接写 return "hello";
    }  
}
```

 <font color="#9ebc19">此目录下的动态资源,不可直接访问,只能通过请求转发的方式进行访问 </font>
```
访问路径:
http://localhost:8080/项目名/hello.action
```

### 简单登录功能
结构:
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1J-SM-folder.png" alt="300" style="zoom:50%;" />

```java
@Controller
public class LoginController {
    //从loginAction进入登录界面login.jsp
    @RequestMapping("/loginAction")
    public String toLogin(){
        return "login";
    }

    @RequestMapping("/loginCheck")
    public String loginCheck(String name, String passwd, HttpServletRequest request){
        //假设 name: hello
        // passwd : world
        if (name.equals("hello")&&passwd.equals("world")){
            //成功跳转hello.jsp
            return "hello";
        }else{
            //验证失败回到/loginAction
            request.setAttribute("mgs","用户名或密码不正确!");
            return "login";
        }

    }
}

```

springmvc-config.xml
```xml
<!--包扫描-->  
<context:component-scan base-package="com.nfjh.springmvc.controller"/>  
<!--视图解析器-->  
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
    <property name="prefix" value="/WEB-INF/jsp/"/>  
    <property name="suffix" value=".jsp"/>  
</bean>
```

web.xml
```xml
<!--前置控制器DispatcherServlet-->
但是过滤器的过滤路径变成了'/'
<url-pattern>/</url-pattern>
```
http://localhost:8080/springmvc_05_webInf_war/loginAction





### 拦截器
![600](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1J-SM-interceptor.png)

```
SpringMVC的拦截器
  针对请求和响应进行的额外的处理.在请求和响应的过程中添加预处理,后处理和最终处理.
  
拦截器执行的时机
  1)preHandle():在请求被处理之前进行操作,预处理
  2)postHandle():在请求被处理之后,但结果还没有渲染前进行操作,可以改变响应结果,后处理
  3)afterCompletion:所有的请求响应结束后执行善后工作,清理对象,关闭资源 ,最终处理.

拦截器实现的两种方式
  1)继承HandlerInterceptorAdapter的父类
  2)实现HandlerInterceptor接口,实现的接口,推荐使用实现接口的方式
```

HandlerInterceptor实现三步

1、存储数据到session中
2、实现HandlerInterceptor接口
3、在springmvc-config.xml文件中注册拦截器
[springmvc_05_webInf]
```java
@Controller
public class LoginController {
    //从loginAction进入登录界面login.jsp
    @RequestMapping("/loginAction")
    public String toLogin(){
        return "login";
    }

    @RequestMapping("/loginCheck")
    public String loginCheck(String name, String passwd, HttpServletRequest request){
        //假设 name: hello
        // passwd : world
        if (name!=null&&passwd!=null&&
            name.equals("hello")&&passwd.equals("world")){
            //成功跳转hello.jsp
            //1、拦截器实现-存储数据到session
            request.getSession().setAttribute("name",name);
            return "hello";
        }else{
            //验证失败回到/loginAction
            request.setAttribute("mgs","用户名或密码不正确!");
            return "login";
        }
    }

    @RequestMapping("/other")
    public String otherPage(){
        return "other";
    }
}




public class LoginInterceptor  implements HandlerInterceptor {
    //拦截器预处理
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
            throws Exception {

        //取出Session中的用户数据进行判断
        HttpSession session = request.getSession();
        Object name = session.getAttribute("name");
        if (name==null){
            request.setAttribute("mgs","用户未登录,请登录!!");
            request.getRequestDispatcher("/WEB-INF/jsp/login.jsp").forward(request,response);
        }

        return true;
    }
}
```

```xml
<!--拦截器-->  
<mvc:interceptors>  
    <mvc:interceptor>  
        <!--拦截路径(全部)-->  
        <mvc:mapping path="/**"/>  
        <!--放行路径-->  
        <mvc:exclude-mapping path="/loginAction"/>  
        <mvc:exclude-mapping path="/loginCheck"/>  
        <!--实现拦截器接口的类-->  
        <bean class="com.nfjh.springmvc.interceptor.LoginInterceptor"/>  
    </mvc:interceptor>  
</mvc:interceptors>
```

不是，关于登录验证的不能拦截,首页展示不能拦截

---

> Citation:
> - []()
> 
> References:
> - []()





