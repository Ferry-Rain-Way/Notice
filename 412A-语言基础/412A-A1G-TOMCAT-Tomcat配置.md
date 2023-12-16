---
title: Tomcat配置
tags:
  - Tomcat
  - 配置
categories:
  - 412A-语言基础
description: 进入文章
---

---

### Tomcat 本地配置
-  1)在使用Tomcat进行开发时,首先需要配置JDK
	  所以第一步使用   java -version 在命令符窗口进行检测
	  没有则创建 [JDK配置](#JDK环境配置)

- 2)下载Tomcat并解压,建议解压到“非系统盘”下
- 3)Tomcat 的必要环境变量配置有三个
```
JAVA_HOME=JDK的根
CATALINA_HOME=Tomcat服务器的根
PATH=%JAVA_HOME%\bin;%CATALINA_HOME%\bin
```

㊟: CATALINA_HOME可能说的不够清楚,举个例子<br>`D:\DEV\dev\Tomcat\apache-tomcat-10.0.20`<br>[Tomcat的版本可能稍有不同]
	- 不要重复配置！！ Path中的`%JAVA_HOME%\bin;`大概率你已经配置过了

- 4)在CMD 中以管理员的运行 startup 查看是否正常运行
- 5)打开网页 http://localhost:8080 看是否正常

	 [正常跳转到此处](#Tomcat_IDEA配置)

- 6)此时你可能会遇到一些问题
	- 1- 例如权限不够 -> 检查你的Tomcat是否放在了C盘下 -> 是则移除 -> 移动到非系统盘的盘符下
	
			-> 重新配置环境变量
	
	- 2-端口被占用
	
		打开 Tomcat根目录 -> conf文件夹 -> 进入server.xml文件
		port="8080" 的8080 修改为另一个端口号( 例如 8088) -> 保存更改
		更改成功后startup -> 注意此时你打开的网页将不再是8080 而是你修改后的端口
		例如 http://localhost:8088
	```xml
	    <Connector port="8080" protocol="HTTP/1.1"
	               connectionTimeout="20000"
	               redirectPort="8443" />
	
	```
	
	- 3-如果依旧存在问题,继续进行环境变量的配置
	
		 在ClassPath的变量值中加入：
	```
	%CATALINA_HOME%\lib\servlet-api.jar;
	```
	（注意加的时候在原变量值后加英文状态下的“;”）  
	
	在Path的变量值中继续补充：[补充没有的即可,不要重复配置]
	```
	%java_home%\bin;%CATALINA_HOME%\bin;%CATALINA_HOME%\lib
	```
	
	- 如果还有问题,发出来一起讨论讨论.


### Tomcat_IDEA配置
以2021.3.3举例,都差不多,不要慌

- 1) 找到 Edit Configuration 
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920002827.png" width = 60%/> </div>
没有Tomcat 图标很正常 , 配好就有了(手动滑稽)

- 2)找到 “+”
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920003116.png" width = 60%/> </div>
- 3)找到 Tomcat Server [别找错了,不是TomEE Server]
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920003543.png" width = 30%/> </div>
	㊟:如果没有出现,向下拉到最下面,把折叠的内容打开
- 4)进入Configure...  

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920004252.png" width = 80%/> </div>
正常情况下IDEA会自动识别出本地Tomcat的根并填充,此时直接点击OK即可
如果没有出现则需要手动添加 (我的是自动识别出了,所以这里只做个示例)
点击"+" -> 点击文件夹图标 -> 找到Tomcat的根(就是上面配置的CATALINA_HOME)
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920004553.png" width = 80%/> </div>

- 5)配置结束会出现以下错误

	图标报红,底部出现 Waring : No artigacts marked for deployment
	不要慌,先不管,出现错误的原因是一个Web项目都没有,继续下去到 6)
	㊟:如果没有Chrome浏览器就换成你的电脑上有的
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920005221.png" width = 80%/> </div>


#### javaWeb项目的创建
目前我知道的创建的方式有两种 
	一种是新建一个Empty Project , 单个项目以Module的形式存在
	另一种直接新建project 单个项目以project 的形式存在

