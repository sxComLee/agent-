---
标题: "AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了"
链接: "https://www.infoq.cn/article/KacfyVt0C9OHv76W6a8A?utm_term=wxgroup"
作者: "[[段楠 | 阶跃星辰 Tech Fellow]],[[熊军军 | 中国人寿 高级工程师]],[[姚旭晨 | Seasalt.ai CEO]]"
创建时间: 2026-01-28T22:44:00+08:00
摘要:
tags:
  - "clippings"
字数: 190
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

- 企业动态
- 行业深度
- AI&大模型
- 出海
- 后端
- 芯片&算力
- 架构
- 大数据
- 软件工程
- 云计算
- 大前端
- 管理/文化

**

**

**

**

**



00:00

[1.0x **](https://www.infoq.cn/article/)

大小：700.67K 时长：03:59

<audio xmlns="http://www.w3.org/1999/xhtml" title="AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了" src="https://static001.geekbang.org/infoq/audio/f7b9d5763d2e28f41a8a7e5cc9f5f43e.mp3"></audio>

![[_resources/AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了/a3d99ac5ed308d7fbf3611612ec73c9a_MD5.jpg]]

为防止大语言模型和 AI Agent 执行嵌入在外部数据中的恶意指令， [所有进入 Agent 上下文的文本在完成校验之前都必须被视为不可信数据](https://medium.com/cyberark-engineering/when-ai-agents-obey-the-wrong-master-913aff17e3ed) ，其中不仅包括用户输入的提示，还包括来自外部系统的各类信息。AI 安全公司 CyberArk 的首席软件架构师 Niv Rabin 表示。为此，他所在的团队提出了一种基于“指令检测”（Instruction Detection）与“历史感知校验”（History-Aware Validation）的方法，用于同时防御恶意输入数据和上下文历史投毒攻击。

  

Rabin 介绍说，团队设计了多种防御机制，并将其组织成一个分层的处理流水线。流水线中的每一层都针对不同类型的威胁，目的是减少单一防护手段不可避免存在的盲区。

  

这些防御措施包括“蜜罐动作”（honeypot actions）以及指令检测器，用于拦截具备指令特征的文本，确保模型最终接触到的仅是经过验证、且不包含指令的数据。同时，这些机制也会应用于整个上下文历史中，以防止所谓的“历史投毒”（history poisoning）。这种攻击方式指的是，原本看似无害的内容片段在多轮交互中逐步累积，最终拼接成一条完整的恶意指令。

  

所谓“蜜罐动作”，本质上是一种用于诱捕恶意意图的安全陷阱，即 Agent 在任何正常业务场景下都不应选择的合成动作。

  

这些动作对应的是一些不会真正执行任何操作的虚拟工具。它们并非用于完成实际任务，而是作为安全信号存在，其工具描述被刻意设计成能够暴露可疑行为。

  

在提示中出现的可疑行为包括对系统内部机制的元层级探测、异常的数据提取尝试，以及试图诱导模型泄露系统提示（system prompt）的操纵行为等。如果 LLM 在动作映射阶段选择了其中一个蜜罐动作，通常就意味着存在明显的异常或越界行为。

  

Rabin 指出，真正的安全风险并不主要来自用户输入，而是来自外部 API 或数据库的返回结果。针对这一问题，团队引入了指令检测器作为关键防护手段。

  

这种检测已经不再是传统意义上对“恶意内容”的搜索，也并非基于关键词、文本毒性或策略违规的判断，而是聚焦于识别文本中所蕴含的意图、行为模式以及指令在结构层面的特征。

  

指令检测器本身是基于 LLM 构建的“裁判模型”。在任何外部数据被送入主模型之前，检测器都会对其进行审查，并被明确要求识别任何形式的指令，无论其表现得多么直白或隐蔽，从而使系统能够在第一时间阻断可疑数据。

  

此外，时间也被证明是一种重要的攻击向量。早期响应中零散存在的恶意指令片段，可能会在后续交互中被重新组合，最终形成一条完整指令。这种现象被称为“历史投毒”。

  

示意图展示了一个典型案例：LLM 被要求分别获取三段数据，单独来看，这些数据完全无害；但合并在一起后，内容实际拼成了一条指令，要求系统停止处理并返回特定结果。

  

![[_resources/AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了/6cac5cd63477faa67177a08df4029037_MD5.webp]]

  

为防止历史投毒，所有历史 API 响应都会与最新获取的数据一并提交给指令检测器，作为一个统一输入进行分析。

> Rabin 指出，历史投毒并不是发生在数据进入系统的入口阶段，而是发生在系统从历史记录中重建上下文的过程中。通过引入这一机制，即便对话历史中隐藏着试图干扰模型推理的细微线索，系统也能够在模型受到影响之前及时发现异常。

  

上述所有步骤都会在同一条流水线中运行。一旦任意一个阶段检测到风险，请求就会在模型处理之前被直接拦截；只有通过全部校验后，模型才会处理已经净化过的数据。

  

Rabin 总结，这种方法的关键在于将 LLM 视为一个长期运行、跨多轮交互的工作流系统，而非一次性的请求响应组件。他在原文中对这一方案进行了更为深入的展开，对于关注 AI 安全问题的读者而言，值得进一步阅读。

  

**原文链接：**

[https://www.infoq.com/news/2026/01/cyberark-agents-defenses/](https://www.infoq.com/news/2026/01/cyberark-agents-defenses/)  

** 划线

** 评论

** 复制

4031

** [AI&大模型](https://www.infoq.cn/topic/AI&LLM) [安全](https://www.infoq.cn/topic/Security) [软件工程](https://www.infoq.cn/topic/1195)

** 轻点一下，留下你的鼓励

![[_resources/AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了/3515adfd59e61e2d1bae123a89bbdcc0_MD5.jpg]]

## 评论

发布

暂无评论

![[_resources/AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了/0650f26131349b4ded56d4aa18707511_MD5.jpg]]

### 推荐阅读

- ###### 落地百余场景、扛过双11，蚂蚁TuGraph流式图计算引擎正式开源！
	** [开源](https://www.infoq.cn/topic/opensource) [产品](https://www.infoq.cn/topic/1137) [大数据](https://www.infoq.cn/topic/bigdata) [安全](https://www.infoq.cn/topic/Security) [社区](https://www.infoq.cn/topic/community) [最佳实践](https://www.infoq.cn/topic/best-practices) [企业动态](https://www.infoq.cn/topic/%20industrynews) [行业深度](https://www.infoq.cn/topic/1168) [数据处理](https://www.infoq.cn/topic/%20dataprocessing) [阿里巴巴](https://www.infoq.cn/topic/alibaba) [编程语言](https://www.infoq.cn/topic/programing-languages) [框架](https://www.infoq.cn/topic/1180) [生成式 AI](https://www.infoq.cn/topic/1183) [实时计算](https://www.infoq.cn/topic/1194) [数字人才培养](https://www.infoq.cn/topic/1205) [工业](https://www.infoq.cn/topic/1173)
- ###### 来自外太空的计算错误：宇宙射线干扰了我的心脏起搏器，我差点因此丧命
- ###### InfoQ 2023 年趋势报告：事件驱动架构、深度学习和人工智能、云原生架构和容器化技术
	** [架构](https://www.infoq.cn/topic/architecture) [AI&大模型](https://www.infoq.cn/topic/AI&LLM) [云原生](https://www.infoq.cn/topic/CloudNative) [容器](https://www.infoq.cn/topic/container) [安全](https://www.infoq.cn/topic/Security) [方法论](https://www.infoq.cn/topic/methodologies) [编程语言](https://www.infoq.cn/topic/programing-languages) [框架](https://www.infoq.cn/topic/1180) [微服务](https://www.infoq.cn/topic/microservice) [生成式 AI](https://www.infoq.cn/topic/1183) [可观测](https://www.infoq.cn/topic/1199) [企业动态](https://www.infoq.cn/topic/%20industrynews)
- ###### AI 给自己建了座“鬼城”：人类被禁言，上万个 AI 自主聊天，有“人”发牢骚、有“人”发鸡汤
- ###### 人口不足千万、芯片厂近200家，以色列技术人如何在芯片领域“挖金山”？| 独家对话Pliops创始团队
- ###### 腾讯披露自研芯片“沧海”最新进展
- ###### Kubernetes 调查报告：配置不当可能导致安全问题
	** [容器](https://www.infoq.cn/topic/container) [安全](https://www.infoq.cn/topic/Security) [微服务](https://www.infoq.cn/topic/microservice)

### 电子书

![[_resources/AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了/934ceff954cc1b470f5394d70dc12a2b_MD5.jpg]]

###### 腾讯云云原生提质增效实践精选集2024

《2024腾讯云云原生提质增效实践精选集》出炉，5大热门技术领域，13个行业精选标杆案例，痛点到解决方案全揭

立即下载

![[_resources/AI Agent 是长期运行的“风险系统”，如果你还只在防 Prompt Injection，说明已经落后一代了/82082a79063aa024fabd4c46017f7009_MD5.jpg]]

Step-Video 开源模型：视频生成基础模型的最新进展、挑战与未来展望

立即下载

全业务流程生产压测与监控实践

立即下载

企业服务出海：LLM 在北美语音市场的跨界应用与挑战

立即下载

- [关于我们](https://www.infoq.cn/about)
	[我要投稿](https://www.infoq.cn/contribute)
	[合作伙伴](https://www.geekbang.org/partner)
	[加入我们](https://www.infoq.cn/link?target=https%3A%2F%2Fwww.lagou.com%2Fgongsi%2Fj43775.html)
	[关注我们](https://infoq.cn/official/account)
- 联系我们
	[内容投稿：editors@geekbang.com](https://www.infoq.cn/article/)
	[业务合作：hezuo@geekbang.com](https://www.infoq.cn/article/)
	[反馈投诉：feedback@geekbang.com](https://www.infoq.cn/article/)
	[加入我们：zhaopin@geekbang.com](https://www.infoq.cn/article/)
	联系电话：010-64738142
	地址：北京市朝阳区望京北路9号2幢7层A701
- InfoQ 近期会议
	[北京 · QCon 全球软件开发大会 2026.4.16-18](https://qcon.infoq.cn/2026/beijing?utm_source=infoq&utm_medium=footer)
	[上海 · AICon 全球人工智能开发与应用大会 2026.6.26-27](https://aicon.infoq.cn/2026/shanghai?utm_source=infoq&utm_medium=footer)
- 全球 InfoQ
	[InfoQ En](https://www.infoq.com/)
	[InfoQ Jp](https://www.infoq.com/jp/)
	[InfoQ Fr](http://www.infoq.com/fr/)
	[InfoQ Br](http://www.infoq.com/br/)