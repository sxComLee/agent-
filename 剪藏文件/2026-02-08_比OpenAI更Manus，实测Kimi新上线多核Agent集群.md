---
标题: "比OpenAI更Manus，实测Kimi新上线多核Agent集群"
链接: "https://mp.weixin.qq.com/s/EpOaCx6VvXS1GFJIjOU9MQ"
作者: "[[卡尔的AI沃茨]]"
阅读星级: 4
内容类型: "深度科普"
创建时间: 2026-02-08T12:21:12.938Z
摘要: |
  本文介绍了Kimi K2.5模型推出的Agent集群功能，通过动态分配多个分工明确的子Agent协同工作，显著提升了任务处理效率和智能化水平，并展示了在信息搜索、图像生成、视频制作等多场景下的应用效果。
tags:
  - "Kimi K2.5"
  - "Agent集群"
  - "人工智能协作"
  - "多模态AI"
  - "自动化工作流"
字数: 5595
状态: "未开始"
总结: |
  Kimi K2.5模型的核心创新在于其**Agent集群**功能，与传统的通用Agent（如OpenAI的Deep Research或Manus的Wide Research）相比，具有以下关键特点：
  1. **分工协作机制**：集群可动态分配数十至上百个子Agent（如收集、验证、统计等角色），每个Agent有专属名称和头像，形成类似专家团队的协作网络，而非执行相同任务的简单并行。
  2. **效率大幅提升**：端到端运行时间减少80%，效率提升400%，且能根据任务复杂度自动调整Agent数量（简单任务仅需单个Agent）。
  3. **多模态与扩展能力**：支持图像和视频理解、256K上下文，并能自主扩展任务范围（如将简单查询转化为丰富搜索网络），无需用户反复干预。
  4. **实际应用展示**：
     - **信息处理**：自动整理GitHub项目、分析简历、生成学习路径。
     - **创意生成**：免费批量生成50张设计海报，并进一步制作HTML画廊和短视频。
     - **动态适应性**：任务执行中Agent会内部“碰头”校准，实现非线性、头脑风暴式的工作流。
  5. **用户友好性**：无需配置API或理解技术协议，用户可专注创意提出，由Agent自主处理执行细节。
  作者认为这代表了AI从“记忆”（长文本）、“推理”到“团队协作”的第三阶段演进，带来了更自然的人机交互体验。
---

# [[比OpenAI更Manus，实测Kimi新上线多核Agent集群]]
### 预读问题
**基于你的目标**：
- Q1:
- Q2:
- Q3:

### 关键图表/代码
![[提取的图表或代码片段]]
### 初步关联
- 已知：[[已掌握的相关热识]]
- 未知：`#\u5f85\u63a2\u7d22`

### 输出目标
- [ ]

# 内容
#flashcards

## Kimi憋了个超级大招，

没有选择像别的通用Agent一样重度依赖Claude，而是选择先做好Agentic模型，结果就是造出来个All in One的Kimi K2.5模型，能理解图片和视频，256K上下文，Agent 集群模式下能稳定召唤100+分身（subagent），

跟Manus的Wide Research不同，分身们可以同时完成不同类型的任务。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpaby8s3Gm9ich5dJyCHFXTh0ZK1iauYmgfjmB1ErvZEj5FFibEaj3syYqPvXw/640?wx_fmt=png&from=appmsg)

分身们还有自己的工牌

很长一段时间，我接触的通用 Agent，比如OpenAI的Deep Research，给我的感觉像是一个聪明的博士生。你给它一个课题，它会花很长时间去深度钻研，最后给你一份详尽的报告。

后来Manus提出了Wide Research，它像是一次性派出去一百个实习生，每个人都去做同样一件事情，比如搜索资料，然后把结果汇总起来。这种模式在处理一些需要大量信息搜集和初步整理的任务时，效率很高。

在Kimi这次的Agent集群上，我看到了一种新的可能性。它派出去的几十上百个Agent，不再是干着同样事情的实习生，而是一个分工明确的团队。并且团队的数量会根据任务的难度动态调整。

从他们放出来的指标上看，比起单Agent，端到端运行时间减少了80%，效率提升400%

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyh7sqFbfL5W2wLsAXce5qlia4QdRJn9F26beNU5vmFI6nSsENsicIe9Kg/640?wx_fmt=jpeg&from=appmsg)

