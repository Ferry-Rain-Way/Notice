---

title: 不支持发行版本
tags: [不支持发行版本17,jdk17 ]
categories: [412A-语言基础]
description: 进入文章

---

---


![](https://gitcode.net/qq_50848214/image/-/raw/master/412A-A1B1-01.png)

**解决:**

查看几处位置,并将其改为适合的JDK版本:

​	1.Project Structure → Project 选择对应的版本

​	2.Project Structure → Module 

​		2.1 选择Sources,查看language level的选择

​		2.2 选择 Dependencies 下拉菜单更换适合的SDK版本

​	3.打开 File | Settings | Build, Execution, Deployment | Compiler | Java Compiler

​		在右侧找到对应的模块Module,修改 target bytecode version,选择jdk版本

​	4.如果以上都检查过了依旧没有效果,且项目使用了Maven搭建,查看pom.xml中有关Java版本的配置
- 4.1 第一种设置方法:在项目的pom文件的properties标签中新增
```xml
<properties>

    <!-- 设置Maven全局变量，使用JDK版本，默认为1.5 -->
    <!-- 源文件（编译时）使用的jdk版本 -->
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <!-- 目标字节码文件使用的jdk版本 -->
    <maven.compiler.target>${java.version}</maven.compiler.target>

    <!-- 自定义全局变量(多用于版本号的定义), 使用方法${lombok.version} -->
    <lombok.version>1.18.16</lombok.version>
    <java.version>1.8</java.version>
    
</properties>

```

- 4.2 第二种设置方法:%% 在项目的pom文件的build中设置 %%
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>${java.version}</source>
                <target>${java.version}</target>
                <encoding>utf-8</encoding>
            </configuration>
            <!-- 当手动引入jar包时，必须声明此项，否则项目会编译失败，Maven找不到手动引入的jar包 -->
            <compilerArguments>
              <!-- jar包的存放路径 -->
              <extdirs>src/main/resources/lib</extdirs>
            </compilerArguments>
        </plugin>
    </plugins>
</build>

```

- 4.3 第三种设置方法在settings文件中配置
> 在profiles中添加一个如下的profile，配置的时所有项目的jdk版本
```xml
<!-- 配置maven的jdk版本 -->
<profile>
    <id>jdk-1.8</id>
    <activation>
        <!-- 该profile是否默认激活 -->
        <activeByDefault>true</activeByDefault>
        <!-- 通过jdk版本前缀来激活当前profile。
             此处当检测到使用的jdk版本是1.8.xxx，则当前profile被激活，!1.8表示激活所有不是以1.8开头的jdk版本
          -->
        <jdk>1.8</jdk>
    </activation>
    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
    </properties>
</profile>

```





---

> Citation:
> - []()
> 
> References:
> - []()
