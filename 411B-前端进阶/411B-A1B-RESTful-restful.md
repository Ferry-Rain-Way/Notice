---
title: RESTful
tags:
  - RESTful
  - 笔记
categories:
  - 411B-前端进阶
description: 进入文章
---
 
---

![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-dee0b0b1b5d69df96c00974ec7b0cef8_1440w.png)
### 一、REST

#### 1.1 REST简介
1. **REST的出处**
> 由[Roy Thomas Fielding](http://www.ics.uci.edu/~fielding/)在他的[博士论文](https://ics.uci.edu/~fielding/pubs/dissertation/top.htm)中提出

---

2. **设计和评估万维网络体系结构关键通信协议的改进建议时所面临的问题**

> [原文](https://ics.uci.edu/~fielding/pubs/dissertation/web_arch_domain.htm#sec_4_2)
> 互联网开发者社区开始担心Web使用的快速增长，沿着早期HTTP的一些糟糕的网络特性，将很快超过互联网基础设施的容量，并导致全面崩溃。Web上的应用程序交互的性质不断变化，使这种情况变得更糟。虽然最初的协议是为单一的请求-响应对设计的，但新的网站使用<font color="#3271ae">越来越多的内嵌图像作为网页内容的一部分，从而产生了不同的浏览交互配置文件</font>。所部署的体系结构在对可扩展性、共享缓存和中介的支持方面有很大的局限性，这使得很难为日益增长的问题开发专门的解决方案。与此同时，软件市场的商业竞争导致了大量新的、偶尔相互矛盾的Web协议功能提案的涌入。
> 互联网工程任务组的工作组致力于Web的三个主要标准：<font color="#3271ae">URI、HTTP和HTML</font>。这些小组的章程是定义在早期Web体系结构中通常一致实现的现有体系结构通信的子集，识别该体系结构中的问题，然后指定一组标准来解决这些问题。这给我们提出了一个挑战：我们<font color="#3271ae">如何将一组新的功能引入到已经广泛部署的架构中，以及我们如何确保它的引入不会对使Web成功的架构属性产生负面影响，甚至破坏</font>？

---

3. [REST的目标](https://ics.uci.edu/~fielding/pubs/dissertation/abstract.htm)
> 万维网的成功很大程度上是因为它的软件体系结构被设计成满足互联网规模的分布式超媒体系统的需求。在过去的十年里，Web通过对定义其体系结构的标准进行一系列修改而得到了迭代式的发展。为了确定Web需要改进的方面并避免不必要的修改，需要一个现代Web体系结构的模型来指导其设计、定义和部署。Roy Thomas Fielding的工作是出于理解和评估基于网络的应用软件的架构设计的愿望，通过原则性地使用架构约束，从而获得所需的功能，性能和社会属性的架构。

---


4. **什么是REST**
- 英文: REpresentational State Transfer
- REST是一种"表述性状态转移"架构的风格、约束

- REST应用与URI
> URI: 通用资源标识符
> 
> [原文:](https://ics.uci.edu/~fielding/pubs/dissertation/evaluation.htm#sec_6_2)
> "REST was used to define the term resource for the URI standard, as well as the overall semantics of the generic interface for manipulating resources via their representations."
> 
> 翻译
> "REST用于定义<font color="#3271ae">URI</font>标准的术语[资源](https://ics.uci.edu/~fielding/pubs/dissertation/evaluation.htm#sec_6_2_1),以及通过其表示操作资源的通用接口的<font color="#3271ae">整体语义</font>"

所以REST风格拆开来理解
- Resource：
	资源,[任何可以被命名的信息，可以是一个实体、对象、文档、图像、实体集合、服务](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_2_1_1)等等，可以通过统一资源标识符（URI）进行"标识"和访问
- Representational：
	"资源"具体呈现出来的形式，叫做它的"表现层"（Representation）
	比如，文本可以用txt格式表现，也可以用HTML格式、XML格式、JSON格式表现，甚至可以采用二进制格式；图片可以用JPG格式表现，也可以用PNG格式表现。
	URI只代表资源的实体，不代表它的形式。严格地说，有些网址最后的".html"后缀名是不必要的，因为这个后缀名表示格式，属于"表现层"范畴，而URI应该只代表"资源"的位置。它的具体表现形式，应该在HTTP请求的头信息中用Accept和Content-Type字段指定，这两个字段才是对"表现层"的描述。
- State Transfer：
	状态变化。对资源的状态进行CRUD从而改变资源的状态，称为状态转移，通过[HTTP动词](https://www.zhihu.com/search?q=HTTP%E5%8A%A8%E8%AF%8D&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A48094438%7D)实现。
	- GET:   从服务器取出资源(一项或多项)
	- POST:  在服务器新建一个资源
	- PUT :  在服务器更新资源（客户端提供<font color="#3271ae">完整</font>资源数据)
	- PATCH: 在服务器更新资源(客户端提供<font color="#3271ae">部分</font>需要修改的)资源数据）
	- DELETE: 从服务器删除资源
	
> 注: <font color="red">URI是资源的地址、位置,也可以说是资源的名称</font>
---



#### 1.2 REST约束原则
[论文原文:](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)

##### 1.客户端-服务端-Client-Server
![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-client_server_style.gif)

通过将用户界面关注点与数据存储关注点分离，我们提高了用户界面跨多个平台的可移植性，并通过简化服务器组件来提高可扩展性。然而，对Web最重要的可能是，这种分离允许组件独立地发展，从而支持多个组织域的Internet规模需求。

这个更专注客户端和服务端的分离，服务端独立可更好服务于前端、安卓、IOS等客户端设备。

---

##### 2.无状态-Stateless
接下来，我们为客户端-服务器交互添加一个约束：通信本质上必须是无状态的，就像[第3.4.3节](https://ics.uci.edu/~fielding/pubs/dissertation/net_arch_styles.htm#sec_3_4_3)中的客户端-无状态-服务器（CSS）风格一样（[图5-3](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#fig_5_3)），这样从客户端到服务器的每个请求都必须包含理解请求所需的所有信息，并且不能利用服务器上存储的任何上下文。因此，会话状态完全保留在客户端上。
![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-stateless_cs.gif)
这种约束导致了可见性、可靠性和可伸缩性的属性。可见性得到了提高，因为监控系统不必查看单个请求数据之外的内容来确定请求的全部性质。可靠性得到提高，因为它简化了从部分故障中恢复的任务[133](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_133)。可伸缩性得到了提高，因为不必在请求之间存储状态，允许服务器组件快速释放资源，并进一步简化了实现，因为服务器不必跨请求管理资源使用。

与大多数体系结构选择一样，无状态约束反映了一种设计权衡。缺点是它可能会通过增加在一系列请求中发送的重复数据（每次交互开销）来降低网络性能，因为这些数据不能留在共享上下文中的服务器上。此外，将应用程序状态放置在客户端会减少服务器对一致应用程序行为的控制，因为应用程序变得依赖于跨多个客户端版本的语义的正确实现

---

##### 3.可缓存性-Cacheability
为了提高网络效率，我们增加了缓存约束，形成[了3.4.4节](https://ics.uci.edu/~fielding/pubs/dissertation/net_arch_styles.htm#sec_3_4_4)中的client-cache-stateless-server风格（[图5-4](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#fig_5_4)）。缓存约束要求对请求的响应中的数据隐式或显式地标记为可缓存或不可缓存。如果一个响应是可缓存的，那么客户端缓存就有权为以后的等价请求重用该响应数据。
![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-ccss_style.gif)
添加缓存约束的优势在于，它们有可能部分或完全消除某些交互，从而通过减少一系列交互的平均延迟来提高效率、可伸缩性和用户感知性能。但是，如果该高速缓存中的陈旧数据与直接向服务器发送请求时获得的数据有很大不同，则该高速缓存可能会降低可靠性。

早期的Web架构，如[图5-5](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#fig_5_5)所示，是由客户端-缓存-无状态-服务器约束集定义的。[](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_11)也就是说，在1994年之前，Web体系结构的设计原理主要集中在通过Internet交换静态文档的无状态客户机-服务器交互上。用于通信交互的协议对非共享缓存有基本的支持，但没有将接口约束为所有资源的一致语义集。相反，Web依赖于使用公共客户端-服务器实现库（CERN libwww）来维护Web应用程序的一致性

![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-early_web_arch.gif)
Web实现的开发人员已经超越了早期的设计。除了静态文档之外，请求还可以识别动态生成响应的服务，例如图像映射[Kevin Hughes]和服务器端脚本[Rob McCool]。中间组件的工作也已经开始，以代理[79](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_79)和共享缓存[59](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_59)的形式，但需要对协议进行扩展，以便它们能够可靠地通信。下面的部分描述了添加到Web体系结构样式中的约束，以指导形成现代Web体系结构的扩展。

---

##### 4.统一接口-Uniform Interface
REST架构风格区别于其他基于网络的风格的核心特征是它强调组件之间的统一接口（[图5-6](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#fig_5_6)）。通过将软件工程的通用性原则应用于组件接口，简化了整个系统的体系结构，提高了交互的可见性。实现与它们提供的服务解耦，这鼓励了独立的可演化性。然而，代价是统一的接口会降低效率，因为信息是以标准化的形式传输的，而不是特定于应用程序需求的形式。REST接口被设计为高效的大粒度超媒体数据传输，针对Web的常见情况进行了优化，但导致接口对于其他形式的架构交互不是最佳的。
![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-uniform_ccss.gif)
为了获得统一的接口，需要多个架构约束来指导组件的行为。REST由四个接口约束定义：资源标识;通过表示操作资源;自描述消息;以及作为应用程序状态引擎的超媒体。这些限制将在[5.2节](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_2)中讨论。

---

##### 5.分层系统-Layered System
为了进一步改善互联网规模需求的行为，我们添加了分层系统约束（[图5-7](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#fig_5_7)）。如[第3.4.2节](https://ics.uci.edu/~fielding/pubs/dissertation/net_arch_styles.htm#sec_3_4_2)所述，分层系统风格通过约束组件行为，使每个组件不能“看到”与其交互的直接层之外，从而允许架构由分层组成。通过将系统的知识限制在一个层上，我们对整个系统的复杂性进行了限制，并促进了基板的独立性。层可用于封装遗留服务并保护新服务免受遗留客户端的影响，通过将不经常使用的功能移动到共享中介来简化组件。中介体还可以用于通过支持跨多个网络和处理器的服务负载平衡来提高系统的可伸缩性。

![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-layered_uccss.gif)
分层系统的主要缺点是它们增加了数据处理的开销和延迟，降低了用户感知的性能[32](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_32)。对于支持缓存约束的基于网络的系统，这可以通过在中介上共享缓存的好处来抵消。将共享缓存放置在组织域的边界可以带来显着的性能优势[136](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_136)。这些层还允许对跨越组织边界的数据实施安全策略，这是防火墙所要求的[79](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_79)。

分层系统和统一界面约束的组合导致了与统一管道和过滤器风格相似的建筑属性（[第3.2.2节](https://ics.uci.edu/~fielding/pubs/dissertation/net_arch_styles.htm#sec_3_2_2)）。虽然REST交互是双向的，但超媒体交互的大粒度数据流可以像数据流网络一样处理，过滤器组件选择性地应用于数据流，以便在内容通过时对其进行转换[26](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_26)。在REST中，中介组件可以主动转换消息的内容，因为消息是自描述的，并且它们的语义对中介可见。


##### 6.按需编码-Code-On-Demand-可选
REST约束集的最后一个增加来自[第3.5.3节的](https://ics.uci.edu/~fielding/pubs/dissertation/net_arch_styles.htm#sec_3_5_3)代码按需样式（[图5-8](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#fig_5_8)）。REST允许通过下载和执行小程序或脚本形式的代码来扩展客户端功能。这通过减少需要预先实现的功能数量来简化客户端。允许在部署后下载功能可以提高系统的可扩展性。然而，它也降低了可见性，因此只是REST中的一个可选约束。
![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-rest_style.gif)
可选约束的概念似乎是一种矛盾修饰法。但是，它在包含多个组织边界的系统的体系结构设计中确实有用途。这意味着架构只有在已知可选约束对整个系统的某些领域有效时才能获得这些约束的好处（并承受其缺点）。例如，如果一个组织内的所有客户端软件都支持Java applet[45](https://ics.uci.edu/~fielding/pubs/dissertation/references.htm#ref_45)，那么该组织内的服务可以通过可下载的Java类来构建，从而获得增强功能的好处。然而，与此同时，组织的防火墙可能会阻止从外部源传输Java applet，因此对于Web的其他部分来说，这些客户端似乎不支持代码按需。一个可选的约束允许我们设计一个体系结构，在一般情况下支持所需的行为，但要理解它可能在某些上下文中被禁用

---

##### 注:风格衍生总结
REST由一组架构约束组成，这些约束是根据它们在候选架构上引入的属性而选择的。虽然这些约束中的每一个都可以单独考虑，但是根据它们从常见架构风格的派生来描述它们，可以更容易地理解它们选择背后的基本原理。[图5-9以图形的方式](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#fig_5_9)描述了REST约束的推导过程，这些约束是根据第3章中所讨论的基于网络的架构风格来确定的

![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-rest_derivation.gif)


**客户端-服务端（Client-Server）**: 这个更专注客户端和服务端的分离，服务端独立可更好服务于前端、安卓、IOS等客户端设备。

**无状态（Stateless）**：服务端不保存客户端状态，客户端保存状态信息每次请求携带状态信息。

**可缓存性（Cacheability）** ：服务端需回复是否可以缓存以让客户端甄别是否缓存提高效率。

**统一接口（Uniform Interface）**：通过一定原则设计接口降低耦合，简化系统架构，这是RESTful设计的基本出发点。

**分层系统（Layered System）**：客户端无法直接知道连接的到终端还是中间设备，分层允许你灵活的部署服务端项目。

**按需代码（Code-On-Demand，可选）**：按需代码允许我们灵活的发送一些看似特殊的代码给客户端例如JavaScript代码。




### 二、RESTful的最佳实践

> 如果一个架构符合REST原则，就称它为RESTful架构。

#### 请求设计
客户端发出的数据操作指令都是"动词 + 宾语"的结构。比如，`GET /articles`这个命令，`GET`是动词，`/articles`是宾语。
例如:

![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-v2-3885a949c41a2765f91f1bd4e2d053e2_1440w.png)

##### HTTP动词
###### 动词介绍

动词根据 HTTP 规范，动词一律大写。
在RESTful API中，不同的HTTP请求方法有各自的含义，这里就展示GET,POST,PUT,DELETE几种请求API的设计与含义分析。针对不同操作，具体的含义如下：
```http
GET /collection：从服务器查询资源的列表（数组）
GET /collection/resource：从服务器查询单个资源
POST /collection：在服务器创建新的资源
PUT /collection/resource：更新服务器资源
DELETE /collection/resource：从服务器删除资源
```
![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-v2-23c1db5e27ac6e5d6d16674f343cece8_1440w.png)


在非RESTful风格的API中，我们通常使用GET请求和POST请求完成增删改查以及其他操作，查询和删除一般使用GET方式请求，更新和插入一般使用POST请求。从请求方式上无法知道API具体是干嘛的，所有在URL上都会有操作的动词来表示API进行的动作，例如：query，add，update，delete等等。

而RESTful风格的API则要求在URL上都以名词的方式出现，从几种请求方式上就可以看出想要进行的操作，这点与非RESTful风格的API形成鲜明对比。

在谈及GET,POST,PUT,DELETE的时候，就必须提一下接口的**安全性和幂等性**，其中安全性是指方法不会修改资源状态，即读的为安全的，写的操作为非安全的。而幂等性的意思是操作一次和操作多次的最终效果相同，客户端重复调用也只返回同一个结果。

上述四个HTTP请求方法的安全性和幂等性如下：

|HTTP Method|安全性|幂等性|解释|
|---|:--|:--|---|
|GET|安全|幂等|读操作安全，查询一次多次结果一致|
|POST|非安全|非幂等|写操作非安全，每多插入一次都会出现新结果|
|PUT|非安全|幂等|写操作非安全，一次和多次更新结果一致|
|DELETE|非安全|幂等|写操作非安全，一次和多次删除结果一致|


###### 动词覆盖，应对服务器不完全支持 HTTP 的情况

有些客户端只能使用GET和POST这两种方法。服务器必须接受POST模拟其他三个方法（PUT、PATCH、DELETE）。

这时，客户端发出的 HTTP 请求，要加上X-HTTP-Method-Override属性，告诉服务器应该使用哪一个动词，覆盖POST方法。


---

##### 宾语


###### 避免在URI中使用动词

> 如果您已经理解了基本知识，那么现在您就会知道在URI中放置动词不是REST风格的。这是因为HTTP动词应该足以描述对资源执行的操作。

例如:
```http
# 错误的写法:
POST: /articles/createNewArticle/

# 正确的写法
POST: /articles/
```

---

###### 使用复数资源名词

可能很难决定是否应该使用复数或单数形式的资源名词。
你应该使用`/article/:id/`（单数）还是`/articles/:id/`（复数）?
我同意`GET /article/2/`是好的，但是`GET /article/`呢?我们得到的是系统中唯一的一篇文章，还是所有的？
```http

GET: /articles/2/ 

POST: /articles/ 
...
```
---


###### 优雅地处理尾随斜杠
URI是否应该有一个尾随的`/`并不是一个真正的争论。
简单地选择一种方式或另一种方式（即，带或不带尾随斜杠），坚持它，并优雅地重定向客户端，如果他们使用错误的约定。


```http
添加尾斜杠
POST: /entities/

不添加尾斜杠
POST: /entities

```
专业提示：大多数Web框架都可以选择优雅地重定向到URL的trailed或untrailed版本。找到这个选项并激活它。

---


###### 分页与过滤信息

用户可能希望检索满足特定条件的项，或者一次检索少量项以提高性能。这正是过滤和分页的目的。通过筛选，用户可以指定返回项应具有的属性。

分页允许用户检索数据集的部分。最简单的一种分页是页码分页，它由`page`和`page_size`决定。
现在的问题是：如何将这些特性合并到RESTful API中？
我的回答是：使用querystring。
我认为使用querystring进行分页的原因很明显。它看起来像这样：
```http
GET: /articles/?page=1&page_size=10
```

但对于过滤来说可能不那么明显。首先，您可能会想到这样做，只检索已发布文章的列表：
```http
GET: /articles/published/
```

设计问题：`published`不是资源！相反，它是您正在检索的数据的一个特征。这类东西应该放在查询字符串中。
所以最后，用户可以像这样检索"第二页的已发表文章，包含20个项目"：
```http
GET: /articles/?published=true&page=2&page_size=20
```

下面是一些常见的参数。

```http
?limit=10：指定返回记录的数量
?offset=10：指定返回记录的开始位置。
?page=2&per_page=100：指定第几页，以及每页的记录数。
?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
?animal_type_id=1：指定筛选条件
```

参数的设计允许存在冗余，即允许API路径和URL参数偶尔有重复。比如，`GET /zoo/ID/animals` 与 `GET /animals?zoo_id=ID` 的含义是相同的。

---

###### 不要嵌套资源
REST API处理资源，检索资源的列表或单个实例是简单的。但是，当您处理相关资源时会发生什么？

假设我们想要检索某个作者的文章列表-即带有`id=12`的作者。基本上有两种选择。
第一个选项是将`articles`资源嵌套在`authors`资源下，例如：
`GET: /authors/12/articles/`

有些人推荐它，因为它确实代表了作者和他们的文章之间的一对多关系。

但是，现在还不清楚您请求的是哪种资源。是作者吗？是文章吗？
同样，[平面比嵌套好](https://www.python.org/dev/peps/pep-0020/#id3)，所以一定有更好的方法......确实有！
我的建议是使用querystring直接过滤`articles`资源：

`GET: /articles/?author_id=12`

这显然意味着：“获取作者#12的所有文章”，对吗

---
###### 其他

- <font color="#3271ae">不符合 CRUD 情况的 RESTful API</font>

在实际资源操作中，总会有一些不符合 CRUD（Create-Read-Update-Delete） 的情况，一般有几种处理方法。

1、使用 POST，为需要的动作增加一个 endpoint，使用 POST 来执行动作，比如: POST /resend 重新发送邮件。

2、增加控制参数，添加动作相关的参数，通过修改参数来控制动作。比如一个博客网站，会有把写好的文章“发布”的功能，可以用上面的 POST /articles/{:id}/publish 方法，也可以在文章中增加 published:boolean 字段，发布的时候就是更新该字段 PUT /articles/{:id}?published=true

3、把动作转换成资源，把动作转换成可以执行 CRUD 操作的资源， github 就是用了这种方法。

比如“喜欢”一个 gist，就增加一个 /gists/:id/star 子资源，然后对其进行操作：“喜欢”使用PUT /gists/:id/star，“取消喜欢”使用 DELETE /gists/:id/star。

另外一个例子是 Fork，这也是一个动作，但是在 gist 下面增加 forks资源，就能把动作变成 CRUD 兼容的：POST /gists/:id/forks 可以执行用户 fork 的动作。

> 其他建议:
	不用大写字母，所有单词使用英文且小写。
	连字符用中杠`"-"`而不用下杠`"_"`




#### 响应设计
##### 状态码
- <font color="#3271ae">使用正确的状态码</font>
一旦你掌握了状态代码，你应该努力始终如一地使用它们。

例如，如果您选择`POST`端点在某处返回`201 Created`，则对每个`POST`端点使用相同的状态代码。

为什么？为什么？因为用户不必担心哪个端点上的哪个方法将在什么情况下返回哪个状态码。

所以要保持一致，如果你偏离了惯例，用大的标志把它记录下来。

一般来说，我坚持以下几点：
```http
GET: 200 OK 
POST: 201 Created 
PUT: 200 OK 
PATCH: 200 OK 
DELETE: 204 No Content
```


---

##### 服务器响应

###### 不返回纯文本
API 返回的数据格式，不应该是纯文本，而应该是一个 JSON 对象，因为这样才能返回标准的结构化数据。所以，服务器回应的 HTTP 头的Content-Type属性要设为application/json。

客户端请求时，也要明确告诉服务器，可以接受 JSON 格式，即请求的 HTTP 头的ACCEPT属性也要设成application/json。

---
###### 消息正文中的空集合
任何时候成功响应的主体为空，状态代码都应该是204（无内容）。对于空集合，例如对没有项目的筛选请求的响应，状态代码应该仍然是204（无内容），而不是200（正常）。


---
###### 发生错误时，不要返回 200 状态码

有一种不恰当的做法是，即使发生错误，也返回200状态码，把错误信息放在数据体里面，就像下面这样。
```json
{
	"status": "failure", 
	"data": { 
		"error": "Expected at least two items in list."
		} 
}
```

正确的做法是，状态码反映发生的错误，具体的错误信息放在数据体里面返回。下面是一个例子。
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json
{
  "error": "Invalid payoad.",
  "detail": {
    "surname": "This field is required."
  }
}
```

###### 提供链接

API 的使用者未必知道，URL 是怎么设计的。一个解决方法就是，在回应中，给出相关链接，便于下一步操作。这样的话，用户只要记住一个 URL，就可以发现其他的 URL。这种方法叫做 HATEOAS。

举例来说，GitHub 的 API 都在 [api.github.com](https://api.github.com/) 这个域名。访问它，就可以得到其他 URL。
```json
{
  ...
  "feeds_url": "https://api.github.com/feeds",
  "followers_url": "https://api.github.com/user/followers",
  "following_url": "https://api.github.com/user/following{/target}",
  "gists_url": "https://api.github.com/gists{/gist_id}",
  "hub_url": "https://api.github.com/hub",
  ...
}
```

上面的回应中，挑一个 URL 访问，又可以得到别的 URL。对于用户来说，不需要记住 URL 设计，只要从 api.github.com 一步步查找就可以了。

HATEOAS 的格式没有统一规定，上面例子中，GitHub 将它们与其他属性放在一起。更好的做法应该是，将相关链接与其他属性分开。
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "In progress",
   "links": {[
    { "rel":"cancel", "method": "delete", "href":"/api/status/12345" } ,
    { "rel":"edit", "method": "put", "href":"/api/status/12345" }
  ]}
}
```


##### 版本控制

[RESTful Web API的版本控制](https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design#versioning-a-restful-web-api)


###### 无版本控制

这是最简单的方法，对于某些内部API来说可能是可以接受的。重要的更改可以表示为新资源或新链接。向现有资源添加内容可能不会带来重大更改，因为不希望看到此内容的客户端应用程序将忽略它。

例如，对URI `https://adventure-works.com/customers/3`的请求应该返回单个客户的详细信息，其中包含客户端应用程序所期望的`id`、`name`和`address`字段：

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{"id":3,"name":"Contoso LLC","address":"1 Microsoft Way Redmond WA 98053"}
```


> 注意:为简单起见，本节中显示的示例响应不包括HATEOAS链接。

如果将`DateCreated`字段添加到客户资源的模式中，则响应将如下所示：


```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{"id":3,"name":"Contoso LLC","dateCreated":"2014-09-04T12:11:38.0376089Z","address":"1 Microsoft Way Redmond WA 98053"}
```

如果现有的客户端应用程序能够忽略无法识别的字段，则它们可能继续正常工作，而新的客户端应用程序可以设计为处理此新字段。然而，如果发生对资源模式的更根本的改变（诸如移除或重命名字段）或者资源之间的关系改变，则这些可能构成阻止现有客户端应用程序正确运行的破坏性改变。在这些情况下，您应该考虑以下方法之一。

###### URI版本控制

每次修改Web API或更改资源架构时，都要向每个资源的URI添加版本号。以前存在的URI应该继续像以前一样操作，返回符合其原始模式的资源。

扩展前面的示例，如果`address`字段被重构为包含地址的每个组成部分的子字段（例如`streetAddress`、`city`、`state`和`zipCode`），则可以通过包含版本号的URI（例如`https://adventure-works.com/v2/customers/3`）来公开资源的此版本：

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{"id":3,"name":"Contoso LLC","dateCreated":"2014-09-04T12:11:38.0376089Z","address":{"streetAddress":"1 Microsoft Way","city":"Redmond","state":"WA","zipCode":98053}}
```

这种版本控制机制非常简单，但依赖于服务器将请求路由到适当的端点。然而，随着Web API经过多次迭代而变得成熟，并且服务器必须支持许多不同的版本，它可能变得笨拙。此外，从纯粹主义者的角度来看，在所有情况下，客户端应用程序都在获取相同的数据（客户端3），因此URI不应该因版本而异。这种方案也使HATEOAS的实现复杂化，因为所有链接都需要在其URI中包含版本号。

###### 查询字符串版本控制

不需要提供多个URI，您可以通过使用附加到HTTP请求的查询字符串中的参数来指定资源的版本，例如`https://adventure-works.com/customers/3?version=2`。如果旧的客户端应用程序省略了version参数，则该参数应默认为有意义的值，例如1。

这种方法具有语义优势，即总是从相同的URI检索相同的资源，但它依赖于处理请求的代码来解析查询字符串并发回适当的HTTP响应。这种方法在实现HATEOAS时也会遇到与URI版本控制机制相同的复杂性。

> 注意:
	一些较旧的Web浏览器和Web代理不会缓存URI中包含查询字符串的请求的响应。这会降低使用web API并且从这样的web浏览器内运行的web应用的性能


###### 标头版本控制

与其将版本号作为查询字符串参数追加，不如实现一个指示资源版本的自定义标头。这种方法要求客户端应用程序将适当的标头添加到任何请求中，尽管如果省略了版本标头，处理客户端请求的代码可以使用默认值（版本1）。以下示例使用名为Custom-Header的自定义标头。此标头的值指示Web API的版本。

版本1：

```http
GET https://adventure-works.com/customers/3 HTTP/1.1
Custom-Header: api-version=1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{"id":3,"name":"Contoso LLC","address":"1 Microsoft Way Redmond WA 98053"}
```

第二版：

```http
GET https://adventure-works.com/customers/3 HTTP/1.1
Custom-Header: api-version=2
```


```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{"id":3,"name":"Contoso LLC","dateCreated":"2014-09-04T12:11:38.0376089Z","address":{"streetAddress":"1 Microsoft Way","city":"Redmond","state":"WA","zipCode":98053}}
```

与前两种方法一样，实现HATEOAS需要在任何链接中包含适当的自定义头。

###### 媒体类型版本控制

当客户端应用程序向Web服务器发送HTTP GET请求时，它应该通过使用Accept头来规定它可以处理的内容的格式，如本指南前面所述。Accept头的用途通常是允许客户端应用程序指定响应的主体是XML、JSON还是客户端可以解析的其他一些常见格式。但是，可以定义自定义媒体类型，其中包括使客户端应用程序能够指示它所期望的资源版本的信息。

下面的示例显示了一个请求，该请求指定了一个值为application/vnd.adventure-works.v1+json的Accept标头。vnd.adventure-works.v1元素向Web服务器指示它应该返回资源的版本1，而json元素指定响应主体的格式应该是JSON：



```http
GET https://adventure-works.com/customers/3 HTTP/1.1
Accept: application/vnd.adventure-works.v1+json
```

处理请求的代码负责处理Accept标头并尽可能地接受它（客户端应用程序可以在Accept标头中指定多种格式，在这种情况下，Web服务器可以为响应正文选择最合适的格式）。Web服务器使用Content-Type头确认响应正文中数据的格式：



```http
HTTP/1.1 200 OK
Content-Type: application/vnd.adventure-works.v1+json; charset=utf-8

{"id":3,"name":"Contoso LLC","address":"1 Microsoft Way Redmond WA 98053"}
```

如果Accept标头未指定任何已知媒体类型，则Web服务器可能会生成HTTP 406（不可接受）响应消息或返回具有默认媒体类型的消息。

这种方法可以说是最纯粹的版本控制机制，并且很自然地适用于HATEOAS，它可以在资源链接中包含MIME类型的相关数据。

> 注意:
	选择版本控制策略时，还应该考虑对性能的影响，特别是Web服务器上的缓存。URI版本控制和查询字符串版本控制方案是缓存友好的，因为相同的URI/查询字符串组合每次引用相同的数据。
	标头版本控制和媒体类型版本控制机制通常需要额外的逻辑来检查自定义标头或接受标头中的值。在大规模环境中，使用不同版本的Web API的许多客户端可能会导致服务器端缓存中出现大量重复数据。如果客户端应用程序通过实现缓存的代理与Web服务器通信，并且仅在其缓存中当前未保存所请求数据的副本时才将请求转发到Web服务器，则此问题可能变得严重。





##### JSON API

**英文版：**[http://jsonapi.org/format/](https://jsonapi.org/format/)
**中文版：**[http://jsonapi.org.cn/format/](http://jsonapi.org.cn/format/) （PS：中文版更新不及时，请以英文文档为准）


这里说一下JSON,其他的格式看文档
在[顶级节点](http://jsonapi.org.cn/format/#document-structure-top-level)使用data、errors、meta，来描述数据、错误信息、元信息，注意data和errors应该互斥，不能再一个文档中同时存在，meta在项目实际上用的很少，只有特别情况才需要用到，比如返回服务器的一些信息




### 三、请求的发送与响应


#### 原生Ajax

##### ajax发送请求
> 了解就行,平常开发使用封装好的axios库发送请求比较多

以下为POST请求
```html
<!--#region  -->
  <button id="btn-post">Ajax发送restful风格的请求:POST新增</button>
  <script type="text/javascript">
    window.onload = function () {
        document.getElementById("btn-post").onclick = function () {
            //1. 创建AJAX核心对象
            var xhr = new XMLHttpRequest();
            //2. 注册回调函数
            xhr.onreadystatechange = function(){
                if (this.readyState == 4) {
                    if (this.status == 200) {
                        //响应类型为json
                       this.responseType = "json"
                       console.log(this.response)
                    }else{
                        alert(this.status)
                    }
                }
            }
            //3. 开启通道
            xhr.open("POST", "http://localhost:8080/student", true)
            //4. 发送请求
            // 设置请求头的内容类型:json格式
            xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8") 
            // 设置响应类型为json
            xhr.responseType = "json";


            // 模拟一段json数据
            var data={
                "name":"张三",
                "age": 12,
                "addr": "北京大兴区"
                }
            var stringData=JSON.stringify(data);
            // send函数中的参数就是发送的数据，这个数据在“请求体”当中发送。
            xhr.send(stringData);

        }
    }
</script>
<!-- #endregion -->
```

以下为DELETE请求
```html
<!--#region  -->
<button id="btn-delete">Ajax发送restful风格的请求:DELETE删除</button>
<script type="text/javascript">
  window.onload = function () {
      document.getElementById("btn-delete").onclick = function () {
          //1. 创建AJAX核心对象
          var xhr = new XMLHttpRequest();
          //2. 注册回调函数
          xhr.onreadystatechange = function(){
              if (this.readyState == 4) {
                  if (this.status == 200) {
                      //响应类型为json
                     this.responseType = "json"
                     console.log(this.response)
                  }else{
                      alert(this.status)
                  }
              }
          }
          //3. 开启通道
          xhr.open("DELETE", "http://localhost:8080/student/1", true)
          //4. 发送请求
          // 设置请求头的内容类型:json格式
          xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8") 
          // 设置响应类型为json
          xhr.responseType = "json";

          // send函数中的参数就是发送的数据，这个数据在“请求体”当中发送。
          xhr.send();

      }
  }
</script>
<!-- #endregion -->
```

那么可以知道,其他的put、patch请求应该是相似的

##### 接收数据
```java
@RestController
// 这个跨域的注解不需要,我测试的时候使用的
@CrossOrigin  
@RequestMapping("/student")  
public class StudentController {  

	// @RequestBody解析请求体中的数据
	@RequestMapping(method = RequestMethod.POST)  
	public String save(@RequestBody Student student){  
		System.out.println("POST:save:==>" + student);  
		return "{}";  
	}  

	// @PathVariable解析路径上的参数
	@RequestMapping(value = "/{id}" ,method = RequestMethod.DELETE)  
	public String delete(@PathVariable String id){  
		System.out.println("DELETE:delete:id==>" + id );  
		return "{}";  
	}  
  
}
```


---

#### 封装后的Ajax

[转载](https://www.cnblogs.com/wwct/p/12396799.html)
##### 请求

```html
<form action="/emps" method="post">
    <input type="hidden" name="_method" value="PUT">
    <input type="text" name="username">
    <input type="password" name="password">
            <input type="submit"/>
</form>
```
###### 方式一:通过 ajax 发送 DELETE 请求（需要带_method参数）

利用 `_method` 参数对 request 请求进行转换，所以这种方式同样需要配置HiddenHttpMethodFilter 过滤器。
以下以删除员工为例子（传递员工编号empId）：
```js
/* 删除员工 */
function deleteEmp(empId){
    $.ajax({
        url : "emps",
        data : {_method : "DELETE", empId : empId},
        type : "POST",
        success : function(result){    
 
        }
    })
}
```

发送表单 ajax 请求：
```js
$("#updateBtn").click(function(){
            $.ajax({
                url : "emps",
                data : $("#updateEmpFormNode").serialize()+"&_method=put",
                type : "post",
                success : function(result){
                    alert(result);
                }
            }) 
 
        })
```

```java
@RequestMapping(value="/emps", method=RequestMethod.PUT)
public String updateEmp(Employee employee) {
    System.out.println(employee);
    return "redirect:success.jsp";
}
```


###### 方式二:直接指定 ajax 请求中的 type 为 put/delete(不带 `_method` 参数)
1. 把上述第二点的表单更新改写为如下：
```js
$("#updateBtn").click(function(){
            $.ajax({
                url : "emps",
                data : $("#updateEmpFormNode").serialize(),
                type : "PUT",
                success : function(result){
                    alert(result);
                }
            })     
 
        })
```

![](https://gitcode.net/qq_50848214/image/-/raw/master/411B-A1B-RESTful-1740128-20200302173628741-2008861850.png)
 原因：  
这问题是由于 Tomcat 本身引起的，导致这个问题是因为 SpringMVC 绑定 POJO 对象时获取不到数据，然后执行更新语句时 sql 语句出错导致的。由于 POJO 的数据都为空，所以被执行的更新语句可能会为 update emp set where empId = ?，反正被执行更新语句肯定是有错的。想要知道为什么获取不到数据，下面首先先了解一下 Tomcat 如何封装数据以及SpringMVC如何绑定数据
```java
1.1 Tomcat 封装表单数据和 SpringMVC 绑定 POJO 对象数据时的流程如下：  
		① Tomcat 首先会将请求体中的数据，封装一个map。  
		② request.getParameter("empName") 就会从这个map中取值。  
		③ SpringMVC封装POJO对象的时候，通过 request.getParamter("empName"); 获取一个字段的值，然后赋值到      POJO 中属性名为 empName 的属性。如：  
				   String temp = (String)request.getParamter("empName");  
				   Employee emp = new Employee();  
				   emp.setEmpName(temp);
1.2 由于 Ajax 发送的是 PUT 请求，Tomcat一看是PUT不会封装请求体中的数据为map，只有POST形式的请求才封装请求体为map，查看 Tomcat 的源码：  
	查找到 protected void parseParameters() 该方法  
	protected String parseBodyMethods = "POST";  
	if( !getConnector().isParseBodyMethod(getMethod()) ) {  
			  success = true;  
			  return;  
	}  
   当 Tomcat 知道是请求不是 POST 请求时，会直接 return，而不会继续往下执行解析封装参数，所以当                        request.getParamter("empName") 从 map 取数据时，由于 empName 参数没有被封装到 map 中，getParmater获取到值为 null。
```

解决方法
2.1 在 web.xml 配置上HttpPutFormContentFilter
```xml
	<filter>
	    <filter-name>HttpPutFormContentFilter</filter-name>
	    <filter-class>org.springframework.web.filter.HttpPutFormContentFilter</filter-class>
	</filter>
	<filter-mapping>
	    <filter-name>HttpPutFormContentFilter</filter-name>
	    <url-pattern>/*</url-pattern>
	</filter-mapping>
```
2.2  HttpPutFormContentFilter 的作用；将请求体中的数据解析包装成一个map。
2.3  request被重新包装，request.getParameter()被重写，就会从自己封装的map中取数据

```java
@RequestMapping(value="/emps", method=RequestMethod.PUT)
public String updateEmp(Employee employee) {
    System.out.println(employee);
    return "redirect:success.jsp";
}
```



###### 方式三:仍然使用PUT DELETE 请求：传递参数的时候data需要设置为json字符串
1.仍然使用put和delete请求，直接指定 ajax 请求中的 type 为 put/delete(不带 `_method` 参数)，并且需要传递参数的时候data需要设置为json字符串。（SpringBoot环境中不需要配置任何东西，其他未知）
```js
var jsonstr = {"id":1,"name":"zsw"};
$.ajax({
    url:"/update",
    type:"PUT",
    contentType:"application/json",//设置请求参数类型为json字符串
    data:JSON.stringify(jsonstr),//将json对象转换成json字符串发送
    dataType:"json",
    success:function(result){
        alert(result);
    },
});
```

客户端需要使用@RequestBody标注
```js
@RequestMapping(value = "update",method = RequestMethod.PUT)
public String update(@RequestBody  Book book){
    System.out.println(book);
    return BookClient.update(book);
}
```


---


#### 原生表单
##### 表单模拟数据发送
> 说明: get与post请求可以直接使用表单发送,但是对于http的其他请求,无法直接发送
> 需要使用post请求模拟发送

```html
  <form id="form" action="http://localhost:8080/student/1" method="post">
    <!-- 使用"_method" 进行模拟,但本质上还是个post请求 -->
    <input type="hidden" name="_method" value="put" />
    姓名：<input name="name" type="text"/>
    年龄：<input name="age" type="number"/>
    地址：<input name="addr" type="text"/>
    <button type="submit" name="提交"/>
  </form>
```


###### HiddenHttpMethodFilter

> 为了对所有进行入的请求进行判断,通过`_method`中的内容,将请求替换为目标请求方式
> 需要在接收数据之前需要添加一个HiddenHttpMethodFilter过滤器

添加的方式有两种1:

###### 方式一,直接在web.xml中进行配置
> **HiddenHttpMethodFilter必须作用于dispatcher前**
```xml
	<!-- HiddenHttpMethodFilter  -->
        <filter>  
                <filter-name>HiddenHttpMethodFilter</filter-name>  
                <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>  
        </filter>  
        <filter-mapping>  
                <filter-name>HiddenHttpMethodFilter</filter-name>  
                <url-pattern>/*</url-pattern>
        </filter-mapping>
        
	    <!-- DispatcherServlet  -->
        <servlet>
			<servlet-name>spring</servlet-name>
			<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
			<init-param>
				<param-name>contextConfigLocation</param-name>
				<param-value>classpath:dispatcher.xml</param-value>
			</init-param>
		</servlet>
	    <servlet-mapping>
			<servlet-name>spring</servlet-name>
			<url-pattern>*.html</url-pattern>
		</servlet-mapping>
```

###### 方式二:使用注解
```java
package com.itheima.config;
// import ...

public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }

    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    @Override
    protected Filter[] getServletFilters() {
        Filter[] filters = new Filter[2];
		// 这个可以忽略,是字符编码的配置
        CharacterEncodingFilter characterEncodingFilter = new CharacterEncodingFilter();
        characterEncodingFilter.setEncoding("UTF-8");
        filters[0] = characterEncodingFilter;
		// HiddenHttpMethodFilter配置
        HiddenHttpMethodFilter hiddenHttpMethodFilter = new HiddenHttpMethodFilter();
        filters[1] = hiddenHttpMethodFilter;
        return filters;
    }
}
```

```java
package com.itheima.config;
// import ...

@Configuration  
@ComponentScan("com.itheima.controller")  
@EnableWebMvc  
public class SpringMvcConfig {  
}
```

###### 源码分析
```java
public class HiddenHttpMethodFilter extends OncePerRequestFilter {
    private static final List<String> ALLOWED_METHODS;
    public static final String DEFAULT_METHOD_PARAM = "_method";
	
	//因为这里固定了参数名称，所以我们在写请求隐含参数名称是必须写成“_method”
    private String methodParam = "_method";

    public HiddenHttpMethodFilter() {
    }

    public void setMethodParam(String methodParam) {
		// 如果在配置过滤器时对methodParam进行了指定,那么前端表单中的"_method"就换成你指定的内容
        Assert.hasText(methodParam, "'methodParam' must not be empty");
        this.methodParam = methodParam;
    }
		
	//处理过程：如果是POST请求就正常使用，如果不是POST请求，就将这个请求名称大写化，然后再使用对应的请求
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
	    
	    // 原来的请求
        HttpServletRequest requestToUse = request;
        if ("POST".equals(request.getMethod()) && request.getAttribute("javax.servlet.error.exception") == null) {
            String paramValue = request.getParameter(this.methodParam);
            if (StringUtils.hasLength(paramValue)) {
                String method = paramValue.toUpperCase(Locale.ENGLISH);
                if (ALLOWED_METHODS.contains(method)) {
	                // 更换了新的请求方式的"请求"
                    requestToUse = new HiddenHttpMethodFilter.HttpMethodRequestWrapper(request, method);
                }
            }
        }
		// 使用"新"的请求继续执行过滤链
        filterChain.doFilter((ServletRequest)requestToUse, response);
    }

    static {
        ALLOWED_METHODS = Collections.unmodifiableList(Arrays.asList(HttpMethod.PUT.name(), HttpMethod.DELETE.name(), HttpMethod.PATCH.name()));
    }

    private static class HttpMethodRequestWrapper extends HttpServletRequestWrapper {
        private final String method;

        public HttpMethodRequestWrapper(HttpServletRequest request, String method) {
            super(request);
            this.method = method;
        }

        public String getMethod() {
            return this.method;
        }
    }
}

```



##### 接收数据
```java
@RestController  

@RequestMapping("/student")  
public class StudentController {  
	// 注: 不添加@RequestBody
	@RequestMapping(value = "/{id}" ,method = RequestMethod.PUT)  
	public String delete(@PathVariable String id, Student student){  
		System.out.println("PUT:id"+ id);  
		System.out.println("PUT:student"+ student);  
		return "{}";  
	}  
}
```

---

#### axios
直接使用对应的请求方式发送即可

js库:[Axios](https://axios.nodejs.cn/docs/intro)






---

> Citation:
> - []()
> 
> References:
> - [REST出处:博士论文:见第五章节](https://ics.uci.edu/~fielding/pubs/dissertation/top.htm)
> - [怎样用通俗的语言解释REST，以及RESTful](https://www.zhihu.com/question/28557115)
> - [方法论：如何学习HTTP](https://juejin.cn/post/7046195769681903630)
> - [一文搞懂什么是RESTful API](https://segmentfault.com/a/1190000038408645)
> - [RESTful API设计：让用户满意的13个最佳实践](https://florimond.dev/en/posts/2018/08/restful-api-design-13-best-practices-to-make-your-users-happy/)
> - [RESTful Web API设计](https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design)
> - [RESTful API 最佳实践](https://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html)
> - [RESTful设计](https://restfulapi.cn/)
> - [细说API - 重新认识RESTful](https://zhuanlan.zhihu.com/p/54976216)
