---

title: git笔记
tags: [git,笔记]
categories: [412B-框架工具]
description: 进入文章
sticky: 80
---

---

![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-index.png)


#### 1.[名词解释](https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576)

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。
先来看名词解释
##### 工作区
就是你在电脑里能看到的目录,比如我的`learngit`文件夹就是一个工作区:
![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-work.png)

##### 版本库
工作区有一个隐藏目录`.git`,这个不算工作区,而是Git的版本库
Git的版本库里存了很多东西,其中最重要的就是称为`stage`(或者叫index)的暂存区,还有Git为我们自动创建的第一个分支`master`,以及指向master的一个指针叫`HEAD`

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-work2.png" width = 80%/> </div>

- 创建两个文件`readme.txt` 、`LICENSE`
- 执行`git add .`
> git add 是将工作区的所有文件添加到暂存区,此时的状态如下

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-work3.png" width = 80%/> </div>

- 执行`git commit`就可以一次性把暂存区的所有修改提交到分支(当前没有创建分支所以就是提交到主分支)
此时状态如下:
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-work4.png" width = 80%/> </div>



#### 2.git基础


| 命令 | 描述 | 
| --- | --- |
| `git init` | 现有的某个项目开始用 Git 管理 |
| `git status` | 检查当前文件状态 |
| `git config --list`  | 查看全局配置 |
| `git add 文件名`  | 开始跟踪新文件，或者把已跟踪的文件放到暂存区 |
| | 跟踪全部文件 `git add .` 或 `git add -A`  | 
| `git commit -m  "描述信息" ` |  暂存区 → 本地仓库(版本库) |
| ` git commit -a -m '描述信息'` | 跳过使用暂存区域,自动把所有已经跟踪过的文件暂存起来一并提交 |
| `git reflog` | 查看命令历史记录 ,可以查看已删除的"commitID" |
| `git ls-files` | 查看已经添加到暂存区的文件 |

---
- 版本回退 : `git reset --hard commitID`
```bash
本条命令执行后将退回到commitID记录所在的状态 
commitID的状态存在,commitID之前的记录删除 |
```

---

- 撤销修改 : `git checkout	-- file`
```bash
例如:  git checkout -- readme.txt
分两种情况
1. 自修改后还没有被放到暂存区,现在,撤销修改就回到和版本库一模一样的状态
2. 已经添加到暂存区后,又作了修改,现在,撤销修改就回到添加到暂存区后的状态
```

---

- 删除文件 : `rm file`
```bash
(当然直接在文件管理器中手动删除效果一样)
例如: rm readme.txt 
如果readme.txt已经被提交到暂存区,执行rm命令,可以通过git checkout -- file恢复
如果readme.txt 未被提交到暂存区,执行rm命令,则改文件无法被恢复
```

---

- `.gitignore` 文件的修改与生效
```bash
#清除缓存
git rm -r –cached .
#重新按照ignore的规则add所有的文件
git add .
#提交和注释
git commit -m "update .gitignore"
```

---

-  git标签
```bash
1.查看现有标签,可带上可选的 -l 选项 --list
git tag 
git tag -s
git tag --list

2.添加轻量标签
git tag 便签名

3.添加附注标签
git tag -a 标签名 -m "标签信息"
-m 选项指定了一条将会存储在标签中的信息。 如果没有为附注标签指定一条信息,Git 会启动编辑器要求你输入信息

4.标签信息和与之对应的提交信息
git show 标签名

5.推送标签到远程仓库
git push origin 标签名 : 推送指定标签

git push 分支名 --tags : 推送全部标签
	推送标签并不会区分轻量标签和附注标签， 没有简单的选项能够让你只选择推送一种标签
	
6.删除标签
git tag -d 标签名
```

---


#### 3.git分支
1. 查看分支             git branch  或 git branch -a
2. 创建本地分支      git branch 分支名
3. 切换分支             git checkout 分支名
4. 创建分支并切换   git checkout -b 分支名

