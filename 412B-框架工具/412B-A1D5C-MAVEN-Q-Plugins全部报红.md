---

title: Maven插件Plugin是报红
tags: [Q,Maven,Plugins]
categories: [412B-框架工具]
description: 进入文章

---

---


##### 类型: 

###### 1.问题信息
Maven的插件报红,但是依赖是正常的

![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D5C-MAVEN-sshot-1.png)
###### 2.问题分析

- 1) 缓存冲突,在本地仓库中存在不同版本的插件,导致版本冲突
- 2) 从 pom.xml文添加后爆红,可能是没有下载完全
- 3) 新引入的项目可能maven库路径不对，可以在爆红一开始查看一下库路径


###### 3.如何解决

*方式1:*
打开:
> File | Settings | Build, Execution, Deployment | Build Tools | Maven | Repositories

![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D5C-MAVEN-image-20231024-170044.png)

找到你配置的本地仓库的然后点击更新按钮等待一段时间,等待更新完成,重启idea (更新的过程可能会比较长,耐心等待)


*方式2:*
- 关闭idea
- 找到idea当前正在使用的Maven的安装的位置
	- ![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D5C-MAVEN-image-20231024-170651.png)
- 查看当前本地仓库的位置,找到`org\apache\maven\plugins` 
	- ![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1D5C-MAVEN-image-20231024-170500.png)
- 删除 plugins下报红的插件,或者删除plugins下的所有文件
- 去setting.xml文件的镜像私服先注释掉
	- 如果实在因为网慢下载不了依赖，可以配置一下阿里镜像，从国内maven库中下载比较快，或者直接从官网下载
- 打开idea,进入项目重新导入插件坐标



---

> Citation:
> - []()
> 
> References:
> - [关于 maven插件爆红或插件版本爆红问题解决（且本地仓库存在相应插件版本）](https://blog.csdn.net/m0_46456778/article/details/123731292)
> - [idea maven搭建plugins 全部爆红](https://blog.csdn.net/weixin_46455069/article/details/105592413)
