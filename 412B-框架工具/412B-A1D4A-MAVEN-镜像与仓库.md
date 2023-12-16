---

title: maven的镜像与仓库
tags: [mirror,repository,Maven,镜像]
categories: [412B-框架工具]
description: 进入文章

---

---

##### 镜像
镜像（Mirror）是一个拦截器，它会拦截MAVEN对远程仓库的相关请求，把请求里的远程仓库的地址，重新定向到镜像里配置的地址。这是对网络加速的考虑，多个镜像按照id字母顺序进行搜索排列。配置镜像后，下载请求会被拦截并转向镜像下载。但并不是所有库都得去镜像下载，所以可以配置mirrorOf，取消一些含有特殊jar包的仓库（例如企业私服）。如果不配置镜像时，默认使用的MAVEN的中央库

---

##### 仓库
仓库（Repository）主要指存放项目中依赖的第三方库的场所。在MAVEN中，这些库文件（如JAR、WAR、ZIP、POM等）被放置在一个集中的仓库中，方便项目团队进行共享和复用。MAVEN仓库可以配置多个，它们按照定义的顺序进行搜索排列。每次更新Maven时，理论上应该从远程仓库下载jar包到本地仓库。

---

##### 区别

仓库是用于存储和管理依赖库的集中式存储库，而镜像是用于加速网络请求的拦截器和重定向器


---

##### 优先级
> 先镜像 → 再仓库
> Before downloading from a repository, [mirrors configuration](https://maven.apache.org/guides/mini/guide-mirror-settings.html) is applied.

- 在本地仓库中寻找，如果没有则进入下一步。
- 在全局配置的私服仓库（settings.xml中配置的并有激活）中寻找，如果没有则进入下一步。
- 在项目自身配置的私服仓库（pom.xml）中寻找，如果没有则进入下一步。
- 在默认设置的中央仓库中(id:central, url:https://repo1.maven.org/maven2/)寻找，如果没有则终止寻找


---

##### 关系
总结:
1. repository(n) : mirror(1)  ✓ 
> maven官网原文:
> 	单个镜像可以处理多个存储库。这通常与存储库管理器一起使用，可以轻松地集中配置后面的存储库列表


2. repository(1) : mirror(n)  × 不合理不正确
> maven官网原文:
> 	请注意，给定存储库最多只能有一个镜像。换句话说，您不能将单个存储库映射到一组定义相同 `<mirrorOf>` 值的镜像。<font color="#3271ae">Maven不会聚合镜像，而只是选择第一个匹配</font>。如果要提供多个存储库的组合视图，请改用存储库管理器。可以在Maven本地设置模型网站上找到设置描述符文档
> 注意: 
> 	官方的Maven存储库位于https://repo.maven.apache.org/maven2，由Sonatype公司托管，并通过CDN在全球范围内分发,存储库元数据中提供了已知镜像的列表。这些镜像可能没有相同的内容，我们不以任何方式支持它们
> 即: repository(1) : mirror(n) 是不对的,或者说是不合理的
>
> 且:同一个repository的多个mirror时，相互之间是备份的关系，只有在仓库连不上的 时候才会切换另一个，而如果在<font color="#3271ae">能连上的情况下找不到包，是不会尝试下一个地址的</font>
> ---



##### mirrorOf

有关于mirrorOf需要注意的事项:

- 当mirrorOf中设置为`*`时,所有请求都会转到mirror镜像中所指的url中,此时<font color="#3271ae">profile中配置的repositories失效</font>,当然profile中的其他配置还是有效的

- mirrorOf设置是您正在使用的镜像的存储库的ID。例如,默认情况下包含的主Maven中央存储库的ID是Central,且MAVEN仅使用匹配到的第一个镜像,其余符合匹配条件的镜像将不起作用。也就是说，如果你的第一个仓库的mirrorOf 配置为 `*` ,则其余镜像配置将不起作用
- mirror的mirrorOf不能和任何mirror的id一致，因为id在setting中唯一，mirrorOf要和repository的id一致



---

> Citation:
> - []()
> 
> References:
> - 推荐阅读文章: [通过配置maven的setting.xml以及项目pom.xml以控制maven仓库调用顺序-CSDN博客](https://blog.csdn.net/Alger_charset/article/details/97396830?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-8-97396830-blog-113787531.235^v38^pc_relevant_sort&spm=1001.2101.3001.4242.5&utm_relevant_index=11)
> - 推荐阅读文章: [一文弄懂 maven 仓库, 仓库优先级, settings pom配置关系及差异_setting pom repositories_成知节的博客-CSDN博客](https://blog.csdn.net/taugast/article/details/113787531)