5. 合并分支    git [merge](https://fanyi.baidu.com/#en/zh/merge) 分支名
>通常情况下 将其他分支加入主分支
>切换到master分支
>执行 git merge 分支名
>例如 git merge dev01

合并前
<div align="left"> <img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-merge-before.png" width = 50%/> </div>

合并后
<div align="left"> <img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-merge-after.png" width = 50%/> </div>

6. 删除分支  git branch -d 分支名
7. 强制删除分支 git branch -D 分支名
8. 冲突
>冲突的产生:不同分支对同一文件的同一行进行了修改

例如:
在master中创建文件file.txt
>file in master branch

创建分支dev01
在master分支中修改file.txt第一行
>file in master branch → master update file

在dev01  分支中修改file.txt第一行
>file in master branch → dev01 update file

<div align="left"> <img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-update.png" width = 50%/> </div>

执行合并分支[将dev01合并至master]:
`$git merge dev01`
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
Automatic merge failed; fix conflicts and then commit the result.

file.txt中的内容:
```bash
|<<<<<<< HEAD
file in master branch → master update file
=======
file in master branch → dev01 update file
>>>>>>> dev01
```

改动文件(解决冲突)并加入暂存区并提交

<div align="left"> <img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-update2.png" width = 50%/> </div>




#### 4.Git远程仓库
#####  Gitee码云注册关联本地
- 注册Gitee码云

- 创建仓库"+" → 新建仓库

- <div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-new.png" style="zoom: 25%;" /></div>

- 配置仓库名

 - 获取密钥
> [本地Git窗口执行]ssh-keygen -t rsa
>  一直回车
>  出现类似以下文字表示成功

<div align="left"> <img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-getkey.png" width = 30%/> </div>

- 查看密钥
> [本地Git窗口执行]cat ~/.ssh/id_rsa.pub 
> 复制密钥

<img align="left" src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-copy-key.png" width = 20%/>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-copy-key2.png" width = 20%/>
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-copy-key3.png" width = 30%/>


- 检查是否成功
>[ 本地Git窗口执行]ssh -T git@gitee.com
>
>出现以下内容成功
>
>> Hi NanFeng! You've successfully authenticated, but GITEE.COM does not provide shell access.

	翻译:你好南风！您已经成功通过身份验证,但GITEE.COM不提供shell访问。
	
	复制仓库地址:
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-copy-url.png" alt="600" style="zoom:33%;" />


##### Git远程仓库命令
- 告诉本地仓库对应的远程仓库是哪一个
>  git remote add origin git@gitee.com:nanfengjinhe/git_test.git

- 查看是否关联成功[git remote](https://www.runoob.com/git/git-remote.html)
> git remote
 - 将<u>本地仓库</u>或本地仓库的<u>更新</u>推送到远程仓库
 >通常使用: git push origin master

```
命令:   
git -f --set-upstream  远端名称 本地分支名:远程分支名

如果远程分支名和本地分支名称相同,则可以只写本地分支
		git push origin master
		
-f 若本地与远程存在冲突,则本地强制覆盖远程
	一般公司会将-f的权限禁用,[防止小白误删/doge]
--set-upstream 推送到远端的同时并且建立起和远端分支的关联关系。
       git push -f --set-upstream origin master:master
```
<img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-respository.png" style="zoom:33%;" />



- 克隆远程仓库
> git clone 仓库远程地址  [仓库名]

- 本地 → 远程 git push .....
- 远程 → 本地 
>方法1:  git fetch 不合并分支   [配合 git merge 分支名使用]
>方法2:  git pull   合并分支


#### 5.Idea_Gitee
- 在 File | Settings | Version Control | Gitee 中找到Gitee
- 点击`Add account`
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-image-20231025-112301.png" width = 80%/></div>
- 同意授权
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-image-20231025-112013.png" width = 50%/></div>
- 会接受到一个邮箱
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-image-20231025-112430.png" width = 50%/></div>
- 出现账号
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-image-20231025-112529.png" width = 50%/></div>
- 找到 Share Project on Gitee
- (直接选择 Version Control也能找到)

<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-image-20231025-112915.png" width = 50%/></div>
- 在Gitee中创建仓库提交
<div align="left"><img src="https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B-GIT-image-20231025-113632.png" width = 50%/></div>

- 如果上一步创建的仓库是私有的,想要开源可以在Gitee仓库的管理中打开






#### 6.关联本地仓库

Git 全局设置:
```bash
git config --global user.name "NanFeng"
git config --global user.email "3483881997@qq.com"
```

创建 git 仓库:
```bash
mkdir git_test
cd git_test
git init 
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/nanfengjinhe/git_test.git
git push -u origin "master"
```


已有仓库?
```bash
cd existing_git_repo
git remote add origin https://gitee.com/nanfengjinhe/git_test.git
git push -u origin "master"
```



####  7.文件配置
##### `.bashrc` 文件

1) `touch ~/.bashrc` : 在用户目录下创建.bashrc文件 
2) `start ~/.bashrc` : 打开`.bashrc`文件 
3) 编辑内容,为git命令起别名,全局有效
```bash
#用于输出git提交日志
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
#用于输出当前目录所有文件及基本信息
alias ll='ls -al'
```
4) `source ~/.bashrc` : 刷新文件

#####  .gitignore 文件


```.gitignore
# / 表示 当前文件所在的目录

# 忽略public下的所有目录及文件
/public/*
#不忽略/public/assets,就是特例的意思,assets文件不忽略
!/public/assets

# 忽略具体的文件

index.php

# 忽略所有的php
*.php

# 忽略 a.php b.php
[ab].php

#匹配规则和linux文件匹配一样
#以斜杠“/”开头表示目录；
#以星号“*”通配多个字符；
#以问号“?”通配单个字符
#以方括号“[]”包含单个字符的匹配列表；
#以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；
```



#### 8.问题集 
```
1、问题复现:
git init
vi file.txt
git branch dev01
→  fatal: not a valid object name: 'master'

致命：不是有效的对象名：“master”
原因：刚创建的 git 仓库默认的 master 分支要在第一次commit之后才会真正建立,否则就像你声明了个对象但没初始化一样 
解决办法：
	先 **git add.添加所有项目文件到本地仓库缓存,再 git commit -m “... 报错** fatal: Not a valid object name: ‘ master ’.
	解决: 执行commit 命令
```



---

> Citation:
> - [[412B-A1B1-GIT][gitignore]]([412B-A1B1-GIT][gitignore].md)
> 
> References:
> - [git官网](https://git-scm.com/book/zh/v2)