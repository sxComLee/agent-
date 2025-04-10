---
标题: "-【教程】用扣子Coze搭一个听故事学英语智能体，用上Deepseek R1满血工具版"
链接: "https://mp.weixin.qq.com/s/Vvwk55Oll7kV_qfZ3TtehA"
作者: "[[向阳乔木]]"
创建时间: "2025-04-10T18:44:07+08:00"
摘要:
tags:
  - "clippings"
字数: "203"
状态: "未开始"
---
# [[预读法介绍]]
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
原创 向阳乔木 *2025年02月28日 10:34* *北京*

> 字数 1741，阅读大约需 9 分钟

## 为什么重写扣子智能体教程

很多朋友大概听过扣子（Coze）这个产品，是字节出品的AI应用开发平台，不需要懂代码，普通人也能创建和发布自己的 AI 智能体。

国内版： https://www.coze.cn/ <sup><span>[1]</span></sup>  
国际版： https://www.coze.com/ <sup><span>[2]</span></sup>

去年底，受朋友邀请，回字节参加公益活动，给大学生讲如何用Coze搭建AI Agent。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet0OONkwfUZsKQa6owSsz9ebUaRyGt5icrQJDfXYAjRO8HDtmMZoqYbmA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

> PPT和文档地址：  
> https://xiangyangqiaomu.feishu.cn/wiki/XWIkwiA0ei94dDk9F6uccvIgnXg <sup><span>[3]</span></sup>

时隔几个月，Coze功能和界面发生了不少变化，最近还推出了满血版的Deepseek R1和V3，加上了Function calling工具调用功能。

值得重写个教程。

打算用一个具体案例，讲讲Coze搭建工作流，并用上满血Deepseek R1工具版。

## 案例：听英语故事学英语智能体

学英语最有效的办法：多听多跟读，把一篇文章或故事读透。

基于这个想法，设计一个智能体实现：

> AI自动抓英文短篇故事，合成英文MP3文件，提取文章中CET4以上的词汇，总结一句话剧情，辅助理解和学习。

效果如下：  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet5Aw9GpMib7BOE54OvibvzwrhrXwUotMMyOyUkPVf15wE2xiaYxsyX3y3w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

> 访问地址：  
> https://www.coze.cn/store/agent/7476096991085412390?bot\_id=true&bid=6fg8b1itg6g09 <sup><span>[4]</span></sup>

或长按或扫描二维码体验  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetw25n4Pdm1M8MkUsxsv64W8rcQzYQPXutjrgCeaNWM3U80TsibJSH6UQ/640?wx_fmt=png&from=appmsg)

## 创建智能体

1. 1\. 选创建智能体  
	![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetcvxrAJ1w25kEYCjO5YDNYEYDyziaVmclP6hZl6g7JK2fS8lfWnmH5yA/640?wx_fmt=png&from=appmsg)
2. 2\. 填写基本资料
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetpicCk3AMakibH022AnwVVPqiaiadSHtvpGibO9qGw7X4OaqMudRoU3zZ5Dg/640?wx_fmt=png&from=appmsg)

  
名称，简单介绍，点击自动生成图标，创建即可。

## 智能体组成

**Prompt：** 描述智能体功能，定义什么时候调用工作流。

**模型：** 这个智能体用什么模型（选的是Deepseek V3 工具调用）

**工作流：** 如何响应处理用户的请求

**数据库：** 存储一些重要数据，这里是存英文故事URL（选用）

最复杂和关键部分是 **工作流** ，安排AI 如何从一个URL地址开始，怎么加工处理各种数据，最终输出什么内容。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet8WucI30EmC7jarHkpWFzhgNOGWiczGTBMzxTicEDhq3Gx8mP0XFXasNQ/640?wx_fmt=png&from=appmsg)

## 工作流搭建

首页 -> 工作空间 -> 资源库 -> 创建工作流  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet9DEMxPSJjvf2F09mlvib8lNia1L5PXtYZABCW7WicqZHWFRSgXvbZRgyQ/640?wx_fmt=png&from=appmsg)

填写工作流名称（英文）和描述（方便AI理解调用，简单清楚）

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet0ia0rRyjRSsMmqf3yrTKX6TzsibOHFndVGbZFvhpKnXF5MOIEru9dsOA/640?wx_fmt=png&from=appmsg)

最终完成版

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet7dh3pvKrAVMunBd0BX4iayooyS8KWA64GSyrxz54nEPUkBibR92XPGIA/640?wx_fmt=png&from=appmsg)