我的体验是从一个很常规的测试开始的。我让它帮我整理一下GitHub上Star数排名前十的Claude Code Skills项目，看看都是做什么的。任务下达后，屏幕上出现了几十个小小的头像，开始分头工作。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyEXpGYISiaGqaQBmhwJoejCic3Z3wmSsOEaH0yl0M5z0LqpPkAXn9VTbQ/640?wx_fmt=png&from=appmsg)

有意思的是，每个Agent都有自己的名字，很Notion风格的头像，有的叫Matt，有的叫Sue，有的叫Max，在任务分配界面，能看到它们每个人负责的方向是不一样的，他们的人设也是有点小巧思在的，

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyZFtg62qZNalmoDF2CT9xAf468FSEaL36miasesFOEESWznZMvN51BLA/640?wx_fmt=png&from=appmsg)

这次先是创建了一个负责收集的Agent，然后又创建了负责验证Skills可行性Agent和聚合统计结果的Agent，

然后收集Agent像是有那个分身术，kukuku整了50个，有的负责搜索Claude Code和MCP Server的组合，有的搜集从MCP改成Skills的项目，甚至有的按照Python或者其他编程语言进行分类搜索。

也就是说它把一个简单的概念，

主动扩展成了一个丰富的搜索网络。

整个过程，我不需要像用Deep Research那样，

反复回答个人偏好来帮它收窄范围。

在五十个 Agent 的自主联想和扩展能力下，

它已经能猜到我想要什么。

光做信息搜集还不够有说服力。我特意找来了Manus发布Wide Research时候的任务提示语，创作五十张非常有设计感的海报，
🎉

一次性生成 50 张适用于纽约快闪生活方式活动的创意海报设计。

活动名称：City Sips: A Taste of New York，一场为期一天的咖啡、音乐与设计体验活动。

每张海报都必须包含日期（2025 年 9 月 14 日）与地点（纽约布鲁克林 Williamsburg）。

风格覆盖要足够广，包含但不限于：粗野主义、街头涂鸦、复古纽约、极简主义、霓虹风、拼贴、超现实。

在版式、字体、配色方案、插画与摄影质感之间做出明显变化。

整体观感要有能量、很城市、文化氛围浓郁，适合印刷与社交媒体投放。请把图片打包成 ZIP 文件发给我。

我没有给任何API或者说我平时用的生图账号，直接就薅到了50张海报，

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyZwf1A47VlQcOt9XNXexuKnKMvp3HPVlbI9zfGABgzkWVJWqSswqkHA/640?wx_fmt=png&from=appmsg)

而且良品率比我想象中要高得多得多。

![image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpaby4Ly9sLtUHg4xXUiaiaEibXrPoBlDSPpOxXDYgM5EYdPVKkvrRpYbtOoqg/640?wx_fmt=png&from=appmsg)

如果在生图的时候，指定模型用Banana2，然后再给一个参考图的话效果会更好，

不花钱的图生成起来就是不心疼。。。

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyfuA0lCd1EiaxJhxq7hRxOD9nZ0MiclUobAr5t2hPSSxJWmpE0LpwxPoQ/640?wx_fmt=jpeg&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyib7iaO4pwajt3neia7JBHZ8ERTWH0JBAic5teStnNSQIs5TDS9TgdoIVzw/640?wx_fmt=jpeg&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyQiaHdvn9yN4yJzqag6TqhZm8MOPX0r5fyMSicnnpFicvFgyCBvIjjaQXA/640?wx_fmt=jpeg&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyMW6c6V93ibCezZWMYynbKFe3mbfC0aiaRebJcoFEuxyWy2M6zDzwdcdA/640?wx_fmt=jpeg&from=appmsg)

Kimi K2.5这次网页生成能力也有很大的提升，我反手就是将这30张图做成画廊展示HTML，每瓶香水都是3D倾斜卡片，鼠标互动可以看到他们的在暗光下的另一面。

还不用担心Agent跟Agent之间没有沟通，他们并不会因为是同时执行任务的 Agent就不能写连贯的故事分镜。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpaby94JxAJ8NFw2ks2LRGXku2tvCJ7S8UtibIKKkqrSbd01fWKTYZObrNgA/640?wx_fmt=png&from=appmsg)

既然图可以，再大胆一点，我当下第一个想法就是视频能不能免费做，

所以直接让它把生成的五十张电商图片，都做成五秒钟的短视频，还就真的做成功的，虽然不是用AI做出来的，在我没有提供任何API和账号的前提下，能把图片加上滤镜并剪辑成片，也足够惊喜了。

