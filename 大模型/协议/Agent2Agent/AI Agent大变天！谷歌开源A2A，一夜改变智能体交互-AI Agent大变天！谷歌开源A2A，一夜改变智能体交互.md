---
标题: "AI Agent大变天！谷歌开源A2A，一夜改变智能体交互-AI Agent大变天！谷歌开源A2A，一夜改变智能体交互"
链接: "https://mp.weixin.qq.com/s/ih2FLqmWhJiRvoXxLu68Ag"
作者: "[[AIGC开放社区]]"
创建时间: "2025-04-11T10:46:07+08:00"
摘要: "谷歌开源首个标准智能体交互协议A2A，支持50多家企业平台，旨在统一Agent生态格局。"
tags:
  - "clippings"
  - "AI"
  - "谷歌"
  - "开源协议"
  - "智能体交互"
  - "编程"
字数: "351"
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
原创 AIGC开放社区 *2025年04月10日 05:09* *河北*

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMkzicbhQ21ADf1STQic8wlSpV24xye1kc3FsLEZG42x42uIFHpfLGLgny4CGN8jEibDre8eRicMyO9xNw/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247519592&idx=1&sn=e0bf48edb7b265ec2f2fed13b29c026b&scene=21#wechat_redirect)

昨晚，谷歌在 Google Cloud Next 25 大会上，开源了首个标准智能体交互协议—— Agent2Agent Protocol （简称 A2A ）。

A2A 将彻底打破系统孤岛，对智能体的能力、跨平台、执行效率产生质的改变，支持 Atlassian 、 Box 、 Cohere 、 Intuit 、 Langchain 、 MongoDB 、 PayPal 、 Salesforce 、 SAP 、 ServiceNow 、 UKG 和 Workday 等主流企业应用平台。

简单来说， 这个 A2A 交互协议有点当年谷歌牵头 80 多家企业搞安卓系统的味道，因为首批就有 50 多家著名企业加入 。随着加入的企业越来越多，会极大提升 A2A 的商业价值以及推动整个智能体生态的快速发展。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMl0JC5erxohgxXHc1FRkicKTaCYXf5TFJass3Gv0CDBE3ESgxGMJia4eLmWvDbq4rYNcLbuxAnEc8ug/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

开源地址： https://github.com/google/A2A

在本次大会上 Agent 成为了重点，除了 A2A 之外， 谷歌还效仿 OpenAI 开源了 Agent 开发套件 ADK ，内部测试工具 Agent Engine ，新的 Agent 市场等 。下面「 AIGC 开放社区」先为大家解读 A2A 的重点内容。

什么是 A2A

A2A 是一种开放协议，为 Agent 提供了一种标准的交互方式，使它们能够相互协作，无论底层框架或供应商是什么。

例如，一家大型电商公司使用了多种企业平台和服务。 Atlassian 用于团队项目管理， Box 用于文件存储和共享， Salesforce 用于客户关系管理， Workday 用于人力资源管理。

以前这些平台上的 Agent 无法自由通信。现在通过 A2A 协议，这些企业平台可以安全、自由地自动化交互数据。

关注 重播 分享 赞

0 / 0

