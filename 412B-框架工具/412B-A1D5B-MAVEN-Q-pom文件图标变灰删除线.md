---

title: pom文件图标变灰删除线
tags: [pom,Maven,图标]
categories: [412B-框架工具]
description: 进入文章

---

---


##### 类型:
###### 1.问题信息
pom.xml文件变灰,有删除线,pom文件失效
![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D5B-MAVEN-sshot-1.png)

###### 2.问题分析

项目中的pom.xml文件被设置在maven忽略清单中


###### 3.如何解决

在File | Settings | Build, Execution, Deployment | Build Tools | Maven | Ignored Files中对已经选中的pom文件取消选中


![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D5B-MAVEN-sshot-2.png)



---

> Citation:
> - []()
> 
> References:
> - [【问题】IDEA Maven pom.xml 变灰 出现删除线_pom文件 横线-CSDN博客](https://blog.csdn.net/G971005287W/article/details/109720580)
