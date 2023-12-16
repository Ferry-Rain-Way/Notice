---

title: Maven配置
tags: [Maven,配置]
categories: [412B-框架工具]
description: 进入文章

---

---

#### 1.下载
下载地址:

[maven镜像:](https://mirrors.bfsu.edu.cn/apache/maven/maven-3/)  进入后找到需要的版本,进入binaries文件夹下载即可,比较快

[maven官网:](https://maven.apache.org/) 找到左侧的Download 找到对因版本,较慢

解压
在你认为合适的地方进行解压,路径上不推荐有中文

#### 2.环境变量配置

- [配置JDK的环境](./JDK安装.md)
- `MAVEN_HOME`
> maven整个项目所在的文件夹,例如:D:\DEV\dev\Maven\apache-maven-3.3.9
- `PATH` → maven所在文件夹的bin文件夹
> %MAVEN_HOME%\bin
- 打开cmd窗口输入 `mvn -v` 显示版本号即为安装成功


#### 3.settings.xml文件简略配置

原文件:
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D4-MAVEN-maven-settings.png" width = 70%/></div>


##### 1)本地仓库的配置

- 找到第一步解压的maven文件夹/conf/settings.xml
- 在settings.xml文件中找到`<localRepository>`标签,填入你认为合适的文件夹路径即可
>我的配置: `  <localRepository>D:/DEV/dev/Maven/localRepository</localRepository>`

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D4-MAVEN-localRepository.png" width = 80%/> </div>


##### 2)多仓库配置

1. 直接找到`<profiles>`标签
2. 在标签中添加需要的仓库  [412B-A1D4B-MAVEN-中央仓库大全](412B-A1D4B-MAVEN-中央仓库大全.md)
```xml
	<profiles>
		<!-- 阿里公共仓配置
		https://developer.aliyun.com/mirror/maven?spm=a2c6h.12873639.article-detail.8.15d64547EyZIFG -->
		<profile>
		  <id>aliyun-public</id> 
		  <repositories>
			<repository>
			  <id>aliyun</id> 
			  <url>https://maven.aliyun.com/repository/public</url> 
			  <releases>
				<!-- 是否开启发布版构件下载 -->
				<enabled>true</enabled>
			  </releases> 
			  <snapshots>
				<!-- 是否开启快照版构件下载 -->
				<enabled>true</enabled> 
				<updatePolicy>always</updatePolicy>
			  </snapshots>
			</repository>
		  </repositories>
		</profile>
	</profiles>
```
3. 激活:
找到`activeProfiles`标签
将配置中的profile的id填入
```xml
	<activeProfiles>
		<activeProfile>aliyun-public</activeProfile>
	</activeProfiles>
```
> 注意别填错了,是profile的id,不是repository的id


##### 3)镜像配置
> [412B-A1D4A-MAVEN-镜像与仓库](412B-A1D4A-MAVEN-镜像与仓库.md)

配置镜像前的说明:
同一个repository的多个mirror时，相互之间是备份的关系，只有在仓库连不上的 时候才会切换另一个，而如果在能连上的情况下找不到包，是不会尝试下一个地址的

- 对于镜像的配置是不推荐的,建议使用repositories进行配置
- 如果使用了镜像的配置,不建议在mirrorOf中配置`*`
- 如果配置了,放在最后一个,这样当其余的镜像都"连接不上时",可以作为保底使用
- 注意:不是连接上了没有依赖,而是连接不上仓库
- 注意Maven的查找顺序应该是按照id的字母顺序进行的查找

---

- 在setting.xml文件中找到`<mirror>`标签,我的是在160-167行
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D4-MAVEN-mirror.png" width = 80%/> </div>
- 将原有的`<mirror>`标签内容替换成以下的任意一个源,此处我选择的是阿里的
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D4-MAVEN-mirror2.png" width = 80%/> </div>


[阿里云](https://developer.aliyun.com/mirror/maven)
- 新版
```xml
	<mirror>
	    <id>aliyunmaven</id>
	    <mirrorOf>*</mirrorOf>
	    <name>阿里云公共仓库</name>
	    <url>https://maven.aliyun.com/repository/public</url>
	</mirror>
```

- <del>旧版,2023.10.20依旧可以使用不推荐</del>
```xml
	<mirror>
	    <id>alimaven</id>
	    <name>aliyun maven</name>
	    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
	    <mirrorOf>*</mirrorOf>
	</mirror>
```

网易
```xml
	<mirror>
	    <id>nexus-163</id>
	    <mirrorOf>*</mirrorOf>
	    <name>Nexus 163</name>
	    <url>http://mirrors.163.com/maven/repository/maven-public/</url>
	</mirror>
```

腾讯云
```xml
	<mirror>
	    <id>nexus-tencentyun</id>
	    <mirrorOf>*</mirrorOf>
	    <name>Nexus tencentyun</name>
	    <url>http://mirrors.cloud.tencent.com/nexus/repository/maven-public/</url>
	</mirror> 
```


##### 4) 全局配置JDK版本
局部配置: [412B-A1D1-MAVEN-maven依赖](412B-A1D1-MAVEN-maven依赖.md) #maven配置jdk
```xml
		 <profile>
			<id>jdk-1.8</id>
			<activation>
				<activeByDefault>true</activeByDefault>
				<jdk>1.8</jdk>
			</activation>
			<properties>  
				<maven.compiler.source>1.8</maven.compiler.source>  
				<maven.compiler.target>1.8</maven.compiler.target>  
				<maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>  
			</properties>
		</profile>
```

#### 4.在idea中的配置
- 在File → Settings → Build,Execution,Deployment → Build Tools → Maven
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D4-MAVEN-maven-idea.png" width = 80%/> </div>
- 分别选择maven的解压路径(同第一步)
- Setting.xml 文件路径
- 本地仓库路径

- 点击左侧的Runner 配置VM Options : `-DarchetypeCatalog=internal`


#### 5.附件下载

##### 简略配置
> 以下仓库地址改成自己的
```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">
  
	<!-- 1.构建系统本地仓库的路径 -->
	<localRepository>D:/DEV/dev/Maven/localRepository</localRepository>
	
	<!-- 2.如果Maven需要和用户交互以获得输入,则设置成true,反之则应为false 默认 为true -->
	<interactiveMode>true</interactiveMode>

	<!-- 3.如果构建系统需要在离线模式下运行,则为true，默认为false。当由于网络设 置原因或者安全因素，构建服务器不能连接远程仓库的时候,该配置就十分有用 -->
	<offline>false</offline>

	<!-- 4.这是一个额外的组标识符列表，当按前缀解析插件时,即当调用像"mvn 前缀:目标" 这样的命令行时，将搜索这些标识符, 
		Maven将自动添加组标识符 "org.apache.maven.plugins" 和 "org.codehaus.mojo"如果它们尚未包含在列表中 
	-->
	<pluginGroups>
	</pluginGroups>

	<!-- 5.用于连接到网络的一个代理的规范 -->
	<proxies>
	</proxies>

	<!-- 6.
	这是身份验证配置文件的列表，由系统中使用的服务器id键入。只要maven必须连接到远程服务器，就可以使用身份验证配置文件。
	指定连接到特定服务器时要使用的身份验证信息，该服务器由系统中的唯一名称（由下面的"id"属性引用）标识
	您应该指定username/password或privateKey/passphrase，因为这两个配对是一起使用的
	-->
	<servers>
	</servers>

	<!-- 7.镜像列表，用于从远程存储库下载工件
	指定要使用的存储库镜像站点，而不是给定的存储库。此镜像服务的存储库具有与此镜像的mirrorOf元素匹配的ID
	ID用于继承和直接查找，并且在一组镜像中必须是唯一的。 
	-->
	<mirrors>
	</mirrors>
   
   <!-- 8.这是一个配置文件列表，可以以各种方式激活，并且可以修改 -->
	<profiles>
		<!-- 阿里公共仓配置
		https://developer.aliyun.com/mirror/maven?spm=a2c6h.12873639.article-detail.8.15d64547EyZIFG -->
		<profile>
		  <id>aliyun-public</id> 
		  <repositories>
			<repository>
			  <id>aliyun</id> 
			  <url>https://maven.aliyun.com/repository/public</url> 
			  <releases>
				<!-- 是否开启发布版构件下载 -->
				<enabled>true</enabled>
			  </releases> 
			  <snapshots>
				<!-- 是否开启快照版构件下载 -->
				<enabled>true</enabled> 
				<updatePolicy>always</updatePolicy>
			  </snapshots>
			</repository>
		  </repositories>
		</profile>
		<!-- 阿里Spring代理仓 -->
		<profile>
			<id>aliyun-spring</id>
			<repositories>
				<repository>
					<id>spring</id>
					<url>https://maven.aliyun.com/repository/spring</url>
					<releases>
						<enabled>true</enabled>
					</releases>
					<snapshots>
						<enabled>true</enabled>
					</snapshots>
				</repository>
			</repositories>
		</profile>
		<!-- 修改所有Maven项目默认JDK版本 -->
		<!--
		 <profile>
			<id>jdk-1.8</id>
			<activation>
				<activeByDefault>true</activeByDefault>
				<jdk>1.8</jdk>
			</activation>
			<properties>  
				<maven.compiler.source>1.8</maven.compiler.source>  
				<maven.compiler.target>1.8</maven.compiler.target>  
				<maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>  
			</properties>
		</profile>
		-->
	</profiles>

	<activeProfiles>
		<activeProfile>aliyun-public</activeProfile>
		<activeProfile>aliyun-spring</activeProfile>
	</activeProfiles>
</settings>
```



##### 原文件
[settings.xml下载](https://gitcode.net/qq_50848214/file/-/raw/master/settings.xml)



---

> Citation:
> [412B-A1D4A-MAVEN-镜像与仓库](412B-A1D4A-MAVEN-镜像与仓库.md)
> [412B-A1D4B-MAVEN-中央仓库大全](412B-A1D4B-MAVEN-中央仓库大全.md)
> 
> References:
> - [maven镜像:](https://mirrors.bfsu.edu.cn/apache/maven/maven-3/)
> - [maven官网:](https://maven.apache.org/)
> - [maven镜像-阿里巴巴开源镜像站 (aliyun.com)](https://developer.aliyun.com/mirror/maven?spm=a2c6h.12873639.article-detail.8.15d64547EyZIFG)
> - 下载地址: [https://maven.aliyun.com/](https://maven.aliyun.com/?spm=a2c6h.13651104.d-5122.8.3dae6e1aiiCAju)