重点有四步：URL抓取、语音合成、图片生成、LLM加工

### URL抓取

点“添加节点”->"插件”，添加一个链接读取插件  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetOymAGkh5Fsq7GX6vwuftnNo4DLQf645d6bpoHt8zu8R6CPqUYjQ0hA/640?wx_fmt=png&from=appmsg)

  
把第一步连到这个插件，点开配置，URL选第一步的input![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetNZdwsZREmvLRSxciatPiaVeoicFYbaCUBs4LobiaYtdWDUust59vlOICWQ/640?wx_fmt=png&from=appmsg)

### 语音合成

点“添加节点”->"插件”，添加一个语音合成插件，推荐搜索“英语文本转语音”，质量高，配置简单。

选个喜欢的声音添加进去。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetywv2nX8w9WSYxd499uyeOfaebHV3H3ZYjmboIvscdVxBmJl9ItAic1g/640?wx_fmt=png&from=appmsg)

点开配置，把上一步插件的content作为text输入。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetibQLbRicVvxzkAXZRzBLOUtf84AA0ibSeQpYZL2rY9qfPjrZa7q4sTlCw/640?wx_fmt=png&from=appmsg)

### LLM加工

因为我们不仅仅只想要一个音频。

还想让AI输出故事原文，提取重点单词，一句话总结等。

点“添加节点” ->"大模型"，然后点开配置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetffpLO1qwW32AVECTviavdLyKr4ibA4eMyZcAdAhrRx3G0W25sIgFjxkg/640?wx_fmt=png&from=appmsg)

**注意：**  
模型选的豆包1.5 pro 256k，感觉上下文空间大些，避免碰到太长的文章。

1. 1\. input选抓取页面插件的“content”字段，也就是抓到文本内容。
2. 2\. 重点：用户提示词，一定要记得引用变量，就是{{input}}，这是让LLM处理的内容。Prompt可以很简单，说明提取什么，设为什么变量。
3. 3\. 输出部分，对应上你设定的变量。

**敲黑板：这部分最重要，以后搭建任何工作流，都可能用到这个方法。**

### 图片生成（可选）

全是文本，看起来不生动，而且视觉输入也对加深记忆有好处。

点“添加节点” ->"图像生成"，连接大模型模块，input选大模型对应的一句话故事总结，提示词用{{input}} 变量。

相当于把故事梗概发给图片生成模型，得到一张故事图片。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetxb01ibmXfIxOllSEiazichMic9MPq8ToMiaeXdgt0uvZTHIMwtIicK1XSECA/640?wx_fmt=png&from=appmsg)

### 调用工作流

把做好的工作流发布后，智能体就可以调用了。

回到智能体编排界面：

1. 1\. 添加一个工作流，选择刚创建好的。
2. 2\. 写Prompt，告诉智能体什么时候调用工作流。
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetKZgVzg4akRibXBEK3Xpuibe2iamzLy9rXY1nc02HD4QKSmH7kk9LRxV4w/640?wx_fmt=png&from=appmsg)

## 故事 URL 数据库

工作流有了，调用也有了，故事URL从哪里找呢？

其实，有很多英文短篇故事网，比如  
https://www.fridayflashfiction.com/100-word-stories <sup><span>[5]</span></sup>

https://www.english-for-students.com/ <sup><span>[6]</span></sup>

虽然能让AI调用插件随时抓取，但感觉存数据库更稳定。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAeticq6AB0yRC33zGR3hywdFJ28cB4wJIYQBC9AD8o0IqYojbvqlBEfnCQ/640?wx_fmt=png&from=appmsg)

可以用Chrome插件如Link grabber采集。

https://chromewebstore.google.com/detail/link-grabber/caodelkhipncidmoebgbbeemedohcdma <sup><span>[7]</span></sup>

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetok2jSuSiadJ9A2FuiclCa6BkuNlEq8kAwQ5NEp2pLHo08bXTticqVlD7A/640?wx_fmt=png&from=appmsg)

或者让AI编程写工具抓取，以后再单独讲。

创建一个数据库，添加一个URL字段，把采集网址按照xlsx模版，粘贴后上传，导入数据库。

## 锦上添花，给工作流绑定卡片

智能体已经能运行，但发现返回音频是一个URL，点击跳转到另一个页面播放。

体验不够好。

