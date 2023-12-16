---

title: fastjson的使用
tags: [fastjson,json,alibaba,文档]
categories: [412B-框架工具]
description: 进入文章

---

---

![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1L1-UTILS-412B-A1L1-UTILS-index.jpg)


| 原类型 | 目标类型       | 方法                             |
| ------ | -------------- | -------------------------------- |
| <font color="#3271ae">序列化</font>  | | |
| Object `任意Java对象` | String | String str = <font color="red">JSON.toJSONString(Object data);</font> |
| Object `任意Java对象` | byte[]  | byte[] bytes =  JSON.toJSONBytes(Object data); |
| <font color="#3271ae">反序列化</font>  | | |
| String  | 具体Java对象       | 目标类 targetObj = <font color="red">JSON.parseObject(String jsonStr,目标类.class)</font> |
| String | JSONObject | JSONObject jsonObj = JSON.parseObject(String jsonStr); |
| byte[] | JSONObject | JSONObject jsonObj = JSON.parseObject(byte[] bytes);   |
| JSONObject | 具体Java对象 | jsonObj.toJavaObject(目标类.class) |
| JSONObject | 具体Java对象 | jsonObj.getObject("属性名",目标类.class);|
| JSONObject | List  | List<目标类> list = jsonObject.getObject("属性名",new TypeReference<List<目标类>>(){});  |
| String | JSONArray  | JSONArray jsonArray =  JSON.parseArray(String jsonStr);  |
| JSONArray | 具体Java对象 | 目标类 targetObj =  jsonArray.getObject(index, 目标类.class); |
| JSONArray | List | List<目标类> list =  jsonArray..toJavaList(目标类.class); |



### 0.fastjson介绍


fastjson是阿里巴巴的开源JSON解析库，它可以解析JSON格式的字符串，支持将Java Bean序列化为JSON字符串，也可以从JSON字符串反序列化到JavaBean


`FASTJSON v2`是`FASTJSON`项目的重要升级，目标是为下一个十年提供一个高性能的`JSON`库。通过同一套`API`