00:00 / 01:22  进度条，百分之0 [播放](https://mp.weixin.qq.com/s/) 00:00 / 01:2201:22 *全屏* 倍速播放中 <video src="https://mpvideo.qpic.cn/0bc3w4bpwaacw4acjupuartvfn6d7o3qf6ya.f10002.mp4?dis_k=75fa07792f04d580dbce0c5f89203951&amp;dis_t=1744336778&amp;play_scene=10120&amp;auth_info=f4LxsOIFLlYw446g+lBxZUE5ZxU0MTtIIWdMZFFdcXBFVRFoREpRLEFKMFpia31G&amp;auth_key=5042b8ec8066bbf76f982c8e6f711337&amp;vid=wxv_3936604640061652993&amp;format_id=10002&amp;support_redirect=0&amp;mmversion=false">您的浏览器不支持 video 标签</video>

继续观看

AI Agent大变天！谷歌开源A2A，一夜改变智能体交互

<audio><source src="https://res.wx.qq.com/voice/getvoice?mediaid=MzA3MzA0MTAyNF8xMDAwMDI3Njk="></audio>

[视频详情](https://mp.weixin.qq.com/s/)

A2A 案例展示

在与合作伙伴设计协议时，谷歌遵循了五个关键原则 。第一， A2A 专注于使 Agent 能够在它们自然的、非结构化的模式下进行协作，即使它们不共享内存、工具和上下文。谷歌正在启用真正的多 Agent 场景，而不是限制 Agent 成为一个工具。

第二，该协议是基于现有的、流行的标准构建的，包括 HTTP 、服务器端事件（ SSE ）、 JSON-RPC 等，这意味着它更容易与企业日常已经使用的现有 IT 堆栈进行集成。

例如，一家电商企业日常使用 HTTP 协议来处理网页数据传输，利用 JSON - RPC 在前后端传递数据指令。引入 A2A 协议后，企业的订单管理系统可以通过 HTTP 与 A2A 协议对接，快速获取相关智能 Agent 提供的物流数据更新，无需大费周章地重新搭建复杂的数据传输通道，能轻松融入现有的 IT 架构，让各个系统协同工作更加顺畅。

第三， A2A 被设计为支持企业级的认证和授权，在推出时与 OpenAPI 的认证方案具有对等性。这点还是很人性的不排斥 OpenAI ，使用 A2A 协议能快速通过身份验证，安全地获取数据，保障数据传输的安全性和合规性，防止数据泄露风险。

第四，谷歌设计 A2A 使其具有灵活性，能够支持从快速任务到可能需要数小时甚至数天（当人类参与其中时）的深入研究等各种场景。在整个过程中， A2A 可以向用户提供实时反馈、通知和状态更新。

以一家科研机构为例，研究人员利用 A2A 协议下的Agent进行新药物研发相关研究。简单的任务如快速检索数据库中已有的药物分子结构信息，几秒内就能完成并反馈给研究人员。但对于复杂任务，像模拟新药物分子在人体环境中的反应，可能需要数天时间。

在这期间，A2A 协议会不断向研究人员推送模拟进度，比如已经完成了多少步骤、当前遇到的问题等，让研究人员随时掌握情况，就像时刻有个助手在汇报工作进展。

第五， Agent 的世界不仅限于文本，所以， A2A 支持各种模态，包括音频、图像和视频流。

A2A 工作原理

A2A 的工作原理是通过促进客户端 Agent 和远程 Agent 之间的通信来实现的。客户端 Agent 负责制定和传达任务，而远程 Agent 则根据这些任务采取行动，以提供正确的信息或执行相应的操作。在这个过程中， A2A 协议有以下几个关键能力。

首先， Agent 可以通过“ Agent 卡”来宣传它们的能力。这些“ Agent 卡”是以 JSON 格式存在的，它们能够让客户端 Agent 识别出哪个远程 Agent 最适合执行特定的任务。

一旦确定了合适的远程 Agent ，客户端 Agent 就可以利用 A2A 协议与之进行通信，将任务分配给它。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMl0JC5erxohgxXHc1FRkicKTbZKGO5xYlibf0MHAGxgVAicld0LWwxGv93XqQXIHPHaNmWNAuEZOjRUQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后，任务管理是 A2A 协议中的一个重要环节。客户端和远程 Agent 之间的通信都是围绕完成任务展开的。协议定义了一个 “ 任务 ” 对象，这个对象具有自己的生命周期。

对于一些简单的任务，可能可以立即完成；而对于一些复杂的、长期的任务， Agent 们可以相互沟通，以保持对任务完成状态的同步。当任务完成时，其输出被称为“工件”。

此外， A2A 还支持 Agent 之间的协作。 Agent 们可以相互发送消息，这些消息可以包含上下文信息、回复、工件或者用户指令。通过这种方式， Agent 们能够更好地协同工作，共同完成复杂的任务。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMl0JC5erxohgxXHc1FRkicKTJqvmzGLFYlDZSSgCgLrib9MCxG4OTL5sPXl6c5nKPuJxOTZlnREMLHA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

最后， A2A 还具备用户体验协商的功能。每条消息都包含 “ 部分 ” ，这些部分是完整的内容片段，例如，生成的图像。

每个部分都有指定的内容类型，这使得客户端和远程 Agent 能够协商所需的正确格式，并且明确包括用户界面能力的协商，比如 iframe 、视频、网络表单等。这样， A2A 就能够根据用户的需求和设备的能力，提供最佳的用户体验。

哪些企业加入了 A2A

其实最让人惊讶的就是， A2A 刚发布就获得了大批著名企业的青睐和加入，包括埃森哲、波士顿咨询集团、凯捷、科尼、 Salesforce 、德勤、甲骨文、 HCL 科技、印孚瑟斯、 KPMG 、 SAP 、麦肯锡、普华永道等 50 多家日常大家能经常听到的企业。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMl0JC5erxohgxXHc1FRkicKTSHvq3KwkFvBXmGBCtgtFuzTHz1GicHcCxiaOI1xeZ2JRcIKASl15icLZQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

首批加入 A2A 的企业

还有一些技术公司也加入了到了 A2A 协议中。例如， Atlassian 以其强大的团队协作工具 Jira 和 Confluence 而闻名。通过加入 A2A ， Atlassian 能够使其工具与各种 Agent 无缝协作，从而进一步提升团队的工作效率和协作能力。

Box 是一家专注于企业级云存储和内容管理服务的公司，它提供的解决方案能够帮助企业安全地存储、共享和管理文件。通过 A2A 协议， Box 可以使其服务与 Agent 相结合，实现更高效的内容管理和自动化工作流程。

Intuit 知名的财务软件公司， QuickBooks 和 TurboTax ，已经被广泛应用于财务管理和税务处理。通过 A2A 协议， Intuit 可以使其软件与 Agent 协作，实现更自动化的财务流程和更高效的税务处理。

MongoDB 是一家提供高性能、开源的 NoSQL 数据库解决方案的公司，其数据库广泛应用于现代应用程序的数据存储和管理。通过 A2A 协议， MongoDB 可以使其数据库服务与智能 Agent 相结合，实现更高效的数据管理和自动化数据处理。

其实看到这里大家应该都清楚了，谷歌就是想统一 Agent 混乱的格局，打造全新的执行、交互标准，这个比前段时间的 MCP 要猛的多啊 ~

本文素材来源谷歌，如有侵权请联系删除

END

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMkzicbhQ21ADf1STQic8wlSpV24xye1kc3FsLEZG42x42uIFHpfLGLgny4CGN8jEibDre8eRicMyO9xNw/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247519592&idx=1&sn=e0bf48edb7b265ec2f2fed13b29c026b&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMn39UgRSNfPoWEv1f3wqa0lXogOTK7yWJGbe0aVGsL8ibBNwAt26Z4iatuaPpoVibWhFel7Dt5jibEibow/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMnR4jHBK9FdVibzjJmiasUIgRQ4ctBMBBEbM4cVicwhNnoka8rOHSkxUQhrHXWTpQVsiaXTVFoyYfZVgg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

素材来源官方媒体/网络新闻素材来源官方媒体/网络新闻 继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过