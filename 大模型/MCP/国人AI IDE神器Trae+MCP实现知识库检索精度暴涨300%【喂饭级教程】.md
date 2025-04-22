---
标题: "国人AI IDE神器Trae+MCP实现知识库检索精度暴涨300%【喂饭级教程】"
链接: "https://mp.weixin.qq.com/s/0TdooxF9hvpkL5SBLHRF0w"
作者: "[[袋鼠帝]]"
创建时间: "2025-04-22T12:21:01+08:00"
摘要: "{{\"One-sentence summary of the article content,translated to Chinese\"}}"
tags:
  - "clippings"
  - "{{\"Analyze the article and create up to 5 tags in comma-separated format. Tags should be in Chinese unless necessary for company names"
  - "person names or abbreviations. One tag must be selected from: \"UI 设计"
  - "AI"
  - "编程"
  - "经济"
  - "效率"
  - "产品\". Other tags should be based on the article's topic"
  - "mentioned people"
  - "companies or products.\"}}"
字数: "147"
状态: "未开始"
---
# [[学习方法/预读法介绍]]
### 预读问题  
**基于你的目标**：
- Q1: 
- Q2: 
- Q3:   

### 关键图表/代码  
![[提取的图表或代码片段]]
### 初步关联  
- 已知：[[已掌握的相关知识]]  
- 未知：`#待探索`  

### 输出目标
- [ ] 

### 总结
- 是什么
- 为什么
- 怎么用

# 内容
#flashcards
![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/3QzcPBL9P1Bry0dwyd9Kczt6HWJzxZHvaliaGXnzEJdwE9Qhl0xwoUiaPYKPicgbRdryw3eQYSp8icS1icCPUJy5pxQ/0?wx_fmt=jpeg)

