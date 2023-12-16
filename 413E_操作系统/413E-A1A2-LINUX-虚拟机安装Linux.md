---
title: 虚拟机安装Linux
tags:
  - Linux
  - 配置
categories:
  - 413E-操作系统
description: 进入文章
---

---

**目录** 

- 1、CentOS7的下载 
- 2、CentOS7的配置 
- 3、CentOS7的安装
- 4、CentOS7的网络配置
  -  4.1、自动获取IP 
  - 4.2、固定获取IP
-  5、XShell连接CentO

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-11977b182e52e6b91dcd56dd027c102f.png)

准备工作：提前下载和安装好VMware。VMware的安装可以参考这一篇文章：[VMware15的下载及安装教程](https://www.cnblogs.com/tanghaorong/p/13210470.html)。

### 1、CentOS7的下载

官网下载地址：[Download](https://www.centos.org/download/)。

进入CentOS下载官网，找到64位的CentOS7版本。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-28cbab981eb66b3cdf26c8942b1b1584.png)

点进来后，发现它给我们列出了所在区域可用镜像源（可以说是非常的良心的），我们随便选择一个，这里以阿里云的为例：

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-9f81f632bbf9510808cc05cd135f76ba.png)

选择标准的CentOS7映像下载。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-8e12c513c2d8e9cff647ae938c7c8e03.png)

下载之后会得到一个ISO文件。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-a7dfe762e84dd32df24e63a7b4750de5.png)



### 2、CentOS7的配置

1、打开“VMware Workstation“软件，选择”创建新的虚拟机“。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-16d07b9393541ba2de36031b06e1b73c.png)

2、选择“典型”选项，然后下一步。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-a227017f99f7f216d595f67c5f165548.png)

3、选择“稍后安装操作系统”，点击下一步。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-a0f20f5d0374205601d0887c22ae17ce.png)

4、客户机操作选择“Linux”,版本选择“CentOS 7 64位”，点击下一步。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-499b245c002c8437d631808065bf8a52.png)

5、输入“虚拟机名称”，选择虚拟机文件保存的位置，点击下一步。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-f7c5a88c33f1e72347b09a51dce05892.png)

6、最大磁盘默认20G大小即可，然后选择“将虚拟机磁盘存储为单个文件”，下一步。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-e896f3aef3b485bfd37777bf3e989d3d.png)

7、点击”自定义硬件配置“。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-e8eb836b1400fc2a541447e90c4c3a18.png)

8、选中”新CD/DVD“，选择”使用ISO映像文件“，然后设置CentOS7的ISO映像路径，点击关闭。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-49f079f16b9c4dd9b2ab43bd3e921d0e.png)

网络适配器默认NAT就好。

9、点击完成，如下。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-567b4b783de1337b1a19f7617766d21c.png)

接下来我们[安装CentOS](https://so.csdn.net/so/search?q=安装CentOS&spm=1001.2101.3001.7020)7。

### 3、CentOS7的安装

1、选中刚刚配置的CentOS7，然后点击“开启此虚拟机”。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-2d35fa82a709d24dc137d4bcaffc8f94.png)

2、虚拟机启动之后会出现如下界面（白色表示选中），默认选中的是Test this media & install CentOS 7。

   我们将鼠标移入到虚拟机中，并按下键盘中的“↑”键，选择Install CentOS 7，最后按下“Enter 键”。

   界面说明：

   Install CentOS 7                     安装CentOS 7

   Test this media & install CentOS 7      测试安装文件并安装CentOS 7

   Troubleshooting                     修复故障

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-392415291978ac2dc09cd85d936cf407.png)

注意： 在虚拟机中的操作，鼠标必须要移入到虚拟机中，否则虚拟机感应不到，无法对其进行操作。

​       鼠标移动到虚拟机内部单击或者按下Ctrl + G，鼠标即可移入到虚拟机中。

​       按下Ctrl + Alt，鼠标即可移出虚拟机。

3、按下Enter进行安装。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-2ab2d98dd984440b62ba61cfcd3d5918.png)

