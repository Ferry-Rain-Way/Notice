---

title: 中央仓库大全
tags: [Maven,settings,xml,配置,阿里,仓库]
categories: [412B-框架工具]
description: 进入文章

---

---

 


## 一、一般使用Maven中央仓库地址 

```html
1. http://www.sonatype.org/nexus/
2. http://mvnrepository.com/ （本人推荐仓库）
3. http://repo1.maven.org/maven2

```


 关于 Maven 远程仓库地址的配置方式有两种： 
 第1种：直接在项目的 pom.xml 文件中进行修改（不推荐，尤其是在多人协助的开发过程中非常的费事费力）； 
 第2种：将 Maven 的远程仓库统一的配置到 Maven 的 Settings.xml 的配置文件中。 


## 二、Maven 中央仓库地址大全 
 1、阿里中央仓库（首选推荐） 

```html
<repository>  
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
</repository> 

```

 2、camunda.com 中央仓库（第2推荐使用） 

```html
<repository>  
    <id>activiti-repos2</id>  
    <name>Activiti Repository 2</name>  
    <url>https://app.camunda.com/nexus/content/groups/public</url>  
</repository>  

```


 3、spring.io 中央仓库 

```html
<repository>  
    <id>springsource-repos</id>  
    <name>SpringSource Repository</name>  
    <url>http://repo.spring.io/release/</url>  
</repository>
```


 4、maven.apache.org 中央仓库 

```html
<repository>  
    <id>central-repos</id>  
    <name>Central Repository</name>  
    <url>http://repo.maven.apache.org/maven2</url>  
</repository>

```


 5、maven.org 中央仓库 

```html
<repository>  
    <id>central-repos1</id>  
    <name>Central Repository 2</name>  
    <url>http://repo1.maven.org/maven2/</url>  
</repository>

```


 6、alfresco.com 中央仓库（第3推荐使用） 

```html
<repository>  
    <id>activiti-repos</id>  
    <name>Activiti Repository</name>  
    <url>https://maven.alfresco.com/nexus/content/groups/public</url>  
</repository>  

```


 7、oschina 中央仓库（需要x墙哟） 

```html
<repository>  
    <id>oschina-repos</id>  
    <name>Oschina Releases</name>  
    <url>http://maven.oschina.net/content/groups/public</url>  
</repository>  

```


 8、oschina thinkgem 中央仓库（需要x墙哟） 

```html
<repository>   
    <id>thinkgem-repos</id>   
    <name>ThinkGem Repository</name>  
    <url>http://git.oschina.net/thinkgem/repos/raw/master</url>  
</repository> 

```


 9、java.net 中央仓库（需要x墙哟） 

```html
<repository>  
    <id>java-repos</id>  
    <name>Java Repository</name>  
    <url>http://download.java.net/maven/2/</url>  
</repository>

```


 10、github.com 中央仓库（需要x墙哟） 

```html
<repository>   
    <id>thinkgem-repos2</id>   
    <name>ThinkGem Repository 2</name>  
    <url>https://raw.github.com/thinkgem/repository/master</url>  
</repository>  

```

 


## 三、Maven 中央仓库配置示例 
 这里使用 Dubbo官方的中央仓库为示例，在 settings.xml 的 profiles 节点中添加如下内容： 

```html
<profile>
	<id>jdk‐1.8</id>
	<activation>
		<activeByDefault>true</activeByDefault>	
		<jdk>1.8</jdk>
	</activation>
	<properties>
		<maven.compiler.source>1.8</maven.compiler.source>
		<maven.compiler.target>1.8</maven.compiler.target>
		<maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
	</properties>
	<!-- dubbo 官方的解决方案 -->
	<repositories>
		<repository>
			<id>sonatype-nexus-snapshots</id>
			<url>https://oss.sonatype.org/content/repositories/snapshots</url>
			<releases>
				<enabled>false</enabled>
			</releases>
			<snapshots>
				<enabled>true</enabled>
			</snapshots>
		</repository>
	</repositories>
</profile>

```

 




---

> Citation:
> - []()
> 
> References:
> - []()