㊟:这两种本质上没有区别,选一种即可
	 第一种创建方法教程 [IDEA工具开发Servlet](https://www.bilibili.com/video/BV1Z3411C7NZ?p=10&vd_source=0623423bf320a03e4028ac01936b80a6) 从08:58开始到“第七步”结束
	 笔记:[附录](#IDEA第一种项目创建方式)
	 (似乎第二种配置方式每次创建都要重新配置一遍Tomcat,我也不确定)


此处直说第二种
- 1) File -> new Project -> java ->

	 next -> next -> 给项目起个名字 ->Finish -> create 
	 如果你的出现了Web Application 勾选上 ,跳过第二步

- 2) 添加框架支持
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920013003.png" width = 40%/> </div>
切换成Project或Package模式
点击项目-> 右击 -> Add Framework Support..

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920012907.png" width = 40%/> </div>
进入后勾选 Web Application

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920013506.png" width = 40%/> </div>

- 3) 补充结构
完整的结构
```
📂项目名
	📂src
		    |---- Servlet程序
	webapproot
	       |------WEB-INF
	            |------classes(存放字节码)
	            |------lib(第三方jar包)
	            |------web.xml(注册Servlet)
	   
	   index.html
	   style.css
	   main.js
       ....
```

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920014334.png" width = 80%/> </div>
File -> project struct -> Modules -> 点击当前项目 

-> Sources
在web -> WEB-INF -> 右键 -> New Folder -> 输入lib -> OK
在web -> WEB-INF -> 右键 -> New Folder -> 输入classes -> OK


切换到Paths
	Compiler Output -> 切换到第二个  ![200](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920015036.png)
	Output path -> 点击最右侧文件夹图标 -> 找到刚刚新建的 classes 文件夹
	Test output path -> 复制Output path 粘贴


切换到Dependencies 
	点击“+” -> JAR or Diretories -> 找到刚刚新建的 lib文件夹 -> OK
	 -> 选择 Jar Diretory -> OK -> Apply


- 4)回到工作区,如果需要使用servlet-api.jsp/jsp-api.jsp
将jar包复制粘贴到lib目录下即可





#### Tomcat配置遗留问题

##### 1.添加Artifact
还记得上面的错误吗
现在回到Tomcat配置中
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920020955.png" width = 80%/> </div>
Deployment -> + -> Artifact ... -> 选中项目 -> OK 即可

添加好Artifact -> OK

如果没有出现 Artifact,在继续看


###### Artifact的添加方法1
Build -> Build Artifacts... -> 选中项目 -> Build 
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920020413.png" width = 80%/> </div>


###### Artifact的添加方法2
如果以上方法中没有依旧出现项目
File -> project struct -> Artifacts 
-> Web Application:Exploded ->From Modules...

㊟:有长得像的,别选错

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920024241.png" width = 80%/> </div>



##### 2.Tomcat控制台乱码
在Tomcat安装包根目录找到`conf\logging.properties`文件,
将
`java.util.logging.ConsoleHandler.encoding = UTF-8`
修改为:
<font color="#3271ae">java.util.logging.ConsoleHandler.encoding = GBK</font>


##### 3.Tomcat首页404

注解:
当所有的配置都完成,Tomcat也可以正常运行
环境配置没有问题, 当前的项目的首页也可以在浏览器中打开
但是  http://localhost:8080 无法访问

在此处选择 
- External Source...
- 找到Tomcat安装包的根
- 找到webapps
- 选中ROOT 添加
- 添加后将ROOT 的 Application context设置为 ``/`


<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1G-TOMCAT-Pasted%20image%2020220920023048.png" width = 40%/> </div>






### 附录
#### JDK环境配置
```
创建：
变量名：JAVA_HOME
变量值：jdk安装路径即可,例如我安装路径：C:\Program Files\Java\jdk-9.0.4
编辑第二个变量名：path
变量值：%java_home%\bin

```







---

> Citation:
> - []()
> 
> References:
> - []()
