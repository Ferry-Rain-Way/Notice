---

title: git拒绝推送
tags: [git问题,rejected,Q]
categories: [412B-框架工具]
description: 进入文章

---

---

##### 类型:
###### 1.问题信息

```bash
! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'gitcode.net:qq_50848214/zettelkasten.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

![](https://gitcode.net/qq_50848214/image/-/raw/master/412B-A1B5A-image-20231105-012151.png)


###### 2.问题分析

Git仓库中已经有一部分代码，所以它不允许你直接把你的代码覆盖上去。  
远程仓库和本地仓库存在差异。  
一般都是因为你在码云创建的仓库有ReadMe文件，而本地没有，造成本地和远程的不同步

###### 3.如何解决

- 1) 方法一、同步
	- 把远程仓库和本地同步，消除差异
```bash
git pull origin master --allow-unrelated-histories
```

	- 重新add和commit相应文件
	- git push origin master
	- 此时就能够上传成功了

如果只是因为本地没有ReadMe文件，那么就在本地生成一个

```bash
git pull --rebase origin master  //本地生成ReadMe文件
git push origin master
```

- 2) 方法二：强推

即利用强覆盖方式用你本地的代码替代git仓库内的内容

```bash
git push -f origin master
```

该命令会强制上传覆盖远程文件，慎用  

- 3) 方法三、

先把git的东西fetch到你本地然后merge后再push

```bash
git fetch
git merge
```


---

> Citation:
> - []()
> 
> References:
> - []()