![image](https://mmbiz.qpic.cn/mmbiz_gif/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyBopIP1vYQdPZrw0CHr1ETvP6Fib3G0uiagDWoXTlxic9ialhbZVYYfk2ibQ/640?wx_fmt=gif&from=appmsg)

看到这里我有点担心算力消耗，实际上Agent集群还可以动态分配SubAgent的数量了，

当我给它一个相对简单的信息搜索任务时，比方帮我搜索DeepSeek团队从2023年到2026年的论文，技术报告和 GitHub链接，并做一个总结，推测一下DeepSeek v4可能会有的技术更新。

这个任务它只用了一个Agent就完成了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyw2lVoBMeAnZbaD1ns5GibIDicNSLfMN39aUHibhAfXHLsdyAic9UeCCGQg/640?wx_fmt=png&from=appmsg)

我还用它解决了一个manus经典多文件案例，这次将25份简历扩张到45份中英文都有互联网联系，要求Agent 集群找到我想要的候选人，
🎉

我是一名人力资源专业人员，正计划招聘一名强化学习（RL）算法工程师。我倾向于寻找具有相关强化学习经验的人选。请协助我将 PDF 简历中的候选人信息整理成一份完整的 Excel 汇总表，内容应包括基本信息以及项目经验的简洁总结（重点突出核心亮点和成就）。请根据候选人在强化学习领域的专业程度进行排名，并向我提供一份包含所有这些信息的、格式整齐的 Excel 文件。希望您能逐一仔细阅读每位候选人的简历。

多文件处理起来基本上没什么压力，

内测这几天我还测了超级多问题，旅游指南，设计10个露营品牌和艺术家联名的产品，还有一个狠活case，真的不舍得压缩，再给大家看一个，

这个是我做Claude Code Skills的灵感之一，可以通过一个博主的视频主页，按照我对TA的印象和不同产品两个维度，把200多个视频划分成完整的学习路径，这样我可以有针对性选有用的视频导入NotebookLM，是个大工程，但是Agent 集群已经帮我完成了70%。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXlNxhdZP3ibzA5S5LuZibpabyoxz1icKhG2LrB5oKUgtSl5uqia52tkic77kkjEpdC9reDqQaLBjt3iaJhA/640?wx_fmt=png&from=appmsg)

这种探索的乐趣，想问啥写啥，还不用担心做到一半被登陆卡住的感觉，让我找回了当初刚接触Manus时那种兴奋感。

这跟我之前熟悉的通用Agent模式是有着一条清晰的界线。常规的工作流Agent，就算进行多路搜索，也像一条装配线。第一波Agent出去搜集零件，然后把零件交给下一个环节进行汇总和组装。整个过程是线性的，一步接着一步。

Agent 集群更像一个动态的头脑风暴。我的一个指令下去，第一波探索者出发了。但关键在于，它们完成初步探索后，不会直接把一堆原始材料丢给我。它们会先进行一次内部碰头，形成一个初步的共识，然后基于这个共识，再分派出任务更明确、方向更聚焦的第二波，第三波，在过程中不断思考和校准。

Kimi 团队自己也把 AGI 的拼图分成了三个阶段。

第一阶段是记忆，像Kimi 1.0的长文本。

第二阶段是推理，模型有了深度思考的智商。

而Kimi 2.5的Agent 集群，是第三阶段，让AI 学会了像团队一样分工协作。每次我提出一个新项目，Kimi就会为我组建一个临时的专家团队。

看到屏幕上那些叫Matt、Sue或是Max的小头像各司其职，真的会产生一种奇妙的代入感。

我甚至会冒出一个念头，希望可以把这次任务里表现特别出色的那个Agent 保存下来，

下次有类似的项目，可以指定让它来操刀。

不需要研究API怎么接，

Skill怎么写，

也不用去理解MCP协议。

我只管天马行空，

怎么执行，

是Agent要头疼的事了。

@ 作者 / 卡尔

最后，感谢你看到这里👏如果喜欢这篇文章，不妨顺手给我们*点赞｜在看｜转发｜评论 📣*

如果想要第一时间收到推送，不妨给我个星标🌟

如果你有更有趣的玩法，欢迎在评论区和我聊聊🤝

更多的内容正在不断填坑中……

![image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXmCDLEEW1wClZOVGFURjmibJmciaYLNhp0N55Y6mPiaCj01eV8yzACqDvWDhicbPm07Wu7bboATuKgAbA/640?wx_fmt=jpeg)
