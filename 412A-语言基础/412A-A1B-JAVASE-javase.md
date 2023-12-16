---

title: java基础学习
tags: [javase,郝斌]
categories: [412A-语言基础]
description: 进入文章
sticky: 100

---

---

## **JAVA概述**

### java概述

#### 1>起源

```java
sun公司Green项目hotjava浏览器
```

#### 2>java特点

```java
简单易学：
    没有c和c++的指针，内存申请和释放
安全性高：
    强类型，垃圾回收机制，禁止非法内存访问。
跨平台：
    作为一种网络语言，其源代码被编译成一种结构中立的中间文件格式。只要有Java运行系统的机器都能执行这种中间代码。
    java源程序被编译成一种与机器无关的字节码格式，在Java虚拟机上运行。硬件操作系统编译器高级语言程序用户
多线程:
即能够使得一个程序同时执行多个任务

```

#### 3>java虚拟机JVM

```java
Java虚拟机(JVM)是一个虚构的计算机，它在实际的硬件和操作系统上运行，并且能够执行Java字节码。Java字节码是由Java编译器从Java源代码编译而来的。JVM是Java平台的核心组件，它使得Java程序能够以“一次编写，到处运行”的方式跨不同的硬件和操作系统平台执行。

JVM的主要组成部分包括：

类加载器(ClassLoader)：用于加载Java类文件(以.class为扩展名)到JVM中。它负责找到和加载类文件，以及管理和回收已加载的类。
执行引擎：用于执行Java字节码。它将字节码翻译成对应平台上的本地机器码，然后通过操作系统调用计算机硬件执行相应的指令。
垃圾回收器(Garbage Collector)：负责自动回收不再使用的内存空间，以释放内存资源供其他对象使用。这样可以避免内存泄漏和内存溢出等问题。
运行时数据区：用于存储Java程序在运行过程中所需的数据和元数据。它包括方法区、堆区、栈区、程序计数器等。
JVM通过这些组成部分来实现Java程序的跨平台运行和内存管理等重要功能。开发者只需要编写一次Java代码，然后将其编译成字节码，就可以在任何安装了JVM的设备上运行该程序，无需对源代码进行修改。
```



#### 4>JVM的平台相关性

```java
java源代码与字节码是与机器无关的，故在装有不同操作系统的机器上，需要有专门为该操作系统开发的JVM,JVM是与机器有关的.
```

#### 5>java的应用领域

```java
1、J2SE ,主要用来开发桌面应用软件
2、J2ME，嵌入式开发，像手机里的软件，掌上电脑
3、J2EE，属于网络编程，JSP等，
```

#### 6>学习目标

```java
了解程序语言及发展历史，掌握语法规则，掌握常用类的使用掌握编程逻辑思维能力：会看懂程序，会调试程序，理解并应用面对对象的设计思想。为将来学习J2EE做准备
```

#### 7>环境变量的设置：

```java
一,java 安装
1.下载java安装文件
安装目录自选但是要记住安装路径。C:\Program Files (x86)\Java
安装过程中 点击下一步即可
安装完成后打开cmd命令输入

java回车
java -version回车//注意此处在java之后有一个空格，如果正确会出现安装的版本


2.搜索：编辑系统环境变量

创建：
变量名：JAVA_HOME
变量值：jdk安装路径即可,例如我安装路径：C:\Program Files\Java\jdk-9.0.4

编辑第二个变量名：path
变量值：%java_home%\bin
环境变量配置名是固定的，但是值是根据你安装具体路径复制过来的。不要直接写别人的
```

#### 8>classpath的设置

```java
为什么要设置path：
    1、在dos的任何目录下我们都可以运行系统自带的命令；
    2、要想在dos下运行用户自己的程序，则必须进入到改程序的当前目录下方课运行； 
    3、如果希望在dos的任何目录下都可以运行自己创建的程序，则需要我们自己手动设置操作系统自带的环境变量path.
path的设置：
    操作系统是利用path变量来寻找当前程序所存放的路径，并且以最先找到的为准。路径与路径之间用分号;分开。

```

#### 9>常见dos命令

```java
cd \ 表示进入当前根目录下
cd A\B\C 表示当前目录下的A文件夹下的B文件夹下的C文件夹下面
E： 进入E盘根目录
dir 查看文件夹下文件信息
cls 清屏
javac name.java 编译java文件
java name 运行java文件，即打开.class文件
编译时写文件名，运行时写文件中的类名。故文件的名字和类名最好一样
    
java带包编译[javac -d . 类名.java]
    例如：
    javac -d . Hello.java
    
```

### 基础知识

#### 1>Java语言的基本要素——标识符

```java
定义：
程序员对程序中的各个元素加以命名时使用的命名记号称为标识符，
包括：类名、变量名、常量名、方法名、……
规则：
    标识符是以字母，下划线(_)美元符($)开头的一个字符序列，后面可以跟字母，下划线，美元符，数字。
    关键字：abstract default if private

```

#### 2>数据类型

```java
基本数据类型：
数值型(整数类型(int，byte，short，long)
浮点类型(float，double))
字符型(char)
布尔型(boolean)
引用数据类型：(类(class)，接口(interface)，数组)；

```

#### 3>输出数据的格式控制：

```java
%d( int, long int, short ,byte)
%f(float,double)
%c(char)
%x,%X,%#X,%#x (int long int )
%s (string)
%b (boolean)
```

#### 4>常量

```java
(1)整型常量：
    十进制，十六进制，八进制
    一个常量整数默认是int类型，如果数字过大，则必须在末尾加L,否则会报错。
    例：long i = 5678678956789；//error
    long i = 5678678956789L；//ok
(2)浮点型：
    一个实数默认是double类型。如果希望一个实数是float类型，可以在数字后面加f(F)。将一个double类型数值付给float类型变量，编译时会报错。
    例：float x = 2.2；//error float x = 2.2f;//ok
(3)字符常量：
    必须用单引号括起来；Java中字符和字符串都用Unicode编码表示；在Unicode编码中一个字符占两个字节。‘a'‘\n' '\uxxxx'特殊字符的常量表示法'\\' '\n'
(4)布尔类型：
    用boolean表示，不能写成bool；布尔型数据只有两个值true和false，且他们不对应于任何整数值。
    定义：boolean b = true
    只能参与逻辑关系运算：&& || == ！= ！

+-------------------------------------------------+
Infinity常量【极限数】与NaN 【非数值：Not a Number】
    float/double a = 3.0;
    小数运算：a/0 结果：Infinity;
			a%0 结果：NaN

+-------------------------------------------------+

```

#### 5>不同类型变量的字节

```java
System.out.println("byte所占位数：    "   + Byte.SIZE      + "    -> 1字节");	
System.out.println("short所占位数：   "  + Short.SIZE      + "    -> 2字节");	
System.out.println("int所占位数：      "    + Integer.SIZE  + "    -> 4字节");	//此处不写Int 而写Integer
System.out.println("long所占位数：    "   + Long.SIZE      + "    -> 8字节");		
System.out.println("char所占位数：    "   + Character.SIZE + "  -> 2字节");	//此处不写char 而写Character
System.out.println("float所占位数: "  + Float.SIZE      + "    -> 4字节");	
System.out.println("double所占位数：" + Double.SIZE      + "    -> 8字节");		


```

#### 6>不同类型的变量相互转换：

```java
一般低字节可以转换成高字节。高字节转换成低字节必须强制转换。
byte b = 10;//1个字节
int i = 6;//4个字节
i = b;//ok b = i；//error 会丢失数据
b = (byte)i；//ok 强制类型转化
//b = i;//本语句错误，上面的(byte)i并没有改变i本身的数据类型。

```
##### 多格式转String
```java 
String.ValueOf(各种类型);

```
##### int转String
```java
int num1 = 9;
int num2 = 12;
		方法一：
				int num3 = num1 + num2;
				String str3 = num3 + "";
			
		方法二：
				String str3 = Integer.toString(num1 + num2);
		
		方法三：
			  	Integer num3 = num1 + num2 ;
			  	String str3 = num3.toString(num3);
		 
		方法四：
				int num3 = num1 + num2;
				Integer it = new  Integer(num3);
				String str3 = it.toString();
		
	
		方法五：
			String str3 = String.valueOf(num1 + num2);
		 
		 
```
##### String转int
```java
1.
	String str = "1233";
	int i = Integer.parseInt(str);
	//int i = Integer.parseInt("1234");
2.

```
##### java中"+"的作用

```java
java中"+"的作用
   1.字符串的连接【字符串+字符串】
    	String str = "hello" + "world!";//str = "helloworld!"
   2.类型转换	【数值+字符串】
       String str = 3.0 + "hello" ;//str = "3.0hello";
   3.ASCII码值相加【单个字符+单个字符】
       ' ' + '!'
       /*
       	空格字符  对应ASCII码：32
      	！		对应ASCII码：33
      	所以计算结果为：65
      */
        ①：int value = ' ' + '!';//value = 65;
        ②：char ch = ' ' + '!';//ch = 'A';
	
 题目：System.out.println('1' + '2' + "" + 3 + 4);
        '1' + '2' = 49 + 50 = 99;
        99 + "" = "99";
        "99" + 3 + 4 = "9934";
```





#### 7>算术运算符：

```java	
(1)“+”可以表示数值的相加，字符串的联接，也能把非字符转换成字符
    串。System.out.println('a'+1);与System.out.println(""+'a'+1);结果98 a1
(2)除法运算符(/)
    跟C语言一样。
(3)取余运算符(%)
    java中允许取余取余运算符的被除数和除数是实数，(与C/C++不同)。但所得余数的正负只和被除数相同。
    取余：a%b
    公式：a-a/b*b
    举例:mod(-10,-3):-10- (-10)/(-3)*(-3)=-1
    记忆：结果符号看a的符号
        
(4)逻辑与，逻辑或。
    跟C语言一样。
(5)位运算符：(0表示正数，1表示负数)
    &(按位与)把两个数字所有的二进制位相与：1&1=1，1&0=0，0&0=0；0&1=0
    |(按位或)把两个数字所有的二进制位相或：1|1=1，1|0=1，0|0=0；0|1=1
    ~(按位取反)把一个数字的所有二进制位取反。~1=0 ~0=1
    ^(按位异或)把两个数字的所有二进制位异或1^1=0，1^0=1，0^0=0；0^1=1
    >>(右移)与C/C++不同，对于有符号数，在右移时，符号位将随同移动，当为正数时，最高位0，最高位补零，而为负数时，最高位为1，最高位补1。移位能让用户实现整数除以或乘以2的n次方的效果。
    >>>(右移)无论最高位是0还是1，左边移空的都补为零。
(6)自增自减
(7)三元运算符boolean b = 20 <= 45 ? true : false;


```



 Java的位运算(bitwise operators)直接对整数类型的位进行操作，这些整数类型包括long、int、short、char和 byte，位运算符具体如下表： <br>
 <br>

| 运算符| 说明 |
| -- | -- |
| << | 左移位，在低位处补0 |
| >> | 右移位，若为正数则高位补0，若为负数则高位补1|
| >>> | 无符号右移位，无论正负都在高位补0|
| &| 与(AND)，对两个整型操作数中对应位执行布尔代数，两个位都为1时输出1，否则0。|
| \| |或(OR)，对两个整型操作数中对应位执行布尔代数，两个位都为0时输出0，否则1。|
| ~| 非(NOT)，一元运算符。|
| ^| 异或(XOR)，对两个整型操作数中对应位执行布尔代数，两个位相等0，不等1。|
| <<=| 左移位赋值。|
| >>= | 右移位赋值。|
| >>>= | 无符号右移位赋值。|
| &=| 按位与赋值。|
| \|= |按位或赋值。|
| ^=| 按位异或赋值。|



#### 8>流程控制
```java
(总体同C语言)
```

#### 9>面向过程设计思想

```java
优点： 
    1、分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现。
    2、以算法为核心，
    3、自顶向下设计，要求一开始必须对问题有很深的了解
    4、将大问题转化为若干小问题来求解
    5、表现形式：
        用函数来作为划分程序的基本单位
    6、直接面向问题
缺点：数据和操作分离开，对数据与操作的修改变得很困难；数据的安全性得不到保证；程序架构的依赖关系不合理

```

