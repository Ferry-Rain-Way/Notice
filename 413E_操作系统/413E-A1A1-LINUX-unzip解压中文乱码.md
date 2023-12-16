---

title: unzip解压乱码
tags: [Linux,乱码,中文,博客搭建,csdn]
categories: [413E-操作系统]
description: 进入文章

---

---


##### 类型:
###### 1.问题信息

unzip解压乱码

###### 2.问题分析

在windows上压缩的文件，是以系统默认编码中文来压缩文件。由于zip文件中没有声明其编码，所以linux上的unzip一般以默认编码解压，中文文件名会出现乱码。
虽然2005年就有人把这报告为bug, 但是info-zip的官方网站没有把自动识别编码列入计划，可能他们不认为这是个问题。Sun对java中存在N年的zip编码问题，采用了同样的处理方式

###### 3.如何解决

1) 第一种：通过unzip行命令解压，指定字符集
```ruby
unzip -O CP936 xxx.zip
```

> 用GBK, GB18030也可以

有趣的是unzip的manual中并无这个选项的说明, `unzip --help`对这个参数有一行简单的说明。 

2) 第二种：在环境变量中，指定unzip参数，总是以指定的字符集显示和解压文件
` /etc/environment中加入2行  `
```ruby
UNZIP="-O CP936"  
ZIPINFO="-O CP936"
```

这样Gnome桌面的归档文件管理器(file-roller)可以正常使用unzip解压中文，但是file-roller本身并不能设置编码传递给unzip
> 注意: 有的系统不能使用 -O 命令, Centos 7.5 版本亲测可用。


3) 第三种: 使用7z解压

安装7zip和convmv
```ruby
# fedora
$ su -c 'yum install 7zip convmv'
# ubuntu
$ sudo apt-get install 7zip convmv
```

执行一下命令解压缩

```ruby
# 使用7z解压缩
$ LANG=C 7za x your-zip-file.zip
# 递归转码，从GBK转为UTF-8
$ convmv -f GBK -t utf8 --notes
```

  
  
作者：lekf123  
链接：https://www.jianshu.com/p/befc1305d6de  
来源：简书  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

---

> Citation:
> - []()
> 
> References:
> - [unzip解压文件中文乱码问题的解决方案](https://blog.csdn.net/guo_qiangqiang/article/details/107163832)
> - [解决linux下zip文件解压后中文乱码问题](https://www.jianshu.com/p/befc1305d6de)
