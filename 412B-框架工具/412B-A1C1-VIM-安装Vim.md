---
title: 安装Vim
tags:
  - vim
  - Linux
categories:
  - 412B-框架工具
description: 进入文章
---

---

### Centos

Centos默认安装`vi`编辑器,但没有安装`vim`

- 查看一下你本机已经存在的包，确认一下你的VIM是否已经安装
> rpm -qa|grep vim

如果有类似以下结果输出:
```bash
vim-filesystem-7.4.160-4.el7.x86_64
vim-minimal-7.4.160-4.el7.x86_64
vim-enhanced-7.4.160-4.el7.x86_64
vim-common-7.4.160-4.el7.x86_64
```
则分别安装
`yum -y install vim-XXX` ,XXX代表需要安装的包,输入开头,然后回车自动补全就行
将以上四个分别安装

- 如果输出的结果是空白的,就直接执行以下命令
```bash
yum -y install vim*
```


### 配置
```bash
vim /etc/vimrc
```

打开文件,找个位置添加以下配置(选择自己需要的)
```bash
"自定义配置
set nu          " 设置显示行号
set showmode    " 设置在命令行界面最下面显示当前模式等
set ruler       " 在右下角显示光标所在的行数等信息
set autoindent  " 设置每次单击Enter键后，光标移动到下一行时与上一行的起始字符对齐
syntax on       " 即设置语法检测，当编辑C或者Shell脚本时，关键字会用特殊颜色显示
```

---

> Citation:
> - []()
> 
> References:
> - []()
