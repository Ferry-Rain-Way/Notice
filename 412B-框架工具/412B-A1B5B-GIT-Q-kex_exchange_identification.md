---
title: kex_exchange_identification
tags:
  - git问题
  - kex_exchange_identification
  - Q
categories:
  - 412B-框架工具
description: 进入文章
---

---


##### 类型:
###### 1.问题信息

> kex_exchange_identification: Connection closed by remote host
```js
kex_exchange_identification: 
read: Software caused connection abort banner exchange: 
Connection to 119.3.229.170 port 22: 
Software caused connection abort fatal:
Could not read from remote repository. 
Please make sure you have the correct access rights and the repository exists.
```
 
翻译:
```js
kex_exchange_identification：
读取：软件导致连接中止横幅交换：
连接至119.3.229.170端口22：
软件导致连接中止致命：
无法从远程存储库中读取。
请确保您具有正确的访问权限并且存储库存在。
```

###### 2.问题分析与解决

- <font color="#3271ae">临时替换成http连接</font>
```bash
# 切换远程URL为https连接
git remote set-url origin https://github.com/xxxxxx/xxxx.git
# 查看是否成功
git remote -v
```

在切换过程中,会填写用户名(邮箱)和token,如果没有token的话,去站点添加一个

---

```bash
# 检查连接状况
ssh -v <username>@<password>
```

---
此问题出现的情况比较多,可以看看下面的方案有没有可以解决的

- <font color="#3271ae">关闭全局代理软件</font>
	- 如果开启了全局代理软件,例如(clash,shadowsock,小飞机等)是否开启了全局代理模式,如果是,则关闭
	- 类似的情况可能还有所处的网络受限制,公司网络、学校网络(我出现这个问题就是使用的学校的校园网)
---

- <font color="#3271ae">检查ssh-rsa公钥配置是否正常配置</font>
	- 验证`ssh -Tv git@github.com`(换成你需要验证的站点)
	- 是否出现问题?
	- 考虑重新配置`ssh-rsa`
- <font color="#3271ae">更改配置文件</font>
	- Win: `c:/users/xxx/.ssh/config`
	- Linux: ` ~/.ssh/config`
```sql
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
# gitlab
Host gitlab.com
HostName gitlab.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/gitlab_id_rsa
```

- <font color="#3271ae">修改对应的文件信息</font>
	- 服务器禁止了本机IP进行连接
	- 让`/etc/hosts.allow` 和`/etc/hosts.deny`里面的所有信息都不生效，全部注销掉，重启SSH服务就可以了.
- <font color="#3271ae">删除配置文件</font>
	- 在`~/.ssh`下找到`known_hosts`文件,清空
	- 本地机接受了远程主机之后,会将此公钥保存在`/.ssh/known_hosts`中，以便之后的验证
---

- <font color="#3271ae">设置并发验证数量</font>
	- 把目标机器sshd_config 的 MaxStartups 设置为更高(默认为10)，这个应该是最大并发验证数量，然后重启sshd

- <font color="#3271ae">修改文件权限为 600</font>
	- `ls -l /etc/ssh`看看这个文件夹下的文件权限是什么
	- 如果不是600，运行命令 `chmod 600 /etc/ssh/`
	- 运行命令后重启ssh `service ssh restart`


---
> Citation:
> - []()
> 
> References:
> -[CSDN](https://blog.csdn.net/WU2629409421perfect/article/details/113357300)
> - [知乎](https://www.zhihu.com/question/20023544/answer/2281816286)
> - [Gitee描述](https://help.gitee.com/enterprise/code-manage/%E6%9D%83%E9%99%90%E4%B8%8E%E8%AE%BE%E7%BD%AE/%E9%83%A8%E7%BD%B2%E5%85%AC%E9%92%A5%E7%AE%A1%E7%90%86/SSH%20Key%20%E7%AA%81%E7%84%B6%E5%A4%B1%E6%95%88%E9%97%AE%E9%A2%98%E8%A7%A3%E7%AD%94%E5%8F%8A%E5%A4%84%E7%90%86%E5%8A%9E%E6%B3%95)
> - [ssh远程登录报错：kex_exchange_identification: Connection closed by remote host](https://cloud.tencent.com/developer/article/1946906)