#### 10>面向对象的设计思想
```java
1、确定该问题由哪些问题组成！先用类模拟出该事物
2、通过类间接解决问题
```
#### 12>内存空间分配 
[详见 String中的equals ](##### string的equals)

#### 11>printf与println 的区别 
```java
import java.lang.String;

class Dian
{
	public int x, y;
	
	public Dian(int x, int y)
	{
		this.x = x;
		this.y = y;
	}

	public String toString()
	{
		return "[" + x + ", " + y + "]";
	}
}


public class TestPrint
{
	public static void main(String[] args)
	{
		Dian d = new Dian(3, 2);
		//System.out.printf("%s\n", d);
		System.out.println(d);
	
		int i, j, k;
		i = 1;
		j = 2;
		k = 3;
		System.out.printf("%d的值 + %d的值 是 %d\n", i, j, k);
		//System.out.println(i + "的值 + " + j + "的值 是 " + k);
		
		int m = 47;
		System.out.println(m);
		System.out.printf("%d\n", m);
		
		System.out.printf("十进制数字%d用十六进制表示是: %#X\n", m, m);
		//System.out.println("十进制数字" + m + "用十六进制表示是: 0X" + Integer.toHexString(m).toUpperCase());
		
		
		System.out.printf("%b\n", "abc".equals("zhangsan"));
		System.out.printf("%d\n", "abc".length());
		System.out.printf("%d\n", "abcadssad".indexOf("ads"));
		
	}
}

```


#### JAVA命名规则  [博客园](https://www.cnblogs.com/liqiangchn/p/12000361.html)

```java
4.JAVA命名规则：
     1.项目名:全部小写
     2.包名:全部小写
     3.方法名、变量名:"小驼峰"	//strMsg
     4.类名、标识符:"大驼峰"	//TestAnimal
     5.常量:全部大写，但此间使用下划线分割 // MAX_LENGTH		

     +-----------------------------------------------------------------+
     |"小驼峰"：第一个单词首字母小写，其余每一单词首字母大写
     |"大驼峰"：每一个单词的首字母大写
     +-----------------------------------------------------------------+	

注意：所有的命名都要遵循：
     1)、名称只能由字母、数字、下划线、$符号组成
     2)、不能以数字开头
     3)、名称不能使用JAVA中的关键字
     4)尽量不要使用拼音；杜绝拼音和英文混用
         对于一些通用的表示或者难以用英文描述的可以采用拼音，
         一旦采用拼音就坚决不能和英文混用。 正例： BeiJing， HangZhou 反例： validateCanShu
	5)命名过程中尽量不要出现特殊的字符，常量除外
```




#### 12>数组

##### 数组概述
```java 
1. 为什么需要数组
        1>为了解决大量同类型数据的存储和使用问题
        2>为了模拟现实世界
2. 什么叫一维数组
        1>为n个变量连续分配存储空间
        2>所有变量的数据类型相同
        3>所有变量所占字节数大小相等
3.数组中的元素可以是基本类型变量，也可以是引用类型变量
```

##### 一维数组的使用
```java
1.声明的语法格式
        1> 类型 var [];
        2> 类型 [] var;
2. 举例代码：
/*
	一维数组的使用_1
*/

public class TestArray_1
{
	public static void main(String[] args)
	{
		//方式一
		int[] arr1;
		arr1 = new int[3];
		arr1[0] = 0;
		arr1[1] = 1;
		arr1[2] = 2;
		showArr(arr1);
		System.out.println("************************");
		
		//方式二
		int[] arr2 = new int[]{0,1,2};
		showArr(arr2);
		System.out.println("************************");


/*		System.out.println(arr1);  //error  一维数组的内容是不能通过System.out.println()直
            接输出的,即便该数组的内容是引用且已经重写了toString方法也不行
	
		int[3] arr3 = new int[]{0,1,2};  //  error
		int[] arr4 = new int[3]{0,1,2};  //error
		int[3] arr5 = new int[3]{0,1,2};  //error
*/

		//方式三
		int[] arr6 = {0,1,2};  //25行
		showArr(arr6);
		System.out.println("************************");
		arr6 = new int[]{5,4,3,2,1};  //arr6本来是指向25行的{1,2,3}， 但是也可以改变 arr6的值，使其指向{5,4,3,2,1}
		showArr(arr6);		
	}
	
	public static void showArr(int[] arr)
	{
		for (int i = 0; i<arr.length; ++i)//length是属性，不是方法，所以这里不加欧豪
			System.out.println(arr[i]);
	}	
}
4.我的总结：
        数组在整体赋值时[]中不能有数字；
```
##### 创建并使用引用类型数组
```java
1.代码：
public class Test {
    public static void main (String args[]){
        MvDate [] m;//栈中分配 m 
        m = new MyDate [10];//堆中分配MyDate[]空间,共10 个，均为null
        for(int i=0; i<10; i++){
            m[i]= new Mydate(i+1,i+1,1990+i);
            //i = 0 时；分配Mydate[0]，存放 1,1,1990  ，此时MyDate中的第一个null改变，存放Mydate[0]的地址，即指向了Mydate[0]的三个元素
            m[i].dispaly();
        }
    }
}

2.引用类型元素组成的一维数组在使用过程中一般存在着两级的指向关系，这是理解多维不等长数组的基础


```
##### 多维数组
```java
1.多维数组举例
    1> int [][] aa = new int [2][3];
    2> int [][] aa = {3,2,7},{1,5},{1,6};//不等长数组

                    |-->  3  2  7
    int aa [][] ——  |-->  1  5
                    |-->  6
```
##### 数组的拷贝
```java
1. 格式：public static void arraycopy(Object arr1, int Pos1, Object arr2, int pos2, int length);
2. 参数：
        arr1 - 源数组
        Pos1 - 源数组中的起始位置
        arr2 - 目标数组//arr2被改变
        pos2 - 目标数据中的起始位置
        length - 要复制的数组元素的数量
3.操作：将arr1 指向的数组中下标从pos1开始的length个元素 "覆盖" 掉arr2指向的数组从pos2开始的length个元素
4.注意："arraycopy()"方法名中全是小写，不能是大写
5.代码：

public class arraycpoy {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int[] a = {1, 2, 3, 4, 5};
		int[] b = {-1,-2,-3,-4,-5};
		
		//-1 1 2 -4 -5
		System.arraycopy(a, 0, b, 1, 2); //是arraycopy 不要写成了 arrayCopy 

		System.out.println("a = ");
		for (int i=0; i<a.length; ++i)
		{
			System.out.printf("%d ",a[i]);//(a[i]);
		}
		System.out.printf("\n");
		
		System.out.println("b = ");
		for (int i=0; i<b.length; ++i)
		{
			System.out.printf("%d ",b[i]);
		}

		
	}

}
/*
 * 在jdk11.8中的运行结果是：
--------------------
a = 
1 2 3 4 5 
b = 
-1 1 2 -4 -5 
--------------------
*/

```
##### 数组排序
```java
1. 方法：
    static void sort(int[] a) 
          对指定的 int 型数组按数字升序进行排序。 
2.代码：
import java.util.*;

public class TestArraysSort_1
{
	public static void main(String[] args)
	{
		int[] data = {1,3,5,7,2,4,6,8,10,9};
		System.out.println("排序前数组data中的内容是:");
		showArray(data);
		
		Arrays.sort(data);
		
		System.out.println("排序后数组data中的内容是:");
		showArray(data);
	}
	
	public static void showArray(int[] data)
	{
		for (int e : data)
			System.out.printf("%d\t", e);
		System.out.println("");
	}
}
/*
	在JDK 1.6中的运行结果是：
------------------------
排序前数组data中的内容是:
1       3       5       7       2       4       6       8       10      9

排序后数组data中的内容是:
1       2       3       4       5       6       7       8       9       10
------------------------
*/
```



## **面向对象**

### 1>封装

#### 类

```java
1.把一类事物静态属性和动态可以执行的操作组合在一起所得的这个概念就是类
2.类是抽象的，用来模拟一类事物，是一个概念
3.一旦定义了，类的概念就永远存在
4.定义：
    class Person
    {
        int age；
        void shout()
        {
        System.out.println("oh,my god!"+ age);
        }
    }
    1>age是类的属性，也叫类的成员变量，也叫字段，也叫域
    2>shout是类的方法，也叫类的成员函数
    3>shout方法可以直接访问同一个类中的age变量
5.访问与引用
    1>对象名.属性//访问对象的属性
    2>对象名.成员方法名()//访问对象的方法
    3>aa.i和aa.j叫做属性引用
    4>访问对象的属性和方法叫做引用
    5>对象引用较为特殊
        A aa  = new A();其中aa叫做类A引用类型的变量，存放在栈中，
        用来指向new出来的对象的“对象引用”

```

#### 对象

```java
1.类的一个个体
2.具体的，实实在在存在的事物
3.生命周期是短暂的，会生成和消亡

```

#### 类与 对象



![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1B-JAVASE-class.JPG)

#### 程序执行过程


![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1B-JAVASE-001.JPG)

#### 访问控制符

```java
1. 需要将类的属性变成私有的，外部类不能直接访问，希望把若干个
    方法变成一个个"按钮"提供给使用者，此时就需要访问控制符。
2.访问控制符有四种：
    public
    private
    protected
    默认【不写】
3.注意：
在一个类的内部，所有的成员可以相互访问，访问控制符是透明的
在一个类的外部:
			通过【类对象名.私有成员名】//error
             的方式是无法访问该对象中的私有成员的，
             这样写编译时会出错!

```

#### 构造方法

```java
1.特点：
不能有返回值 
方法名与类名相同 
可以有多个
2.注意：
    默认生成无参无方法体无返回值的构造函数
    自己一旦定义，编译器将不再生成默认的构造函数
    生成一个类对象时能且只能调用其中一个构造函数

```

#### 初始化

```java
1.当一个对象被创建会对其中各种成员变量自动进行初始化赋值
```

| 成员变量类型        | 初始值             |
| ------------------- | :----------------- |
| byte                | 0                  |
| short               | 0                  |
| int                 | 0                  |
| long                | 0L                 |
| float               | 0.0F               |
| double              | 0.0D               |
| char                | '\u0000'(表示为空) |
| boolean             | Flase              |
| All  reference type | Null               |

```java
2.局部变量：
    1>方法中的形参
    2>方法内部变量
    3>main中的变量
3.
    1>如果在定义的时候不初始化，则它的值是系统自动分配好的
        默认值!
    2>如果在定义的同时赋初值，则是可以的,也就是说该值是生
        效的。注意在C++中则不可以，在C++中一个类的数据成
    	员不能在定义的同时初始化，它只能在构造函数中初始
    	化 如果在定义的同时赋初值，当然生效，但如果在构造
    	函数中又改变了定义时赋的初值，则该数据成员最终的
    	值就是构造函数中修改之后的那个值，
    	因为:
    	/*系统会先执行定义时赋的初值，然后再执行构
        造函数中赋的初值*/
            
4.	局部变量未初始化，其内部是垃圾值，Java要求局部变量在
    使用前必须初始化
    
```



#### Static

```java
1.凡是Static修饰的成员都是静态成员
2.静态成员都是属于类的
	1>类的对象共用一个static属性或方法
    2>没有对象也可以通过类名的方式访问类
    	的内部static成员
  	  

3.
    非静态可以访问静态
    静态不可以访问非静态

4. 通过类名只能访问一个类中的非私有静态成员
   私有静态成员也不可以通过对象名访问

5.静态代码块 static{} 

```

#### this

```java
非静态方法默认都含有一个this指针
this代表正在调用本方法的对象

```

#### final

```java
修饰类
    该类不能被继承
修饰方法
    该方法可以被继承但不能被重写
修饰属性
    表示该属性能且只能赋值一次，并只能选两种中一种赋值
        1.定义的同时显式的初始化
        2.构造方法中初始化



```

#### 函数重载

```java
函数重载:【方法名可以相同】(注：与C语言不同)
//以下示例省略方法体

	1同名不同参
		参数的
			  1>个数不同
			  	test(int i)
			  	test(int i,int j)
			  	
			  2>数据类型不同
			  	test(String str ,int i)
			  	test(int k,int i)
			  	
			  3>在数据类型不同的前提下，顺序不同 
	  			test(String str ,int i)
	  			test(int i,String str )
	  			
	  			
	  			
	2返回值不能作为是否构成重载的依据
			 	void test(int i)
				int  test(int i)
				×错误，不构成函数重载



	3访问控制符也不能作为是否构成重载的依据
				protected void  test(int i)
				public    void  test(int i)
				×错误，不构成函数重载
```

### 2>继承

#### 定义

```java
extends
子类继承了父类成员


1.概念：
    特殊类的对象具有一般类的对象的属性和行为，
    称特殊类对一般类的继承【子类对父类的继承】

2.动物与狗：
    狗继承了动物的属性与行为，
    而不是动物继承了狗的特征。

3.子类：关注子类与父类不同的特征：
       子类根据需求增加自己的新的属性和行为
	   父类与子类是相对而言的
       构造方法不能被继承

4.继承的优点：
    1.可实现代码重复使用，设计应用程序变得简单

5.结构：
    class son extends father
    {
        /*单继承,即一下写法
        错误:
        class son extends father ,mon{}
        
        但可以使用接口弥补单继承的缺陷
        */
    }

6.所有的类默认继承Object类
    
    
    
 
```

#### 权限

| 访问说明符/不同情况      | public | protected | default | private |
| :----------------------- | :----- | :-------- | :------ | :------ |
| 同包同类                 | √     | √        | √      | √      |
| 访问同包不同类           | √     | √        | √      |         |
| 同包不同类继承           | √     | √        | √      |         |
| 不同包继承               | √     | √        |         |         |
| 访问不同包无任何关系的类 | √     |           |         |         |



#### 子类访问父类成员的三种方式

```java
1.在子类内部访问父类成员
2.通过子类对象名访问父类成员
3.通过子类类名访问父类成员
```

#### 内存

```java
私有”成员物理上已经被继承过来，
只不过逻辑上程序员不能去访问它,
因此继承必须谨慎，否则会造成内存浪费
```

#### 注意事项

```java
非私有成员才可以被子类继承
重写：
    重写方法必须和被重写方法具有相同的方法名、参数列表、返回值类型
    重写方法的访问权限不能小于被重写方法

```

##### java只支持单继承

### 3>多态

#### 定义

```java
1.定义：同一代码可以随上下文的不同而执行不同的操作，俗称多态
即：
    一个父类的引用它既可以指向父类对象也可以指向子类对象
    它可以根据当前时刻指向的不同，自动调用不同对象的方法
2.注意事项：
    通过父类的引用只能访问子类从父类继承的成员
    只有父类的引用本身指向一个子类对象时，
    我们才可以把父类的引用强制转化为子类的引用
```

#### 重写

```java
规则：
    1.子类与父类中方法的方法头相同【方法名、返回值、形参】
    2.重写中：子类方法的访问权限低于或等于父类
    		private 最高
    		public  最低
   
重写范围 
    1> final  修饰的方法不能被重写
    2> static 修饰的方法不能被重写，但可以重新声明  ☆此处有疑问？
    3>
    	同包  ：除 private 和 final 的方法
    	不同包：子类只能重写父类声明为 public protected 及 非 final 方法
    
    4>异常：
    

```

#### 代码

```java
package 笔记;


class A{
	
	void k() {
		System.out.println("父类方法被调用 ");
	}
	void f() {
		System.out.println("hello A");
		
	}
}

class B extends A{
	
	//f()
	public void f() {
		System.out.println("hello B");

	}
	
	void g() {
		System.out.println("这是g方法");

	}
	void k() {
		System.out.println("子类方法被调用 ");
	}
	//子类重写的范围大于父类
	
	
}

public class 重写 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

/*
		A a = new A();//父类的引用指向父类
		a.f();// "hello A"


		/*
		只有父类的引用本身指向子类才可以将其强制转换成子类的引用
		B b = (B)a; //error		
		 a = new B();//父类的引用指向子类
		 a.f();     //"hello B"
		 
		 
		 B b = (B)a;
		 
		 b.f();//"hello B"
		 
*/

		 A aa = new A();
		 B bb = new B();
		 
/*1.父类 ->子类->子类 	 转化过程
		 aa.f();//"hello A"
		 aa = bb;//子类直接给父类没问题
		 aa.f();//"hello B"
		 bb  =(B)aa;
		 bb.f();//"hello B"
		
		 
*/
		 
/*2.父类 ->子类 
		 aa.f();//"hello A"
		 aa = (A)bb;
		 aa.f();//"hello B"
		 
*/
		 
		 
/*3.子类->父类 
		// bb = aa;//error
	 
		 bb = (B)aa;//error

*/		 

		 
/*
/4.子类转成父类
  子类中的方法不是特有的，优先调用子类的
		 aa = bb;
		 
		 A a2 = (A)aa;
		 
		 a2.f();
*/		 
		 
/*
 指向子类的父类引用 -> 父类转 ：随意

指向子类的父类引用 -> 子类转   ：强转

子类->父类    ：随意
父类->子类    ×


*/
    

		 
/*		 a.g(); error 只能访问从父类继承的成员【成员属性和成员方法】
		 				子类特有成员不能被访问

*/

		
	}

}

```









### 4>相关知识



#### 抽象类

```java
1.抽象类 [可见度 abstract class A] 
       1>不可以实例化抽象类对象，但抽象类可以实现多态
       2>一个抽象类"通常"都含有抽象方法,也就是说抽象类中可以全是普通的方法
       3>只重写抽象类部分抽象方法的类也必须标记为 abstract
       4>有一个抽象方法就必须是抽象类
       4>抽象类可以有构造方法
    
    总结：除了无法实例化对象外，与普通类无异
       
 2.抽象方法  
   public  abstract int fangfa(int i);//注意：没有花括号

```

#### 接口

```java
1.格式：
        "现有：
            "类： MM , NN
            "接口 QQ, VV, KK, LL

        1>接口：
                //1.基本格式
                    [可见度] interface 接口名称
                    {
                         int a = 0;//等效与 public   static  final int a = 0;
                         void f(); //等效与 public   abstract void f();
                    }


                //2.接口只能继承接口,并且允许多继承
                interface A3 extends QQ,VV{  
                }

        2>类：
                //3.类可以继承类，实现接口
                class  A1 extends NN implements VV,QQ{
                /*
                 * 类：
                 * 1.只能继承一个类
                 * 2.接口可以多个
                 */

         3>总结："接口只能继承接口,并且允许多继承
                "类可以继承类,实现接口
```

```java
2.注意事项：
```



|          | 接口                       | 类                       |
| -------- | -------------------------- | ------------------------ |
| 继承接口 | √   [此处代表接口继承接口] | ×   [此处代表类继承接口] |
| 实现接口 | ×                          | √                        |
|          |                            |                          |
| 继承类   | ×                          | √                        |
| 实现类   | ×                          | ×                        |

```java
3."抽象类：
    1.抽象类同上表格
	{
    	并且：
    	1> "抽象类可实现接口
            并且可以不实现接口中的方法，但是继承
           抽象类的实体类必须实现接口中的方法。
       	2> "抽象类可以继承实体类
            但前提是实体类必须有明确的构造函数
            原因：抽象类有方法,也具备继承性
	}
```



```java
 4.定义：
    1.接口是抽象类型,也是抽象方法的集合，但不是类
    2.注意事项：
        "方法：
            1>接口没有构造方法
            2>接口中的所有方法必须是抽象方法,且必须是 public  
    			即：接口中方法都是 
                        "  public abstract " 
                        例如： public abstract void f();

    	    3>不可以定义接口对象，但接口可以实现多态
                    可以实例化一个继承了抽象类的子类，
                    然后将抽象类的引用指向子类的对象。
            
		    4>重写接口方法时, public 不能省
                	   /*【原因】
                        接口中方法默认是  public abstract 
                        子类在重写时父接口时，
                        由于子类方法访问权限不高于父接口方法，
                            {
                                即子类方法范围>=父接口方法范围
                                比如： public > 默认
                            }
                        父接口中方法范围已经是最大【 public 】
                        子类方法范围不能在小，即 public 不可省略*/


                
        "属性：
    		1>接口不能包含成员属性,除了 public static  final 变量
     			即：接口中属性都是 
                        " public static final " 
                        例如: public static final int a = 0 ;

                        /*【原因】
                        接口中属性默认是  public static final 
                        由final修饰的属性只能赋一次值，
                        且只能是在定义时显示赋值
                        或构造方法赋值，又由于接口中没有构造方法，所以
                        只能在定义时显示赋值*/


 5.接口支持多重继承
    	书写时：先继承在实现["顺序不能错"]
    	 [可见度] class 类名 extends MM implements KK,LL{
		 }
    
   
 6.举例：
        线程创建
        GUI事件处理
        容器的组织方式
        serializable接口



```

## **高级部分**

### 1>异常

#### 什么是异常

```java
异常(Exception)是程序运行过程中发生的事件，该事件可以中断程序指
令的正常执行流程。
```

#### 为什么需要异常

```java
某些程序出现的问题是无法涌讨逻辑判断【if、else if等】来解决
的，Java提供的异常处理机制可以很好的解决这个问题

例如：编程实现把键输入的数字赋给整型变量
Scanner sc = null;
try{
    sc = new Scanner(System.in);
    int i = sc.nextint();
    System.out.printf("%d\n", i);
catch (InputMismatchException e){
	System.out.printIn("读取错误，程将终止");
}


```



#### 异常的处理机制

```java
异常的处理机制(重点)
    1. 当Java程序运行时出现问题时，系统会自动检测到该错误
       并立即生成一个与该错误对应的异常对象
    2. 然后把该异常对象提交给Java虚拟机
    3. Java虚拟机会自动寻找相应的处理代码来处理这个异常，
       如果没有找到，则程序终止!
    4. 程序员可以自己编写代码来捕捉可能出现的异常，并编写代
       码来处理相应的异常
```

#### 常见的异常

```java
1. NullPointerException: 空指针异常
2.ClassCastException: 类型强制转换异常
3.ArrayIndexOutOfBoundsException: 数组下标越界异常
4.ArithmeticException:算术运算异常
5.NumberFormatException: 数字格式异常
```

#### 异常的分类

##### Throwable

```java
异常的分类
1.Error:
        由Java虚拟机生成并抛出，包括动态链接失败、虚拟机错误等，Java
        程序无法对此错误进行处理。

2.Exception:
        一般程序中可预知的问题，其产生的异常可能会带来意想不到的结果
        因此"Java编译器要求Java程序必须捕获或声明所有的非运行时异常"
            
3.RuntimeException:	【继承自Exception】
        Java虚拟机在运行时生成的异常，如被0除等系统错误、数组下标超
        范围等，/*其产生比较频繁，处理麻烦，对程序可读性和运行效率影响
        太大*/。因此由系统检测，"用户可不做处理"，系统将它们交给缺省的异
        常处理程序(当然，必要时，用户可对其处理)。
    
```



```java
4.处理
        error是系统的错误，程序员无法处理这些异常
        Exception是程序员可以捕获并处理的异常。
        RuntimeException的子类异常，是可以处理也可以不处理的异常//注解①
        凡是继承自Exception但又不是RuntimeException子类的异常必须捕捉并处理
    
//注解①
 异常分为运行时异常(RuntimeException)、受检异常(Exception)、系统错误error。

RuntimeException，也就是运行时异常，表示代码本身存在BUG，比如ArrayIndexOutOfBoundsException，数组下标越界，数组定义的长度不够实际使用，代码若不调BUG进行处理肯定还会报错，控制台一旦报RuntimeException，就必须在代码中找BUG，因为代码BUG是人为粗心制造的，不是try-catch一下就能解决的。try-catch用在代码BUG上是毫无意义的，只需要写代码时谨慎点就能减少BUG，而不是try-catch。
    
非RuntimeException，就是受检异常。比如处理文件流时的I/O问题，就属于编译时异常，相当于假设有IO异常就利用try-catch对其进行处理，或者 throws即可。
error，通常是系统出现了不可控制的错误，这个通常与程序无关，所以是不需要处理的。

下面给出运行时异常与受检异常的清晰定义：

①受检查异常表示程序可以处理的异常，如果抛出异常的方法本身不能处理它，那么方法调用者应该去处理它，从而使程序恢复运行，不至于终止程序。例如，喷墨打印机在打印文件时，如果纸用完或者墨水用完，就会暂停打印，等待用户添加打印纸或更换墨盒，如果用户添加了打印纸或更换了墨盒，就能继续打印。

②运行时异常表示无法让程序恢复运行的异常，导致这种异常的原因通常是由于执行了错误操作。一旦出现了错误操作，建议终止程序并仔细的debug，因此Java编译器不检查这种异常。
   
```

#### 异常的处理步骤

##### 异常的处理步骤

```java
try 
{
    可能出现异常的代码快
}
catch(ExceptioName1 e)
{
    当产生ExceptionName1 异常时的处理措施
}
catch(ExceptioName2 e)
{
    当产生ExceptionName2 异常时的处理措施
}
......
finally
{
    无论是否捕捉到异常都必须处理的代码
}

```

##### 捕提处理异常注意问题

```java
try {
    语句1;
    语句2;
}catch(){}
catch(){}
finally(){}

1.若语句1抛出异常，语句2永远不会执行
2.无论try中代码是否抛出异常，finally中代码都会得到执行

/*
经典题
+---------------------------------------+
1>
try {
	return ;}
finally{
	System.out.println("1");}
运行结果：1
+---------------------------------------+
2>
int a = 1,b=2;
try {
	 a = 3/0;
	 b = 3;
	
}catch(Exception e) {
	System.out.println("1");
}
finally{
	System.out.printf("%d\n",b);
}
运行结果：
1
2
*/
+---------------------------------------+
```



##### Finally

```java
    1. 无论try所指定的程序块中是否抛出异常，也无论catch语句的异常类型是否与所抛弃的异常的类型一致，
       finally中的代码一定会得到执行
    2. finally语句为异常处理提供一个统一的出口，使得在控制流程转到程序的其他部分以前，能够对程序的
       状态作统一的管理
    3. 通常在finally语句中可以进行资源的清除工作。如关闭打开的文件，删除临时文件
```

##### throw

```java
1.throw用来抛出异常
2.格式：
    throw new 异常名(参数)；//从本质上来说这是 new出一个类对象，以及调用构造函数
3.假设f方法抛出了A异常，则f方法有两种方式来处理A异常
    1>throws A
        谁调用f方法，谁处理A异常，f方法本身不处理A异常
    2>try{···}catch{···}
        f方法本身自己来处理A异常
4.要抛出的异常，必须是Throwable的子类
  

```

##### throws

```java
1.格式：
void f() throws A
{
    ······
    ······
}

2.thows A表示调用f方法时f方法可能会抛出A类异常，建议您调用f方法时
最好对f方法可能抛出的A类异常进行捕捉
3.throws A不表示f方法一定会抛出A类异常
4.throws A，f方法也可以不抛出A类异常
5.throws A不表示调用f方法时，必须的对A异常进行捕捉
    1> 假设A是RuntimeException子类异常
    2> 由于RuntimeException的子类异常可以处理也可以不处理，所以编译器允
       许你调用f方法时，对f方法抛出的RuntimeException子类异常不进行处理

 6.强烈建议:
 1.对 thorws出的所有异常进行处理
 2.如果一个方法内部已经对A异常进行了处理，就不要再throws A
```



##### 异常的两种处理方法

#### 自定义异常

```java
package com.ghy.a3;
//import java.io.*;

//自定义异常，异常必须继承自Exception
class SuanException extends  Exception
{
	public SuanException(String str)
	{
		super(str);
	}
	
}

class Y
{
	int f(int a,int b)throws SuanException
	{
		int m =0;
		if(b==0)
		{
			System.out.printf("qqqqqqqqqq\n");//可执行
			throw new SuanException("\n\n算数异常O(∩_∩)O!\n");//本质上这是new出一个类对象，以及调用构造函数
			//System.out.printf("qqqqqqqqqq\n");//执行不到的代码
		}
		else
			m = a/b;
	
		return m;
		
	}
}

public class 自定义异常 {

	public static void main(String[] args)//throws SuanException  
	{
		// TODO Auto-generated method stub
		Y yy = new Y();
		try
		{
			yy.f(7, 0);
		}
		catch(Exception a) 
		{
			a.printStackTrace();
		}
	}

}

```

#### 异常的优缺点

```java
优点：
    1. 强制程序员考虑程序的安全性与健壮性
    2. 增强了程序员对程序的可控性(处理完错误程序可以继续运行)
    3. 有利于代码的调试
    4. 把错误处理代码从常规代码中分离出来

缺点:
    1. 异常并不一定能够使程序的逻辑更清晰
        因为有时我们必须得编写代码捕捉异常，所以可能会导致程序的逻辑非常混乱

    2. 异常并不能解决所有的问题

```

#### 异常的注意事项

```java
1. 异常的范围
    子类覆盖了基类方法时，
        子类方法抛出异常的范围不能大于基类方法抛出的异常范围
        子类方法可以不抛出异常，也可以只抛出基类方法的部分异常
        但不可以抛出基类方法以外的异常
2. 先catch子类异常再catch父类异常
	如果先catch父类异常再catch子类异常，则编译时会报错
3. 所有的catch只能有一个被执行
4. 有可能所有的catch都没有执行
5. catch与catch之间不能有其他代码
```

### 2>线程
#### 程序
```java 
1.程序： 
    是一个严格有序的指令集合。程序规定了完成某一任务时，计算机所需做的各种操作，以及这些操作的执行。

2.单道程序设计环境：
    1>计算机中除了操作系统之外，只存在一个用户程序，即用户程序独占整个计算机资源。
    2>特点：
        资源的独占性
        执行的顺序性
        结果的再现性
3.多道程序设计环境：
    1>计算机中除了操作系统之外，存在多个用户程序，这些程序同时运行
    2>特点：
        间断性：由于资源共享合作，并发程序相互制约，造成合作执行间断
        失去封闭性：程序首外界影响
        结果不可再现性
```

#### 线程的概念
##### 进程
```java
1. 进程的由来
     为了不破坏“程序”这个词原有的含义，而又能刻画多个程序共同
     运行是呈现出的新特征，所以引入了进程的概念
2.进程：
    是一个动态的实体，是程序在某个数据集上的执行。它有自己的生命体，
    它因创建而产生，因调度而运行，因等待资源或事件而被处于等待状态，因
    完成任务而被撤销
3.举例：
    一个记事本程序同时打开三个文本，则产生了三个进程
4.我的理解：
    由于程序与程序运行之间不再是一一对应的关系，需要创造一个新的词语来描述他们之间的关系，这就是进程
5.进程的缺点：
    浪费时间与资源，因此创建了线程
```
##### 线程
```java
1.定义：
    一个程序运行时的不同执行路径
2.多线程的优势
    1>多线程编程简单，效率高 (能直接共享数据和资源,多进程不能)
    2>适合于开发服务程序 如 (Web服务，聊天服务等)；
```

#### 如何创建一个线程
##### 方法一：继承Thread
```java
1.步骤：
    1>创建一个继承Thread的类(假定类名为A)，并重写Thread中的run方法
    2>构建一个A类对象，假定对象名为aa
    3>调用aa的start方法
2.注意问题：
    1> Thread中start()方法的功能就是创建一个新的线程，并自动
      调用该线程的 run()方法，直接调用 run()方法是不会创建一个
      新的线程的
 
    2>执行一个线程实际就是执行该线程run方法中的代码
     执行完aa.start()；后并不表示aa所对应的线程就一定会立即得
     到了执行，aa.start()；执行完后只是表示aa线程具有了可以
     立即被CPU执行的资格，但由于想抢占CPU执行的线程很多
     CPU并不一定会立即去执行aa所对应的线程
     参见TestThreadStart.java

    3>一个Thread对象能且只能代表一个线程，
     一个 Thread对象不能调用两次 start()方法，否则会抛出
     java.lang.lllegalThreadStateException异常
     参见TestThreadStart2.java
3.代码：
一种方法是将类声明为 Thread 的子类。该子类应重写 Thread 类的 run 方法。接下来可以分配并启动该子类的实例
class A extends Thread
{
	public void run()
	{
		while (true)
		{
			System.out.println("AAAA");
		}			
	}
	
}

public class TestThread_1
{
	public static void main(String[] args)
	{
		A aa = new A();
		aa.start(); //aa.start(); 会自动调用run方法
		while (true)
		{
			System.out.println("BBBB");
		}
	}
}

```
<img src="F:\仓库\思维导图\图片\线程状态切换.jpg" style="zoom: 40%;" />

##### 方法二：实现了Runnable接口
```java
1.步骤：
    1>定义一个实现了Runnable接口的类，假定为A
    2>创建A类对象aa,代码如下
         A aa=newA();
    3>利用aa构造一个Thread对象t,
        Thread tt = new Thread(aa);
    4>调用t中 的start方法
         tt.start(); 

2.代码：
一种方法是声明实现 Runnable 接口的类。该类然后实现 run 方法。然后可以分配该类的实例，在创建 Thread 时
作为一个参数来传递并启动。
        class A implements Runnable
        {
            public void run()
            {
                while (true)
                {
                    System.out.println("AAAA\n");
                }
            }
        }



        public class TestThread_2
        {
            public static void main(String[] args)
            {
                A aa = new A();
                //aa.start();  //error
                Thread t = new Thread(aa); ////public Thread(Runnbale r) 

                t.start();
                
                while (true)
                {
                    System.out.println("BBBB\n");
                }
            }
        }


```
#####
```java
class TT extends Thread
{
	public void run()
	{
		while (true)
		
			System.out.println("继承Thread类的线程执行！！\n");
			
	}
	
}


class Ra implements Runnable
{
        public void run()
        {
        	while(true)
                System.out.println("实现Runnable接口的线程执行！！\n");
        
    }
}


public class Punnable_2 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

			TT th1 = new TT ();
			th1.setPriority(TT.NORM_PRIORITY+5);
		
			Ra ra = new Ra();
			Thread th = new Thread (ra);
			
			System.out.printf("th1 :%s\n",th1.getPriority());
			System.out.printf("th :%s \n",th.getPriority());
			
			th1.start();
			th.start();
			
			
			
	}

}


```
##### 推测Thread 内部代码
```java 
public interface Runnable
{
    public void run()
    {
        如果该线程是使用独立的 Runnable 运行对象构造的，则调用该 Runnable 对象的 run 方法；否			
         则，该方法不执行任何操作并返回。
    }

}

public class Thread extends Object implements Runnable
{
    Runnable target = null;
    public Thread{
    	}
    public Thread(Runnable target){
       this.target = target;
    }
	void start() {
          使该线程开始执行；Java 虚拟机调用该线程的 run 方法} 
	 public void run() {
        if (target != null) 
            target.run();
        }
}

--------------------------------------------------------------------------------------------------------------

API：
Runnable 接口应该由那些打算通过某一线程执行其实例的类来实现。类必须定义一个称为 run 的无参数方法。 

设计该接口的目的是为希望在活动时执行代码的对象提供一个公共协议。例如，Thread 类实现了 Runnable。激活的意思是说某个线程已启动并且尚未停止。 

此外，Runnable 为非 Thread 子类的类提供了一种激活方式。通过实例化某个 Thread 实例并将自身作为运行目标，就可以运行实现 Runnable 的类而无需创建 Thread 的子类。大多数情况下，如果只想重写 run() 方法，而不重写其他 Thread 方法，那么应使用 Runnable 接口。这很重要，因为除非程序员打算修改或增强类的基本行为，否则不应为该类创建子类。

CSDN：
不论是继承Tread类创建线程还是实现Runnable接口创建线程，启动线程一般都是调用Thread类的start()方法，然后由虚拟机自动调用Thread类的run()方法
综合上述五种情况分析：
1.如果没有继承Thread类只是创建普通Thread类对象，则线程什么都不做
2.如果继承了Thread类：
    a.如果重写了run()方法：则JVM调用该方法
    b.如果没有重写run()方法:则JVM调用JDK自己定义的run()方法
         I.如果指定了target，则调用target的run()方法
         II.如果没有指定target，则什么都不做。

```
##### Thread 的常用方法
```java
1.格式：
    public final void setName(String name)设置当前线程的名字
    public static Thread currentThread()返回对当前正在执行的线程对象的引用
    public final String  getName();返回当前线程的名字

2.使用：
    Thread.setName(String name)
		设置当前线程的名字
	Thread.currentThread()
		返回当前线程的引用
	Thread.getName()
		返回当前线程的名字
3.代码：

class A extends Thread
{
	public void run()
	{
		//System.out.println("AAAA");
		System.out.printf("%s在执行!\n", Thread.currentThread().getName());
	}                       //currentThread()方法是静态的，此处使用类名.方法调用
}

public class TestThread_3
{
	public static void main(String[] args)
	{
		A aa1 = new A();
		aa1.setName("张三");
		aa1.start();
		
		A aa2 = new A();
		aa2.start();
		
		A aa3 = new A();
		aa3.setName("李四");
		aa3.start();
		
		//System.out.println("BBBB");
		System.out.printf("%s在执行!\n", Thread.currentThread().getName());
	}
}

```


#### 线程的控制 
##### 线程控制的基本方法

| 方法                    | 功能                                                         |
| ----------------------- | :----------------------------------------------------------- |
| isAlive ( )              | 判断线程是否还"活"着，即线程是否还未终止                     |
| getPriority( )           | 获得线程的优先级数值                                         |
| setPriority( )           | 设置线程的优先级数值                                         |
| Thread.sleep ( )        | 将当前线程睡眠指定亳秒数                                     |
| join ( )                 | 调用某线程的该方法，将当前线程与该线程“合并，即等待该线程结束，再恢复当前线程的运行。 |
| yield( )                 | 让出CPU,当前线程进入就绪队列等待调度。                       |
| wait ( )                 | 当前线程进入对象的wait pool.                     |
| notify( ) / notifyAll () | 唤醒对象的wait poo1中的一一个/所有等待线程                   |



##### 优先级控制

```java
1.  Java提供一个线程调度器来监控程序中启动后进入就绪状态的所有线程。
    线程调度器按照线程的优先级决定应调度哪个线程来执行。

2.  线程的优先级用 数字表示，范围从1到10, 一个线程的缺省优先级是5。
        1>Thread.MIN PRIORITY=1
        2>Thread.MAX_ PRIORITY= 10
        3>Thread.NORM PRIORITY= 5

3.  使用下述线方法获得或设置线程对象的优先级。
        1>int getPriority();
        2>void setPriority(int newPriority);

4.主线程的缺省优先级是5，子线程的优先级默认与其父线程相同

5. 通常高优先级的线程将先于优先级低的线程执行，但并不
   总是这样，因此实际开发中并不单纯依赖优先级来决定线
   程运行次序  

6.代码：TestPriority.java
            Thread t1 = new Thread(new T1());
            Thread t2 = new Thread(new T2());
            t1.setPriority(Thread.NORM_PRIORITY + 3); 
            t1.start();
            t2.start();
            t1 优先级比 t2 高，执行完t1再执行t2 //考虑把本语句注释掉后会怎样
/*
详见源码
t1 与t2 交替执行；
*/
```
[时间片轮转](http://c.biancheng.net/view/1247.html)

##### 线程的休眠、让步、挂起和恢复
###### 休眠
```java
1.  线程休眠:暂停执行当前运行中的线程，使之进入阻塞状
    态，待经过指定的“延迟时间”后再醒来并转入到就绪状态。

2.  Thread类提供的相关方法:
        1> public static void sleep(long millis)
        2> public static void sleep(long millis, int nanos)

3.  由于是静态方法，可以由Thread直接调用

4. sleep()方法会抛出InterruptedException异常，我们必须得
        对其进行捕捉
        try{
	 	     Thread.sleep(1000); //这里的Thread.sleep(1000)会抛出异常,必须
                                      //的进行捕捉，不能在9 的后面添加 throws Exception
		}catch (Exception e){  }
	    

5. 注意问题：
        "无论是继承Thread类的run方法还是实现 Runnable接口的run方法，都不能抛出任何异常"
        原因：重写方法抛出异常的范围不能大于被重写方法排除的异常范围 【TestSleep2. java】


	
```
###### 让步
```java
1.  让出CPU，给其他线程执行的机会

2.  让运行中的线程主动放弃当前获得的CPU处理机会，但不是
    使该线程阻塞，而是使之转入就绪状态。
        public static void yield()   【TestYield.java】


```
###### 挂起和恢复
```java
1.  线程挂起:暂时停止当前运行中的线程，使之转入阻塞状态，并且不会
    自动恢复运行。
2.  线程恢复:使得一个已挂起的线程恢复运行

3.  Thread类提供的相关方法:
        1> final void suspend()
        2> public final void resume()
        3> suspend()方法挂起线程时并不释放其锁定的资源。这可能会影响其他线
           程的运行，且容易导致线程的死锁，已不提倡使用
```
##### 线程的串行化
```java
1. 在多线程程序中，如果在一个线程运行的过程中要用到另一
   个线程的运行结果，则可进行线程的串型化处理。

2. public final void join() throws InterruptedException 【TestJoin.java】

3.代码：
public class TestJoin {	
	public static void main(String args[]){
		MyRunner r = new MyRunner();
		Thread t = new Thread(r);
		t.start();
		try{
			t.join(); //7行
            /**暂停当前正在执行t.join();的线程
            [主线程：这里这样说是为了方便理解，但默认主线程与子线程的缺省相同]
           		直到t所对应的线程运行终止之后，当前线程才会获得继续执行的机会*/
		}catch(InterruptedException e){
			e.printStackTrace();
		}
		for(int i=0;i<50;i++){
			System.out.println("主线程:" + i);
		}
    }
}

class MyRunner implements Runnable {
	public void run() {
		for(int i=0;i<50;i++) {
			System.out.println("子线程: " + i);
		}
	}
}

```
##### 线程的生命期控制
```java
如何结束一个线程
注意：此方法不一定可以起作用
public class TestShutThread
{
	public static void main(String[] args)
	{
		A aa = new A();
		Thread tt = new Thread(aa);
		tt.start();
		
		try
		{
			Thread.sleep(5000);
		}
		catch (Exception e)
		{
			e.printStackTrace();
		}		
		
		aa.shutDown();
	}	
}

class A implements Runnable
{
	private boolean flag = true;
	
	public void run()
	{
		while (flag)
		{
			System.out.println("AAAA");
			  
		}
	}
	
	public void shutDown()
	{
		this.flag = false;
	}
}
```




#### 线程同步
##### 线程同步知识点
###### 同步概念
```java
1.定义：
	通常，一些同时运行的线程需要共享数据。在这种时
	候，每个线程就必须要考虑与其他-起共享数据的线程的
	状态与行为，否则的话就不能保证共享数据的一-致性，从
	而也就不能保证程序的正确性

2.不同步带来的问题：
	当有两个线程A和B同时使用了Stack类的-一个对象时，现在我要求:先把r存
	入Stack中，再将r取出来
	下面的步骤详细演示了AB线程不同步所带来的问题
		1>操作之前，堆栈中有两个字符:
			data=|a |c |  |  |  |  index= 2
		2>A执行push中的第一条 语句data[index]='r':
			data=|a |c |r |  |  | 	index= 2		//2还没有被存入

		3> A还没有执行index++语句，A被B中断，B执行pop()方法, 返回'c':
			data=|a |c |r |  |  |	index = 1	//取出的是'C'却不是‘r'
	
		4>A继续执行index++语句:
			data=|a |c |r |  |  |		index = 2
			最终结果是: 'r'没有被存入，取出的是'C'而不是'r


```
###### Synchronized关键字
```java 
1.synchronized可以用来修饰.
    一个方法
    一个方法内部的某个代码块

2.Synchronized修饰方法
    1>  Synchronized修饰一个方法时，实际霸占的是该方法的this
        指针所指向的对象,即Synchronized修饰一个方法时，实际
        霸占的正在调用该方法的对象
    2>附注:
        霸占的专业术语叫锁定，霸占住的那个对象专业术语叫做监听器



3.Synchronized修饰代码块
    1>格式:
            synchronized(类对象名aa) I/1行
                {
                同步代码块//3行
                } //4行

    2>功能:
        synchronized(类对 象名aa)的含义是:判断aa是否已经被其他线程
        霸占，如果发现已经被其他线程霸占，则当前线程陷入等待中，如果
        发现aa没有被其他线程霸占，则当前线程霸占住aa对象，并执行3行
        的同步代码块，在当前线程执行3行代码时，其他线程将无法再执行3
        行的代码(因为当前线程已经霸占了aa对象),当前线程执行完3行的代
        码后，会自动释放对aa对象的霸占，此时其他线程会相互竞争对aa的
        霸占，最终CPU会选择其中的某一个线程执行

    3> 最终导致的结果是:
        一个线程正在操作某资源的时候，将不允许其它线程操作该资源，即一次
        只允许一个线程处理该资源
```
###### notify 和 wait
```java
1.格式：
	this.notify();
2.功能:
	1> 不是叫醒正在执行this.notify();的当前线程
	2> 而是叫醒一个现在正在wait this对象的其他线程，如果有多个线程正
	   在wait this对象，
	3> 通常是叫醒最先wait this对象的线程,但具体是叫醒哪一个这是由系统调
	   度器控制，程序员无法控制
3.分析：
	假设现在有T1、T2、T3、T4 四个线程
	我们在T4线程中执行了aa.notify()语句
	则即便此时 T1 T2 T3 没有 一个线程因为wait aa对象而陷入阻
	塞状态，T4线程中执行aa.notify方法时也不会有任何错误
	本程序就证明了这一点
	执行aa.notify方法时如果一个线程都没有叫醒，这是可以的
									【TestNotify.java】
									【SyncTest.java  】
4.总结：
	1>aa.wait()
		将执行aa. wait()的当前线程转入阻塞状态，让出CPU的控制权
		释放对aa的锁定
	2>aa.notify()
		假设执行aa. notify()的当前线程为T1
		如果当前时刻有其他线程因为执行了aa.wait()而陷入阻塞状态，则叫醒其中的一个，
		所谓叫醒某个线程就是令该线程从因为wai而陷入阻塞的状态转入就绪状态
	3>a.notifyAll()
		叫醒其他所有的因为执行了aa.wait()而陷入阻塞状态的线程


5.代码：
public class SyncStack
{
	private int index = 0;
	private char []data = new char[6];
	public synchronized void push(char c)
	{
		while(index == data.length)
		{
			try{
				this. wait(); //7行
				}
			catch(InterruptedException e){}
		}
			this.notify(); //10行
			data[index]=c;
			index++;
			System.out.println("produced: "+c);
	}
}

public synchronized char pop()
{
	while(index ==0)
	{
		try{
			this. wait();
			}
		catch(Exception e){}
	}
	this.notify(); //20行
	index--;
	System.out.println("消费: "+data[index]);
	return data[index]; //23行
}
/*
1.要注意的问题
	1>执行完20行的代码后，程序绝对不会立即切换到另一个线程
	2>0行代码叫醒的是其他线程，叫醒的不是本线程
	3>在最开始，P和C刚开始执行时，即便P没有wait,也可以在C中
	notify,即便C没有wait,也可以在P中notify

 2.解释说明：
	假设现在有两个线程P(生产)和C(消费)，
	P生产已满，执行7行代码陷入阻塞状态，同时释放P
	线程对this的锁定，这时候C线程会得到this对象的标
	志位开始运行。另外C线程执行完20行代码后，程序并
	不会立即转到P线程开始运行，因为C执行notify,只是
	叫醒P，让P从因为wait this对象而陷入阻塞的状态进
	入就绪状态，
	记住:一个线程notify,该线程并不会释放对this的锁
	定，只有C执行完23行的代码后，C才会释放对this的
	锁定，这时候C和P会同时争夺对this的锁定，具体执
	行哪个由系统调度器决定
*/


```
##### 线程同步案例
###### 买票
```java

1.买票程序
    if (票数>0)
    {
        买一张票；
        票数减一；
    }

2> "继承Thread" 方法买票
class A extends Thread
{
	public static int tickets = 1000;  //static不能省
	public static String str = new String("哈哈");  //static不能省
		
	public void run()
	{
		while (true)
		{
			synchronized (str)
			{
				if (tickets > 0)
				{
					System.out.printf("%s线程正在卖出第%d张票\n",
						Thread.currentThread().getName(), tickets);
					--tickets;	
				}
				else
				{
					break;
				}
			}
		}
	}
}

public class Q21
{
	public static void main(String[] args)
	{
		A aa1 = new A();
		aa1.start();	
			
		A aa2 = new A();
		aa2.start();		
	}
}

3> "实现Runnable接口"方法买票
class A implements Runnable
{
	public int tickets = 1000;//计算机运行较快，次数多，结果明显
	String str = new String("哈哈");
		
	public void run()  
	{
		String str = "哈哈";  
		
		while (true)
		{
			synchronized (str)  
			{
				if (tickets > 0)
				{
					System.out.printf("%s线程正在卖出第%d张票\n",
						Thread.currentThread().getName(), tickets);
					--tickets;	
				}
				else
				{
					break;
				}
			}
		}		
	}
}

public class TestTickets_9
{
	public static void main(String[] args)
	{
		A aa = new A();
		Thread t1 = new Thread(aa);
		t1.start();	
		
		Thread t2 = new Thread(aa);
		t2.start();	
			
	}
}

```
###### 生产和消费问题
```java
生产消费[经典问题]
一个仓库最多容纳25个产品，制造商现在要制造50件产品存入
仓库，消费者要从仓库取出这50件产品来消费

制造商制造产品和消费者取出产品的速度很可能是不一样的
编程实现两者的同步  【ProducerConsumer.java】


package com.ghy.a2;
//仓库
class Warehouse
{
	private char house [] = new char [25];
	private int cnt = 0;
	
	//生产
	public synchronized  void push(char ch)
	{
		if(cnt==house.length) 
		{
			try
			{
				this.wait();
			}
			catch (Exception e)
			{
			}
			
		}
		this.notify();//叫醒消费线，可以消费了
		house [cnt] = ch;
		System.out.printf("生产第%d个商品%c\n",cnt+1,ch);
		cnt++;
	}

	//消费
	public synchronized  void pop()
	{
		if(cnt==0)
		{
			try
			{
				this.wait();
			}
			catch (Exception e)
			{
			}
		}
		this.notify();//叫醒生产线，可以生产了
		System.out.printf("消费第%d个商品%c\n",cnt,house [cnt-1]);
		cnt--;
	}
	
}

//生产
class Production implements Runnable
{
	Warehouse w = null;
	Production (Warehouse w){this.w = w;}//指向同一个仓库
	
	public void run()
	{	int i;
		char ch = 'a';
		for(i=0;i<50;++i)
		{
			ch = (char)('a'+i);
			w.push(ch);
		}
	}

}

//消费
class Consumption implements Runnable
{
	Warehouse w = null;
	Consumption (Warehouse w){this.w = w;}
	
	public void run()
	{
		 int i;
		 for(i=0;i<50;++i)
		 {
				// try{
					// Thread.sleep(100);
					//}
				//catch (Exception e){}	
				 w.pop();
		 }
		
	}
	
}


public class 生产与消费 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		Warehouse   ww = new Warehouse();
		Production  pr = new Production (ww);
		Consumption co = new Consumption(ww);
		
		Thread p = new Thread (pr);
		Thread c = new Thread (co);
		p.setName("生产线 ");
		c.setName("消费线");
		p.start();
		c.start();
		
	}

}

```







### 3>常用类和常用方法

#### Math

```java

java.lang.Math类提供了常用的数学运算方法
      和两个静态常量E(自然对数的底数) 和PI(圆周率)


double d = Math.random()//生成[0.0-1.0)之间的随机数
double d2 =  Math.random()*10;//生成[0-10)之间的随机数,不含10
int random = (int)(Math.random()*10);//0-9之间的整数随机数
Math.random()*10 + 1;//


```



#### Random

```java
1>【步骤：】
    import java.util.Random;
    Random random = new Random();
    random.next...();
    /*例如：random.nextInt();
                生成随机数的范围：int范围
                */
    random.next...(Type);
    /*例如：random.nextInt(10);
                生成随机数的范围：0-10
          */

2>随机数种子
        Random random = new Random(种子);//可以是无参的
    注意：对于相同的种子,生成的随机数是相同的且是固定的
        对于不同的种子,生成的随机数是不同的,
    如果是无参的构造方法,即没有“显式”的种子,
    但“隐式”的种子是存在的,且对于每一次使用构造方法,
    几乎每一次的种子都不一样


3>常用的尽量保证随机数不同的方法
    1.无参
    2.将当前的毫秒做种子


```



#### Date

```java
/*

帮助文档：
getTime:
public long getTime()

返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。
返回：自 1970 年 1 月 1 日 00:00:00 GMT 以来此日期表示的毫秒数。
 */

		package Test;
		import java.util.*;
		public class TestDate {

			public static void main(String[] args) {
				// TODO Auto-generated method stub

				//1.创建第一个Date对象
				Date date0  = new Date ();
				double timeOne = date0.getTime()/1000.0;//改成秒数

				//System.out.printf("%.0f\n",timeOne);

				//2.时间间隔
				Scanner sc = new Scanner(System.in);
				String str = sc.nextLine();

				//3.创建第二个Date对象

				Date date1  = new Date ();
				double timeSecond = date1.getTime()/1000.0;//改成秒数
				//System.out.printf("%.0f\n",timeSecond);

				System.out.printf("%.0f\n",timeSecond-timeOne);//计算时间差

			}

		}
```


#### ResourceBundle
```java
 private static ResourceBundle bundle = ResourceBundle.getBundle("resources/jdbc");
    private static String driver = bundle.getString("driver");
    private static String url = bundle.getString("url");
    private static String user = bundle.getString("user");
    private static String password = bundle.getString("password");
```







### 4>GUI

#### 组件与容器
```java
1.	组件(Component)是图形用户界面的基本组成元素，凡是能
	够以图形化方式显示在屏幕上并能够与用户进行交互的对象
	均为组件，如菜单、按钮、标签、文本框、滚动条等。
2.组件分类   
		1>java.awt.Component 
		2>Java.awt.MenuComponent
		3>说明:抽象类java.awt.Component是除菜单相关组件之外所有Java
		  AWT组件类的根父类，该类规定了GUI组件的基本特性，如尺寸、位
		  置和颜色效果等，并实现了作为一个GUl部件所应具备的基本功能
3.容器:
		1>组件通常不能独立地显示出来，必须将组件放在一定的容器中才可以显示出来。
		2>有一类特殊的组件是专门用来包含其他组件的，这类组件叫做容器，
			java.awt.Container是 所有容器的父类,java.awt.Container
			继承自 java.awt.Component  
		3>容器类对象本身也是一个组件，具有组件的所有性质，但反
		  过来组件却不一定是容器

4.Frame常用的方法  


		1>public void setBounds(int x,int y,int width, int height)
			设置窗体的位置和大小，x和y表示窗体左上角距离屏幕的水平和垂直
			距离，with和height是 窗体本身的宽度和高度
		2>public void setSize(int width, int height)
			设置窗体的大小，with和height是窗体本身的宽度和高度
		3>public void setVisible(boolean flag);
			设置窗体是否可见，true表示可见，false表示不可见
		4>public void setBackground(Color c)
			设置窗体的背景色
									TestFrame_ 1.java
									TestFrame_ 2.java
									TestFrame_ 3.java

									

5.Panel
		1>panel是容纳其他组件的组件
		2>panel是容器
		3>panel不能单独存在，必须得被添加到其他容器中
			Panel类拥有从其父类继承来的
				setBounds(int x,int y,int width,int height)
				setSize(int width, int height)
				setLocation(int x,int y)
				setBackground(Color c)
				setLayout(LayoutManager mgr)等方法。
				Panel的构造方法为:
				Panel()使用默认的FlowLayout类布局管理器初始化
				Panel(LayoutManager layout)使用指定的布局管理器初始化
										【TestPanel 1.java】

6.注意：
		Frame f = new Frame("标题！"); 
		Panel p = new Panel ();
		//f与p都是容器，但f可单独显示出来，p不行
```
<img src="F:\仓库\思维导图\图片\容器分布图.jpg" style="zoom: 40%;" />

#### 布局管理器

##### 概念
```java
1.	容器对其中所包含组件的排列方式，包括组件的位置和大小.
	设定，被称为容器的布局(Layout)

2.	为了使图形用户界面具有良好的平台无关性，Java语言提供
	了布局管理器来管理容器的布局，而不建议直接设置组件在
	容器中的位置和尺寸

3.	每个容器都有一个默认的布局管理器，当容器需要对某个组
	件进行定位或判断其大小尺寸时，就会自动调用其对应的布
	局管理器

4.	在AWT中，常见的布局管理器:
	1> GridLayout	 BorderLayout	FlowLayout
        [网格布局]    [边界布局]       [流式布局]
	2> Frame 默认的布局管理器： BorderLayout (记忆：FBL )
	3> Panel 默认的布局管理器:	FlowLayout
```
##### FlowLayout布局管理器
```java
1. FlowLayout 是Panel类的默认布局管理器。
	1>FlowLayout布局管器对组件逐行定位，行内从左到右，一行排满后换行
	2>不改变组件的大小， 按组件原有尺寸显示组件，可设置不同的组件间距，
	  行距以及对齐方式

2.FlowLayout 布局管理器默认的对齐方式是居中。


3. 
	1>	new FlowLayout(FlowLayout.RIGHT,20,40);
			右对齐， 组件之间水平间距20个像素，垂直间距40个像素
	2>	new FlowLayout(FlowLayout.LEFT);
			左对齐, 水平和垂直间距为缺省值(5)
	3>	new FlowLayout();
			使用缺省 的居中对齐方式,水平和垂直间距为缺省值(5) 

									【TestFlowL ayout.java】
									【TestFlowI ayout2.java】

```
##### BorderLayout布局管理器
```java      
1.  BorderLayout是Frame类的默认布局管理器

2. BorderLayout将整个容器的布局划分成
	1>东(EAST)
	2>西(WEST)
	3>南(SOUTH)
	4>北(NORTH)
	5>中(CENTER) 五个区域，组件只能被添加到指定的区域

2. 如不指定 组件的加入部位，则默认加入到CENTER区
3. 每个区域只能加入一个组件， 如加入多个，则先前加入的会被覆盖。

4. BorderLayout型布局容器尺寸缩放原则: 
	1> 北、南两个区域在水平方向缩放
	2>东、西两个区域在垂直方向缩放
	3>中部可 在两个方向上缩放
									【GUl/TestBorderLayout. java】

```
##### GridLayout布局管理器
```java
1.  GridLayout型布局管理器将空间划分成规则的矩形网格，每个单元格区
	域大小相等。组件被添加到每个单元格中，先从左到右添满一行后换
    行，再从上到下

2.在GridLayout构造方法中指定分割的行数和列数:
	 GridLayout(3,4)


3.注意：
   GridLayout是 以行数为准的 //重点

```
##### 布局管理器总结
```java
1. Frame是一一个顶级窗口，Frame的默认布局管理器为BorderLayout

2. Panel无法单独显示，必须添加到某个容器中。
	Panel的缺省布局管理器为FlowL ayout。

3. 当把Panel作为一个组件添加到某个容器中后，该Panel仍然可以有自己
   的布局管理器

4. 使用布局管理器时，布局管理器负责各个组件的大小和位置，因此用户无
   法在这种情况下设置组件大小和位置属性，如果试图使用Java语言提供
   的 setLocation(),setSize(),setBounds()等方法， 则都会被布局管
   理器覆盖

5. 如果用户确实需要亲自设置组件大小或位置，则应取消该容器的布局管理
   器，方法为:
		setLayout(null)


```



##### 十个按钮

```java 
import java.awt.*;

public class 十个按钮 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//十个按钮
		Button b1  =new  Button("1");
		Button b2  =new  Button("2");
		Button b3  =new  Button("3");
		Button b4  =new  Button("4");
		Button b5  =new  Button("5");
		Button b6  =new  Button("6");
		Button b7  =new  Button("7");
		Button b8  =new  Button("8");
		Button b9  =new  Button("9");
		Button b10 =new  Button("10");
		
		//整体
		Frame f = new Frame("十个按钮");
		f.setLayout(new GridLayout(2,1));
		
		//上面的
		Panel p1 = new Panel ();
		p1.setLayout(new BorderLayout());
		//上中
		Panel p1_1 = new Panel();
		p1_1.setLayout(new GridLayout(2,1));
	
		
		//组合上
		p1.add(b1, BorderLayout.WEST);
		p1_1.add(b3);
		p1_1.add(b4);
		p1.add(p1_1, BorderLayout.CENTER);
		p1.add(b2, BorderLayout.EAST);
		

		//下面的
		Panel p2 = new Panel ();
		p2.setLayout(new BorderLayout());
		
		//下中
		Panel p2_2 = new Panel();
		p2_2.setLayout(new GridLayout(2,2));

		//组合下
		p2.add(b5, BorderLayout.WEST);
		p2_2.add(b7);
		p2_2.add(b8);
		p2_2.add(b9);
		p2_2.add(b10);
		p2.add(p2_2);
		p2.add(b6, BorderLayout.EAST);
	
		f.add(p1);
		f.add(p2);
		f.setBounds(45, 45, 400, 400);
		f.pack();
		f.setVisible(true);
		
	
	}

}
```


#### 事件处理
##### 事件处理相关概念
```java
1.事件处理相关概念:
	1>事件(Event)
		用户对组件的一个操作，称之为一一个事件
	2>事件源(Event Source)
		能够产生事件的GUl组件对象，如按钮、文本框等。
	3>事件处理方法(Event Handler)
		能够接收、解析和处理事件类对象,实现与用户交互功能的方法。
	4>事件监听器(Event Listener)
		可以处理事件的一一个类。

2.默认情况下事件源不会自动产生任何事件，程序员需要做两件事:
		1>告诉事件源可以自动产生哪类事件，即:向事件源注册某种事件的事
		件监听器对象

		2>设计好可以处理这种事件的事件监听器

		3>一旦完成了这两步操作，当用户对事件源进行操作时，事件
		源就会自动产生事件，事件源就会自动把产生的事件封装成
		一个事件对象，事件源就会自动把封装好的事件对象传递给
		事件监听器
		
		4>事件监听器收到事件源发送过来的事件时，事件监听器就会
		自动调用相应的事件处理方法来对该事件进行相应的处理



```


##### 事件处理步骤

```java
1. 假设事件为XXXX
	1>向事件源注册某种事件的事件监听器对象
		addXXXXListener.(...);
	2>设计好可 以处理这种事件的事件监听器
	   class类名implements XXXXListener

	{
		重写XXXXListener接口中的方法
	}

2.	要想设计出能够处理XXXX事件的监听器，只需要编写出实现了
	XXXXListener接口的类就OK了，因为XXXXListener接口中已经定义了
	可以处理XXXX事件的方法

3.代码：
	import java.awt.*;

	import java.awt.event.ActionEvent;
	import java.awt.event.ActionListener;

	public class 测试平台 {

		public static void main(String[] args) {
			// TODO Auto-generated method stub

			Frame f = new Frame ();
			Button b1 = new Button("OK");
			f.add(b1);

			AA aa = new AA();
			b1.addActionListener((ActionListener) aa);
			
			f.pack();//按钮适应窗口大小
			f.setVisible(true);
			
		}

	}
	class AA implements ActionListener
	{
		public void actionPerformed(ActionEvent a)
		{
			System.out.printf("世界!\n");
		}
	}

```
##### 事件处理与窗口关闭代码
```java
import java.awt.*;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.awt.event.WindowListener;


public class 事件处理 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Frame f = new Frame ();
		Button b1 = new Button("OK");
		f.add(b1);
		
		
		f.addWindowListener(new NN() );
		
		
		
		NJ n = new NJ();
		b1.addActionListener((ActionListener) n);
		
		
		f.pack();
		f.setVisible(true);
		
	}

}

class NJ implements ActionListener
{
	public void actionPerformed(ActionEvent a)
	{
		System.out.printf("世界!\n");
	}
	
}

class NN extends WindowAdapter 
{

/*WindowListener 中有很多抽象方法 ，如果NN实现接口，
  却不重写这些抽象方法，则NN会变成抽象类，但很明显这
  不是我们想达到的效果
 我们只想 调用关闭窗口的方法

方法一： 重写NN"实现"WindowListener接口中的全部抽象类方法

方法二：NN extends WindowAdapter 
public void windowClosing(WindowEvent arg0) {
		// TODO Auto-generated method stub
		System.exit(-1);

	
*/
	/*
	@Override
	public void windowActivated(WindowEvent arg0) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void windowClosed(WindowEvent arg0) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void windowClosing(WindowEvent arg0) {
		// TODO Auto-generated method stub
		System.exit(-1);
	}

	@Override
	public void windowDeactivated(WindowEvent arg0) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void windowDeiconified(WindowEvent arg0) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void windowIconified(WindowEvent arg0) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void windowOpened(WindowEvent arg0) {
		// TODO Auto-generated method stub
		
	}
	*/
	public void windowClosing(WindowEvent arg0) {
		// TODO Auto-generated method stub
		System.exit(-1);}
}
```
##### 三个文本框
```java
import java.awt.*;
import java.awt.event.*;
public class 测试平台 {
	
	public static TextField t1,t2,t3;
	//公有，静态
	public static void main(String[] args) {
	
		Frame f = new Frame();
		 t1 = new TextField(30);
		 t2 = new TextField(30);
		 t3 = new TextField(30);
		
		//Label 标签
		Label Lb = new Label("+");
		Button b = new Button("=");
		f.setLayout(new FlowLayout());
		f.add(t1);
		f.add(Lb);
		f.add(t2);
		f.add(b);
		f.add(t3);
		
		b.addActionListener(new CL());
	
		f.pack();
		f.setVisible(true);
		
		
		
	}
}


class CL implements ActionListener
{
	@Override
	public void actionPerformed(ActionEvent a)
	{
		String str1 = 测试平台.t1.getText();
		String str2 = 测试平台.t2.getText();
		int num1 = Integer.parseInt(str1);
		int num2 = Integer.parseInt(str2);
		
		
		String str3 = Integer.toString(num1 + num2);
		
		测试平台.t3.setText(str3);
		
	}
}
/*
该程序缺点：
1.主函数代码过多
2.程序逻辑混乱

解决：
直接创建新的类
在创建一个方法，把代码放入方法中就可
*/
```
```java
/*
	2009年6月29日10:34:02
	文本框内容相加 方法二：
		通过在B类中定义A类的属性，就可以达到在B类访问A类成员目的
		但是通过这种方式无法访问A类私有成员
		
		本方式既繁琐又有局限性，不推荐
*/

import java.awt.*;
import java.awt.event.*;

public class 测试平台2号
{
	
	public static void main(String[] args)
	{
		TF tf = new TF();
		tf.launch();			 
	}
}

class TF
{
	public TextField tf1, tf2, tf3;
	
	public void launch()
	{
		tf1 = new TextField(30);
		tf2 = new TextField(30);
		tf3 = new TextField(30);
		Button bn = new Button("=");
		Label Lb = new Label("+");
		Frame f = new Frame("文本框相加示例");
		f.setLayout(new FlowLayout());
		f.add(tf1);
		f.add(Lb);
		f.add(tf2);
		f.add(bn);
		f.add(tf3);
		
		bn.addActionListener(new MyMonitor(this));
		
		f.pack();
		f.setVisible(true);
	}
}

class MyMonitor implements ActionListener
{
	private TF tf;
	
	public MyMonitor(TF tf)
	{
		this.tf = tf;
	}
	
	@Override
	public void actionPerformed(ActionEvent e)
	{
		String str1 = tf.tf1.getText();
		String str2 = tf.tf2.getText();
		int num1 = Integer.parseInt(str1);
		int num2 = Integer.parseInt(str2);
		int num3 = num1 + num2;
		
		tf.tf3.setText(num3+"");
	}
}
```
##### 计算器
```java


```



#### 内部类

```java
1.定义:
	在A类的内部但是所有方法的外部定义了一一个B类，则B类就是A类的
	内部类，A是B的外部类

2. 可以把内部类当做包裹它的外部类的一个成员，这是理解内
  部类的关键

3.内部类的优点:
		1>内部类的所有方法都可以访问外部类的所有成员
		2>增加程序的安全性，有效避免其他不相关类对该类的访问
4.何时使用
	如果一个B类要使用A类的所有成员，并且B类不需要被除A类以外的
	其他类访问，则我们应当把B类定义为A类的内部类
											【TestTextField 1.java】
											【TestTextField_ 2.java】
											【TestTextField 3.java】



```

#### 匿名类
```java




```
```java
java.awt		抽象窗口工具包，调用本地系统方法实现功能需求
java.swing		基于awt，跟多组件，完全有java实现，轻量，可移植

"顶层容器
awt    Frame
swing  JFrame 
"中间容器[非必须]
充当基本组件的容器，不可独立显示
awt     Panel
swing   JPanel

"常用控件
JPanel			//添加面板
JLabel 			//添加标签
JTextField 		//添加文本框
ButtonGroup 	//单选按钮组
JRadioButton 	//单选按钮
JCheckBox 		//复选按钮
JList 			//下拉表
JComboBox 		//列表框

    
```



### 5>IO

#### 什么叫流

```c
1.引入代码：
        package 流;
        import java.io.*;
        public class TestFileReader {
            public static void main(String[] args)throws Exception 
            {
                // TODO Auto-generated method stub
                    FileReader fr = new FileReader("D:\\桌面文件\\二叉树.txt");
                //注解：①
                    int ch;//整型数值
                    ch = fr.read();//返回该字符的二进制  整型数值

                    while(ch!=-1)//【文件读取到末尾返回-1 】【字符从0开始】 
                    {
                            System.out.printf("%c", (char)ch);
                            ch = fr.read();//【文件指针自动后移】
                    }
                fr.close();
            }
        }  
 /*
 注解①：
	1.fr产生，fr叫流，或流对象
	2.结构：
						fr管道	
		【程序】<=================== 【文件】

		注意：箭头指向程序"即从文件中读数据"
		fr.read()相当于管道上的小按钮       	
 */

2.流与类的关系
   定义："用于程序和设备之间传输数据的管道"，
    	是一个"特殊的类"，则这个类有一个新
    	的名字叫流//例如：FileReader
    
    流一定是类，但类不一定是流

```
<img src="D:\桌面文件\Markdown笔记\图片\流的定义.JPG" style="zoom:50%;" />



#### 流的分类

````java 
1.流有多种分类方法，可按照不同角度划分:
	按数据流的方向不同可以分为输入流和输出流。
    按处理数据单位不同可以分为字节流[一个字节]和字符流[两个字符]。
    按照功能不同可以分为节点流和处理流。

2.J2SDK所提供的所有流类型位于包java.io内都分别继承自以下四
	种抽象流类型。

````

|            | 字节流         | 字符流   |
| ---------- | -------------- | -------- |
| **输入流** | *InputStream*  | *Reader* |
| **输出流** | *OutputStream* | *Writer* |

```java
3.原始流与包裹流关系
	[即节点流和处理流的关系]    
```

<img src="D://桌面文件//Markdown笔记//图片//原始流与包裹流.jpg" style = "zoom:50%;">

##### 四大基本抽象流

```java
'InputStream、OutputStream、Reader、Writer'
1.	在java中一个字符占用两个字节
    
2.	InputStream和OutputStream读写数据的单位是一个字节
	Reader和Writer读写数据的单位是一个字符
    
3.	InputStream、OutputStream、Reader、Writer都是抽象类，或者说
	都是抽象流，通常我们使用的都是它们的子类
 
我的理解：以程序本身的视角读与写
    	InputStream、Reader   程序读
    	OutputStream、Writer  程序写
```

###### InputStream

```java
   
//@-----------------------InputStream-----------------------------
 以InputStream为例学习四种抽象流：
 InputStream常用方法：
 1> public int read() throws IOException
        读取一个"字节"并以整数形式返回
        如果读取到输入流的末尾则返回-1
    
2> public int read(byte []b);throws IOException
	'1' 从输入流中读取一定数量的字节，并将其存储在缓冲区数组b中
		以整数形式返回实际读取的字节数
    
	'2' 如果b的长度为0,则不读取任何字节并返回0;如果因为流位于文
        件末尾而没有可用的字节，则返回值-1;

    例子:
    FileInputStream fis = new FilelnputStream("d:\\share\\errorlog.txt");
    int len = fis.read(buf); //注解②

    "文件" -> "程序"
    /*注解②：
    		"文件" -> "buf数组"
            从fis流所联的d:\\share\\errorlog.txt文件中
            读取数据，并将读取出来的数据写入buf数组中，返回值是实际写入
            buf数组的字节个数，如果读取到文件的结尾，则返回-1

            buf是数组名.length >= len

            while()
            {
                byte [] buf = new byte[1000];
                len = fis.read(buf);
            }

            1M多的文件，循环读取，不停对len在最后一次中
            可能就会小
    */

3> 
public int read(byte[] b, int off, int len) throws IOException     
     /*从调用read的方法的对象所关联的设备中读取
     	字节放到b所在的数组中*/      
    '1'从输入流中最多读取len个字节的数据并存入byte数组中
    '2'"b表示读取的数据要存入的数组的名字
    '3'"off表示第一个读出的数据要存入的位置，是下标
    '4'len表示最多能读取的字节数
    '5'将从输入流所关联到的设备中读取的第一个字节存储在元素
       b[off]中，下一个字节存储在b[off+1]中，依次类推。
        "读取的字节数最多等于len
    '6'尝试读取len个字节，但读取的字节也可能小于该值。以整数形
       式返回实际读取的字节数
    '7'如果读到了文件的末尾，则返回-1 .

4>
    void close()  throws IOException//重要
    关闭此输入流并释放与该流关联的所有系统资源
    long skip(long n) throws IOException
    跳过和丢弃此输入流中数据的n个字节。
    这个用的很少

//---------------------------------------------------------------
```

###### OutputStream

```java
//@-----------------------OutputStream-----------------------------
1.OutputStream流中常用的方法
    "程序" -> "文件"
        //向输出流中写入一个字节数据,该字节数据为参数b的低8位
        void write (int b) throws IOException
    
        //将一个字节类型的数组中的数据写入输出流
        void write (byte[] b) throws I0Exception
    
        //将一个字节类型的数组中的从指定位置(off)开始的
        //len个字节写入到输出流
        void write (byte[] b， int off ,int len)throws IOException
    
        //关闭流释放内存资源
        void close() throws IOException
        //将输出流中缓冲的数据全部写出到目的地
        void flush() throws IOException
    
        "true"
        输入流.read(buf);
        输出流.write(b);

/*----------
error：
输出流.read(buf);
输入流.write(b);
----------*/

```

###### Reader

```java
     //读取一个字符并以整数的形式返回(0~255) ,
    //如果返回-1已到输入流的末尾。
    int read() throws IOException
    //读取一系列字符并存储到一个数组buffer,
    //返回实际读取的字符数，如果读取前已到输入流的末尾返回-1
    int read(char[] cbuf) throws IOException
    //最多读取length个字符
    //并存储到一个数组buffer,从length位置开始
    //返回实际读取的字符数，如果读取前以到输入流的末尾返回-1
    int read(char[] cbuf， int offset， int length)
    throws IOException
    //关闭流释放内存资源
    void close () throws IOException
    //跳过n个字符不读，返回实际跳过的字节数
    long skip (long n) throws IOException

```

###### Writer

```java
    //向输出流中写入一个字符数据,该字节数据为参数b的低16位
    void write (int c) throws IOExcepti on
    //将一个字符类型的数组中的数据写入输出流,
    void write (char [ ] cbuf) throws IOE xception
    //将一个字符类型的数组中的从指定位置(offset)开始的
    //length个字符写入到输出流
    void write (char[] cbuf, int offset，int length)
    throws IOException
    //将一个字符串中的字符写入到输出流
    void write (String string) throws IOException
    //将一个字符串从offset开始的length个字符写入到输出流
    void write (String string, int offset, int length)
    throws IOException
    //关闭流释放内存资源
    void close () throws IOException
    //将输出流中缓冲的数据全部写出到目的地
    void flush() throws IOException

```
##### 字节流与字符流的使用区别
```java
1. "字符流读写文本文件
    package 流;
    import java.io.*;
    public class TestReadtoWrite {

        public static void main(String[] args) throws Exception {
            // TODO Auto-generated method stub
            FileReader fr = new FileReader
               ("D:\\English\\eclipse-jee-photon-R-win32\\java高级\\src\\流					\\TestReadtoWrite.java");
            FileWriter fw = new FileWriter("d:\\桌面文件\\a.txt");
            
            int binaryNumber;//二进制数
            binaryNumber = fr.read();
            while(-1!=binaryNumber) 
            {
                fw.write(binaryNumber);
                binaryNumber = fr.read();
            }
            
            //输出流刷新
            fw.flush();

            //关闭
            fr.close();
            fw.close();

        }

    }

"输出流中存在 flush() 方法
"不刷新可能写入失败
2.字符流无法处理非文本文件 
    
3.字节流读取非文本文件
    package 流;
    import java.io.*;


    public class 字节流读取非文本文件测试 {

        public static void main(String[] args) throws Exception
        {
            // TODO Auto-generated method stub
            //D:\桌面文件\CSS\music\TestMusic.mp3
            FileInputStream   fis = new FileInputStream("D:\\桌面文件						\\CSS\\music\\TestMusic.mp3");
            
            FileOutputStream  fos = new FileOutputStream("D:\\a.mp3");
            int binaryNumber = 0;
            binaryNumber = fis.read();
            while(-1!=binaryNumber) {
                fos.write(binaryNumber);
                binaryNumber = fis.read();
            }

            fos.flush();

            fis.close();
            fos.close();

            /*---------------------------
            运行成功

            .mp3可以听
            同理可测试其他的非文本文件

            ---------------------------*/		
        }
    }
//@-------------------------总结--------------------------
1. FileInputStream和FileOutputStream可以完成所有格式文件的赋值
    
2. FileReader和FileWriter只可以完成文本文件的复制，却无法完成视频
    格式文件的复制
        '1'因为字节是不需要解码和编码的，将字节转化为字符才存在解码和解码的问题
        '2'字节流可以从所有格式的设备中读写数据，但字符流只能从文本格式的设备中
        	读写数据

```




##### 文件流 
```java
1.文件流包括
    FilelnputStream FileOutputStream  -字节流
    FileReader      FileWriter		  -字符流

2.FilelnputStream的使用
    '1'	InputStream是用来读取字节的，是个抽象类，我们通常使
    	用的是该类的子类
    '2'	FilelnputStream是InputStream的子类，利用
    	FilelnputStream可以将一个文件的内容按字节为单位读取出来
    
    '3'FilelnputStream有一个很常用的构造函数
         public FileInputStream(String fileName) throws FileNotFoundException
         利用该构造函数可以实现将输入流连接到某个文件的功能
         必须对本构造函数抛出的异常进行捕捉
         如果用字符串来表示操作系统的文件路径时，我们可以使用"\\"和"/"两种方式来作为文
          件夹的路径分隔符
        FileOutputStream同理，不再赘述

    
```
##### 缓冲流
```java
1.缓冲流概述：
    缓冲流就是带有"缓冲区"的"输入输出流"
    缓冲流可以显著的减少我们对IO访问的次数，保护我们的硬盘!
    缓冲流本身就是"处理流"(处理流也叫包裹流)
    缓冲流必须得"依附于节点流"(节点流也叫原始流)
    处理流是包裹在原始节点流上的流，相当于包括在管道上的管道!
    
 			 " 包裹流"
    "_______________________________"
    		___________________________________
    			原始流
    		___________________________________
    "_______________________________"
    
2.缓冲流要"套接"在相应的节点流之上，对读写的数据提供了缓冲的功能，
  提高了读写的效率，同时增加了一些新的方法。
  J2SDK提供了四种缓存流，其常用的构造方法为:
        BufferedReader (Reader in)
        BufferedReader (Reader in, int sz) //sz 为自定义缓存区的大小
        Bufferedwriter (writer out)
        Bufferedwriter (Writer out,int sz)
        BufferedInputstream (Inputstream in)
        BufferedInputStream (Inputstream in, int size)
        Bufferedoutputstream( Outputstream out)
        Bufferedoutputstream (Outputstream out,int size)

3.
    缓冲输入流支持其父类的mark和reset方法。
    BufferedReader 提供了 readLine 方法用于读取一行字符串[以r或\n分隔]
    BufferedWriter 提供了 newLine  用于写入一个行分隔符。
    对于输出的缓冲流，写出的数据会先在内存中缓存，使用flush方法将会使内存中的数据
    立刻写出。

4.缓冲流[读写文件代码] 
    package 流;
    import java.io.*;
    public class 缓冲流Buffered__ {

        public static void main(String[] args)throws Exception {
            // TODO Auto-generated method stub
            BufferedInputStream   bis = 
            new BufferedInputStream(new FileInputStream("D:\\桌面文件						\\CSS\\music\\TestMusic.mp3"));
            BufferedOutputStream  bos = 
            new BufferedOutputStream( new FileOutputStream("D:\\a5.mp3"));
            byte []buf = new byte[1024];
            int len = 0;
            len = bis.read(buf);//程序从文件中读入数据，写入buf数组
            while(-1!=len) {
                bos.write(buf,0,len);//程序从buf数组读出数据,
                len = bis.read(buf);
            }

            bos.flush();
            bos.close();
            bis.close();

            System.out.println("OK!");
        }
    }

5.BufferedOutputStream 和 BufferedInputStream
    '1'BufferedOutputStream:带缓冲的输出流， 允许一次向硬盘写
    		入多个字节的数据
    '2'BufferedInputStream:带缓冲的输入流，允许一次向程序中读
    		入多个字节的数据
    '3'"BufferedOutputStream和BufferedInputStream都是包裹流,
       "必须的依附于OutputStream和InputStream
            例子:	
            利用BufferedOutputStream和BufferedInputStream完成大容量文
            件的复制，这远比单纯利用FilelnputStream和FileOutputStream
            要快得多



6.易错点：
    '1':
    BufferedInputStream bis = new BufferedInputStream(
    new FileInputStream("D:\l综艺\电影\猫和老鼠\CD4.rmvb")); 
    //bis 输入流有个默认的缓冲区，大小为32个字节
    byte[] buf= new byte[1024];
    int len = bis.read(buf, 0, 1024);
            /*
            一定要注意，bis.read(buf, 0, 1024);这不是从buf中读数据，而是从
            bis所关联到的“D:综艺\电影\猫和老鼠\CD4.rmvb”文件中读取数
            据，并将读取的数据写入bis自己的默认缓冲区中，然后再将缓冲区
            的内容写入buf数组中，每次最多向buf数组中写入1024个字节，返
            回实际写入buf数组的字节个数，如果读到了文件的末尾，无法再向
            buf数组中写入数据，则返回-1
            */
	'2':
        BufferedInputStream流中有
        	public int read(byte[] b)
        	方法用来把从当前流关联到的设备中读取出来的数据存入一
        	个byte数组中
            
        BufferedOutputStream流中有
        	public int write(byte[] b)
        	方法用来把byte数组中的数据输出到当前流所关联到的设备中
            
        如果我们希望用BufferedInputStream和BufferedOutputStream
        完成“将一个设备中的数据导入另一个设备中”，我们就应该定义一
        个"临时的byte类型的数组"，用这个临时数组作为输入流与输出流进
        行交互的"中转枢纽"!

6.注意：
	'1'
     BufferedInputstream BufferedOutputStream要比
	FileInputStream FileOutputStream读写数据的速度快
    
    '2'
        我们"只有
            BufferedInputStream
            BufferedOutputStream类
            BufferedWriter
            BufferedReader
        "没有
            BufferedStream
            BufferedFileInputStream(但有FileOutputStream)
            BufferredFileOutputStream (但有FileInputStream)
            BufferedFileReader(但有FileReader)
            BufferedFileWriter(但有FileWriter)
        "所以前四个流都是包裹流

            
7.BufferedReader 和 BufferedWriter
            
'1'代码：
package 流;
/*
利用 BufferedReader 和 BufferedWriter 完成文本文件的复制
*/
    import java.io.*;
    public class BufferedReaderAndbufferedWriter
    {
        public static void main(String[] args)t	hrows Exception
        {
            BufferedReader br = null;
            BufferedWriter bw = null;
            try
            {
                br = new BufferedReader(
                new FileReader("d:\\English\\eclipse-jee-photon-R-win32\\java高级				\\src\\流\\BufferedReaderAndbufferedWriter.java"));
                bw = new BufferedWriter(
                            new FileWriter("d:\\Writer.txt"));
                String str = null;

                while (null != (str=br.readLine()))  //从此处是null
                    /*br.readLine()读取一行字符，但会将读取的换行符自动丢弃,
                    即返回的String对象中并不包括换行符*/
                {
                    bw.write(str);
                    bw.newLine();  //写入一个换行符  这行不能省
                }
                bw.flush();
            }
            catch (FileNotFoundException e)
            {
                e.printStackTrace();
                System.exit(-1);
            }
            catch (IOException e)
            {
                e.printStackTrace();
                System.exit(-1);
            }
            finally
            {
                try
                {
                    bw.close();
                    br.close();
                }
                catch (IOException e)
                {
                    e.printStackTrace();
                    System.exit(-1);
                }
            }
        }
    }
	'2'小结:
        Reader FileReader InputStream FileInputStream
        BufferedInputStream流中都没有readLine方法
        DatalnputStream流中有readLine方法，但已经被标记为过时
        BufferedReader流中有readLine方法，并且该方法是可以正确被使用的
        BufferedReader流中有readLine是个非常有用的方法，
        BufferedReader是个要经常使用的流
        利用BufferedReader和BufferedWriter可以提高读写文本文件内容的速度

```

##### 数据流

```java
DatalnputStream 和 DatalOutputStream

1.DatalnputStream能够以一种与机器无关的方式，直接从底层字节输入流读
  取Java基本类型和Srina类型的数据，常用方法包括
        常见方法:
            public DatalnputStream(InputStream in)
            public final boolean readBoolean(
            public final byte readByte()
            public final char readChar()
            public final double readDouble()
            public final float readFloat()
            public final int readInt()
            public final long readLong()
            public final short readShort()
            public final String readUTF()

    DatalnputStream是包裹流，"必须依附于InputStream

2.   DataOutputStream能够以一种与机器无关的方式，直接将Java基本类
	 型和String类型数据写出到其他的字节输出流
        常见方法:
            public DataOutputStream(OutputStream in)
            public final boolean writeBoolean()
            public final byte writeByte()
            public final char writeChar()
            public final double writeDouble()
            public final float writeFloat()
            public final int writelnt()
            public final long writeLong()
            public final short writeShort()
            public final String writeUTF()	
	DataOutputStream是包裹流，"必须依附于OutputStream

                
                
3.例子:
    编程实现将long类型数据写入byte数组，然后再从byte数组中把该数
    据读出来

	附注:
        这是Socket编程中经常要完成的功能,
        因为网络编程中经常要把数值型数据存入byte数组中,然后把byte数组打
        包成数据包(即DatagramPacket)，再把数据包经过网络传输到目的机,
        目的机再从byte数组中把原数值型数据还原回来
                
	本程序要使用到
        ByteArrayInputStream
        ByteArrayOutputStream
        DatalnputStream
        DataOutputStream


1.数据流的小案例：

        //1.长整型数据
        long n = 9876543210L;		
        //2.创建 ByteArrayOutputStream baos管道
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        //3.创建依附于 baos管道的 DataOutputStream 包裹流 dos管道
        DataOutputStream dos = new DataOutputStream(baos);
        //4.使用DataOutputStream中的writeLong()方法将长整型的二进制数据写入系统默认缓冲区数组
        dos.writeLong(n);
        dos.flush();
        //5.使用ByteArrayOutputStream中的toByteArray()方法将数据写入自定义byte类型数组   
        byte buf[] = baos.toByteArray();//我的理解：将默认数组可视化,可以通过数组名操作
        //6.创建ByteArrayInputStream bais管道 使用已有的buf数组作为缓冲区
        ByteArrayInputStream bais = new ByteArrayInputStream(buf);
        //7.创建依附于bais管道 的DataInputStream dis 管道
        DataInputStream dis = new DataInputStream(bais);
        //8.使用dis中的readLong()方法将缓冲区中的数据以long类型读出
        long l = dis.readLong();		
        dos.close();	

```


##### 转换流

```java
1.只有两种："字节流"转"字符流"
    OutputStreamWriter流是把OutputStream流转化成Writer流的流
    InputStreamReader是把InputStream转化成Reader
    
2.OutputStreamWriter和InputStreamReader都是包裹流

3.[案例：]如何将键盘输入的字符组成字符串直接赋给String对象
    	String str    = null;
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		str = br.readLine();
		System.out.println("str = " + str);
	【该示例未增加异常捕获】【完整：TestStringInput.java】
        
4.
    String str= "123";
    BufferedReader br =new BufferedReade r( new
    InputStreamReader(System.in));

 如果直接输入回车 的话，则
    '1'br.readLine()会丢弃回车符，而不是返回回车符,即
       br.readLine(遇到回车符时终止读取，并且会把读取到的回
       车符自动丢弃掉
    '2'br.readLine()返回的是""而不是null,表示空字符串
		null表示空指针，空指针就是空地址，空地址就是不指向任何
		存储单元的意思

```





##### Print流

```java
Print流只有输出，没有输入
分类:
    PrintWriter 输出字符
    PrintStream 输出字节
        
        
StringWriter sw = new StringWriter();
PrintWriter pw = new PrintWriter(sw);
exception.printStackTrace(pw);
String details = sw.toString();
```

##### Object流

```java
1.有四大抽象流：'InputStream、OutputStream、Reader、Writer'一般我们使用他们的子类
    
2.  FilelnputStream FileOutputStream  -字节流
    FileReader      FileWriter		  -字符流
    这四种可以直接连接到文件，例如： FileWriter fw = new FileWriter("d:\\桌面文件\\a.txt");

3.缓冲流都是"包裹流"，所以使用前与一个流被包裹，通常是2中的四种
     	例如： BufferedWriter bw = new BufferedWriter( new FileWriter("d:\\Writer.txt"));

4.
```









### 6>容器(集合)

#### 容器

##### 定义

```java 
如果一个类是专门用来存放其它类对象的，则这个类有另一个特殊的词叫做容器[或者说"集合"]
```



##### 为什么需容器

```java
1.数组存在两个缺陷:
    数组长度难以扩充
    数组中元素类型必须相同
        
容器可以弥补数组的这两个缺陷
举例:.
    假设A是个类名
    A[]arr = new A[10];
    表示分配了一个数组，数组的每个元素都是A类对象的一个引用，但是如果想扩充数组的长度，
    比如希望数组的长度变成15，我们是不能直接在原数组内存的后面追加内存的，必须得另外
    分配长度为15的内存空间，然后利用System. arraycopy()方法来把原数组的内容拷贝到新内
    存中，很明显，这即耗时。又耗内存!所以一旦数组内存已分配，你想改变数组的长度，效率
    就会变的很低

```



##### 容器的框架图


#### 分类和使用

```java
容器与现实的对应关系
	1.集合就是将若干用途、性质相同或相近的"数据"组合而成一个整体
    
	2.数学上集合类型可以归纳为三种
        集 (Set)
        	Set集合中不区分元素的顺序，不允许出现重复元素
        列表 (List)
       		List集合区分元素的顺序，且允许包含重复元素
        映射(Map)
        	映射中保存成对的"键-值"(Key-Value) 信息，映射中不能包含重复的键
        	每个键最多只能映射一个值。
    
Java设计了三个接口来对应数学上的三种集合类型，这三个
接口名字分别是Set List Map

```





##### Collection`接口`

```java
1. Collection接口中的方法介绍
	int size();
		返回此collection 中的元素数
	boolean isEmpty() ;
	boolean containesAll(Collection c);
    	判断形参c所指向的集合中所有的元素是不是已经全部包含在了当前集合中
    	是，返回true，否则返回false
    lterator iteratof();
    	返回能够遍历当前集合所有元素的迭代器
	Object[] toArray()
        容器不是数组，不能通过下标的方式访问容器中的元素
        只有数组才可以通过下标来访问
	   返回一个包含此 collection中所有元素的数组
	  【TestArrayDistToArray.java】
            
    boolean add(Object e);
    	把e添加到当前集合中
    boolean remove(Object o);
    boolean addAll(Collection c);
    	把c中所有的元素添加到当前集合中
    boolean removeAll(Collection c);
    void clear();
    	把当前容器中的所有元素清除
    boolean equals(Object o);
    int hashCode() ;

2.重写toString()方法
    Collection c = new ArrayList();
    ······
    System.out.println(c);

    本语句等价于：
    [调用第一个元素的toString方法,调用第二个元素的toString方法,调用第三个元素的toString方法····]
    "强烈建议:所有添加到Collection容器中的对象都应该重写父类Object的toString方法"
```



###### List

```java
1. List接口是Collection的子接口，实现List接口的容器类中的元素是有顺序的，而且可以重复
2. List容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素
3. J2SDK所提供的List容器类有 ArrayList,LinkedList等.
    
Object get (int index)//获取下标为 index 的元素
Object set (int index,Object element);//将下标为index的元素修改为element
void add(int index,Object element) ;//在下标为index的位置插入为element
Object remove (int index) ;//移除
int indexof(Object o);//返回此列表中首次出现的指定元素的索引，
					//或如果此列表不包含元素，则返回 -1
int lastIndexOf((Object o);//最后一次出现o的位置

```



```java
"ArrayList 与 LinkedList的比较"
ArrayList和LinkedLis部都实现了List接口中的方法，但两者内部实现不同
ArrayList底层采用"数组"完成，而LinkedList则是以一般的"双向链表"完成，
    其内每个对象除了数据本身外，还有两个引用，分别指向前一个元素和后一个元素。
如果我们经常在List的开始处增加元素，或者在List中进行播
入和删除操作，我们应该使用LinkedList，否则的话，使用
ArrayList将更加快速
    -ArrayList存取速度快，插入删除慢
    -LinkedList存取速度慢，插入删除速度快

```







###### Set

```java
1.因为Set和List都是继承自Collection接口，所以Set和List中有很多方法是一样的
List接口中有 add，set, indexOf方法，但是Set接口中却只有add方法，没有set， indexOf方法，因为Set是无序不能重复的，不存在某元素具体位置这个概念
    


2.Set接口是Collection的子接口，Set接口没有提供额外的方法，
	即：Set中所有方法都来自Collection

3.J2SDKAPI中所提供的 Set容器类有 HashSet, TreeSet等

4.Set容器可以与数学中“集合”的概念相对应

5.存放入HashSet 容器中的类必须要实现 equals()和hahsCode方法,
	Set的"不允许重复"需要程序员手书写额外的代码实现
        复习：equals方法默认比较"内存地址"
        	相同吗？
        		相同：true
			    不相同：false 
         改写：比较"内容"是否相同
        		相同：true
        		不相同：false 
        
6.为什么要重写equals()和hashCode()方法
	预备知识:
        1>散列码:
            Object中的hashCode方法会返回该对象的内存真实地址的整数
            化表示，这个形象的不是真正地址的整数值就是哈希码
        2>"过程
          /*向HashSet中添加对象时，HashSet先通过该对象的 hashCode()计算出
            相应的桶,然后再根据equals()方法找到相应的对象。如果容器中已存在该
            对象则不再添加，如果不存在，则添加进去!
         */
 
7."什么类必须得重写equals()和hashCode()方法
    Hashtable HashSet HashMap都必须的同时实现 equals()方法和 hashCode(方法,
    TreeSet和TreeMap则不需要实现equals(方法和hashCode()方法

8."怎样重写equals() 和hashCode()方法
	利用系统重写了自带类的hashCode方法
       @Override
      public int hashCode(Object obj)
     {
            return new Integer(id).hashCode;
      }
    ----------------------------------------
     public int hashCode(Object obj)
     {
            return new String(id + name).hashCode;
      }                       
    只需要保证对于相同的内容，hashCode返回相同的值即可
                                
9.TreeSet类
            1>TreeSet类实现了Set接口
            2>TreeSet是一个有序集合，TreeSet中元素将按照升序排列
                缺省是按照自然顺序进行排列，因此TreeSet中元素要实现
                Comparable接口
            3>记住：所有可以进行排序的类都应该实现Comparable接口
            4>TreeSet实例
                    Collection c = new TreeSet();
                    c.add(""123");
                    c.add("456");
                    c.add("234);
                    c.add("111"");
                    c.add(""678'");
                    Iterator it= c.iterator();
                    while (it.hasNext(){
                         System.out.println(it.next());
                    }

10.HashSet和TreeSet的比较
    HashSet是基于Hash算法实现的，其性能通常都优于
    TreeSet。我们通常都应该使用HashSet，在我们需要排序的
    功能时，我们才使用TreeSet。

```

```java
import java.util.HashSet;
import java.util.Set;
class Students
{
	private int id;
	private String name;
	
	public Students (int id ,String name) {
		this.id =id;
		this.name= name;
		
	}
	@Override
	public String toString() {
		return  this.id + "," +  this.name;
	}
	@Override 
	public int hashCode()
	{
//		return id*this.name.hashCode();
		return new String(id+name).hashCode();
	}
	@Override 
	public boolean equals(Object obj)
	{
		Students stu = (Students)obj;
		return this.id == stu.id&&this.name == stu.name;
	}
	
}

public class TestHashCode {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Set S = new HashSet();
		S.add(new Students(12,"张三"));
		S.add(new Students(15,"李四"));
		S.add(new Students(15,"李四"));
		S.add(new Students(12,"张三"));
		S.add(new Students(12,"王五"));
		System.out.println(S);//输出顺序可能与添加顺序不同
	}
}

```








##### Collection`s`==类==

```java
Collection接口的实现类，如ArrayList 、 LinkedList本身
并没有提供排序，倒置，查找等方法，这些方法是由
Collections类来实现的，该类有很多public static方法，可
以直接对Collection接口的实现类进行操作

"Collections类常用算法"
类 java.uti1.collections 提供了一些静态方法实现了基于List容器的一些常用算法.

void sort(List)对List容器内的元素排序
void shuffle(List) 对List容器内的对象进行随机排列
void reverse(List)对List容器内的对象进行逆续排列【倒置】
void fill(List, Object)用一个特定的对象重写整个List容器
void copy (List dest,List src)将src List容器内容拷贝到dest List容器
    										【dest:目的 src:源】
int binarySearch(List，Obieet)对于顺序的List容器，采用折半查找的方法查找特定对象
//记住，使用binarySearch()方法的前提是该容器已升序排序，且只能是升序
 若是降序，则先倒置

+---------------------------------------------------+

List lt=new LinkedList(); /7行
it.add("111");
It.add("222");
It.add("333");
Svstem.out.printIn(lt);
Collections.fill(lt ,"888");
System.out.printIn(It);

[111,222,333]
[888,888,888]
+---------------------------------------------------+                                              
```



##### Comparale接口

```java

基本类型数据和String类型数据，它们彼此的比较标准Java语言本身已经提供好了
用户"自定义类对象"之间比较的标准Java语言本身是没有提供
所以如果一个容器中含有用户自定义类型的数据，并且我们
需要对容器中元素进行"排序"，或"查找"某一元素时，我们就必
须得制定容器中元素与元素之间比较的标准
凡是需要进行对象比较/排序的场合均可考虎实现Comparable接口
    

class Student implements Comparable{
	private int id;
	private String name;
	
	public Student (int id ,String name) {
		this.id =id;
		this.name= name;
		
	}
	@Override
	public String toString() {
		return  this.id + "," +  this.name;
	}
	@Override
	public int compareTo(Object o) {
		// TODO Auto-generated method stub
		Student stu = (Student)o;
        //子类特有属性无法被父类使用，所以向下转型
		if(this.id==stu.id)
			return 0;
		else if(this.id>stu.id)
				return 1;
		else 
			return -1;
	
	}
}

public class TestList {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		ArrayList L = new ArrayList();
		L.add(new Student(12,"张三"));
		L.add(new Student(15,"李四"));
		L.add(new Student(12,"王五"));
		
		Collections.sort(L);
		System.out.println(L);
		
	}
}

所有可以"排序"的类都实现了java.1ang.Comparable 接
口，Comparable接口中只有一个方法
public int compareTo(object obj);该方法
返回0表示    this==obj
返回正数表示 this> obj
返回负数表示 this< obj
实现了Comparable 接口的类通过实现 compareTo 方法从
而确定该类对象的排序方式。

   
    
```



##### Iterator接口

```java
"通过以上的学习我们知道对于不同的集合，其内部的存储结构不同的"
1.Ilterator接口用来以统一的方式对集合中的各个元素进行遍历
2.Iterator接口的对象又称为迭代器，利用该对象可以方便的遍
  历容器中的元素
3.所有实现了Collection接口的容器类都有一个Iterator()方法
  该方法返回一个实现了Iterator接口的对象

4.Ilterator方法介绍
   
    1>示意图：												   
          -----□----------□----------□----------□----			  
     	游标 ↑   next() ↑			元素		
    【返回游标划过元素】
	2>boolean hasNext():
		是用来判断当前游标的后面还是否存在元素，如果存在返回直，否则返回假  
	3>Object next();
		先返回当前游标右边的元素，然后游标后移一个位置

    4>void remove()
        删除最近返回的元素,在调用remove之前，我们至少保证先调用一次
        next方法,而且调用next之后只能调用一次remove方法
        remove()方法"不推荐使用"
            






```





##### Map

```java
java.util.Map接口描述了映射结构，Map结构允许以键集、
值集合或键~值映射关系集的形式查看某个映射的内容。
    
1.主要方法:
    Object put(Object key, Object value)
    Object get(Object key)
		注意Map接口中并没有Object get(Object value)
    boolean isEmpty()
    void clear()
    int size()
    boolean containsKey(Object key)
    boolean containsValue(Object value)
        
2.预备知识:哈希表
    哈希表的定义:
        哈希表不是只存储需要保存的数据，而是既保存数据，也保存该数据的主键，实际是。
        先保存主键，然后哈希表会根据某种算法自动计算出以当前主键为主键的数据的存储位
        置，然后再把该数据保存进去
    哈希表:
        假设待保存的数据是val,val的主键是key，则哈希表是先存储key，然后哈希表会自动
        根据key计算出val的存储位置，并最终把val存储进去
    哈希表注意事项:
        Hash即哈希表又称散列表
        哈希表主要是为了提高数据的存储速度和查找速度而设计的
        哈希表是人类的一种追求，人很难设计出完美的哈希表
        几乎所有的哈希表都会产生哈希冲突
        Java中是利用桶来解决哈希冲突的

        
```



#### 小结

```java
----------------------------------------------------------------------------------
1.框架图
Collection 接口
	List
		ArrayList
		LinkedList
		----------------------------------------------------------------------------------
		1.Collection接口中有一个方法iterator() 可以返回一个Iterator接口的对象It
			使用该对象的it.hasNext()来判断当前游标的后面还是否存在元素，如果存在返回直，否则返回假
			使用该对象的it.next()方法返回当前"游标"扫过的元素,如果不存在,抛出NoSuchElementException异常

		----------------------------------------------------------------------------------
		2."Collections类"中有很多静态方法,可以提供给List、ArrayList、LinkedList集合使用
			例如排序,倒置,复制,填充,二分查找【使用前先排序】
		----------------------------------------------------------------------------------




	Set
		HashSet -- 重写hashCode 、equals方法【性能优于TreeSet,排序除外】

		TreeSet -- 向此集合中添加的对象的"类"需要实现Comparable接口

	Map
		HashMap
		TreeMap
		----------------------------------------------------------------------------------
		    Object put(Object key, Object value)
		    Object get(Object key)//注意Map接口中并没有Object get(Object value)
		    boolean isEmpty()
		    void clear()
		    int size()
		    boolean containsKey(Object key)
		    boolean containsValue(Object value)

		keySet()
		返回此映射中所包含的键的 Set 视图。该 set 受映射的支持，所以对映射的更改将反映在该 set 中，
		反之亦然。如果在对 set 进行迭代的同时修改了映射(通过迭代器自己的 remove 操作除外)，则迭
		代结果是不确定的。该 set 支持元素的移除，通过 Iterator.remove、Set.remove、removeAll、
		retainAll 和 clear 操作可从该映射中移除相应的映射关系。它不支持 add 或 addAll 操作。
		----------------------------------------------------------------------------------


		两个程序【一部分】TestHashMap_1.java&TestHashMap_2.java
		----------------------------------------------------------------------------------
		HashMap hm = new HashMap();
		hm.put(1001, new Student(1001, "zhangsan", 20));  //自动封装
		hm.put(1003, new Student(1003, "lisi", 30)); //自动封装
		hm.put(new Integer(1004), new Student(1004, "wangwu", 10));
		hm.put(1002, new Student(1002, "baichi", 20)); //自动封装

		//遍历所有的元素
		System.out.println("hm容器中所有的元素是:");
		Set s = hm.keySet();  //获取到当前容器键的集合，实际就是Integer对象的集合
		Iterator it = s.iterator();
		while (it.hasNext()){
			//int Key = (Integer)it.next();   // (Integer) 不能省， 利用了自动拆分技术
			Integer Key = (Integer)it.next();
			System.out.println(hm.get(Key));
		}

		System.out.println("直接查找某一元素");
		System.out.println( hm.get(1003) );
		System.out.println( hm.get(1005) );	  //如果找不到 则直接返回null，而不是抛出异常
		----------------------------------------------------------------------------------
		Map m1 = new HashMap();
		m1.put("one", 1);
		m1.put("two", 2);
		m1.put("three", 3);
		System.out.println("1-> " + m1);
		System.out.println("2-> " + m1.size());
		m1.put(66.6, 'm');  //Map中键和值的类型是任意的，这也是Map强大的重要表现
		m1.put(123L, 34);
		System.out.println("3-> " + m1.size());
		System.out.println("4-> " + m1);

		System.out.println(m1.containsKey("three")); //true  ontainsKey 不要写成了containKey
		System.out.println(m1.containsValue(34));  //true
		System.out.println(m1.containsValue(123L));  //false
		----------------------------------------------------------------------------------


```


### 7> 泛型

#### 什么是泛型

##### 背景

```java
JAVA推出泛型以前，程序员可以构建一个元素类型为Object
的集合，该集合能够存储任意的数据类型对象，而在使用该集合的
过程中，需要程序员明确知道存储每个元素的数据类型，否则很容
易引发ClassCastExceptian异常。

ArrayList list = new ArrayList();
list.add("hello");
list.add(12);
list.add(true);

for(int i=0;i<list.size();i++)
{
    Object obj = list.get(i);
    String str = (String)obj;//当obj 为Integer对象时，抛出异常
    System.out.println(str);
}

```



##### 泛型的概念

```java
泛型的概念
Jeva泛型 (generics) 是JDK5中引入的一个新特性，泛型提供了编译时类型安全监测机制，
该机制允许我们在编译时检测到非法的类型数据结构。
泛型的本质就是"参数化类型"，也就是所操作的数据类型被指定为一个参数

```



##### 泛型的好处

```java
类型安全
消除了强制类型的转换
```



#### 泛型类、泛型接口

##### 泛型类

###### 1.泛型类的定义语法

```java
1.泛型类的定义语法
    class 类名 <泛型标识,泛型标识,...>
    {
        private 泛型标识 变量名;
        ..........
    }

    常用的泛型标识：T、E、K、V

E - Element (在集合中使用，因为集合中存放的是元素)
T - Type(Java 类)
K - Key(键)
V - Value(值)
N - Number(数值类型)
？ -  表示不确定的java类型
S、U、V  - 2nd、3rd、4th types
```

###### 2.泛型类的使用语法

```java

2.泛型类的使用语法 //泛型类在创建对象的时候，来指定操作的具体数据类型.
    1> 类名<具体的数据类型> 对象名  = new 类名<具体的数据类型>();

	2> Java1.7以后，"后面"的<>中的具体的数据类型可以省略不写
    	类名<具体的数据类型> 对象名= new 类名<>():
	3> 泛型类在创建对象的时候，没有指定类型，将按照Object类型来操作
    4> 泛型类不支持基本数据类型
	5> 同一泛型类，根据不同的数据类型创建的对象，本历上是同一类型
        【即：类类型】

举例：

    class Test <K,V>{
        private K name;
        private V age;

        public Test(K name, V age) {
            super();
            this.name = name;
            this.age = age;
        }

        @Override
        public String toString() {
            return "Test [name=" + name + ", age=" + age + "]";
        }
    }
    public class test_01 {

        public static void main(String[] args) {
        // TODO Auto-generated method stub
        Test<String,Integer> t1 = new Test<>("冰墩墩",21);
		System.out.println(t1);
		Test<String,Double> t2 = new Test<>("冰墩墩2",22.0);
		System.out.println(t2);
		//泛型类在创建对家的时候，没有指定类型，将按照Object类型来操作
		Test t3 = new Test("s",3);
		System.out.println(t3);
		//
		System.out.println(t1.getClass());
		System.out.println(t2.getClass());
		System.out.println(t1.getClass()==t2.getClass());
        }
    }
   //---------------运行结果： ---------------
   Test [name=冰墩墩, age=21]
    Test [name=冰墩墩2, age=22.0]
    Test [name=s, age=3]
    class 泛型.Test
    class 泛型.Test
    true


```



###### 从泛型类派生子类

```java
    子类也是泛型类，子类和父类的标识要一致,或子类中含有父类的泛型标识
        class ChildGeneric<T> extends Generic //此时父类默认 Object 类型
        class ChildGeneric<T> extends Generic<T>
        class ChildGeneric<T,K,V> extends Generic<T>
    子类不是泛型类，父类要明确泛型的数据类型
    	class ChildGeneric extends Generic<String>

```


#####  泛型接口

```java
泛型接口的定义语法
interface 接口名称 <泛型标识,泛型标识,...>
{
    泛型标识 方法名();
    ....

}
实现类不是泛型类，接口要明确数据类型
实现类也是泛型类，实现类和接口的泛型标识要一致,或实现类包含接口泛型标识
    //泛型接口
    interface GenericInterface <T>{
    	T getValue();
    }
    //泛型类
    class  TestGenic implements GenericInterface<String>{
    	@Override
    	public String getValue()
    	{

    		return "";
    	}
    }

    class TestGe <T,E> implements GenericInterface<T>{
    	@Override
    	public T getValue()
    	{
    		T a1 = null;
    		return a1;
    	}
    }
```



##### 泛型方法
```java
    1.
        泛型类,是在实例化类的时候指明泛型的具体类型
        泛型方法,是在调用方法的时候指明泛型的具体类型

    2.语法:
        修饰符 <T,E,...> 返回值类型 方法名(形参列表){
            方法体..
        }

    3.public与返回值中间<T>非常重要,可以理解为声明此方法为泛型方法

    4.只有声明了<T>的方法才是泛型方法,泛型类中的使用了泛型标识的成员方法
        并不是泛型方法

    5.  <T>表明该方法将使用泛型类型T，此时才可以在方法中使用泛型类型T

    6.与泛型类的定义一样,此处T可以随便写为任意标识，常见的如T、E、K、V等形
        式的参数常用于表示泛型

    7.泛型方法中泛型标识列表中的方法与泛型类的泛型列表无关

    8.非泛型类中可以含有泛型方法

    9.泛型方法可以设置为 static ,含泛型标识的非泛型方法不可声明为 static
        换句话说,如果static方法要使用泛型能力,就必须使其成为泛型方法


/**--------
拓展：
对象名getClass().getSimpleName()
可以达到查看此对象的类型
----------*/
//我看到的比较有意思的一个方法
    public <E> void print(E... e)
    {
        for(E e1:e){
            System.out.println(e);
        }
    }
```



#### 类型通配符

##### 什么是类型通配符
```java
    类型通配符一般是使用"?"代替具体的类实参
    所以,类型通配符是类型实参,而不是类型形参

    class Box <E>
    {
    	private E first;

    	public E getFirst() {
    		return first;
    	}

    	public void setFirst(E first) {
    		this.first = first;
    	}

    }


    class TestBox{
        public static void main (String [] args)
        {
            Box<Number> box1 = new Box<>();
            box1.setFirst(100);
            showBox(box1);


            Box<Integer> box2 = new Box<>();
            box2.setFirst(200);
            showBox(box2);//注意此处
            /**
            错误分析:
                按照我们通常的思维：Integer Extends Number
                根据多态的思想，此处是无法通过改变
                类型构成重载,若改成Object呢，也是不行的，
                因为和Number一样，都是继承【多态】的知识

            */
        }

    //    public static void showBox(Box<Number> box)
    //    {
    //        Number first = box.getFirst();
    //        System.out.println(first);
    //    }
        public static void showBox(Box<?>box) {

        }
      //  public static void showBox(Box<Integer> box)
       // {
          /**
          error
          分析：根据泛型的使用语法知识我们知道：

          >	5> 同一泛型类，根据不同的数据类型创建的对象，本历上是同一类型
          >【即：类类型】

             他们的本都是同一类型，即Box类类型,对于个数相同，类型相同的
             方法，他们是无法构成重载的
          */
    //    }
    }
```





##### 类型通配符的上限

```java

语法
    类/接口 <? extends 实参类型>

    要求该泛型的类型，只能是实参类型，或实参类型的子类类型
    "重点：类型通配符的上限 list 是无法添加元素的,即使你的格式是正确的"
    例如:现在有
        Animals
        Cat extends Animals
        MinCat extends Cat

    public static void main (String []args){
        ArrayList<Animals> animals = new ArrayList<>();
        ArrayList<Cat> cat = new ArrayList<>();
        ArrayList<MinCat> mincat = new ArrayList<>();

        //showAnimal(animals);//error
        showAnimal(cat);//true
        showAnimal(mincat);//true

    }
    有一方法：
//1.泛型上限通配行，传递的集合类型，只能是Cat 或Cat的子类类型

    public static void showAnimal(ArrayList<? extends Cat> list){//类型通配符的上限为Cat
/*
"重点：类型通配符的上限 list 是无法添加元素的,即使你的格式是正确的"
list.add(new Cat());//error

解释：使用上限通配符，无法确定当前类型，比如当前类型为MinCat ,
            但你对list中添加 new Cat()明显这是不正确的就，也是解释不通的
*/
    }


对于addAll()方法，也遵循这样的规律：
当A被B继承,B被C继承
当B 创建对象时，b.addAll(t);
//则t只能是 b对象 或者是 c对象
```


##### 类型通配符的下限

```java

```




### 8>网络编程基础

#### 基本概念

```java
1.网络程序
    能够"接受另一台计算机发送过来的数据"或者能够"向另一台计算机发送数据"的
    程序叫做网络程序

2.IP:
能够在网络中唯一标示一台主机的编号就是IP
网络中每台主机都必须有一个惟一的IP地址;
IP地址是一个逻辑地址;
因特网上的IP地址具有全球唯一性;
32位，4个字节，常用点分十进制的格式表示，例如:192.168.0.16

```







### 9>Object

#### toString

```java

1.所有的类都默认自动继承了Object类
2.Object类中的toString方法返回的是类的名字和该对象哈希码组成的一个字符串 
3.System.out.println(类对象名)；
    实际输出的是该对象的toString()方法所返回的字符串
    calss A
    {
    }
    public class TestA
    {
        public static void main (String []args)
        {
            A aa = new A();
            System.out.println(aa);
            //等价于System.out.println(aa。toString());
        }
    }
    /*
    运行结果：A@de6ced 
    类名@aa对象保存地址十六进制
    */
4.为了实际需要，建议子类重写父类Object继承的toString方法
    public String toString (){
        
    }
+-------------------------------------------------+
对任意类A，假设aa是该A类的一个实例
System.out.println(aa); 等价于System.out.println(aa.toString());
Object 类中含有 toString方法
Java中所有的类默认都继承了Object的toString方法
建议所有的子类都重写toString方法         
+-------------------------------------------------+
eclipse 重写toString()快捷键
光标停在在需要重写的类中，Alt + Shift + S
Generate toString()

                     
                     
```

#### equals

```java
1.所有的类都从Object类中继承了equals方法
2.Object类中equals方法源代码：     
  public boolean equals(Object obj)
        {
                return this == obj;
        }
3.如果是同一块内存，则Object中的equals方法返回true，如果是不同的内存，则返回false
4.如果希望不同内存，但相同内容的两个对象，调用equals时返回true,则我们需要重写父类的
  equals方法

5.重写代码：
class A
{
	int i;
	public N(int i)
	{
		this.i = i;
	}
	public boolean equals(Object obj)
	{
		aa = (A)obj;
		if(this.i==aa.i)
			return true;
		else
			return false;
	}

}
	
public class Equals_1 {
	
	public static void main (String []args)
	{
		A aa = new N(2);
		A bb = new N(2);
		System.out.printf("%b \n",aa.equals(bb));
	}
}
6.注意：String中的equals方法已经被重写了
    String str1 = "abc";
    String str2 = "abc";
    str.equals(str2);//返回结果为 true
【同样的软件自带的类中的equals全部重写了】
```




#### 字符串比较 

```java

Java字符串比较(3种方法)以及对比 C++ 时的注意项
字符串比较是常见的操作，包括比较相等、比较大小、比较前缀和后缀串等。在 Java 中，比较字符串的常用方法有 3 个：equals() 方法、equalsIgnoreCase() 方法、 compareTo() 方法。

其中最常用的是 equals() 方法，下面详细介绍这 3 个方法的使用。

equals() 方法
equals() 方法将逐个地比较两个字符串的每个字符是否相同。如果两个字符串具有相同的字符和长度，它返回 true，否则返回 false。对于字符的大小写，也在检查的范围之内。equals() 方法的语法格式如下：

str1.equals(str2);
str1 和 str2 可以是字符串变量， 也可以是字符串字面量。 例如， 下列表达式是合法的：

"Hello".equals(greeting)
下面的代码说明了 equals() 方法的使用：

String str1 = "abc";
String str2 = new String("abc");
String str3 = "ABC";
System.out.println(str1.equals(str2)); // 输出 true
System.out.println(str1.equals(str3)); // 输出 false
例 1
在第一次进入系统时要求管理员设置一个密码，出于安全考虑密码需要输入两次，如果两次输入的密码一致才生效，否则提示失败。具体实现代码如下：

public static void main(String[] args) {
    String sys = "学生信息管理";
    System.out.println("欢迎进入《" + sys + "》系统");
    System.out.println("请设置一个管理员密码：");
    Scanner input = new Scanner(System.in);
    String pass = input.next(); // 设置密码
    System.out.println("重复管理员密码：");
    input = new Scanner(System.in);
    String pass1 = input.next(); // 确认密码
    if (pass.equals(pass1)) { // 比较两个密码
        System.out.println("已生效，请牢记密码：" + pass);
    } else {
        System.out.println("两次密码不一致，请重新设置。");
    }
}
运行该程序，由于 equals() 方法区分大小写，所以当两次输入的密码完全一致时，equals() 方法返回 true，输出结果如下所示：

欢迎进入《学生信息管理》系统
请设置一个管理员密码：
abcdef
重复管理员密码：
abcdef
已生效，请牢记密码：abcdef
否则输出如图下所示的结果：

欢迎进入《学生信息管理》系统
请设置一个管理员密码：
abcdef
重复管理员密码：
aBcdef
两次密码不一致，请重新设置。
equalsIgnoreCase() 方法
equalsIgnoreCase() 方法的作用和语法与 equals() 方法完全相同，唯一不同的是 equalsIgnoreCase() 比较时不区分大小写。当比较两个字符串时，它会认为 A-Z 和 a-z 是一样的。

下面的代码说明了 equalsIgnoreCase() 的使用：

String str1 = "abc";
String str2 = "ABC";
System.out.println(str1.equalsIgnoreCase(str2));    // 输出 true
例 2
在会员系统中需要输入用户名和密码进行检验，下面使用 equalsIgnoreCase() 方法实现检验登录时不区分用户名和密码的大小写，具体的代码实现如下所示。

public static void main(String[] args) {
    String sys = "学生信息管理";
    System.out.println("欢迎进入《" + sys + "》系统");
    System.out.println("请输入管理员名称：");
    Scanner input = new Scanner(System.in);
    String name = input.next(); // 获取用户输入的名称
    System.out.println("请输入管理员密码：");
    input = new Scanner(System.in);
    String pass = input.next(); // 获取用户输入的密码
    // 比较用户名与密码，注意此处忽略大小写
    if (name.equalsIgnoreCase("admin") && pass.equalsIgnoreCase("somboy")) { // 验证
        System.out.println("登录成功。");
    } else {
        System.out.println("登录失败。");
    }
}
在上述代码中，由于使用 equalsIgnoreCase() 方法进行比较，所以会忽略大小写判断。因此输入 ADMIN 和 SOMBOY 也会验证通过，如下所示：

欢迎进入《学生信息管理》系统
请输入管理员名称：
ADMIN
请输入管理员密码：
SOMBOY
登录成功。
否则输出结果如下所示：

欢迎进入《学生信息管理》系统
请输入管理员名称：
admin
请输入管理员密码：
sommboy
登录失败。
equals()与==的比较
理解 equals() 方法和==运算符执行的是两个不同的操作是重要的。如同刚才解释的那样，equals() 方法比较字符串对象中的字符。而==运算符比较两个对象引用看它们是否引用相同的实例。

下面的程序说明了两个不同的字符串(String)对象是如何能够包含相同字符的，但同时这些对象引用是不相等的：

String s1 = "Hello";
String s2 = new String(s1);
System.out.println(s1.equals(s2)); // 输出true
System.out.println(s1 == s2); // 输出false
变量 s1 指向由“Hello”创建的字符串实例。s2 所指的的对象是以 s1 作为初始化而创建的。因此这两个字符串对象的内容是一样的。但它们是不同的对象，这就意味着 s1 和 s2 没有指向同一的对象，因此它们是不==的。

因此，千万不要使用==运算符测试字符串的相等性，以免在程序中出现糟糕的 bug。从表面上看，这种 bug 很像随机产生的间歇性错误。

对于习惯使用 C++ 的 String 类的人来说，在进行相等性检测的时候一定要特别小心。C++ 的 String 类重载了==运算符以便检测字符串内容的相等性。可惜 Java 没有采用这种方式，它的字符串“看起来、感觉起来”与数值一样，但进行相等性测试时，其操作方式又类似于指针。语言的设计者本应该像对 C++ 那样也进行特殊处理， 即重定义==运算符。

当然，每一种语言都会存在一些不太一致的地方。C 程序员从不使用==对字符串进行比较，而使用 strcmp 函数。Java 的 compareTo 方法与 strcmp 完全类似。所以下面我们来介绍 Java 的 compareTo 方法。

compareTo() 方法
通常，仅仅知道两个字符串是否相同是不够的。对于排序应用来说，必须知道一个字符串是大于、等于还是小于另一个。一个字符串小于另一个指的是它在字典中先出现。而一个字符串大于另一个指的是它在字典中后出现。字符串(String)的 compareTo() 方法实现了这种功能。

compareTo() 方法用于按字典顺序比较两个字符串的大小，该比较是基于字符串各个字符的 Unicode 值。compareTo() 方法的语法格式如下：

str.compareTo(String otherstr);
它会按字典顺序将 str 表示的字符序列与 otherstr 参数表示的字符序列进行比较。如果按字典顺序 str 位于 otherster 参数之前，比较结果为一个负整数；如果 str 位于 otherstr 之后，比较结果为一个正整数；如果两个字符串相等，则结果为 0。

提示：如果两个字符串调用 equals() 方法返回 true，那么调用 compareTo() 方法会返回 0。

例 3
编写一个简单的 Java 程序，演示 compareTo() 方法比较字符串的用法，以及返回值的区别。代码如下：

public static void main(String[] args) {
    String str = "A";
    String str1 = "a";
    System.out.println("str=" + str);
    System.out.println("str1=" + str1);
    System.out.println("str.compareTo(str1)的结果是：" + str.compareTo(str1));
    System.out.println("str1.compareTo(str)的结果是：" + str1.compareTo(str));
    System.out.println("str1.compareTo('a')的结果是：" + str1.compareTo("a"));
}
上述代码定义了两个字符串“A”和“a”，然后调用 compareTo() 方法进行相互比较。最后一行代码拿“a”与“a”进行比较，由于两个字符串相同比较结果为 0。运行后的输出结果如下：

str = A
str1 = a
str.compareTo(str1)的结果是：-32
str1.compareTo(str)的结果是：32
str1.compareTo('a')的结果是：0

```



#### String

##### string的equals
```java 
1. str1 ==  str2 
	用来比较str1变量本身所占内存的值和str2变量本身所占内存的值是否相等
        1>  String str1 = "hello";
            String str2 = "hello";  //str1 和 str2 都指向了匿名对象"hello"
        2>
            String str3 = new String("hello");  //str3 和 str4 很明显指向的是不同的对象
            String str4 = new String("hello");
2.str3.equals(str4)
        1> 是用来比较str1变量本身所占内存的值所指向的对象和str2变量本身
	       
           所占内存的值所指向的对象的内容是否相等
	       也就是说如果str1和str2占用不同的内存，但是这两个不同内存的值是一样的，
	       Stirng.equals()方法也会返回true.

        2> 但是Object中的equals()方法却是返回false,Object类中的Equals方法
	       Object中就含有equals()方法，不过String类重写了Object中的equals()方法
3.内存分配空间：
        1>普通属性：自身所占用的空间在堆(heap)中

        2>局部变量：自身所占用的空间在栈(stack)··

        3>静态变量、字符串常量······数据段(data segment)
                str1 与str2 在堆中分配，而"hello"这个字符串在数据段中分配，并且在数据段中只有一份"hello"的拷贝，由str1 与str2共用，即str1与str2都存放"hello"的地址，都指向"hello"这个字符串。

        /*
            在JDK 1.8中的运行结果是： 
        -------------------------------
        str1 == str2
        str3 != str4
        str3.equals(str4) == true
        -------------------------------
        */
        我的总结：
        1. String str1 = "hello"; // 数据类型 变量名 = "赋值内容"; 
        2. String str3 = new String("hello"); // 类名 对象名 = new 类名(" ") 
        3. str3.equals(str4) //调用已经改写后的equals方法
```
##### String类的常用方法
```java
1.  public char charAt(int index) 返回字符串中第index个字符。
             1>  String str = "hello";
            		char ch = str.charAt(1);
            2> 从零开始，例如上面的结果是'e'
    public int s.length() 返回字符串的长度
    public int indexOf(String str2) 
                1>.返回字符串中出现str的第一个位置
                2>.s1.indexOf(s2),返回s2在s1中的位置
                3>初始值为-1，从零开始计数
                String str = "ABCDEFGHIG";
				System.out.printf("%d\n",str.indexOf("A"));//运行结果：0	
    public int indexOf(String str2,int fromIndex)
                2>str1.indexOf(str2,fromIndex)
                1>返回从fromIndex开始,str中出现str2的第一个位置
                               
    public boolean equalsIgnoreCase(String another)
                比较字符串与another是否一样(忽略大写)
    public String replace(char oldchar,chat newchat)
                在字符串中用newchar字符替换oldchar字符

2.静态重载方法
public static String valueOf()//可将基本类型数据转换为字符串
    举例：public static String valueOf(int i)

```

#### StringBuff
##### StringBuff的由来
```java
1.String类对象一旦创建就不可更改
2.如果经常对字符串内容进行修改，则使用StringBuffer.
3.如果经常对字符串内容进行修改而使用String的话，就会导致即耗空间又耗时间!
    例子：
        String s1=“abasdmasc";
        String str2="123";
        String s1=s1+s2;
        删除str1中的字母d
4.StringBuffer对象的内容是可以改变的
5.String类中没有修改字符串的方法，但是StringBuffer类中却有大量修改字符串的方法

```
##### StringBuff构造函数
```java
public StringBuffer()
创建一个空的没有任何字符的StringBuffer对象
public StringBuffer(int capacity)
创建一个不带字符，但具有指定初始容量的字符串缓冲区。
public
StringBuffer(String str)
创建一个StringBuffer对象，包含与str对象相同的字符序列
```
##### StringBuff举例
```java
public class TestStringBuffer
{
        public static void main(String[] args)
        {
            StringBuffer sb = new StringBuffer();
            sb.append("abc");
            sb.append("123");
            System.out.println("sb = " + sb); //sb = abc123
            sb.insert(3, "--");
            System.out.println("sb = " + sb); //sb = abc--123
            sb.delete(2,6); //把下标从2开始到6-1结束的字符删除
            System.out.println("sb = " + sb); //sb = ab23
            sb.reverse();
            System.out.println("sb = " + sb); //sb = 32ba
            String str = sb.toString();
            System.out.printf("str = " + str); //str = 32ba
        }
}

```





### 10>枚举
##### 基本概念
```java
1.为什么需要枚举
          我的理解，但逻辑上输入不合法的问题

2.定义：
          枚举指一组固定的"常量"组成的"类型"

3.使用：
          [访问控制符] enum 枚举名{
                    常量值,常量值
          }

          例如：
          enum Genders{
          	男,女
          }
          class Student {
          	Genders sex;

          }
          public class ENUM {

          	public static void main(String[] args) {

          		Student stu = new Student();
          		stu.sex = Genders.女;
          		System.out.println(stu.sex);
          		stu.sex = Genders.valueOf("男");
          		System.out.println(stu.sex);
          		stu.sex = Genders.valueOf("nv");//无枚举常量,抛出IllegalArgumentException异常
          	}
          }
          /*
          女
          Exception in thread "main" 男
          java.lang.IllegalArgumentException: No enum constant 枚举.Genders.nv
          	at java.lang.Enum.valueOf(Unknown Source)
          	at 枚举.Genders.valueOf(ENUM.java:1)
          	at 枚举.ENUM.main(ENUM.java:19)
          */

4.枚举的好处:
          类型安全
          易于输入
          代码清晰

5.实战演练：
          根据用户输入今天星期几，对用户一周做的事情做提示

          1>我写的：
              enum Week{//注解①
              一,二,三,四,五,六,日
          }
        class ToDo
        {
            Week today;

            public  ToDo(String  week){
                try{
                    this.today = Week.valueOf(week);
                }catch(IllegalArgumentException e){
                    System.out.println("No enum constant");
                    System.exit(-1);//退出
                }
                if(today==Week.一||today==Week.二||today==Week.三
                   ||today==Week.四||today==Week.五)
                    System.out.println("上班");
                else
                    System.out.println("休息");
            }
        }

        public class Enum_Exercise01 {

            public static void main(String[] args) {
                // TODO Auto-generated method stub
                ToDo todo = new ToDo("一");
            }


          2>老师写的：
                   使用switch  case 语句          
              	   JDK7以后，switch已经支持 int、char、String、enum 类型的参数

/**
 注解①：

     疑问：此处为什么加public 会报错
          查找enum 的本质是什么,感觉像是一种特殊的类
          所以使用 public 会与主类冲突

          枚举类和普通类的区别是什么：
          a. 使用enum定义的枚举类默认继承了java.lang.Enum类；
          b. 枚举类的构造器只能使用private访问控制符；
          c. 枚举类的所有实例必须在枚举类中显式列出(, 分隔 ;结尾)。
                   列出的实例系统会自动添加public static final修饰；
         【增加：】java中枚举都继承自java.lang.Enum类，所以枚举类不能继承别的类，但是可以实现接口

		 原文链接：https://blog.csdn.net/Mind_programmonkey/article/details/117200105

*/
          https://www.cnblogs.com/happyPawpaw/archive/2013/04/09/3009553.html
          https://www.cnblogs.com/fantyovo/p/14769799.html?ivk_sa=1024320u

```

 




### 11>包装类

```java
1.包装类及其作用
  Object：
      Boolean
      Number :Byte Short  Integetr Long Float Double等
      Character

  作用：
      提供了一系列实用的方法
      "集合不允许存放基本数据类型,存放数字时,要使用包装类型"
      /**
      import java.util.ArrayList;
      import java.util.List;

      List list = new ArrayList();
      list.add(Object);
      */

  使用：
    1]以每个包装类对应的某本数据类型作为参数
    //基本教据类型-->包装类
          double d = 88;
		  Double D = new Double(d);

     2]除Character以外，以字符串作为参数
         Double D = new Double("87.9");
		 System.out.println(D+1);//是88.9,不是87.91

     3] 注意：
         1.Character传参使用''
         2.对于布尔类型数据,若"使用字符串传参"
         	1>内容只要是true/false 即可,不区分大小写
         		Boolean b = new Boolean("TrUe");
				System.out.println(b);//true

			2>内容若不是true/false 则结果显示false
    			Boolean b = new Boolean("hello");
				System.out.println(b);//false
				/**Boolean(String s)源码
                   public Boolean(String s) {
                          this(parseBoolean(s));
                    }

                    public static boolean parseBoolean(String s) {
                       return ((s != null) && s.equalsIgnoreCase("true"));
                                      }
                   */

2.包装类的常用方法
          1>...value() 包装类转换成"基本类型"
                    byteValue()、shortValue()、intValue()等8种方法

                    Integer integer = new Integer(25);
                    int i =  integer.intValue();

          2> Type.toString() 以字符串形式返回包装对象表示的基本类型数据("基本类型->字符串")
                    String sex=Character.toString('男');
                    String id = Integer.toString(25);
                    /**还是那句话:由Oracle公司提供的可以重写toString的类都重写了toString方法
                    【几乎所有】
                        源码举例：
                        public static String toString(char c) {
                            return String.valueOf(c);
                        }
                    */
                    最常用的还是String str = Type + "";

          3> parse...() 除了Character,把字符串转换为相应的基本数据类型数据
                    int num=Integer.parselnt("36");
                    boolean bool=Boolean.parseBoolean("false");

          4> valueOf()Character,把字符串转换为相应包装类
                    String f1ag = "china";
                    Boolean bFlag = Boolean.valueOf(f1ag);
                    System.out.println(bFlag);//false

                    /**
                        public static Boolean valueOf(String s) {
                            return parseBoolean(s) ? TRUE : FALSE;
                        }
                    */

/**
eclips快捷键：
1.:Alt + Shift + s
    构造方法：Generate Canstructor using Fields.

查看源码：
    ctr+shift+t：快速找到某个类
    ctr+t:查看当前类的子类

*/
```




### 11>正则表达式

#### (1)为什需要正则表达式?

```java

      |-- 1.正则表达式应用场景
            文本编辑器的搜索
            登录网站、输入密码时的验证
            判断是否是微信号、手机号、邮箱、纯数字
            ....

      |-- 2.概念
            正则表达式是对字符串操作的一种逻辑公式，
            就是用事先定义好的一些特定字符、及这些特定字符的组合，
            组成一个“规则字符串”，这个“规则字符串”用来表达对字符串的一种"过滤逻辑"

            /*MyNote：
            字符串的格式匹配 -- 用特殊的字符串A 去匹配字符串B【C、D 】
            */

      |-- 3.起源
            正则表达式实际上是一门独立的学科，大部分编程语言都支持正则表达式。
            //但每种语言的正则表达式之间有细微的差别
            正则表达式最初使用在"医学"方面，用来表示神经符号等。目前使用最多
		      的是计算机编程领域，用作字符串格式匹配。包括搜索方面等。

           [百度百科](https://baike.baidu.com/item/正则表达式)

      |-- 4.特点
           1-灵活性、逻辑性和功能性非常的强；
           2-可以迅速地用极简单的方式达到字符串的复杂控制。
           3-对于刚接触的人来说，比较晦涩难懂。

```



#### (2)正则表达式在"java"中的语法

```java
      |-- 1.java.util.regex 包主要包括以下三个类：
            ->Pattern 类：【模式类】
                  pattern 对象是一个正则表达式的编译表示。Pattern 类没有公共构造方法。
                  要创建一个 Pattern 对象，你必须首先调用其公共静态编译方法，它返回一个 Pattern 对象。
                  该方法接受一个正则表达式作为它的第一个参数。

            ->Matcher 类：【匹配器类】
                  Matcher 对象是对输入字符串进行解释和匹配操作的引擎。
                  与Pattern 类一样，Matcher 也没有公共构造方法。
                  你需要"调用 Pattern 对象"的 matcher 方法来获得一个 Matcher 对象

            ->PatternSyntaxException：【异常类】
                  PatternSyntaxException 是一个非强制异常类，它表示一个正则表达式模式中的语法错误。

          "  注意: 正则表达式写好后，没有错对之分，返回结果只是true和false"

```



#### (3)如何使用正则表达式

```java
      |-- 1.案例分析:
                  //内容
                  Stringcontent="1998这是一2188个字符串123heihei空间！@8976与777好8888YU";
                  String regstr="\\d\\d\\d\\d";
                  //2创建模式对象[即正则表达式对象]
                  Pattern pattern=Pattern.compile(regstr);
                  //3.创建匹配器
                  //说明:创建匹配器matcher，按照正则表达式的规则去匹配content字符串
                  Matcher m=pattern.matcher(content);
                  //4.开始匹配
                  while(m.find()){
                  System.out.println("Find:"+m.group(0));}


      |-- 2.深入了解：
            ->m.find()完成的操作以及group[0]的含义
                  1.根据指定的规则,定位满足规则的子字符串(比如1998)
                  2.找到后，将子字符串的开始的索引记录到Matcher对象m的属性int[] groups;
                        groups[0] = 0 ,把该子字符串的结束的索引+1的值记录到groups[1] = 4
                  3.同时记录oldLast的值为子字符串的结束的索引+1的值即4， 即下次执行find时，就从4开始匹配

            ->源码
                  /**
                  源码:
                         public String group(int group) {
                                if (first < 0)
                                    throw new IllegalStateException("No match found");
                                if (group < 0 || group > groupCount())
                                    throw new IndexOutOfBoundsException("No group " + group);
                                if ((groups[group*2] == -1) || (groups[group*2+1] == -1))
                                    return null;
                                return getSubSequence(groups[group * 2], groups[group * 2 + 1]).toString();
                            }
                  */

           ->分析matcher.group(0)执行操作
                        String content = "1998这是一2188个字符串123heihei空间！@8976与777好8888YU";

                        【非分组情况：String regstr = "\\d\\d\\d\\d";】
                              第一次：
                                  根据groups[0]=0,groups[1] = 4 ,对[0,4)的位置进行截取返回 ->1998
                              第二次：
                                根据groups[0]=7,groups[1] = 11 ,对[0,11)的位置进行截取返回->2188
                                //注意此时下标任然是0,1但所针对范围改变
                        |---------------------------------------------------------------------------
                        第一个()为第一组,第二个()为第二组,以此类推
                              String content = "1998这是一2188个字符串123heihei空间！@8976与777好8888YU";
                              String regstr = "(\\d\\d)([a-zA-z]+)";
                              //2创建模式对象[即正则表达式对象]
                              Pattern pattern = Pattern.compile(regstr);
                              //3.创建匹配器
                              //说明:创建匹配器matcher， 按照 正则表达式的规则去匹配 content字符串
                              Matcher m = pattern.matcher(content);
                              //4.开始匹配
                              while (m.find()) {
                              System.out.println("Find: 0->" + m.group(0));
                              System.out.println("Find: 1->" + m.group(1));
                              System.out.println("Find: 2->" + m.group(2));
                              //System.out.println("Find: 3->" + m.group(3));//异常，下标越界 java.lang.IndexOutOfBoundsException: No group 3
                              }
                              /*---------------------
                              运行结果：
                                    Find: 0->23heihei
                                    Find: 1->23
                                    Find: 2->heihei
                                    Find: 0->88YU
                                    Find: 1->88
                                    Find: 2->YU

                                    分析23heihei
                                    groups[0]:16    groups[1]:24
                                    groups[1]:16    groups[1]:18
                                    groups[2]:18    groups[2]:24

                                    分析:88YU
                                    groups[0]:39    groups[1]:43
                                    groups[1]:39    groups[1]:41
                                    groups[2]:41    groups[2]:43
                              ---------------------*/



```



#### (4)正则表达式--元字符

```java
      |-- 1.转义号\\
            ->说明:在我们使用正则表达式去检索某些特殊字符的时候，需要用到转义符号，否
                        则检索不到结果，甚至会报错的。
                        案例:用$去匹配"abc$(" 会怎样?
                                    用(去匹配"abc$(" 会怎样?

            ->注意：【菜鸟教程】
                  在其他语言中，\\ 表示：我想要在正则表达式中插入一个普通的(字面上的)反斜杠，请不要给它任何特殊的意义。
                  在 Java 中，\\ 表示：我要插入一个正则表达式的反斜线，所以其后的字符具有特殊的意义。
                  所以，在其他的语言中(如 Perl)，一个反斜杠 \ 就足以具有转义的作用，而在 Java 中正则表达式中则需要有
                  两个反斜杠才能被解析为其他语言中的转义作用。也可以简单的理解在 Java 的正则表达式中，
                " 两个 \\ 代表其他语言中的一个 \，这也就是为什么表示一位数字的正则表达式是 \\d，而表示一个普通的反斜杠是 \\"
                  /**MyNote:
                        简来说就是在java正则表达式中  "\\" 表示 请注意,我后面的是有特殊意义的字符了,例如：\\$
                  */

            ->常见的需要使用转义的字符
                        /      \      ()      []      {}

                        .      ?      $      *      +  ^

            注意："[]内的特殊字符不需要转义，他就代表普通字符"
      |-- 2.字符匹配符
            -> ----------------------------------------------------------------------------------------
                  [] -  ^      【列表、范围、反】
                  [xyz]      字符集。匹配包含的任一字符。例如，"[abc]"匹配"plain"中的"a"。
                  [^xyz]    反向字符集。匹配未包含的任何字符。例如，"[^abc]"匹配"plain"中"p"，"l"，"i"，"n"。
                  [a-z]      字符范围。匹配指定范围内的任何字符。例如，"[a-z]"匹配"a"到"z"范围内的任何小写字母。
                  [^a-z]    反向范围字符。匹配不在指定的范围内的任何字符。例如，"[^a-z]"匹配任何不在"a"到"z"范围内的任何字符。

            -> ----------------------------------------------------------------------------------------
                  .       任意字符     '\n'除外
                  \\d       数字[0-9]
                  \\D      非数字[^0-9]
                  \\w       数字、大小写字母、下划线[A-Za-z0-9_]//顺序也变,即：[0-9A-Za-z_]、[_a-zA-Z0-9]等表达相同含义
                  \\W      不是w匹配的内容[^A-Za-z0-9_]
                  \\s       空白字符
                  \\S      非空白字符
            ->----------------------------------------------------------------------------------------
                  (?i) 不区分大小写
                              "(?i)abc"      abc不区分大小写      可以匹配abc、ABC、Abc、aBc等
                              "a(?i)bc"      bc不区分大小写
                              "a((?i)b)c" 只有b不区分大小写
                              Pattern pattern = Pattern.compile(regstr,Pattern.CASE_INSENSITIVE);//不区分大小写

            ->----------------------------------------------------------------------------------------


      |-- 3.选择匹配符
                  | 或        例如："Ab|ac" 匹配Ab ac

      |-- 4.限定符:用于指定其前面的字符和组合项连续出现多少次
                  *            指定字符重复次数无要求
                  +            1次起步                            例如：m+(abc)+        以至少1个m开头，后接任意个abc的字符串-mmabc、mabcabc
                  ?            0-1
                  {n}       只能是n次
                  {n,}      n次起步
                  {n,m}    n-m次//注解①
                                    /**MyNote :
                                          注解①：java 匹配默认是贪婪匹配，即尽可能匹配长的
                                                      String content = "aaaaaa";
                                                      String regstr = "{3,4}";
                                                      结果为aaaa
                                                      匹配了一个aaaa ,不够在匹配一个aaa
                                    */
      |-- 5.定位符
                  ^      指定起始字符
                  $      指定结束字符
                  \\b 匹配目标字符串的边界：空格前、字符串的结尾
                              he\\b      ->hehu'he'    ss'he'-<有颜色表示匹配到
                  \\B 与\\b相反

      |-- 6.非贪婪匹配【?】
                  当此字符紧随任何其他限定符(*、+、?、{n}、{n,}、{n,m})之后时，匹配模式是"非贪心的"。
                  "非贪心的"模式匹配搜索到的、尽可能短的字符串，而默认的"贪心的"模式匹配搜索到的、尽可能长的字符串。
                  例如，在字符串"oooo"中，"o+?"只匹配单个"o"，而"o+"匹配所有"o"



      |-- 6.分组捕获
            ->非命名分组
                  String regStr = "(\\d\\d)(\\d)"
            ->命名分组
                  (?<组名>表达式)
                        组名不能包含任何标点符号，并且不能以数字开头。可以使用单引替代尖括号

                        String regStr = "(?<group1>\\d\\d)(?<group2>\\d)"
                        ...
                        System.out.println("Find: 0->" + m.group(1));
                        或
                        System.out.println("Find: 0->" + m.group("group2"));

      |-- 7.非捕获分组
                  (?:pattern)
                        匹配 pattern 但不捕获该匹配的子表达式，即它是一个非捕获匹配，不存储供以后使用的匹配。
                        这对于用"or"字符 (|) 组合模式部件的情况很有用。
                        例如，'abcd(?:A|B|C)'是比 'abcdA|abcdB|abcdC' 更经济的表达式
                        //MyNote：需要注意的是该方法并不是真正意义上的分组,所以只能使用m.group(0)获取结果

                  (?=pattern)例如：'Windows (?=95|98|NT|2000)' 匹配"Windows 2000"中的"Windows"，但不匹配"Windows 3.1"中的"Windows"。

                  (?!pattern)例如：'Windows (?!95|98|NT|2000)' 匹配"Windows 3.1"中的 "Windows"，但不匹配"Windows 2000"中的"Windows"







/**MyNote:**
            w,Word,单词.\w匹配包括下划线的任何单词字符.等价于'[A-Za-z0-9_]'
            s,Space,空白,空格.\s匹配任何空白字符,包括空格、制表符、换页符等等.等价于 [ \f\n\r\t\v]
            b,boundary,边界,界限.\b匹配一个单词边界,就是...比如've\b',可以匹配love里的ve而不匹配very里有ve
            d,Digital,数字的.\d匹配一个数字字符.等价于 [0-9]
            r,return,回车.\r匹配一个回车符.等价于 \x0d 和 \cM
            t,tabulator key,制表符.匹配一个制表符.等价于 \x09 和 \cI
            v,Vertical,垂直(制表符)匹配一个垂直制表符.等价于 \x0b 和 \cK
            u,Unicode,Unicode字符
            c,Control,控制
            f,Form-feed,换页
            n,liNe feed.换行
            Num,数字(正整数)
            x,heX,十六进制
*/




```



### 12>反射机制

![](./attachments/Snipaste_2022-08-04_15-44-14.jpg)

![](./attachments/Snipaste_2022-08-05_11-09-55.jpg)


![](./attachments/Snipaste_2022-08-05_11-11-27.jpg)


```java
反射机制

1、概念:
	加载完类之后，在堆中就产生了一个Class类型的对象(一个类只有一个Class对象)，
	这个对象包含了类的完整结构信息。通过这个对象得到类的结构。这个Class对象就像一面
	镜子，透过这个镜子看到类的结构，所以，形象的称之为：反射
2、优点:
	可以动态的创建和使用对象(也是框架底层核心)，使用灵活，没有反射机制，框架技术就失去底层支撑。
3、缺点：
	使用反射基本是解释执行，对执行速度有影响.


4、优化/暴破
	Method和Field，Constructor对象都有setAccessible()方法
	setAccessible作用是启动和禁用访问安全检查的开关
	参数值为true表示反射的对象在使用时取消访问检查，提高反射的效率。
	参数值为false则表示反射的对象执行访问检查

	使用:
	在拿到后对象进行设置
	例如         fieldName.setAccessible(true);


-----


//3.使用反射机制解决
//(1)加载类，返回Class类型的对象
	cls Class cls = Class.forName(classfullpath);
//(2)通过cls 得到你加载的类com.hspedu.Cat 的对象实例
	Object o = cls.newInstance();

//(3)通过cls 得到你加载的类com.hspedu.Cat 的methodName"hi"的方法对象11即：在反射中，可以把方法视为对象(万物皆对象)
	Method method1 = cls.getMethod(methodName)；
//(4)通过method1 调用方法：即通过方法对象来实现调用方法
	System.out.println(method1.invoke(o));
	//传统方法 对象.方法()，反射机制 方法.invoke(对象)

```








```java
2、反射机制(比较简单，因为只要会查帮助文档，就可以了。)

	2.1、反射机制有什么用？
		通过java语言中的反射机制可以操作字节码文件。
		优点类似于黑客。(可以读和修改字节码文件。)
		通过反射机制可以操作代码片段。(class文件。)

	2.2、反射机制的相关类在哪个包下？
		java.lang.reflect.*;

	2.3、反射机制相关的重要的类有哪些？

		java.lang.Class：代表整个字节码，代表一个类型，代表整个类。

		java.lang.reflect.Method：代表字节码中的方法字节码。代表类中的方法。

		java.lang.reflect.Constructor：代表字节码中的构造方法字节码。代表类中的构造方法

		java.lang.reflect.Field：代表字节码中的属性字节码。代表类中的成员变量(静态变量+实例变量)。

		java.lang.Class：
			public class User{
				// Field
				int no;

				// Constructor
				public User(){

				}
				public User(int no){
					this.no = no;
				}

				// Method
				public void setNo(int no){
					this.no = no;
				}
				public int getNo(){
					return no;
				}
			}

1、回顾反射机制

	1.1、什么是反射机制？反射机制有什么用？
		反射机制：可以操作字节码文件
		作用：可以让程序更加灵活。

	1.2、反射机制相关的类在哪个包下？
		java.lang.reflect.*;

	1.3、反射机制相关的主要的类？
		java.lang.Class
		java.lang.reflect.Method;
		java.lang.reflect.Constructor;
		java.lang.reflect.Field;

	1.4、在java中获取Class的三种方式？
		第一种：
			Class c = Class.forName("完整类名");
		第二种：
			Class c = 对象.getClass();
		第三种：
			Class c = int.class;
			Class c = String.class;

	1.5、获取了Class之后，可以调用无参数构造方法来实例化对象

		//c代表的就是日期Date类型
		Class c = Class.forName("java.util.Date");

		//实例化一个Date日期类型的对象
		Object obj = c.newInstance();

		一定要注意：
			newInstance()底层调用的是该类型的无参数构造方法。
			如果没有这个无参数构造方法会出现"实例化"异常。

	1.6、如果你只想让一个类的“静态代码块”执行的话，你可以怎么做？
		Class.forName("该类的类名");
		这样类就加载，类加载的时候，静态代码块执行！！！！
		在这里，对该方法的返回值不感兴趣，主要是为了使用“类加载”这个动作。

	1.7、关于路径问题？

		String path = Thread.currentThread().getContextClassLoader()
						  .getResource("写相对路径，但是这个相对路径从src出发开始找").getPath();

		String path = Thread.currentThread().getContextClassLoader()
						  .getResource("abc").getPath();	//必须保证src下有abc文件。

		String path = Thread.currentThread().getContextClassLoader()
						  .getResource("a/db").getPath();	//必须保证src下有a目录，a目录下有db文件。

		String path = Thread.currentThread().getContextClassLoader()
						  .getResource("com/bjpowernode/test.properties").getPath();
						  //必须保证src下有com目录，com目录下有bjpowernode目录。
						  //bjpowernode目录下有test.properties文件。

		这种方式是为了获取一个文件的绝对路径。(通用方式，不会受到环境移植的影响。)
		但是该文件要求放在类路径下，换句话说：也就是放到src下面。
		src下是类的根路径。

		直接以流的形式返回：
		InputStream in = Thread.currentThread().getContextClassLoader()
								.getResourceAsStream("com/bjpowernode/test.properties");

	1.8、IO + Properties，怎么快速绑定属性资源文件？

		//要求：第一这个文件必须在类路径下
		//第二这个文件必须是以.properties结尾。
		ResourceBundle bundle = ResourceBundle.getBundle("com/bjpowernode/test");
		String value = bundle.getString(key);


2、今日反射机制的重点内容
	2.1、通过反射机制访问对象的某个属性。
	2.2、通过反射机制调用对象的某个方法。
	2.3、通过反射机制调用某个构造方法实例化对象。
	2.4、通过反射机制获取父类以及父类型接口。

```






### 13>注解

#### 注解使用

```java
3、注解

	3.1、注解，或者叫做注释类型，英文单词是：Annotation
		疑问：注解到底是干啥的？？？？？？？？？

	3.2、注解Annotation是一种引用数据类型。编译之后也是生成xxx.class文件。

	3.3、怎么自定义注解呢？语法格式？

		 [修饰符列表] @interface 注解类型名{

		 }

	3.4、注解怎么使用，用在什么地方？

		第一：注解使用时的语法格式是：
			@注解类型名

		第二：注解可以出现在类上、属性上、方法上、变量上等....
		注解还可以出现在注解类型上。

	3.5、JDK内置了哪些注解呢？

		java.lang包下的注释类型：

			掌握：
			Deprecated 用 @Deprecated 注释的程序元素，
			不鼓励程序员使用这样的元素，通常是因为它很危险或存在更好的选择。

			掌握：
			Override 表示一个方法声明打算重写超类中的另一个方法声明。

			不用掌握：
			SuppressWarnings 指示应该在注释元素(以及包含在该注释元素中的
			所有程序元素)中取消显示指定的编译器警告。

	3.6、元注解
		什么是元注解？
			用来标注“注解类型”的“注解”，称为元注解。

		常见的元注解有哪些？
			Target
			Retention

		关于Target注解：
			这是一个元注解，用来标注“注解类型”的“注解”
			这个Target注解用来标注“被标注的注解”可以出现在哪些位置上。

			@Target(ElementType.METHOD)：表示“被标注的注解”只能出现在方法上。
			@Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, MODULE, PARAMETER, TYPE})
				表示该注解可以出现在：
					构造方法上
					字段上
					局部变量上
					方法上
					....
					类上...

		关于Retention注解：
			这是一个元注解，用来标注“注解类型”的“注解”
			这个Retention注解用来标注“被标注的注解”最终保存在哪里。

			@Retention(RetentionPolicy.SOURCE)：表示该注解只被保留在java源文件中。
			@Retention(RetentionPolicy.CLASS)：表示该注解被保存在class文件中。
			@Retention(RetentionPolicy.RUNTIME)：表示该注解被保存在class文件中，并且可以被反射机制所读取。

	3.7、Retention的源代码

			//元注解
			public @interface Retention {
				//属性
				RetentionPolicy value();
			}

            RetentionPolicy的源代码：
                public enum RetentionPolicy {
                     SOURCE,
                     CLASS,
                     RUNTIME
                }

			//@Retention(value=RetentionPolicy.RUNTIME)
			@Retention(RetentionPolicy.RUNTIME)
			public @interface MyAnnotation{}



	3.8、Target的源代码


	3.9、注解在开发中有什么用呢？

		需求：
			假设有这样一个注解，叫做：@Id
			这个注解只能出现在类上面，当这个类上有这个注解的时候，
			要求这个类中必须有一个int类型的id属性。如果没有这个属性
			就报异常。如果有这个属性则正常执行！

	3.10、注解属性
		public @interface MyAnnotation {
		    /**
		     * 我们通常在注解当中可以定义属性，以下这个是MyAnnotation的name属性。
		     * 看着像1个方法，但实际上我们称之为属性name。
		     * @return
		     */
		    String name();

		    /*
		    颜色属性
		     */
		    String color();

		    /*
		    年龄属性
		     */
		    int age() default 25; //属性指定默认值

		}

	3.11、value 的省略：
	当注解中有且仅有一个属性,属性名为value时,
	此时在使用该注解时,属性名可以省略
	//声明
	public @interface AnnotationTest01{
		String value ();
	}

	//使用
	@AnnotationTest01("test")




 	注解当中的属性可以是哪一种类型？
        属性的类型可以是：
            byte short int long float double boolean char String Class 枚举类型
            以及以上每一种的数组形式。

```



#### 通过反射机制读取注解

```java
"包：TestAnnotation"

@Retention(RetentionPolicy.RUNTIME )//希望此注解可以被反射机制读取
public @interface MyAnnotation {
    String value();
    int age();
    int [] ss();
}


@MyAnnotation(value = "a",age=21,ss=1)
public class A{
    public void method(){

    }
}



public class TestAnnotation {
    public static void main(String[] args) throws ClassNotFoundException {

        //反射机制读取注解
        Class<?> aClass = Class.forName("TestAnnotation.A");

        //判断A是否有注解
        boolean annotationPresent = aClass.isAnnotationPresent(MyAnnotation.class);

        System.out.println(annotationPresent);
        if (annotationPresent) {
            //获取注解对象
            MyAnnotation annotation = (MyAnnotation)aClass.getAnnotation(MyAnnotation.class);
            String value = annotation.value();
            System.out.println(value);
            int age = annotation.age();
            System.out.println(age);
            int[] ss = annotation.ss();
            for(int n :ss){
                System.out.println(n);
            }
        }


    }
}


```

![](05-后端/JAVA/javase/attachments/Snipaste_2022-10-29_16-17-09.png)


### 14>小知识补充

#### 桌面地址&系统字体列表

```java
1、获取桌面地址
    引包:
    import javax.swing.filechooser.FileSystemView;
    import java.io.File;
    获取:
    FileSystemView fsv = FileSystemView.getFileSystemView();
    File com = fsv.getHomeDirectory();
    String path = com.getAbsolutePath();
    
    
2、获取所有系统字体
        GraphicsEnvironment environment = GraphicsEnvironment.getLocalGraphicsEnvironment();
        String[] listData = environment.getAvailableFontFamilyNames();
        
```


#### 文件猜码

```java
    /**
     * 文件猜码
     * @param inputStream 等待猜码文件的输入流
     * @param isAutoClose 是否对输入流进行关闭
     * @return 猜码结果
     */


public static String guessCharset(InputStream inputStream, boolean isAutoClose) {
        String charset = "GBK";
        byte[] first3Bytes = new byte[3];
        BufferedInputStream bis = null;
        try {
            boolean checked = false;
            bis = new BufferedInputStream(inputStream);
            bis.mark(50*1024*1024);
            int read = bis.read(first3Bytes, 0, 3);
            if (read == -1)
                return charset;

            if (first3Bytes[0] == (byte) 0xFF && first3Bytes[1] == (byte) 0xFE) {
//                charset = "UTF-16LE";
                charset = "UTF-8";
                checked = true;
            } else if (first3Bytes[0] == (byte) 0xFE
                    && first3Bytes[1] == (byte) 0xFF) {
//                charset = "UTF-16BE";

                checked = true;
            } else if (first3Bytes[0] == (byte) 0xEF
                    && first3Bytes[1] == (byte) 0xBB
                    && first3Bytes[2] == (byte) 0xBF) {
                charset = "UTF-8";
                checked = true;
            }
            bis.reset();
            if (!checked) {
                // int len = 0;
                //int loc = 0;

                while ((read = bis.read()) != -1) {
                    //loc++;
                    if (read >= 0xF0)
                        break;
                    if (0x80 <= read && read <= 0xBF) // 单独出现BF以下的，也算是GBK
                        break;
                    if (0xC0 <= read && read <= 0xDF) {
                        read = bis.read();
                        if (0x80 <= read && read <= 0xBF) // 双字节 (0xC0 - 0xDF)
                            // (0x80
                            // - 0xBF),也可能在GB编码内
                            continue;
                        else
                            break;
                    } else if (0xE0 <= read && read <= 0xEF) {// 也有可能出错，但是几率较小
                        read = bis.read();
                        if (0x80 <= read && read <= 0xBF) {
                            read = bis.read();
                            if (0x80 <= read && read <= 0xBF) {
                                charset = "UTF-8";
                                break;
                            } else
                                break;
                        } else
                            break;
                    }
                }

            }
        } catch (Exception e) {
            return "UTF-8";
        }finally{
            if(isAutoClose){
                try {
                    bis.close();
                } catch (Exception e) {
                }
            }
        }

        return charset;
    }
```

####  发送HTTP请求方式总结

源代码：[http://github.com/lovewenyo/HttpDemo](http://github.com/lovewenyo/HttpDemo" title="源代码链接)

##### 1. HttpURLConnection 
 使用JDK原生提供的net，无需其他jar包；  
 HttpURLConnection是URLConnection的子类，提供更多的方法，使用更方便。 

```java
package httpURLConnection;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;

import java.net.HttpURLConnection;
import java.net.URL;

public class HttpURLConnectionHelper {

    public static String sendRequest(String urlParam,String requestType) {

        HttpURLConnection con = null;  

        BufferedReader buffer = null; 
        StringBuffer resultBuffer = null;  

        try {
            URL url = new URL(urlParam); 
            //得到连接对象
            con = (HttpURLConnection) url.openConnection(); 
            //设置请求类型
            con.setRequestMethod(requestType);  
            //设置请求需要返回的数据类型和字符集类型
            con.setRequestProperty("Content-Type", "application/json;charset=GBK");  
            //允许写出
            con.setDoOutput(true);
            //允许读入
            con.setDoInput(true);
            //不使用缓存
            con.setUseCaches(false);
            //得到响应码
            int responseCode = con.getResponseCode();

            if(responseCode == HttpURLConnection.HTTP_OK){
                //得到响应流
                InputStream inputStream = con.getInputStream();
                //将响应流转换成字符串
                resultBuffer = new StringBuffer();
                String line;
                buffer = new BufferedReader(new InputStreamReader(inputStream, "GBK"));
                while ((line = buffer.readLine()) != null) {
                    resultBuffer.append(line);
                }
                return resultBuffer.toString();
            }

        }catch(Exception e) {
            e.printStackTrace();
        }
        return "";
    }
    public static void main(String[] args) {

        String url ="http://int.dpool.sina.com.cn/iplookup/iplookup.php?ip=120.79.75.96";
        System.out.println(sendRequest(url,"POST"));
    }
}

```

 


##### 2. URLConnection 
 使用JDK原生提供的net，无需其他jar包；  
 建议使用HttpURLConnection 

```java
package uRLConnection;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLConnection;

public class URLConnectionHelper {

    public static String sendRequest(String urlParam) {

        URLConnection con = null;  

        BufferedReader buffer = null; 
        StringBuffer resultBuffer = null;  

        try {
             URL url = new URL(urlParam); 
             con = url.openConnection();  

            //设置请求需要返回的数据类型和字符集类型
            con.setRequestProperty("Content-Type", "application/json;charset=GBK");  
            //允许写出
            con.setDoOutput(true);
            //允许读入
            con.setDoInput(true);
            //不使用缓存
            con.setUseCaches(false);
            //得到响应流
            InputStream inputStream = con.getInputStream();
            //将响应流转换成字符串
            resultBuffer = new StringBuffer();
            String line;
            buffer = new BufferedReader(new InputStreamReader(inputStream, "GBK"));
            while ((line = buffer.readLine()) != null) {
                resultBuffer.append(line);
            }
            return resultBuffer.toString();

        }catch(Exception e) {
            e.printStackTrace();
        }

        return "";
    }
    public static void main(String[] args) {
        String url ="http://int.dpool.sina.com.cn/iplookup/iplookup.php?ip=120.79.75.96";
        System.out.println(sendRequest(url));
    }
}

```

 


##### 3. HttpClient 
 使用方便，我个人偏爱这种方式，但依赖于第三方jar包，相关maven依赖如下： 

```html
<!-- https://mvnrepository.com/artifact/commons-httpclient/commons-httpclient -->
<dependency>
    <groupId>commons-httpclient</groupId>
    <artifactId>commons-httpclient</artifactId>
    <version>3.1</version>
</dependency

```

 


---

 

```java
package httpClient;

import java.io.IOException;

import org.apache.commons.httpclient.HttpClient;
import org.apache.commons.httpclient.HttpException;
import org.apache.commons.httpclient.methods.GetMethod;
import org.apache.commons.httpclient.methods.PostMethod;
import org.apache.commons.httpclient.params.HttpMethodParams;

public class HttpClientHelper {
    public static String sendPost(String urlParam) throws HttpException, IOException {
        // 创建httpClient实例对象
        HttpClient httpClient = new HttpClient();
        // 设置httpClient连接主机服务器超时时间：15000毫秒
        httpClient.getHttpConnectionManager().getParams().setConnectionTimeout(15000);
        // 创建post请求方法实例对象
        PostMethod postMethod = new PostMethod(urlParam);
        // 设置post请求超时时间
        postMethod.getParams().setParameter(HttpMethodParams.SO_TIMEOUT, 60000);
        postMethod.addRequestHeader("Content-Type", "application/json");

        httpClient.executeMethod(postMethod);

        String result = postMethod.getResponseBodyAsString();
        postMethod.releaseConnection();
        return result;
    }
    public static String sendGet(String urlParam) throws HttpException, IOException {
        // 创建httpClient实例对象
        HttpClient httpClient = new HttpClient();
        // 设置httpClient连接主机服务器超时时间：15000毫秒
        httpClient.getHttpConnectionManager().getParams().setConnectionTimeout(15000);
        // 创建GET请求方法实例对象
        GetMethod getMethod = new GetMethod(urlParam);
        // 设置post请求超时时间
        getMethod.getParams().setParameter(HttpMethodParams.SO_TIMEOUT, 60000);
        getMethod.addRequestHeader("Content-Type", "application/json");

        httpClient.executeMethod(getMethod);

        String result = getMethod.getResponseBodyAsString();
        getMethod.releaseConnection();
        return result;
    }
    public static void main(String[] args) throws HttpException, IOException {
        String url ="http://int.dpool.sina.com.cn/iplookup/iplookup.php?ip=120.79.75.96";
        System.out.println(sendPost(url));
        System.out.println(sendGet(url));
    }
}

```

 


##### 4. Socket 
 使用JDK原生提供的net，无需其他jar包；  
 使用起来有点麻烦。 

```java
package socket;
import java.io.BufferedInputStream;  
import java.io.BufferedReader;  
import java.io.BufferedWriter;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.io.OutputStreamWriter;  
import java.net.Socket;  
import java.net.URLEncoder;  

import javax.net.ssl.SSLSocket;  
import javax.net.ssl.SSLSocketFactory;  

public class SocketForHttpTest {  

    private int port;  
    private String host;  
    private Socket socket;  
    private BufferedReader bufferedReader;  
    private BufferedWriter bufferedWriter;  

    public SocketForHttpTest(String host,int port) throws Exception{  

        this.host = host;  
        this.port = port;  

        /**  
         * http协议  
         */  
        // socket = new Socket(this.host, this.port);  

        /**  
         * https协议  
         */  
        socket = (SSLSocket)((SSLSocketFactory)SSLSocketFactory.getDefault()).createSocket(this.host, this.port);  


    }  

    public void sendGet() throws IOException{  
        //String requestUrlPath = "/z69183787/article/details/17580325";  
        String requestUrlPath = "/";          

        OutputStreamWriter streamWriter = new OutputStreamWriter(socket.getOutputStream());    
        bufferedWriter = new BufferedWriter(streamWriter);              
        bufferedWriter.write("GET " + requestUrlPath + " HTTP/1.1rn");    
        bufferedWriter.write("Host: " + this.host + "rn");    
        bufferedWriter.write("rn");    
        bufferedWriter.flush();    

        BufferedInputStream streamReader = new BufferedInputStream(socket.getInputStream());    
        bufferedReader = new BufferedReader(new InputStreamReader(streamReader, "utf-8"));    
        String line = null;    
        while((line = bufferedReader.readLine())!= null){    
            System.out.println(line);    
        }    
        bufferedReader.close();    
        bufferedWriter.close();    
        socket.close();  

    }  


    public void sendPost() throws IOException{    
            String path = "/";    
            String data = URLEncoder.encode("name", "utf-8") + "=" + URLEncoder.encode("张三", "utf-8") + "&" +    
                        URLEncoder.encode("age", "utf-8") + "=" + URLEncoder.encode("32", "utf-8");    
            // String data = "name=zhigang_jia";    
            System.out.println(">>>>>>>>>>>>>>>>>>>>>"+data);              
            OutputStreamWriter streamWriter = new OutputStreamWriter(socket.getOutputStream(), "utf-8");    
            bufferedWriter = new BufferedWriter(streamWriter);                  
            bufferedWriter.write("POST " + path + " HTTP/1.1rn");    
            bufferedWriter.write("Host: " + this.host + "rn");    
            bufferedWriter.write("Content-Length: " + data.length() + "rn");    
            bufferedWriter.write("Content-Type: application/x-www-form-urlencodedrn");    
            bufferedWriter.write("rn");    
            bufferedWriter.write(data);    

            bufferedWriter.write("rn");    
            bufferedWriter.flush();    

            BufferedInputStream streamReader = new BufferedInputStream(socket.getInputStream());    
            bufferedReader = new BufferedReader(new InputStreamReader(streamReader, "utf-8"));    
            String line = null;    
            while((line = bufferedReader.readLine())!= null)    
            {    
                System.out.println(line);    
            }    
            bufferedReader.close();    
            bufferedWriter.close();    
            socket.close();    
    }    

    public static void main(String[] args) throws Exception {  
        /**  
         * http协议测试  
         */  
        //SocketForHttpTest forHttpTest = new SocketForHttpTest("www.baidu.com", 80);  
        /**  
         * https协议测试  
         */  
        SocketForHttpTest forHttpTest = new SocketForHttpTest("www.baidu.com", 443);  
        try {  
            forHttpTest.sendGet();  
        //  forHttpTest.sendPost();  
        } catch (IOException e) {  

            e.printStackTrace();  
        }  
    }  

}  

```

 




## **附录**
### 常用工具类

#### JDBCUtil
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
        InputStream in = JDBCUtils.class.getClassLoader().getResourceAsStream("dbcconfig.properties");
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
               */

//        BasicDataSource dbs=new BasicDataSource();
//        dbs.setDriverClassName(driverClassName);
//        dbs.setUrl(url);
//        dbs.setUsername(username);
//        dbs.setPassword(password);
//        Connection conn=dbs.getConnection();

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

#### JDBCUtil_ThreadLocal
```java

import java.sql.*;
import java.util.ResourceBundle;

/**
 * JDBC工具类
 * @author 老杜
 * @version 1.0
 * @since 1.0
 */
public class DBUtil {

    private static ResourceBundle bundle = ResourceBundle.getBundle("resources/jdbc");
    private static String driver = bundle.getString("driver");
    private static String url = bundle.getString("url");
    private static String user = bundle.getString("user");
    private static String password = bundle.getString("password");

    // 不让创建对象，因为工具类中的方法都是静态的。不需要创建对象。
    // 为了防止创建对象，故将构造方法私有化。
    private DBUtil(){}

    // DBUtil类加载时注册驱动
    static {
        try {
            Class.forName(driver);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    // 这个对象实际上在服务器中只有一个。
    private static ThreadLocal<Connection> local = new ThreadLocal<>();

    /**
     * 这里没有使用数据库连接池，直接创建连接对象。
     * @return 连接对象
     * @throws SQLException
     */
    public static Connection getConnection() throws SQLException {
        Connection conn = local.get();
        if (conn == null) {
            conn = DriverManager.getConnection(url, user, password);
            local.set(conn);
        }
        return conn;
    }

    /**
     * 关闭资源
     * @param conn 连接对象
     * @param stmt 数据库操作对象
     * @param rs 结果集对象
     */
    public static void close(Connection conn, Statement stmt, ResultSet rs){
        if (rs != null) {
            try {
                rs.close();
            } catch (SQLException e) {
                throw new RuntimeException(e);
            }
        }
        if (stmt != null) {
            try {
                stmt.close();
            } catch (SQLException e) {
                throw new RuntimeException(e);
            }
        }
        if (conn != null) {
            try {
                conn.close();
                // 思考一下：为什么conn关闭之后，这里要从大Map中移除呢？
                // 根本原因是：Tomcat服务器是支持线程池的。也就是说一个人用过了t1线程，t1线程还有可能被其他用户使用。
                local.remove();
            } catch (SQLException e) {
                throw new RuntimeException(e);
            }
        }
    }

}

```






### GUI 美化、工具类、方法

#### 美化_全局样式

```java
javax.swing.UIManager类
javax.swing.UIManager类是Swing界面管理核心，管理Swing应用程序样式。
LookAndFeel抽象类
与javax.swing.UIManager类密切相关的就是LookAndFeel抽象类。它除了提供static方法，还定义抽象的个性化设置方法由子类实现。
Sun提供了三个LookAndFeel子类：javax.swing.plaf.metal.MetalLookAndFeel(Metal样式)、com.sun.java.swing.plaf.motif.MotifLookAndFeel(Motif样式)、com.sun.java.swing.plaf.windows.WindowsLookAndFeel(Windows样式)。
    
Java中的几种LookandFeel(此部分代码在main方法打开GUI界面之前实现)
    
一、
1、Metal风格(默认)
String lookAndFeel ="javax.swing.plaf.metal.MetalLookAndFeel";
UIManager.setLookAndFeel(lookAndFeel);

2、Windows风格
String lookAndFeel ="com.sun.java.swing.plaf.windows.WindowsLookAndFeel";
UIManager.setLookAndFeel(lookAndFeel);

3、Windows Classic风格
String lookAndFeel ="com.sun.java.swing.plaf.windows.WindowsClassicLookAndFeel";
UIManager.setLookAndFeel(lookAndFeel);

4、Motif风格
String lookAndFeel ="com.sun.java.swing.plaf.motif.MotifLookAndFeel";
UIManager.setLookAndFeel(lookAndFeel);

5、Mac风格 (需要在相关的操作系统上方可实现)
String lookAndFeel ="com.sun.java.swing.plaf.mac.MacLookAndFeel";
UIManager.setLookAndFeel(lookAndFeel);

6、GTK风格 (需要在相关的操作系统上方可实现)
String lookAndFeel ="com.sun.java.swing.plaf.gtk.GTKLookAndFeel";
UIManager.setLookAndFeel(lookAndFeel);
7、可跨平台的默认风格
String lookAndFeel =UIManager.getCrossPlatformLookAndFeelClassName();
UIManager.setLookAndFeel(lookAndFeel);

8、当前系统的风格
String lookAndFeel =UIManager.getSystemLookAndFeelClassName();
UIManager.setLookAndFeel(lookAndFeel);

9、
nimbus:
"com.sun.java.swing.plaf.nimbus.NimbusLookAndFeel"



使用：创建代码块添加在属性下，方法之外
例如：
{
  try {
       UIManager.setLookAndFeel("com.sun.java.swing.plaf.nimbus.NimbusLookAndFeel");
  } catch (ClassNotFoundException | InstantiationException | IllegalAccessException| UnsupportedLookAndFeelException e) {
            e.printStackTrace();
   }
}


或
try
    {
        for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels())
        {
            if ("Nimbus".equals(info.getName()))
            {
                javax.swing.UIManager.setLookAndFeel(info.getClassName());
                break;
            }
        }
    }
        catch(Exception e)
    {
        System.out.println(e);
    }








单个组件添加皮肤包
try {

            UIManager.setLookAndFeel("皮肤包");
            SwingUtilities.updateComponentTreeUI(组件);
    } catch (ClassNotFoundException | InstantiationException | IllegalAccessException| UnsupportedLookAndFeelException e) {
            e.printStackTrace();
        }
```


```

#### 图片

##### JLabel、JButton添加图片

```java

    /**
     * JLabel 、JButton
     * @param path 图片路径
     * @param componentWidth 将添加的组件最大宽度
     * @param jComponent 添加容器
     * 只做图片显示作用建议配合滚动面板使用
     */
    public  void setImageIcon(String path,int componentWidth,JComponent jComponent){
        path = path.replace("\\","/");

        ImageIcon image = new ImageIcon(path);
        int xPx = image.getIconWidth();
        int yPx = image.getIconHeight();
        
        //固定宽
        if(xPx<=componentWidth){
            image.setImage(image.getImage().getScaledInstance(xPx,yPx, Image.SCALE_SMOOTH ));//800, 450);
        }else {
            //计算高度缩小倍率
            float scaling = (float) ((double)componentWidth/xPx);
            //缩小高度
            yPx = Math.round(scaling*yPx);
            image.setImage(image.getImage().getScaledInstance(componentWidth,yPx,Image.SCALE_SMOOTH ));
        }


        //JLabel
        if(jComponent instanceof JLabel){
            JLabel jLabel = (JLabel)jComponent;
            jLabel.setIcon(image);
        }
		//JButton
        if(jComponent instanceof JButton){
            JButton jButton =  (JButton)jComponent;
            jButton.setIcon(image);
        }

    }



```



```java
先创建JLable对象、然后在使用 setIcon方法时,可以反复通过setIcon 对JLable中的图片进行更改
    且不支持gif图片的添加
    
再创建JLable对象的同时添加支持GIF图片的添加,但不支持更改,只能够进行一次添加
    即: 
    ImageIcon image = new ImageIcon(path);
    JLable jlable = new JLable(image);
```







#### 组件透明

```java
JButton 
  setContentAreaFilled(false);

普通组件、文本框、文本区域等
    setOpaque(false);
	注意：当配合“全局美化样式”时使用，透明效果失效
```



#### 圆角窗口

```java
前提：
    当使用了圆角窗口，将失去窗口的移动、窗口的放大、窗口缩小等能力
    目前通过配合使用JFramePro解决窗口拖拽问题
    
1、在使用之前，创建一个JFramePro窗,并为其设置窗口的大小
    否则下面的将会失效
    
2、
//setBounds(100, 100, 400, 270);
setSize(400,270);
//需要配合JFramePro使用
final Shape shape = new RoundRectangle2D.Double(0d, 0d, this.getWidth(), this.getHeight(),圆角宽度，圆角高度);
this.addComponentListener(new ComponentAdapter() {
   //为窗口设置圆角
   @Override
   public void componentResized(ComponentEvent e) {
           窗口对象.setShape(shape);//不能使用this
       }
   });

3、JFramePro
import javax.swing.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.MouseMotionAdapter;

public class JFramePro extends JFrame  {
    int mouseAtX;
    int mouseAtY; //实现拖动：定义全局变量:

    public JFramePro(){
        setUndecorated(true);//设置窗体的标题栏不可见
        /*
         * 设置窗体可拖动
         */
        addMouseListener(new MouseAdapter()
        {
            public void mousePressed(MouseEvent e)
            {
                /*
                 * 获取点击鼠标时的坐标
                 */
                mouseAtX = e.getPoint().x;
                mouseAtY = e.getPoint().y;
            }
        });
        addMouseMotionListener(new MouseMotionAdapter()
        {
            public void mouseDragged(MouseEvent e)
            {
                setLocation((e.getXOnScreen()-mouseAtX),(e.getYOnScreen()-mouseAtY));//设置拖拽后，窗口的位置
            }
        });

    }
}
```





#### 圆角文本框、文本区域

```java
import javax.swing.*;
import java.awt.*;


public class BPosTextField extends JTextField {//文本区域改成 extends JTextArea即可

    private int radius;
    public BPosTextField(){
    }

    public BPosTextField(int colums, int radius) {
        super(colums);
        setOpaque(true);
//        setBorder(null);

        setRadius(radius);

    }


    @Override
    protected void paintBorder(Graphics g) {
        Graphics2D g2 = (Graphics2D) g.create();
        g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
//        g2.setColor(new Color(102, 102, 102));
        g2.setColor(null);
        g2.drawRoundRect(0, 0, getWidth() - 1, getHeight() - 1, getRadius(), getRadius());
    }

    public void setRadius(int radius) {
        this.radius = radius;
        repaint();
    }

    public int getRadius() {
        return radius;
    }

    @Override
    public Insets getInsets() {
        int value = getRadius()/2;
        return new Insets(value,value,value,value);
    }
}


```



#### 圆角组件

```java
使用
 组件对象.setBorder(new RoundBorder(color));

package HumpConversion.TranslateUI;

import javax.swing.border.Border;
import java.awt.*;

public class RoundBorder implements Border {
    private Color color;

    public RoundBorder(Color color) {// 有参数的构造方法
        this.color = color;
    }
    public RoundBorder() {// 无参构造方法
        this.color = Color.BLACK;

    }

    public Insets getBorderInsets(Component c) {
        int value = 15 / 2;
        return new Insets(value, value, value, value);

    }

    public boolean isBorderOpaque() {
        return false;
    }

    // 实现Border(父类)方法
    @Override
    public void paintBorder(Component c, Graphics g, int x, int y, int width,int height) {
        g.setColor(color);
        g.drawRoundRect(0, 0,
                c.getWidth()-1 , c.getHeight()-1 ,
                15,15);

    }
}
```



#### 滚动面板

```java
使用：
JScrollPane jsp = new JScrollPane(contentBta,
ScrollPaneConstants.VERTICAL_SCROLLBAR_AS_NEEDED,
ScrollPaneConstants.HORIZONTAL_SCROLLBAR_AS_NEEDED);

//竖直方向滚动条
jsp.getVerticalScrollBar().setUI(new NewScrollBarUI());
//水平方向滚动条
jsp.getHorizontalScrollBar().setUI(new NewScrollBarUI());




import java.awt.AlphaComposite;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.GradientPaint;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.Rectangle;
import java.awt.RenderingHints;

import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JScrollBar;
import javax.swing.plaf.basic.BasicScrollBarUI;


public class NewScrollBarUI extends BasicScrollBarUI {

    @Override
    protected void configureScrollBarColors() {

        // 滑道
        if (this.scrollbar.getOrientation() == JScrollBar.VERTICAL) {
            trackColor = Color.black;

            setThumbBounds(0, 0, 3, 10);
        }
        if (this.scrollbar.getOrientation() == JScrollBar.HORIZONTAL) {
            trackColor = Color.black;

            setThumbBounds(0, 0, 10, 3);
        }
        // trackHighlightColor = Color.GREEN;

    }

    /**
     * 设置滚动条的宽度
     */

    @Override
    public Dimension getPreferredSize(JComponent c) {

        // TODO Auto-generated method stub
        if (this.scrollbar.getOrientation() == JScrollBar.VERTICAL) {
            c.setPreferredSize(new Dimension(6, 0));
        }
        if (this.scrollbar.getOrientation() == JScrollBar.HORIZONTAL) {

            c.setPreferredSize(new Dimension(0, 6));
        }

        return super.getPreferredSize(c);
    }


    // 重绘滑块的滑动区域背景

    public void paintTrack(Graphics g, JComponent c, Rectangle trackBounds) {

        Graphics2D g2 = (Graphics2D) g;

        GradientPaint gp = null;

        //判断滚动条是垂直的 还是水平的

        if (this.scrollbar.getOrientation() == JScrollBar.VERTICAL) {

            //设置画笔

//            gp = new GradientPaint(0, 0, Color.decode("#007C8E"),
//
//                    trackBounds.width, 0, Color.decode("#007C8E"));
            gp = new GradientPaint(0, 0, Color.decode("#FFFFFF"),

                    trackBounds.width, 0, Color.decode("#FFFFFF"));
        }

        if (this.scrollbar.getOrientation() == JScrollBar.HORIZONTAL) {

            /*gp = new GradientPaint(0, 0, new Color(80, 80, 80),

                    trackBounds.height, 0, new Color(80, 80, 80));*/
            gp = new GradientPaint(0, 0, Color.decode("#FFFFFF"),

                    trackBounds.width, 0, Color.decode("#FFFFFF"));

        }


        g2.setPaint(gp);

        //填充Track

        g2.fillRect(trackBounds.x, trackBounds.y, trackBounds.width,

                trackBounds.height);

        //绘制Track的边框
        /*       g2.setColor(new Color(175, 155, 95));
         g2.drawRect(trackBounds.x, trackBounds.y, trackBounds.width - 1,
                trackBounds.height - 1);
                */

        if (trackHighlight == BasicScrollBarUI.DECREASE_HIGHLIGHT)

            this.paintDecreaseHighlight(g);

        if (trackHighlight == BasicScrollBarUI.INCREASE_HIGHLIGHT)

            this.paintIncreaseHighlight(g);

    }


    @Override
    protected void paintThumb(Graphics g, JComponent c, Rectangle thumbBounds) {

        // 把绘制区的x，y点坐标定义为坐标系的原点

        // 这句一定一定要加上啊，不然拖动就失效了

        g.translate(thumbBounds.x, thumbBounds.y);

        // 设置把手颜色

        g.setColor(Color.decode("#343a40"));

        // 画一个圆角矩形

        // 这里面前四个参数就不多讲了，坐标和宽高

        // 后两个参数需要注意一下，是用来控制角落的圆角弧度

        // g.drawRoundRect(0, 0, 5, thumbBounds.height - 1, 5, 5);

        // 消除锯齿

        Graphics2D g2 = (Graphics2D) g;

        RenderingHints rh = new RenderingHints(RenderingHints.KEY_ANTIALIASING,

                RenderingHints.VALUE_ANTIALIAS_ON);

        g2.addRenderingHints(rh);

        // 半透明

        g2.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER,

                0.5f));

        // 设置填充颜色，这里设置了渐变，由下往上

        // g2.setPaint(new GradientPaint(c.getWidth() / 2, 1, Color.GRAY,

        // c.getWidth() / 2, c.getHeight(), Color.GRAY));

        // 填充圆角矩形
        if (this.scrollbar.getOrientation() == JScrollBar.VERTICAL) {
            g2.fillRoundRect(0, 0, 40, thumbBounds.height - 1, 5, 5);
        }
        if (this.scrollbar.getOrientation() == JScrollBar.HORIZONTAL) {
            g2.fillRoundRect(0, 0,thumbBounds.width - 1, 40 , 5, 5);
        }
    }


    /**
     * 创建滚动条上方的按钮
     */

    @Override

    protected JButton createIncreaseButton(int orientation) {

        JButton button = new JButton();

        button.setBorderPainted(false);

        button.setContentAreaFilled(false);

        button.setBorder(null);

        return button;

    }

    /**
     * 创建滚动条下方的按钮
     */

    @Override

    protected JButton createDecreaseButton(int orientation) {

        JButton button = new JButton();

        button.setBorderPainted(false);

        button.setContentAreaFilled(false);

        button.setFocusable(false);

        button.setBorder(null);

        return button;

    }

}

```





---

> Citation:
> - []()
> 
> References:
> - [郝斌老师-java入门](https://www.bilibili.com/video/BV1ps411F7Sn?vd_source=3fe14331de51767865a1e0e5e9b9e1c5)