4、等待系统加载完成。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-e1f28f133b69e65f197d3611e50afc09.png)

5、选择使用哪种语言，推荐使用英文。但如果是第一次安装，建议先安装中文版的熟悉一下，之后再选择英文的进行实践，这里就介绍中文的，下滑至底部选择中文。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-08e288f90f9b8701ca7889fe8acbbaab.png)

6、【本地化】只配置日期和时间，键盘和语言支持没有特殊情况默认就好。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-e944a667028d1816dfedaca08167b5e4.png)

7、中国范围内都选择为上海（因为只有上海可选），并选择为24小时制，设置完成后单击完成按钮

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-1e8778e4f745b297f536c05e6f6ceacc.png)

8、【软件】中只配置软件选择，安装源系统会自动识别，所以不用管。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-7e41beaf50bea1362d4bfeff3adfbffc.png)

9、然后我们选择安装的系统是否含有界面，界面一般对于我们来说用处不大，而且CentOS的界面不好操作，所以这里选择最小安装。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-43153a709f9ec57c1c5e96df26640f5a.png)

10、【系统】中只配置安装位置，指的是系统如何分区，其它的都默认就好。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-479d49925eb281605d8047ef37ea40d2.png)

11、对分区不清楚的就选择自动配置分区，这里演示我要配置分区。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-8fb60057cf41105360061af5d8e06129.png)

12、手动分区我们要选择标准分区，然后点击下面的“+”添加分区。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-a228811298a84c17425b053f9c8f323f.png)