- 和FASTJSON 1相比，性能有非常大的提升，解决了autoType功能因为兼容和白名单的安全性问题
- 支持`JSON/JSONB`两种协议，[`JSONPath`](https://alibaba.github.io/fastjson2/jsonpath_cn) 是一等公民。
- 支持全量解析和部分解析。
- 支持`Java`服务端、客户端`Android`、大数据场景。
- 支持`Kotlin`
- 支持`JSON Schema` [https://alibaba.github.io/fastjson2/json_schema_cn](https://alibaba.github.io/fastjson2/json_schema_cn)
- 支持`Android`
- 支持`Graal Native-Image`

> 相关文档查看本文引用


### 1.导入依赖:

> 按需选择以下的一种

##### 1.普通
在`fastjson v2`中，`groupId`和`1.x`不一样，是`com.alibaba.fastjson2`：
```xml
<dependency> 
	<groupId>com.alibaba.fastjson2</groupId>
	<artifactId>fastjson2</artifactId> 
	<version>2.0.41</version> 
</dependency>
```

##### 2.旧版本兼容
如果原来使用`fastjson 1.2.x`版本，可以使用兼容包，兼容包不能保证100%兼容，请仔细测试验证，发现问题请及时反馈
```xml
<dependency> 
	<groupId>com.alibaba</groupId>
	<artifactId>fastjson</artifactId> 
	<version>2.0.41</version> </dependency>
```

##### 3.SpringFramework等框架中使用
如果项目使用`SpringFramework`等框架，可以使用`fastjson-extension`模块，使用方式参考 [SpringFramework Support](https://alibaba.github.io/fastjson2/spring_support_cn)。
```xml
<dependency>
    <groupId>com.alibaba.fastjson2</groupId>
    <artifactId>fastjson2-extension</artifactId>
    <version>2.0.41</version>
</dependency>
```




### 2.基本使用

#### 1.速查表

| 原类型 | 目标类型       | 方法                             |
| ------ | -------------- | -------------------------------- |
| <font color="#3271ae">序列化</font>  | | |
| Object `任意Java对象` | String | String str = <font color="red">JSON.toJSONString(Object data);</font> |
| Object `任意Java对象` | byte[]  | byte[] bytes =  JSON.toJSONBytes(Object data); |
| <font color="#3271ae">反序列化</font>  | | |
| String  | 具体Java对象       | 目标类 targetObj = <font color="red">JSON.parseObject(String jsonStr,目标类.class)</font> |
| JSONObject | 具体Java对象 | jsonObj.toJavaObject(目标类.class) |
| JSONObject | 具体Java对象 | jsonObj.getObject("属性名",目标类.class);|
| JSONObject | List  | List<目标类> list = jsonObject.getObject("属性名",new TypeReference<List<目标类>>(){});  |
| String | JSONArray  | JSONArray jsonArray =  JSON.parseArray(String jsonStr);  |
| JSONArray | 具体Java对象 | 目标类 targetObj =  jsonArray.getObject(index, 目标类.class); |
| JSONArray | List | List<目标类> list =  jsonArray..toJavaList(目标类.class); |


#### 2.JSONObject

##### 2.1 获取基本类型对象

```java
String text = "{\"id\": 2,\"name\": \"fastjson2\"}"; 
JSONObject obj = JSON.parseObject(text); 
int id = obj.getIntValue("id"); 
String name = obj.getString("name");
```

##### 2.2 获取任意java对象
```java
// User 本身
class User {
}
JSONObject jsonObj = ...
User user = jsonObj.toJavaObject(User.class);


// User 做为另一个对象的属性,属性名为user
class Clazz{
	private User user;
}
JSONObject jsonObj = ...
User user = jsonObj.getObject("user", User.class);


// User做为另一个对象的List集合中的数据
clazz Clazz{
	private List<User> users;
}
JSONObject jsonObj = ...
List userList = jsonObj.getObject("users", List.class);

/*
以上会存在警告: Unchecked assignment:
可以使用:
1. 使用注解屏蔽警告:(不推荐)
		 @SuppressWarnings("unchecked")
		 List userList = jsonObj.getObject("users", List.class);
		
2. 使用`TypeReference`指定泛型的具体类型：
	    List<User> userList = jsonObject.getObject("users", new TypeReference<List<User>>() {});
*/
```


#### 3.JSONArray
##### 3.1 获取基本类型对象
```java
String text = "[2, \"fastjson2\"]"; 
JSONArray array = JSON.parseArray(text); 
int id = array.getIntValue(0); 
String name = array.getString(1);
```


##### 3.2 获取任意java对象
```java
class User{
	private Integer age;
	private String name;
	
	// getter&setter
	// toString
}

/*
注意: 以下User数组或User集合虽然放在了Claz中
	 但是JSONArray中只有User的数据
*/

// 1. 数组
class Clazz {
	private User[] userArray = new User[2];
}

String userArrayString = "[{\"age\":19,\"name\":\"王五\"},{\"age\":24,\"name\":\"赵六\"}]";  
JSONArray jsonArray = JSON.parseArray(userArrayString);  
User object = jsonArray.getObject(0, User.class);

// 2.集合
class Clazz{
	private List<User> users;
}

String userArrayString = "[{\"age\":19,\"name\":\"王五\"},{\"age\":24,\"name\":\"赵六\"}]";  
JSONArray jsonArray = JSON.parseArray(userArrayString);  
List<User> users = array.toJavaList(User.class);

```




#### 4.小试牛刀
```java
public class User {  
	private Integer age;  
	private String name;
	// getter&setter
	// toString
}
public class Clazz {  
	private String clazzName;  
	private List<User> users;  
	private User[] userArray = new User[2];
	// getter&setter
	// toString
}
```

```java

User user1 = new User(21, "张三");
User user2 = new User(22, "李四");
List<User> users = new ArrayList<>();
users.add(user1);
users.add(user2);
User[] userArray = new User[2];
userArray[0] = new User(19,"王五");
userArray[1] = new User(24,"赵六");

Clazz clazz = new Clazz("计科3班",users,userArray);


System.out.println("=======1.JSON序列化[ Object → String]=======");
String jsonString = JSON.toJSONString(clazz);
System.out.println("jsonString → "+jsonString);

System.out.println("\n======2.JSON反序列化[ String → Object]======");
Clazz clazzObj = JSON.parseObject(jsonString, Clazz.class);


System.out.println("\n======3.JSONObject的使用======");
// {"clazzName":"计科3班","userArray":[{"age":19,"name":"王五"},{"age":24,"name":"赵六"}],"users":[{"age":21,"name":"张三"},{"age":22,"name":"李四"}]}
// 3.1. String → JSONObject
JSONObject jsonObject = JSON.parseObject(jsonString);

// 3.2 读取自定义类型数据
// 3.2.1 使用getObject("key",类型.class)
List<User> userList = jsonObject.getObject("users", new TypeReference<List<User>>() {});
System.out.println("userList → " +userList);
// 3.2.2 使用toJavaObject(类型.class)
// 例如: User user = obj.toJavaObject(User.class);
// 3.3 读取基本类型数据
String clazzName = jsonObject.getString("clazzName");
System.out.println("clazzName → " + clazzName);

System.out.println("\n======4. JSONArray的使用======");
JSONArray userJsonArray = jsonObject.getJSONArray("userArray");
System.out.println("userJsonArray → " + userJsonArray);

// 4.1 读取自定义类型数据
User userWang = userJsonArray.getObject(0, User.class);
System.out.println("userWang → " + userWang);
	// 4.2 读取基本类型数据
	// 使用JSONArray实例对象.getXXXValue(index)
	// XXX代表基本数据类型,例如 studentJsonArray.getIntValue(0);
	// 这里我的数据中没写就不演示了

// 4.3 转成List
List<User> javaList = userJsonArray.toJavaList(User.class);
System.out.println("javaList → "+ javaList);

// parseArray
String userArrayString = "[{\"age\":56,\"name\":\"老王\"},{\"age\":45,\"name\":\"老张\"}]";
JSONArray ja = JSON.parseArray(userArrayString);
User object = ja.getObject(0, User.class);
System.out.println(object);


```

```java
=======1.JSON序列化[ Object → String]=======
jsonString → {"clazzName":"计科3班","userArray":[{"age":19,"name":"王五"},{"age":24,"name":"赵六"}],"users":[{"age":21,"name":"张三"},{"age":22,"name":"李四"}]}

======2.JSON反序列化[ String → Object]======

======3.JSONObject的使用======
userList → [User{age=21, name='张三'}, User{age=22, name='李四'}]
clazzName → 计科3班

======4. JSONArray的使用======
userJsonArray → [{"age":19,"name":"王五"},{"age":24,"name":"赵六"}]
userWang → User{age=19, name='王五'}
javaList → [User{age=19, name='王五'}, User{age=24, name='赵六'}]
User{age=56, name='老王'}
```




---

*更详细的内容可点击以下链接查看*

> Citation:
> - []()
> 
> References:
> - [fastjson-github地址](https://github.com/alibaba/fastjson)
> - [阿里巴巴-fastjson2文档](https://alibaba.github.io/fastjson2/)
> - [# 在 Spring 中集成 Fastjson2](https://alibaba.github.io/fastjson2/spring_support_cn)
> - [`JSONB`格式文档](https://alibaba.github.io/fastjson2/jsonb_format_cn)
> - [`FASTJSON v2`性能有了很大提升，具体性能数据看这里](https://alibaba.github.io/fastjson2/benchmark_cn)
> - [fastjson对泛型的反序列化_unchecked assignment](https://blog.csdn.net/fromzerojiyuan/article/details/121528304)