经研究发现，原来可以把工作流返回的数据，通过设计一个卡片界面输出。

卡片可以调用播放器组件，文本组件，像搭积木一样，做一个GUI的界面，而不再是纯文本回复。

“首页”-"工作空间"-“资源库”-"卡片"

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet1jQGTgfIDJBIfedCjvx4pq6QCDLmQV57pDVAW2ibuxuLwrcnFOO8amQ/640?wx_fmt=png&from=appmsg)

搭建英语故事学习卡片，用上了播放组件，文本组件，图片组件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetQg8NTZSJCb1DutIBEF8WgMb4wuIqOtLzAoLK1QB5SPezt2Byt0eSxw/640?wx_fmt=png&from=appmsg)

卡片设计完，一定要设定变量。  
有了变量，才能把工作流输出的数据，显示在卡片上。

以音频为例，创建一个“音频”变量，点击音频组件，找到音频变量绑定。  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetXDeiahn0lrV2xIFY1xbJnpVK1Y8cyh1KzYpKkcSibn0TmBbb6VoEKNeg/640?wx_fmt=png&from=appmsg)

其他同理

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetae2DFYiajXwXYcsRl3G2I3pPZmgAtaFhWsbMLqQsBICK8U3k92yVuSQ/640?wx_fmt=png&from=appmsg)

**卡片制作发布后，如何绑定智能体和工作流呢？**

回到智能体编排界面，鼠标hover在工作流位置，会出现一排icon，点击绑定卡片数据

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetx9uBxvRvebsl6OPFZl6OVmZRbWD7KxbNn49KvOqYHkmnGy7M9Dvrlw/640?wx_fmt=png&from=appmsg)

挨个点选绑定对应的变量：

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetiavwHwCeyJSx0IQsgeE5qr4lNwLr6T7aEoWo5gEN5R7q8pspK5WBoMw/640?wx_fmt=png&from=appmsg)

### 快捷指令

现代人都很懒，能点选，绝不打字。

所以为了体验，可以给智能体加一些对话框上方的快捷操作按钮。

比如我创建一个“听故事”按钮。  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetYnLwjFP1XmCaxHGBEOe06bxJdsAX5B55AqoUCc5DZy9wFwncgXYnicQ/640?wx_fmt=png&from=appmsg)

指令内容很简单，为了模拟用户打字内容，调起工作流。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetzMyr3YAJj7HcrOAtPuxW1yNuiaxpficVaKj86E6OV4RQluVD7ibWK7BBg/640?wx_fmt=png&from=appmsg)

## 发布智能体

可以选很多发布渠道，比如豆包、飞书等等。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAet5YTsa2ZUF6I2WicYH5ib8rLEQVyB1C4dj8jZuAbkicymyumyLfG4PWRKg/640?wx_fmt=png&from=appmsg)

融入推理模型 Deepseek R1 工具版后，感觉对工具的调用变的更准确。

能看到AI推理过程，对写提示词和调试，也变的更轻松。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCV662lHz5aHM4QqCicGMgAetH5RBZanh9iaXOGmHjdSw7w98gRT3pmH0bYU0hjibtsBbd0BFdsibxkUrA/640?wx_fmt=png&from=appmsg)

虽然仍存在一些小问题，但这个演化方向没毛病。

另外，最近一直在研究MCP协议，Raycast工作流。

AI工具的演化方向越来越清晰：

> 人类用自然语言跟AI对话，AI则用模型推理能力，调用各种外部工具、知识库解决用户问题。

扣子（Coze）添加 Deepseek R1满血版，而且刻意加了工具调用能力，也是往这个方向努力。

非常期待今年AI Agent的大爆发，这样人类就可以变的“更懒”一些

#### 引用链接

`[1]` https://www.coze.cn/:  
`[2]` https://www.coze.com/:  
`[3]` https://xiangyangqiaomu.feishu.cn/wiki/XWIkwiA0ei94dDk9F6uccvIgnXg:  
`[4]` https://www.coze.cn/store/agent/7476096991085412390?bot\_id=true&bid=6fg8b1itg6g09:  
`[5]` https://www.fridayflashfiction.com/100-word-stories:  
`[6]` https://www.english-for-students.com/:  
`[7]` https://chromewebstore.google.com/detail/link-grabber/caodelkhipncidmoebgbbeemedohcdma:  

  

向阳乔木

干货满满，一杯咖啡的鼓励！

 **微信扫一扫赞赏作者**

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过