我们分别创建三个分区：**/boot区、swap交换分区、根分区/**

13、添加 /boot分区，用来放启动文件，大小300MB足矣，然后点击“添加挂载点”。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-55a8649eb4915c1c97cf34d23497f0a3.png)

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-5149d19a99f04702c23e744a59baede5.png)

14、添加 swap分区，这个是交换分区，一般情况是物理内存的2倍大小，用于物理内存不足时使用，可能造成系统不稳定，

​    所以看情况，可以设置小一点，甚至设置为0MB，这里我设置为512MB，然后点击”添加挂载点“。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-3aa01f0f2bf9e0047119b2ae7d508fe2.png)

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-9b979d9e2ac98bff78d11e1a7ba04a6d.png)

15、增加根分区，表示所有空间大小，这里不填写大小，即默认剩余的空间都给根分区，然后点击”添加挂载点“。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-7af4f867579e30ab73b636233df4ce1c.png)

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-e9048090da863b16e9742290f41e9404.png)

16、点击”完成“。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-e47469195ca0586c7dd8c24203169306.png)

17、点击”接受更改“。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-5b08cbcd8569f76a30fc5531cb1666e2.png)

18、回到界面，点击“开始安装“。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-33fa2a93a4e631c5ae5036f8bff58c6b.png)

19、接下来配置用户设置。

（1）、设置管理员ROOT密码，这是最高权限root用户的密码（默认账号为root，密码为现在要设置的）。

​      在实际中root密码越复杂越好，因为这里只是演示，所以密码就没有那么复杂了。

​      提示：这个密码非常重要，请务必牢记！！！

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-2665ea0c9f69a9217f07708c494ceaef.png)

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-c0889512fd18b723686d8ccc82e20964.png)

（2）创建用户，这里就是普通的用户，权限比较低，这一步我们可以省略。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-27bed63b871792c5c95416f43d47ce12.png)

20、用户设置好了之后，等待CentOS安装完成，，然后点击“完成配置”。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-d3879061b1eab0512c95ed99b6b094fa.png)

21、等待配置全部完成后“点击重启”。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-12d584e0f64295e6045565e3237aa806.png)

22、CentOS的启动之后的界面如下。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-e9eb22d761a34a674b26e0dd8866e24a.png)

23、下面我们来登录CentOS，使用默认账号为root，密码为 你在前面安装时设置的root密码

**注意：在输入密码时，linux为了安全起见，是看不到你输入的密码。\**同时，如果是使用的是键盘右边的数字键盘输入密码的话，建议查看一下num lock键是否开启。\****

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-c4348571c4ad5254712997b269714380.png)

24、使用普通用户登录，普通用户的权限较低，很多地方不能操作，所以使用较少。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-a480777f888a0044f7cc0e4e3338a5ab.png)

至此，CentOS7的安装全部完成了。

说明：CentOS 7默认安装好之后是没有自动开启网络连接的！所以下面我们还要配置一下CentOS7的网络。

### 4、CentOS7的网络配置

因为前面在设置CentOS7的网络适配器的时候，设置是NAT模式。

所以这里有两种方法，一种是自动获取IP，另一种是固定获取IP



#### 4.1、自动获取IP

①、首先要确保的是CentOS为NAT模式。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-ca499c4a788c6bd0169dad91723ce156.png)

②、在VMware界面（管理员方式启动）点击“编辑”里面的“虚拟网络编辑器”，然后勾选DHCP服务将IP地址分配给虚拟机，并设置子网IP(默认就好)。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-89f63c44af7d4281453fff6cedd97638.png)

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-d6f314c13a816a775b0b289f520f9305.png)

③、点击NAT模式旁边的“NAT设置”，然后修改与子网IP同网段下的网关IP，就是前三位必须相同，

​    即192.168.30要相同，最后一位数不相同即可（其实已经自动设置好了，默认），最后点击“确认”保存设置。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-862ba15a9039a007c1579d19a5514632.png)

④、然后启动虚拟机，进入网络配置文件目录：cd /etc/sysconfig/network-scripts/，并且用 ls 命令查看是否有ifcfg-xxx名称的配置文件（ifcfg-lo除外），如果没有则说明网卡没有被识别，这种只能重装或者换个CentOS的版本。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-2a4833134b05402a3f2e12945bca904c.png)

⑤、编辑ifcfg-ens33文件：vi ifcfg-ens33。按 i 进入insert编辑模式，

​    将BOOTPROTO设为dhcp，将ONBOOT设为yes，

​    按下Esc进入命令模式输入:wq保存并退出。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-5e8e3b892c59dca336d57c6064936368.png)

⑥、配置完成之后输入：service network restart，重启网卡让网卡设置生效，之后就可以上网了。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-350aacfcce642a05a01b341c5614e13f.png)

⑦、输入ip addr检查一下动态分配的IP，可以发现分配的动态IP为192.168.30.128。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-cd64ce0f5c6ab1fa87d8ac3b4639c1cc.png)

⑧、最后验证是否可以访问外网。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-f963c3982ec77125d4e08a53d28467ed.png)

发现是可以访问外网的。自动获取IP至此就介绍完了，下面介绍另一种方式。



#### 4.2、固定获取IP

①、点击“编辑”里面的“虚拟网络编辑器”,取消勾选DHCP服务将IP地址分配给虚拟机。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-0eeb9ce060dc4a7bf1830a31c0efea79.png)

②、启动虚拟机，进入网络配置文件目录：cd /etc/sysconfig/network-scripts/，然后编辑ifcfg-ens33文件：vi ifcfg-ens33。按shift+i进入insert编辑模式，

  修改以下内容：

- BOOTPROTO=static 启用静态IP地址
- ONBOOT=yes   开启自动启用网络连接

  添加以下内容：

- IPADDR=192.168.30.100   设置IP地址
- NETMASK=255.255.255.0  子网掩码
- GATEWAY=192.168.30.2  设置网关

  注意：IPADDR不能和子网IP冲突(最后一位只要在0~255范围内随便取一个数字，这里选择100)，GATEWAY即”NAT设置“里面的网关IP。

  最后按下Esc进入命令模式输入:wq保存并退出。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-df86539bc673f0629d618afb31fdd923.png)

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-97c090595c0211c09b6b61c513d93e6a.png)

 修改和添加内容后如下图：

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-1a6a29648e35b8b7006868e16f5ca914.png)

③、输入service network restart 重启网卡让网卡设置生效。

④、输入ip addr检查一下IP。

⑤、验证是否可以访问外网：ping www.baidu.com。

如果ping www.baidu.com不通，那么再测试一下百度的ip地址14.215.177.38能否ping通，如果ip能通而域名不通则说明DNS解析有误，需要设置DNS。

⑥、设置DNS（有两种方式）。

注意：DNS服务器可以只配一个，也可以配置多个，下面我用的是两个免费的DNS服务器，查看IP地址，测试联网。

----第一种是在 ifcfg-ens33 文件的后面进行添加DNS1=xxx.xxx.xxx.xxx。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-edc152e01d4ab409c317fd1a58a1be87.png)

注意改完后重启网卡才能生效。

----第二种方式是改vi /etc/resolv.conf或者直接echo -e "nameserver 114.114.114.114\nnameserver 223.5.5.5" >>/etc/resolv.conf。(\n是换行的意思)

使用vi命令添加的时候要注意格式：

- nameserver xxx1.xxx1.xxx1.xxx1
- nameserver xxx2.xxx2.xxx2.xxx2



使用echo命令则直接运行就可以了。

两种方式完成后的效果是一样的，如下图：

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-0233b80f27455dc92f672ad5abd0c815.png)


常用的免费DNS地址：

- 国内移动、电信和联通通用的DNS：114.114.114.114。
- 阿里：首选：223.5.5.5 备用：223.6.6.6
- 百度 ：180.76.76.76
- 腾讯：首选：119.29.29.29，备用：119.28.28.28
- 谷歌 8.8.8.8

详细可以参考：[分享目前可用的免费公共DNS服务器IP地址大全（2020年04月23日更新） - 小小的一世](http://www.suozy.cn/post-21.html)

网络配置完成我们就可以使用远程工具连接配置的IP访问该CentOS7服务器了，下面来介绍一下Xshell工具。

### 5、XShell连接CentOS7

我们实际在启动CentOS之后，通常都不会直接在VMware操作CentOS，而是使用工具，推荐使用Xshell。

Xshell下载地址：[家庭/学校免费 - NetSarang Website](https://www.netsarang.com/zh/free-for-home-school/)，一般都和Xftp一起下载。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-96432629203e8696a6a741bcf5ee6147.png)

到时候会发两条邮箱给你，下载之后就是傻瓜式安装。

XShell连接CentOS7的操作步骤：

①、仅仅安装了Xshell工具也还是不能连上CentOS7的，对电脑还需要一些配置（是不是非常麻烦，哈哈，程序员要有耐心，不然以后怎么找女朋友呀！）。

​    我们在电脑上打开：控制面板—>网络和 Internet—>网络和共享中心—>更改适配器—>找到MVnet8—>右键属性—>双击Internet协议版本4。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-b6f7227f90fce49a2e5f61e20d8059b0.png)

在前面的设置中，我本机IP和网关的网段是在192.168.30.0~255之间的。CentOS7静态获取的地址是192.168.30.100，这个我记得很清楚。

所以我的配置如下，你自己根据你的网段来设置，但注意别和虚拟机的IP和网关相同就是了。



![img](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-5dfdff30264326c23221b73318a3e284.png)

②、启动CentOS7，打开Xshell软件，点击“新建”。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-72bd2b978e6d4ba7685c9dc3e58d672b.png)

③、填写虚拟机的IP地址，其它默认不管，然后点击“连接”。

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-3da441410c855e1e0e0af44103992a33.png)

④、之后会弹出登录的用户名和密码

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-aed859c70b36b4759e888cd70576f8e6.png)

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-f696bd6f3803e382fb52e723a76d9054.png)

连接成功啦！

![image](https://gitcode.net/qq_50848214/image/-/raw/master/413E-A1A2-LINUX-f6719b3f879f517a44ed4de570b848eb.png)

文章知识点与官方知识档案匹配，可进一步学习相关知识


---

> Citation:
> - []()
> 
> References:
> - [在VMware中安装CentOS7（超详细的图文教程](https://blog.csdn.net/qq_45743985/article/details/121152504)
