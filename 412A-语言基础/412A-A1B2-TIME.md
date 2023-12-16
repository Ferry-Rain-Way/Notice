---

title: java时间处理
tags: [时间,获取时间,Date,符号,yyyy,MM,dd,HH,mm,ss,csdn,nanoTime,System,专栏]
categories: [412A-语言基础]
description: 进入文章

---
 
---

#### 1.时间符号含义
常用格式: `yyyy-MM-dd HH:mm:ss`

| 符号 | 含义                                              |
| ---- | ------------------------------------------------- |
| gg   | 时期或纪元                                        |
| y    | 不包含纪元的年份。不具有前导零                    |
| yy   | 不包含纪元的年份。具有前导零。                    |
| yyyy | 包含纪元的四位数的年份                            |
| Y | [Week Yea](https://cn.bing.com/search?q=Week+Year&form=ANNTH1&refig=9f86ca32454b4841a13dc0a15debc830) |
| M    | 月份数字。一位数的月份没有前导零                  |
| MM   | 月份数字。一位数的月份有一个前导零                |
| MMM  | 月份的缩写名称，在AbbreviatedMonthNames中定义     |
| MMMM | 月份的完整名称，在MonthNames中定义。              |
| d    | 月中的某一天。一位数的日期没有前导零。            |
| dd   | 月中的某一天。一位数的日期有一个前导零。          |
| ddd  | 周中某天的缩写名称，在AbbreviatedDayNames中定义。 |
| dddd | 周中某天的完整名称，在DayNames中定义。            |
| h    | 12小时制的小时。一位数的小时数没有前导零。        |
| hh   | 12小时制的小时。一位数的小时数有前导零。          |
| H    | 24小时制的小时。一位数的小时数没有前导零。        |
| HH   | 24小时制的小时。一位数的小时数有前导零。          |
| m    | 分钟。一位数的分钟数没有前导零。                  |
| mm   | 分钟。一位数的分钟数有一个前导零。                |
| s    | 秒。一位数的秒数没有前导零。                      |
| ss   | 秒。一位数的秒数有一个前导零。                    |
| SSS  | 毫秒                                              |
| f    | 秒的小数精度为一位。其余数字被截断。              |



--- 


#### 2.获取时间的方式

在Java中获取当前时间的方法有很多种，下面列出了几种常见的方法：
推荐使用java.time包下的类，在java8中的新特性里提供了三种时间类LocalDate、LocalTime、LocalDateTime,因为它们提供了更好的时间和日期处理功能,


##### 1>  LocalDate-年月日
相当于`yyyy-mm-dd`
```java
//获取当前年月日
LocalDate localDate = LocalDate.now();

// 通过构造方法构造指定的年月日
LocalDate localDate1 = LocalDate.of(2077, 7, 17);

```

可以用这个获取单个年月日、星期等
```java
int year = localDate.getYear();
int year1 = localDate.get(ChronoField.YEAR);
Month month = localDate.getMonth();
int month1 = localDate.get(ChronoField.MONTH_OF_YEAR);
int day = localDate.getDayOfMonth();
int day1 = localDate.get(ChronoField.DAY_OF_MONTH);
DayOfWeek dayOfWeek = localDate.getDayOfWeek();
int dayOfWeek1 = localDate.get(ChronoField.DAY_OF_WEEK);

```


##### 2> LocalTime-时分秒

只获取时分秒

```java
LocalTime localTime = LocalTime.now();

// 通过构造方法指定
LocalTime localTime1 = LocalTime.of(13, 51, 10);

```

单独获取时分秒
```java
int hour = localTime.getHour();
int hour1 = localTime.get(ChronoField.HOUR_OF_DAY);
//获取分
int minute = localTime.getMinute();
int minute1 = localTime.get(ChronoField.MINUTE_OF_HOUR);
//获取秒
int second = localTime.getSecond();
int second1 = localTime.get(ChronoField.SECOND_OF_MINUTE);

```


##### 3>LocalDateTime -年月日时分秒

```java
LocalDateTime now = LocalDateTime.now();
System.out.println(now);
DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
System.out.println(now.format(formatter2));


LocalDateTime localDateTime1 = LocalDateTime.of(2077, Month.SEPTEMBER, 7, 17, 17, 17);


LocalDateTime localDateTime2 = LocalDateTime.of(localDate, localTime);
LocalDateTime localDateTime3 = localDate.atTime(localTime);
LocalDateTime localDateTime4 = localTime.atDate(localDate);
```


##### 4> Instant-秒&毫秒
#System #nanoTime
```java
// 创建Instant对象
Instant instant = Instant.now();
// 获取秒
long currentSecond = instant.getEpochSecond();
// 获取毫秒
long currentMilli = instant.toEpochMilli();
//常用获取毫秒
long l = System.currentTimeMillis();

// 获取纳秒
System.nanoTime()
```



##### 5> java.util.Date
java.util.Date

```java
import java.util.Date;

// 获取当前时间
Date now = new Date();
```




### 3.时间格式化

#### DateTimeFormatter
###### 时间 → 字符串 

使用java.time包下的类
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;


// 获取当前时间
LocalDateTime now = LocalDateTime.now();
System.out.println("当前时间: " + now);

// 格式化时间
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
String formattedNow = now.format(formatter);

/*
console:
当前时间: 2023-10-09T23:25:28.120597300
2023-10-09 23:25:28
*/
```


###### 字符串 → 时间

在Java中，你可以使用 `DateTimeFormatter` 类将日期格式的字符串转换为 `LocalDateTime`。以下是一个例子：

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;


String dateString = "2023-06-24T10:15:30";
DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
LocalDateTime date = LocalDateTime.parse(dateString, formatter);
System.out.println(date);

/*console:
2023-06-24T10:15:30
*/
```

在这个例子中，我们使用了预定义的 `DateTimeFormatter.ISO_LOCAL_DATE_TIME`,
它可以解析像我们提供的那样格式的日期字符串
此外还有这些预定义的时间格式字符

![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1B2-TIME-sshot-1.png)

|格式化器|示例|
|---|---|
|ofLocalizedDate(dateStyle)|‘2021-01-03’|
|ofLocalizedTime(timeStyle)|‘10:15:30’|
|ofLocalizedDateTime(dateTimeStyle)|‘3 Jun 2021 11:05:30’|
|ISO_LOCAL_DATE|‘2021-12-03’|
|ISO_LOCAL_TIME|‘10:15:30’|
|ISO_LOCAL_DATE_TIME|‘2021-12-03T10:15:30’|
|ISO_OFFSET_DATE_TIME|‘2021-12-03T10:15:30+01:00’|
|ISO_ZONED_DATE_TIME|‘2021-12-03T10:15:30+01:00[Europe/Paris]’|


如果你的日期字符串格式不同，你需要定义自己的 `DateTimeFormatter`。例如，如果你的日期字符串是这样的 "24/06/2023 10:15:30" ,你可以这样定义 `DateTimeFormatter`：

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm:ss");
```
注意，这些格式必须与你的日期字符串匹配，否则 `LocalDateTime.parse()` 方法会抛出 `DateTimeParseException`。


#### SimpleDateFormat

注:但其实在JDK8中，是不推荐使用的,因为SimpleDateFormat是线程不安全的。所以我们在JDK8应用中推荐用Instant代替Date，LocalDateTime带Calendar，DateTimeFormatter代替SimpleDateFormat，官方解释是simple beautiful strong immutable thread-safe(简单美观强不可变线程安全)


##### 时间 → 字符串
使用<del>java.text.SimpleDateFormat</del>类来格式化时间:

```java
import java.text.SimpleDateFormat;
import java.util.Date;


// 获取当前时间
Date now = new Date();
// 格式化时间
SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
String formattedNow = formatter.format(now);
System.out.println("格式化后的当前时间: " + formattedNow);

/*console:
格式化后的当前时间: 2023-10-09 23:29:42
*/
```

##### 字符串 → 时间
```java
  //字符串转时间
	String startDateStr = "2020-10-09 00:00:00";
	SimpleDateFormat sdf =   new SimpleDateFormat( "yyyy-MM-dd HH:mm:ss" );
	Date startDate = sdf.parse(startDateStr);
	System.out.println(startDate);
```


### 4.时区

```
GMT:1972年之前,格林威治时间（GMT）一直是世界时间的标准,
	1972年之后,GMT 不再是一个时间标准了

UTC: 是现在全球通用的时间标准,
	全球各地都同意将各自的时间进行同步协调,
	比 GMT更精准，以原子时计时
```

> *详细文章:* [113A-A1B-TIME-时区](../../../113-引文盒/113A-博客-引文/文档类/113A-A1B-TIME-时区.md)


在Java中表示时区:
##### 1.使用TimeZone类
```java
String patternStr = "yyyy-MM-dd HH:mm:ss";
// 北京时间（new出来就是默认时区的时间）
Date bjDate = new Date();
// 获取指定地区的时间
TimeZone newYorkTimeZone = TimeZone.getTimeZone("America/New_York");
// 时区转换: 北京时区时间 → 纽约时区时间
DateFormat newYorkDateFormat = new SimpleDateFormat(patternStr);
new YorkDateFormat.setTimeZone(newYorkTimeZone);

```

注:Date具有时区无关性
以上的Date所输出的时间是一致的,TimeZone 只代表 时区
是通过了"格式刷"输出不一样的时间形式


##### 2.使用ZoneId
在JDK 8之前，Java使用`java.util.TimeZone`来表示时区。而在JDK 8里分别使用了`java.time.zone.ZoneRules`表示时区，ZoneOffset表示UTC的偏移量。

获取时区
```java
System.out.println(ZoneId.from(ZonedDateTime.now()));  
System.out.println(ZoneId.from(ZoneOffset.of("+8")));

/*console:
Asia/Shanghai
+08:00
*/
```

注:`ZoneId.from(LocalDateTime.now()`是错误写法,原因是ZoneId.from只接受带时区的类型，LocalXXX是不行的，使用时稍加注意

ZoneOffset是偏移量:使用的效果和ZoneId类似,通过偏移量去计算时间,但是不建议使用这种写法
```java
@Test
public void test6() {
    System.out.println("最小偏移量：" + ZoneOffset.MIN);
    System.out.println("最小偏移量：" + ZoneOffset.MAX);
    System.out.println("中心偏移量：" + ZoneOffset.UTC);
    // 超出最大范围
    System.out.println(ZoneOffset.of("+20"));
}

输出：
最小偏移量：-18:00
最小偏移量：+18:00
中心偏移量：Z

java.time.DateTimeException: Zone offset hours not in valid range: value 20 is not in the range -18 to 18
```


##### 3.设置默认时区
ZoneId获取默认时区底层依赖的是`TimeZone.getDefault()`方法
```java
// JDK 1.8之前做法
System.out.println(TimeZone.getDefault());
// JDK 1.8之后做法
System.out.println(ZoneId.systemDefault());
```

##### 4.最佳实践
永远显式的指定你需要的时区，即使你要获取的是默认时区
```javascript
// 方式一：普通做法
LocalDateTime.now();

// 方式二：最佳实践
LocalDateTime.now(ZoneId.systemDefault());
```


---

> Citation:
> - [113A-A1B-TIME-时区](../../../113-引文盒/113A-博客-引文/文档类/113A-A1B-TIME-时区.md)
> - [113A-WithNotNID-彻底弄透Java处理GMT&UTC日期时间](../../../113-引文盒/113A-博客-引文/文档类/113A-WithNotNID-彻底弄透Java处理GMT&UTC日期时间.md)
> 
> References:
> - [Java获取时间&时间格式化最全总结](https://blog.csdn.net/weixin_43876186/article/details/108845805)
> - [关于时间格式yyyy-MM-dd HH:mm:ss具体讲解](https://blog.csdn.net/u011150924/article/details/55505060)
> - [yyyyMMddHHmmss转变为日期格式](https://blog.csdn.net/paullinjie/article/details/75085673)
> - [java日期与字符串互转](https://blog.csdn.net/CleverCode/article/details/115373280)