原创 袋鼠帝 [袋鼠帝AI客栈](https://mp.weixin.qq.com/s/)

2025-04-22 09:15:51

精确发文时间由壹伴提供

手机阅读

大家好，我是袋鼠帝

一直以来我写了不少 AI知识库 相关的分享。

但是很多朋友可能都面临一个 痛点：

就是满怀期待的把资料“投喂”进知识库后，以为大模型能把所有资料完整“消化吸收”了。结果一测试发现 问答效果不尽如人意。

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicKE5s93urtSicRlL6zuWWFlPica3T2ma62CfvQEehOEKs4fscD9XKIzUQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicVAOibQD6LqzaAkKPLlJibV44ic0rCQfLr7CvSWUicIKNS8lczV1QhVhSFw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

咱们得先明白，RAG它不是银弹，不是全能的，它也有局限性，并不适合所有场景。

RAG的原理其实网上已经有非常多的资料了，这里就不详细赘述了。

下面这个图， 形象的展示了RAG的工作原理

![1111.png](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicnkrfDgu9hN6OvnvUKTSyIYW2NOyicQEicCmf5bH6JdxhGJR0DuGHAfJw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我们先探讨一下 RAG的局限性：

  

1.文件分片： 文件分片本身不是局限性，但是分片导致原本连贯的内容被分割，就会导致后期检索到的内容信息缺失。

  

2.检索不精确： 因为RAG是使用向量比对的方式（数学的维度）来查询语义相近的内容，但是这也会导致有时候匹配的内容可能并不是我们想要的信息。

  

3.没有全局概念： 由于知识库里面的文件都是分片存储，每次回答只会检索部分内容，所以，很难准确回答一些全局性的问题（或者说统计型的问题），比如知识库中的老师一共有多少位，一季度有多少个订单等等。

第一个问题（文件分片导致上下文丢失）其实在我之前的一篇文章里面已经给出了一个解决方案。

就是大力出奇迹：使用超长上下文的模型，把相关的不相关的内容出来都检索丢进去，给大模型自己判别，所以这个模型还必须有超强的"大海捞针"能力。感兴趣的朋友可以看看。

> 超长上下文开源模型minimax-01，支持400万tokens
> 
> 袋鼠帝，公众号：袋鼠帝AI客栈 [dify v1.1.0接入这个开源LLM，知识库效果直接起飞，真可以封神了！【喂饭级教程】](https://mp.weixin.qq.com/s/7y6ep0UJkZLvcvaowrilog)

那么剩下的两个问题，可以 搭配传统的数据库来解决。

其实一个月前就有朋友给我提过这个方案。

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicQ0vfcUhy4cHKhD4fldExsTxpRuJ46cGqHV9vXNOoYhdxsfAONicYCWw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

但是，那时候，我觉得这个方案还没有很成熟，而且操作起来较为繁琐，所以就一直没有分享。

直到最近MCP的大火，至少让AI大模型接入数据库的门槛又降低不少。

以及我平时最最喜欢用的 字节旗下的AI IDE神器：Trae ，终于终于 支持MCP了！

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1Bry0dwyd9Kczt6HWJzxZHvM0tdNoL153s9wZIDHUdaxzDsUPeIyKJFgYSdZqFPprDjP7tz1yM8DA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

国内版Trae下载地址：  

https://www.trae.com.cn/

海外版Trae下载地址（需要科学上网）：

https://www.trae.ai/

它直接就内置了 数据库的MCP-Server ，这意味着我们可以通过MCP把数据库一键接入大模型。

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicbicxvoKicrWoamGrsLMvoic8cnu7ed1mgAunuqF48e6EsBNAgbFZKyicjQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

本期将主要以PostgreSQL这个简单、轻量的关系型数据库为例，带大家接入（同时它应该也能满足大部分的使用场景了）。

*声明，数据库方案更适合表格类型的数据，文本建议参考“大力出奇迹方案“*

另外 使用Trae的MCP能力 ，也 需要先在本地安装Python环境、Node环境 （这块网上资料很多），也可以问AI～

好了，接下来我们开始喂饭。

  

一、安装PostgreSQL

PostgreSQL官网下载地址：

https://www.postgresql.org/download/

自行选择合适的平台下载即可（跟着流程点点点）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicZEic3IBovIjsK7jvvKEZAuCLbroJ2QnIpfFN1FyDo25pa3MPml15aYQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后我们在安装一个图形化界面，方便操作数据库。

我们选择这个免费的 dbeaver

下载地址： https://dbeaver.io/download/

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicbVWS5ObB1PGrrex8rOLxic6IiaNgv9ibBrZjozuhSF7Zf45picC4plGUyw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

打开dbeaver，点击右上角的小+号，选中PostgreSQL添加

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicKjMyzBCfUvK9RtgK9WDeNLTIMbWaZG5RiceLrd1pBAmLXUxchwqPdUg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

其他 默认配置即可，在下图，我们只需要填上安装PostgreSQL过程中的自己设置的密码，点击完成

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAic7L2bEZ4zyViclDEQKss9p2GJMZibcX1XWOvMjMtlp8TpqDcbraDWF7xw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

添加好本地的PostgreSQL之后，左边会出现一个小图标，双击一下连接数据库。

可能会要求安装连接数据库的相关驱动，跟着步骤安装即可

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicaMTrqYJsAx6sXECTE3ARZ1wOoNy7KyYEk8ojSuB3HYvmTibeKqW0awQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

驱动安装成功之后，可以看到数据库大象图标那里有个小勾。

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicw7wtibvd7DbZAcZqG7hGAughTjZuhFcwQLFMQN1brMWbq2J8SzRSMuw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

Trae中配置PostgreSQL MCP

打开Trae，按照下图方式，如果第一次没有MCP，会提示需要添加MCP

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicNIgxibahmatUlZXZfGIElTKq13ficjyrdaUtRDapTfA1kMFw8jcManwA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着就进入到MCP市场了，添加PostgreSQL

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicU05YMetEbIoEib0xhd2OGrhNJjhxLx505ZHJU3zyVswMqJye8pN7POQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这里特别注意

上面复制的PostgreSQL url不能直接粘贴使用，需要参考它给出的格式调整一下

postgresql://postgres:密码@127.0.0.1:5432/postgres

其他的都一样，大家把连接中的密码改成自己的就行

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAickFeTEUhmcCOCTicGZXfgy7CJhgVUdS5tlwictZanQp0hfWZHRSzlxxDQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上一步，点击确认后

使用mac的朋友如果报这种错，说明相关路径没有权限

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAic3P4uGFKnWS4HzhhvrEWN8KYej6G4byibzQouDB2a4icFkb900JXXIgLA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以在终端运行一下这个命令：

sudo chown \-R $(whoami) ~/.npm

*PS：其他任何报错都可以丢给Trae，让AI帮你解决*

直到PostgreSQL MCP变为可使用状态，就代表配置好了

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicnFibBhYjjfHkEUDphm3ibQSPcsoZeic4eib5He2Y2iaDjYiasFicQHcsZnDKQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

并且，为了安全，只提供了查询功能，无法进行增、删、改 。

  

测试PostgreSQL MCP效果

接下来我们需要把测试数据导入PostgreSQL中

我准备了一个Excel表格

是我之前在某宝爬取的一些内存条商品信息，一共135行

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAic7pFARtUUrVMjDU2W36ckuGW3mHwD5icaJAzcgSzHFY5MtsflbzyArBw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

咱们直接用前两天刚刚发布的 「扣子空间」 ，让它把这个表格转为可直接导入PostgreSQL的sql文件。

提示词：

我想把这个Excel导入PostgreSQL（表需要新建），根据这个Excel的内容，帮我生成导入所需的sql文件，记得把列名翻译成英文，考虑字段的字符串长度是否够等因素，生成后供我下载。

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicGcWJdOcnMwbkDkR9rzEjgVRTPyviaqg7aV3aID86MHWCJTsF74petrg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

说实话，扣子空间真挺好用的，半分钟不到就搞定了

*如果是在以前，估计得写代码，或者用Excel表达式吭哧吭哧搞半天*

直接把生成的sql文件下载下来

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicRSOrNEIuer0ruNNtkhibviciajXVv2S8X0UynPDKkAYkRS6jNCVmRVQjw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

按照下图的步骤，把数据导入PostgreSQL数据库中

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicWGIlSBVYNeCeOwZqpia2ySZftrJoBtD7R8yAWR8ozNTAYZp1yCUTibUQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以按下图方式查看导入成功的数据

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicRPC8z0pwnTOY5VibTrrOaXNVBichHqKFucCZmDrdWeLTdqDvNHPWs0sg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后我们就可以开始在Trae中测试了

注意：由于大模型并不知道表格的结构和信息，我们需要把表格结构连同问题一起发过去（如果是智能体就可以把表格结构放到系统提示词中）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAick8icyLN4GMLeLnOOAeBKVG85OgVg9X2Pc7O2skETDOnnGY6H8dzV2ng/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

表格结构在之前生成的sql文件里面可以找到（如下图红框中这段）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAic18RG6QRNxy4iccxJeHcl3WncpUDbdTAWvK32JLMoZEo2YO5V5ib5P3Hg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

查询结果完全正确～

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1D4DTVT3vnnI1zFqflQUnAicvpsTib1iaEnkmIWhfIfT1gibw76m2dias7BAUicMaPC0Oso5fAibmWSdblPg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这个方案是由大模型写sql语句来进行查询，所以，查询精度是可以保证的。

亲测，Claude3.7还是比新版DeepSeek好用。。。至少sql语句写的更符合要求。

这个方案还可以结合RAG一起用：比如做一个工作流，搞一个大模型在最前面判断，用户问题如果是全局，或者统计性质的，就走数据库。否则就走RAG，这样结合起来，将会极大的提升整个知识库的检索精度。

写到这里，我不经想起当年刚做程序员的时候，有几个月每天都写各种复杂的sql，从生疏，到炉火纯青，现在看来好像没有多大用处了，因为AI完全可以秒出。

不经感叹，技术发展的真快，而我们，好像只能不断紧跟时代的步伐，才不至于被淘汰。

**能看到这里的都是凤毛麟角的存在！**

****如果觉得不错，随手点个赞、在看、转发三连吧~****  

********如果想第一时间收到推送，也可以给我个星标 ⭐********

********谢谢你耐心看完我的文章~********

********![图片](https://mmbiz.qpic.cn/mmbiz_gif/3QzcPBL9P1DeeTshdIQEz6zgAPa0jzuyq3icAKbvfvGO3A8MLftrrqYv5U4Hy8JO6hjbQibickJVvUgha2EpgHARg/640?wx_fmt=gif&from=appmsg&wxfrom=5&wx_lazy=1&tp=webp)********

Trae 1

数据库 1

知识库 15

MCP 4

继续滑动看下一个

袋鼠帝AI客栈

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功