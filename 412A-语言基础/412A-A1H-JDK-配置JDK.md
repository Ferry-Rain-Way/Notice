---
title: 配置JDK
tags:
  - jdk
  - 配置
categories:
  - 412A-语言基础
description: 进入文章
---

---

一,java 安装

1.下载java安装文件
任选一个链接进入下载需要的JDK
[http://www.codebaoku.com/jdk/jdk-index.html](http://www.codebaoku.com/jdk/jdk-index.html)
[https://jdk.java.net/archive/](https://jdk.java.net/archive/)
[https://www.oracle.com/java/technologies/downloads/archive/](https://www.oracle.com/java/technologies/downloads/archive/)


- 安装目录自选但是要记住安装路径。例如: `C:\Program Files (x86)\Java`不推荐路径上有中文
- 安装过程中 点击下一步即可
- 安装完成后打开cmd命令输入`java -version`,如果正确会出现安装的版本



2.搜索：编辑系统环境变量


![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1H-JDK-image-20231111-013323.png)
进入后找到环境变量

<font color="#3271ae">创建</font>第一个变量
变量名：`JAVA_HOME`
变量值：刚刚jdk安装路径,例如我安装的路径：`C:\Program Files\Java\jdk-9.0.4`


![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1H-JDK-image-20231111-013626.png)

<font color="#3271ae">编辑</font>第二个变量名: Path
变量值：`%java_home%\bin`
环境变量配置名是固定的


![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1H-JDK-image-20231111-013921.png)



---

> Citation:
> - []()
> 
> References:
> - []()
