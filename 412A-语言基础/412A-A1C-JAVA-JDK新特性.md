---

title: JDK新特性
tags: [jdk,新特性,jdk17,recored,switch,text,block,var,sealed,密封类]
categories: [412A-语言基础]
description: 进入文章

---

---

## 1. JDK 关注的新特性

### 1.0环境准备

- JDK 17 (最低)
- Maven 构建和依赖管理，版本选择 3. 6 以上
- IDEA 2022. 3. 1 Ultimate
- 数据库：MySQL 5 以上版本

### 1.1Record
##### Record的作用
> 解决重复编写JavaBean中的相同代码


Java 14 中预览的新特性叫做Record，在Java中，Record是一种特殊类型的Java类。可用来创建不可变类，语法
简短。参考[JEP 395 ](https://openjdk.java.net/jeps/ 395 ). Jackson 2. 12 支持Record类。


JavaRecord的特点

- 带有全部参数的构造方法
- public访问器
- toString(),hashCode(),equals()
- 无set，get方法。没有遵循Bean的命名规范
- 类是final,不能被其他类继承
> 由于隐式的继承了java.lang.Record类,所以不能在继承其他类
> 虽然隐式的继承了Record类,但是我们依旧不能像`public record Student(String name) extends Record`这样显示的写出来
- 不可变类，通过构造创建Record
- 属性final不可修改
- 不能声明实例属性，能声明static成员

##### 定义

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1C-JAVA-record.png" width = 40%/> </div>

> 在idea中创建Class,如果没有出现Record,检查项目使用的JDK版本


```java
1. 创建Record类
public record Student(Integer id,String name,String email,Integer age) {
}
2.创建Record对象
    //同Class的使用,在需要使用的地方  
    Student lisi = new Student( 1001 , "lisi","lisi@qq.com", 20 );
    System.out.println("lisi = " + lisi.toString());
     //需要注意的是Record的类没有get方法,在需要单独获取的时候使用  对象名.属性名()  的形式获取
    System.out.println("lisi.name() = " + lisi.name());
    //同理: 由于没有set方法,属性值只能赋值一次

```

**实例方法、静态方法的使用与Class相同,不再赘述**
只需要注意在Record方法中的**this**表示当前实例

##### 构造方法
我们可以在 Record 中添加构造方法， 有三种类型的构造方法分别：

-  **紧凑**型构造方法没有任何参数，甚至没有括号
- **规范**构造方法是以所有成员作为参数
- **定制**构造方法是自定义参数个数

编译前:StudentRecord.java
```java
/**
 * 如果没有出现Record
 * 在Product Struct中检查module的JDK版本
 * Alt + insert → 生成测试类
 *  在测试类中Alt + insert → 生成测试方法
 */

public record StudentRecord(Integer id,String name,String email ,Integer age) {
    //规范构造函数是自带的,不用写,也不能写

    //紧凑型构造方法
    public StudentRecord{
        if(id<1){System.out.println(id);}
    }

    //自定义构造方法
    public StudentRecord(Integer id, String email) {
        //注意:自定义构造方法"第一行"必须调用 this() 方法进行传参,否则会报错
        this(id, null, email, null);
        System.out.println("自定义构造方法");
    }
}
```
编译后:StudentRecord.class
```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package com.power.record;

public record StudentRecord(Integer id, String name, String email, Integer age) {
    public StudentRecord(Integer id, String name, String email, Integer age) {
        if (id < 1) {
            System.out.println(id);
        }

        this.id = id;
        this.name = name;
        this.email = email;
        this.age = age;
    }

    public StudentRecord(Integer id, String email) {
        this(id, (String)null, email, (Integer)null);
        System.out.println("自定义构造方法");
    }

    public Integer id() {
        return this.id;
    }

    public String name() {
        return this.name;
    }

    public String email() {
        return this.email;
    }

    public Integer age() {
        return this.age;
    }
}
```

**Record**结成接口的使用和普通class没有区别,不在赘述

##### Local Record
Record 可以作为局部对象使用。在代码块中定义并使用 Record，下面定义一个 SaleRecord
```java
    public static void main(String[] args) {
        //定义 Java Record
        record SaleRecord(String saleId,String productName,Double money){};
        //创建 Local Record
        SaleRecord saleRecord = new SaleRecord("S22020301", "手机", 3000.0);
        //使用 SaleRecord
        System.out.println("销售记录 = " + saleRecord.toString());
    }
```

##### 嵌套和instanceof
> 多个 Record 可以组合定义， 一个 Record 能够包含其他的 Record
> 我们定义 Record 为 Customer，存储客户信息，包含了 Address 和 PhoneNumber 两个Record


```java
方式1:
    //声明
    public record Person(String name,Integer age) {
    }
    //判断obj是否为Record类型
   if( obj instanceof Person(String name, Integer age) ){}

方式2:
    //声明并/判断obj是否为Record类型
    if(obj instanceof Person(String name, Integer age) person){}
```

##### 两个方法
```java
    Customer customer = new Customer(....);

    RecordComponent[] recordComponents = customer.getClass().getRecordComponents();

    for (RecordComponent recordComponent : recordComponents) {
        System.out.println("recordComponent = " + recordComponent);
    }

    boolean record = customer.getClass().isRecord();
    System.out.println("record = " + record);
```

##### 总结

- abstract 类` java.lang.Record` 是所有 Record 的父类。
- 有对于 equals(),hashCode(),toString()方法的定义说明
- Record 类能够实现 `java.io.Serializable` 序列化或反序列化
- Record 支持泛型，例如 `record Gif<T>( T t ) { }`
- `java.lang.Class` 类与` Record` 类有关的两个方法：
> boolean isRecord() : 判断一个类是否是 Record 类型
> RecordComponent[] getRecordComponents()：Record 的数组，表示此记录类的所有记录组件


### 1.2 Switch
##### 箭头表达式
```java
    @Test
    public void testSwitch() {
        int week = 7;
        String memo = "";
        switch (week) {
            case 1 -> memo = "星期日，休息";
            case 2, 3, 4, 5, 6 -> memo = "工作日";
            case 7 -> memo = "星期六，休息";
            default -> throw new IllegalArgumentException("无效的日期：");
        }
        System.out.println("week = " + memo);//week = 星期六，休息
    }
```

1. 在使用  -> 时,单个语句直接写,多个语句用{}包裹
2. 可以注意到以上写法中并没有使用break,这是因为新语法
        只会执行匹配的语句,没有穿透效应
3. 在新语法中进行判断赋值也比较方便
4. case 标签-> 与 case 标签：不能混用

```java
        旧:
            int opt;
            switch (fruit) {
            case "apple": opt = 1; break;
            case "pear":
            case "mango":opt = 2; break;
            default:opt = 0;break;
            }
        新:
         String fruit = "apple";
            int opt = switch (fruit) {
                case "apple" -> 1;
                case "pear", "mango" -> 2;
                default -> 0;
            }; // 注意赋值语句要以;结束

```


##### yield
```java

    @Test
    public void testYield(){
        int week = 2;
    //yield 是 switch 的返回值， yield 跳出当前 switch 块
    String memo = switch (week){
            case 1: yield "星期日，休息";
            case 2,3,4,5,6: yield "工作日";
            case 7: yield "星期六，休息";
            default: yield "无效日期";
        };
        System.out.println("week = " + memo);//week = 工作日
    }

```




##### switch判断Record
```java

    @Test
    public void testSwitchRecord(){
        //创建三个Record 不能使用局部Record

        Line line = new Line(20);
        Rectangle rectangle = new Rectangle(10,20);
        Shape shape = new Shape(20,30);

        Object obj = line;

        //此处使用需要JDK19+
        int result = switch(obj) {
            case Line(int x  ) -> {
                System.out.println("线的长度为:"+ x);
                yield x;
            }
            case Rectangle(int w,int h) -> w*h;
            case Shape(int width,int height) -> {
                System.out.println("周长为:"+ 2*(width+height));
                yield width*height;
            }
            default -> 0;
        };
    }
```

### 1.3 Text Block

Text Block 处理多行文本十分方便，省时省力。无需连接 "+",单引号，换行符等。
Java 15 ,参考[JEP 378](https://openjdk.org/jeps/378)

##### 文本块
语法：使用三个双引号字符括起来的字符串

```java
""" 
内容
"""
```

例如:
```java
例如：
String name = """lisi"""; //Error 不能将文本块放在单行上
String name= """lisi
20 """; //Error 文本块的内容不能在没有中间行结束符的情况下跟随三个开头双引号

String myname= """
zhangsan
20
"""; //正确
```

文本块定义要求：

- 文本块以三个双引号字符开始，后跟一个行结束符
- 不能将文本块放在单行上
- 文本块的内容也不能在没有中间行结束符的情况下跟随三个开头双引号

***三个双引号字符""" 与两个双引号""的字符串处理是一样的。与普通字符串一样使用。例如equals(),"==",
连接字符串（”+“）， 作为方法的参数等***

##### 文本块的空白
**前置空白**
1.第二行(内容的第一行)与尾行的"""对齐
如果我们明确需要前置空格，则可以使用indent()方法
例如如下代码会将4个额外的前导空格添加到我们的JSON代码段中

```java
String text = """
        {
            "name": "FunTester",
            "age": "30"
        }
        """.indent(4);
```
2.第二种方法是
第二行(内容的第一行)与尾行的"""不对齐,
尾行的三个引号在前
他们之间的差距就是添加的前置空格数量

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1C-JAVA-blank.png" width = 60%/> </div>

控制台效果:
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1C-JAVA-blank2.png" width = 60%/> </div>

##### 文本块方法
1. str.indent(number) 添加前置空白
2. formatted()
```java
public void fun4(){
    String info= """
        Name:%s
        Phone:%s
        Age:%d
        """.formatted("张三","13800000000",20);
    System.out.println("info = " + info);
}
```
3. String stripIndent()：删除每行开头和结尾的空白
4. String translateEscapes() ：转义序列转换为字符串字面量


##### 转义
使用新的转义序列，我们可以将单行的内容拆分为多行，而无需创建实际的行终止符
```
String text = """
        1
        2 \
        3 \
        4
        5
        """;
```
控制台:
```
1
2 3 4
5
```

转义三引号
```
String text = """
        测试文本 \"""
        """;
```
控制台输出:
`测试文本 """`

##### 总结

1.多行字符串，应该使用 Text Block
2.当 Text Block 可以提高代码的清晰度时，推荐使用。比如代码中嵌入 SQL 语句
3.避免不必要的缩进，开头和结尾部分
4.不要同时使用空格和制表符,这样将导致不规则的空白
5.对于大多数多行字符串， 分隔符位于上一行的右端，并将结束分隔符位于文本块单独行上。例如:
```java
String colors= """
                red
                green
                blue
                """;
```

### 1.4 var
##### 版本
在 **JDK 10 及更高版本**中，您可以使用 var 标识符声明具有非空初始化式的局部变量，这可以帮助您编写简洁的
代码，消除冗余信息使代码更具可读性，谨慎使用

##### var 声明局部变

var 特点:

- var 是一个保留字，不是关键字（可以声明 var 为变量名）
- 方法内声明的**局部变量**，必须有**初值**
- 每次声明一个变量，不可复合声明多个变量。 var s1="Hello", age=20; //Error
- var **动态类型**是编译器根据变量所赋的值来推断类型
- var 代替显示类型，代码**简洁**，减少不必要的排版，混乱。

var 优缺点
- 代码简洁和整齐
- 降低了程序的可读性（无强类型声明）

实例:
```java
//通常
try (Stream<Customer> result = dbconn.executeQuery(query)) {
//...
}

//推荐
try (var customers = dbconn.executeQuery(query)) {
//...
}
比较 Stream<Customer> result 与 var customers
```

##### 使用时候使用 var

- 简单的临时变量
- 复杂，多步骤逻辑，嵌套的表达式等，简短的变量有助理解代码
- 能够确定变量初始值
- 变量类型比较长

```java
public void fun1(){
    var s1="lisi";
    var age = 20;
    for(var i=0;i<10;i++){
        System.out.println("i = " + i);
    }
    List<String> strings = Arrays.asList("a", "b", "c");
    for (var str: strings){
        System.out.println("str = " + str);
    }
}
```


### 1.5 密闭类sealed
##### sealed
sealed 翻译为密封，密封类(Sealed Classes)的首次提出是在 Java15 的 JEP 360 中，并在 Java 16 的 JEP 397 再
次预览，而在 Java 17 的 JEP 409 成为正式的功能

Sealed Classes 主要特点是**限制继承**，Java 中通过继承增强，扩展了类的能力，复用某些功能。当这种能力不受控。
与原有类的设计相违背，导致不预见的异常逻辑

Sealed Classes **限制无限的扩张**

Java 中已有 sealed 的设计

- final 关键字，修饰类不能被继承
- private 限制私有类
sealed 作为关键字可在 class 和 interface 上使用，**结合 permits 关键字**,定义限制继承的密封类


##### Sealed Classes
sealed class 类名 permits 子类 1,子类2 ,子类..,子类N {}
> permits 表示允许的子类，一个或多个
> 即允许permits后面的子类列表继承 当前类

子类声明有三种

- final 终结，依然是密封的
- sealed 子类是密封类，需要子类实现
- non-sealed 非密封类，扩展使用，不受限

举例:
```java

//第一种 final → 不允许继承
public final class Circle extends Shape {
}
//第二种 sealed class → 只允许RoundSquare继承
public sealed class Square extends Shape permits RoundSquare {
    @Override
    public void draw() {
    System.out.println("=======Square 图形======");
    }
}
//密封类的子类的子类 
public final class RoundSquare extends Square{
}
//非密封类 ， 可以被扩展。放弃密封
public non-sealed class Rectangle extends Shape {
}
```


##### Sealed Interface
密封接口同密封类

声明密封接口
```java
public sealed interface SomeService permits SomeServiceImpl {
    void doThing();
}
```

实现接口
```java
public final class SomeServiceImpl implements SomeService {
    @Override
    public void doThing() {
    }
}
```

**以上类和接口要在同一包可访问范围内**

---

> Citation:
> - []()
> 
> References:
> - [文章来源:动力节点](#)





