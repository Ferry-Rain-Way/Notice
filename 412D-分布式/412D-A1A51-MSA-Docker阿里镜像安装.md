---
title: Docker阿里镜像安装
tags:
  - docker
  - 安装
  - 镜像
categories:
  - 412D-分布式
description: 进入文章
---

---

[转载](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

**加速器地址**

```url
https://gbgy0oma.mirror.aliyuncs.com
```

### 1.Ubuntu或CentOS

#### 1.1安装／升级Docker客户端

>  推荐安装1.10.0以上版本的Docker客户端，参考文档[docker-ce](https://yq.aliyun.com/articles/110806)
>

#### 1.2配置镜像加速器


针对Docker客户端版本大于 1.10.0 的用户

您可以通过修改daemon配置文件`/etc/docker/daemon.json`来使用加速器

```bash
# 创建文件夹
sudo mkdir -p /etc/docker

# 创建daemon.json文件并写入配置
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://gbgy0oma.mirror.aliyuncs.com"]
}
EOF
# 重新加载配置
sudo systemctl daemon-reload

# 重新启动docker
sudo systemctl restart docker
```





### 2.Mac


#### 2.1安装／升级Docker客户端
> 对于10.10.3以下的用户 推荐使用Docker Toolbox
>
> Mac安装文件：http://mirrors.aliyun.com/docker-toolbox/mac/docker-toolbox/
>
> 对于10.10.3以上的用户 推荐使用Docker for Mac
>
> Mac安装文件：http://mirrors.aliyun.com/docker-toolbox/mac/docker-for-mac/




#### 2.2配置镜像加速器
针对安装了Docker Toolbox的用户，您可以参考以下配置步骤：

创建一台安装有Docker环境的Linux虚拟机，指定机器名称为default，同时配置Docker加速器地址。

```bash
docker-machine create --engine-registry-mirror=https://gbgy0oma.mirror.aliyuncs.com -d virtualbox default
```

查看机器的环境配置，并配置到本地，并通过Docker客户端访问Docker服务。

```bash
docker-machine env default
eval "$(docker-machine env default)"
docker info
```

针对安装了Docker for Mac的用户，您可以参考以下配置步骤：

在任务栏点击 Docker Desktop 应用图标 -> Perferences，在左侧导航菜单选择 Docker Engine，在右侧输入栏编辑 json 文件。将

https://gbgy0oma.mirror.aliyuncs.com加到"registry-mirrors"的数组里，点击 Apply & Restart按钮，等待Docker重启并应用配置的镜像加速器。

#### 2.3 相关文档

[Docker 命令参考文档](https://docs.docker.com/engine/reference/commandline/cli/)

[Dockerfile 镜像构建参考文档](https://docs.docker.com/engine/reference/builder/)





### 3.Windows


#### 3.1安装／升级Docker客户端

> 对于Windows 10以下的用户，推荐使用Docker Toolbox
>
> Windows安装文件：[http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/](http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/?spm=5176.8351553.0.0.4ef81991iLpxYs)
>
> 对于Windows 10以上的用户 推荐使用Docker for Windows
>
> Windows安装文件：http://mirrors.aliyun.com/docker-toolbox/windows/docker-for-windows/




#### 3.2配置镜像加速器

针对安装了Docker Toolbox的用户，您可以参考以下配置步骤：

创建一台安装有Docker环境的Linux虚拟机，指定机器名称为default，同时配置Docker加速器地址。

```bash
docker-machine create --engine-registry-mirror=https://gbgy0oma.mirror.aliyuncs.com -d virtualbox default
```

查看机器的环境配置，并配置到本地，并通过Docker客户端访问Docker服务。

```bash
docker-machine env default
eval "$(docker-machine env default)"
docker info
```

针对安装了Docker for Windows的用户，您可以参考以下配置步骤：

在系统右下角托盘图标内右键菜单选择 Settings，打开配置窗口后左侧导航菜单选择 Docker Daemon。编辑窗口内的JSON串，填写下方加速器地址：

```bash
{
  "registry-mirrors": ["https://gbgy0oma.mirror.aliyuncs.com"]
}
```

编辑完成后点击 Apply 保存按钮，等待Docker重启并应用配置的镜像加速器。

#### 3.3注意

Docker for Windows 和 Docker Toolbox互不兼容，如果同时安装两者的话，需要使用hyperv的参数启动。

```bash
docker-machine create --engine-registry-mirror=https://gbgy0oma.mirror.aliyuncs.com -d hyperv default
```

Docker for Windows 有两种运行模式，一种运行Windows相关容器，一种运行传统的Linux容器。同一时间只能选择一种模式运行。

#### 3.4 相关文档

[Docker 命令参考文档](https://docs.docker.com/engine/reference/commandline/cli/?spm=5176.8351553.0.0.4ef81991iLpxYs)

[Dockerfile 镜像构建参考文档](https://docs.docker.com/engine/reference/builder/)





> Citation:
> - []()
> 
> References:
> - [转载:原文](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

