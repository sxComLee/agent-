---
标题: "-Google 一夜十二次，能否逆袭当回 AI 界老大｜一文看懂 Google Cloud Next 25 AI 大更新"
链接: "https://mp.weixin.qq.com/s/1XvMbtamuXPObEjC1_cIpQ"
作者: "[[一泽Eze]]"
创建时间: "2025-04-10T19:16:50+08:00"
摘要:
tags:
  - "clippings"
字数: "917"
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
原创 一泽Eze *2025年04月10日 16:20* *浙江*
今天早上看到 Google 开完了他们的 Google Cloud Next 25，发了近 20 个 AI 相关的模型、应用、开发工具、硬件。

这次发的内容特别多，很多信息散落在大量公告中。

我选了 AI 相关重点和效果演示，整理了这份全网最清晰 Google Cloud Next 25 AI 更新解读，方便大家跟上最新进展。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwvbUad1saiatAWTUkkJCiaXEldAoWRKautDibnzCjzgzcmznibJ9icZq18xQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

先给个总结：

1. 1. Google 公布了很多重磅、酷炫的 AI 模型与工具，但不少好东西都是期货，求谷歌快点放出来
    
2. 2. Gemini 2.5 Flash 即将发布，高性价比推理。 结合此前登顶的 2.5 Pro， 能否逆袭当回 AI 界老大？
    
3. 3. 特别的，发了让 Agent 无缝协作的 A2A 协议，主导全球 Agent 未来协同规范
    
4. 4. 全面公开了 Google AI 的 601 项 AI 落地案例，对应用层创业者指出明路。
    

  

本文共耗时 8 小时，整理了 5 个 AI 新模型、1 个面向未来的 AI 协议，以及 6 项其他重点更新。

下文提到的所有公告原文、产品体验与 Waitlist 地址，都统一整理在文末。（感谢关注、点赞、转发、在看）

![](http://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsjlBcGR8q3ib7p0eFyNLI0TyvG90WgiaqRjuibEhe68o9NxsgDHuqC2Y2QIkymRGxsibXr3VDCTqbnJw/300?wx_fmt=png&wxfrom=19)

**一泽Eze**

💎 懂些 AI 提示词与落地应用 🧬 本职是产品 🎐 初心仍在，希望能「做自己认同的内容，改善一小撮人的生活」

19篇原创内容

公众号

---

## 🧠 5 个 AI 模型更新

首先是 5 个 AI 模型更新，我绘制了这份看板，方便大家速览：

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5Swef7eGdFnR4dLAPd4iapa3mBhDtTlvW9rZTqHsaPeIby7DckRaofBjDA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

### Gemini 2.5 Flash：快来了，是推理模型，主打快速、便宜

此前 Google 已经推出了 Gemini 2.5 Pro 推理模型，拥有 100W tokens 上下文（实测在超出上下文对话中，依旧能遵循指令，精准回忆早期对话记忆），而且支持多模态提示。在众多 Benchmark 测试中，取得了最高排名。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwYGeuOyTw8D0QRg0xHA2NPM25CZABydzmQkNskTF5OT9T8UWOjTUJrg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

确实非常厉害，目前一泽的日常主力模型就是 2.5 Pro，前几天备受好评的[「万能文生图提示框架」](https://mp.weixin.qq.com/s?__biz=MzIzNDU0NzY1MA==&mid=2247486198&idx=1&sn=eefa18e33d1918cc31e944611178c9a1&scene=21#wechat_redirect)中，就使用它获得了最佳的体验效果。

  

现在 Gemini 2.5 Flash 也快来了，与前代 2.0 Flash 不同的是：

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwFKQoPhsJmGCyicw6QB14OMmx21iaFfGXtSSujbTsiaic0Zdew4KeasEf8g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- 这次是个推理模型，但依然延续了快速、便宜好用的优点
- 推理程度会根据对话任务复杂度，动态适应（不傻傻地对简单常识问题进行长推理实在是太有必要了🤔）
- 开发者可以自定义模型的推理程度，便于控制成本
- 正式发布还需要时间，再等等，很快在 Vertex AI 中可用

  

---

### Veo 2：超一流视频生成模型，现已开放 waitlist 申请

Veo 2 绝对是值得关注的视频生成模型，现在还支持 P 视频、关键帧生成视频、扩展画面、镜头控制等特性：

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5Swib7ofx3tLgcdbRSn7oOaMFPyL9xo3Poo0YsufC3Q8WPxoW55BS3lj7w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwDk72ddibIny7D9dCn0S0vjlKWKAeVPafX6iaW5HYDk85L6JibqXvwZcrQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- P 视频：无需手动修图，移除视频中不需要的元素。注意看，左图是有吊威亚的，右图的绳子就被自然 P 掉了

，时长00:04

- 关键帧生成视频：用首尾画面（最左为首图、最右为尾图），生成视频，画面效果非常稳定

，时长00:05

- 扩展画面：可以对已有视频画面进行自然扩展，虽然效果不算特别高级，但很适合把一些横版视频变成竖版，方便投稿到 TikTok 等竖屏内容平台

，时长00:05

- 镜头控制：可以在视频生成时，调整镜头构图、摄像机角度和控制节奏，将摄像机向不同方向移动，创建延时摄影效果，或生成无人机跟随风格的镜头。

，时长00:15

PS：Google VideoFX 用的就是 Veo 2 模型（不得不说 Google 家的产品入口、关系是真的复杂）

![图片](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5Swvk0gWVDu4biblFRyqHhqZpM4jAYVQXWce8ibiaqMhzvuBWiavP2giawnReQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

注：Veo2 现已开放 waitlist 申请，申请地址请在文末获取。

吐槽：Google Cloud 和 Vertex AI 的界面是真难用。如无必要，还是等 VideoFX 这类 to C 入口开放了再用吧

  

---

### Chirp 3：只需 10 秒语音样本，即可创建逼真的自定义语言

和 Veo 2 一起被更新到 Vertex AI 的还有 Chirp 3，是 Google 的音频理解与生成模型。

Chirp 3 提供了超过 35 种语言（含中文）的自然逼真的语音，并支持八种音色选项。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5Sw74jPvaiaMDjQwEJ1l9dNzoeiaJ7ewTAhiczvZNgFfH5NxIKys95clbCYg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- 亮点一：支持通过 10 秒的短录音，就能生成非常逼真的自定义语音

- 因为 Chirp 3 现在只能通过 API 调用，所以没能直接上手。暂时不确定用于学习的 10 秒短录音是必须跟读固定文本，还是随意任何一条清晰的录音也可以。
- 如果是后者，那就非常有意思，你可以拿游戏、动漫里的角色的任何一段音频，合成对应的虚拟人语音（捏虚拟老婆，啊不，正经 AI 伴侣），对于开发者还是阿宅都非常有价值。
- 当然，也希望 Google 抓紧做好安全策略，以防自己的语音被别人拿去随意合成。
- 下面是个 Chirp 3 的实际音频效果，展示了无停顿和有停顿的语音区别，挺自然的。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwTE4QUibibXxXVKNM82Gy2aHJkVA1qiauxuMuq73lJGHJfFaOegma7wCFg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**让我看看，是的，我看到了**,一泽Eze,2秒

**让我看看，[长时间暂停]是的，我看到了**,一泽Eze,3秒

- 亮点二：区分音频中的说话人身份，提升音频转文本的易用性

- 天下苦音频转写不能区分人声久矣。这下好了，现在能够区分多个说话人录音中“哪句话是谁说的”。这也是这项技术必然的需求趋势。
- 会议摘要、播客分析、访谈录音转写会方便很多。

  

---

### Lyria：文本到音乐生成模型，也开放 waitlist 申请

Lyria 也被更新到了 Vertex AI ，可从简单文本提示创建完整音乐作品。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwQicbGK48gH9W1973vGPQpL1f9IEBmNJicibeicde5qbJtws9QBeRUHdzJQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

不过没看出来特别的亮点，像海螺音乐的效果也不错。

以下是官方放出的演示音频：

，时长00:29

👋 看过就好。

注：Lyria 现已开放 waitlist 申请，申请地址见文末。

  

---

### Imagen 3：图像生成和编辑能力改进，更擅长对象移除和图像修复了

Imagen 3 已经放出来很久了，[《万能文生图提示词框架》](https://mp.weixin.qq.com/s?__biz=MzIzNDU0NzY1MA==&mid=2247486198&idx=1&sn=eefa18e33d1918cc31e944611178c9a1&scene=21#wechat_redirect)就通过 ImageFX（Imagen 3）生成了很多产品、游戏、家居设计的图像样例。绝对是被低估的、头一档的文生图模型。

![图片](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwfTM5aQoPSemzVgxIAByMelf1Q5KWS41jsb13VQ3BGCfKKiaLj6jFZvQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

一泽万能文生图框架，测试 Imagefx 效果

Imagen 提升了编辑/修复功能效果，能够快速移除、重绘图像中不需要的对象、瑕疵。

下图是官方演示：

左图为原图，中间是旧版本，右图是 Imagen3 版本

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5Swjrko1EOIWsWcHYcjY5spApiayzSRcQBHEpRtPqROFUrbjPS3LC6dYlg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Imagen 3一如既往的稳定，实力真的被大大低估了。

你可以在 Gemini 应用、ImageFX 开始使用它。

  

---

## 🔌 1 个面向未来的 AI 协议

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwicGDxIXOpfBiaejICt2w5WPyTFDb6U7I5mDPddtfjJWPefaiauIsiaXyWg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### Agent 2 Agent：让 Agent 们无缝协作的新协议

😂 AI 开发者好不容易在 WaytoAGI 社区、AI 博主们的共学努力下，逐渐搞懂 MCP 是什么。

现在 Google 又搓出了特殊的协议—— Agent 2 Agent。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwoG9fZaMHibMMLIny7osHzuNqfyZHtXibbl5OiaJZaojcnpJ0Jvg94DRzg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

如果要看小科普，隔壁那个很快的数字肝帝已经发了，可以去看看：[《5000字长文带你看懂，Agent世界里的A2A、MCP协议到底是个啥》](https://mp.weixin.qq.com/s?__biz=MzIyMzA5NjEyMA==&mid=2647670295&idx=1&sn=ea6fff7684a113ab12fdfc120991aaa4&scene=21#wechat_redirect)

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5Swj37hRI99YYkDczAsTuzmorvsYun4oB7iatxfIKLJZupRkoibUMd1zpYA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

大意是：

- A2A 是一种用于 Agent 与 Agent 联动协作的开放协议，是对 Anthropic 模型上下文协议 (MCP) 的补充
- MCP 侧重于为 Agent 接入各类工具与信息
- A2A 更侧重让“你要用的 Agent”（客户端 Agent）能够与“提供第三方支持的 Agent”（远程 Agent）进行联动，前者负责制定、传达任务，后者负责执行
- 在 A2A 连接的过程中，Agent 之间可以互相发送消息，传达上下文信息、回复等
- A2A 协议的连接，可以持续保持很久，直到完成任务

  

官方也给了一个演示视频，用来看效果：

，时长01:22

类 A2A 协议在未来 AI Agent 全面落地的时代，当然非常重要。

但不管怎么样，在类 MCP 生态还未健全、Workflow 到底能不能算 Agent 都没分清楚的现在，普通人甚至大部分开发者，也都没必要过多关注 A2A 协议。

Don't be so serious.

如果你喜欢研究技术，可移步官方 Github 仓库：https://github.com/google/A2A

  

---

## 🗂️ 其他 AI 应用、开发者工具和 601 个案例

除了前面的模型更新、 A2A 协议外，谷歌还面向一般用户、开发者更新了一堆应用和开发工具，以及 601 个真实 AI 应用案例。

  

就挑一些重点说，按主观优先级排列：

  

### Firebase Studio：搭载最强 AI 的云端 AI 编程工具，支持一键部署应用

Google 也发布了他们自己的 AI 编程工具，得益于 Google Cloud 的云资源，开发者可以用 Firebase 一站式完成应用开发的全流程。

包括 AI coding、编译构建、云服务部署、运行 的一切。

确实很方便，而且不需要下载 IDE，在云端就可以完成 AI 编程。

，时长00:17

他们的首页是这样的。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwXRIfiaXicPs3jg4RuQwhQzy2azC2XmbtLPCSkJQuAocE7WA64eUpqoow/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

具体的 Coding 界面长这样，操作体验和其他 AI 编程应用一致。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwLSj42dCzjLIEsQ9GVuUJm1FkmcaOawAibvM7botnBSgs7EsPoHlSsDw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

得益于最强 Gemini 2.5 Pro 的加持，你能体验到这个星球上现在一流的 Coding 体验。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwANpicwEVGCkwhIeVhfLYNkrCUzPMJDmz9sJ1TpxV0sEjSEWlXkCMpyQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以前往https://idx.google.com/体验。

  

---

### ADK：Google 的新 Agent 开发框架

ADK，全称 Agent Development Kit。也是 Google 新发布的开发框架，适用于构建 Multi-Agent 系统的开发。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwfuCx8H8H9ZXJicdgNkxJUlUHPbiblkOLMN2OjMniclMA4HDu87j6ib0bPw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

以下是官方介绍的优势：

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwicwZA9AicTxZLK42R4NWRJwnGK1R5zd0MCl416o6TBApNCmwBzmywFLg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

开发者可以自行前往 https://google.github.io/adk-docs 查看具体项目

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwAmN1Hdgrib3eIU3JwgBVjhKLDhKzpgsfGdyRS2rzmu5QibRuyZORh6Vg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

---

### Google Workspace ：集成大量 AI 服务

Google 给 Workspace 套件追加了大量的 AI 能力。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwDicn0KU3uusUJo2BuIOYlM9iaWkECn5BvoRJianiaj7iaxbCJAsvgwiacUjw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

为 Docs、Sheets、Meet、Chat 等日常工具带来更多 AI 功能：

- 可以把 Google 文档变成音频版本，或者用播客风格概括文档亮点
- Google 文档新增“帮我改进”功能
- Vids 可用 Veo2 视频生成模型
- Sheets 支持用 AI 自动分析数据，并生成洞察

对了，普通用户在 Google Doc 中无法体验

---

### Google AI Studio 整体 UI 优化

Google 这次还是没选择优化他们的 Google Cloud 控制台设计，而是选择了继续优化 AI Studio。

整体设计风格向 Gemini Web 应用靠拢，变清晰了不少。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5Swlia9iaA7tH6Om4B2KjoUfg5sXtBvR3GUwueNOM7hCEGfxaLJwx0VsKkQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这算个小添头，还不错，用起来会更顺手。

  

---

### Google 的 601 个真实客户带来的 AI 案例

Google 更新了过去一年他们推动的 AI 客户案例。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwRvWbcmVW7rL6DfJR5PmcvMnB89ggG2jQia4l632jogicRczKIjeeMsKw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在去年 Google Cloud Next 24 时，这个案例列表还只有 101 个，现在已经多了 500 个。狠狠秀了一把肌肉。

  

用 Gemini 总结这 601 个应用场景，涉及的应用场景如下：

- 客户代理： 提升客户服务（如聊天机器人、个性化推荐、订单处理）
- 员工代理： 提高员工效率（如自动化任务、信息检索、内容生成、协作）
- 创意代理： 加速创意内容生成（如广告、图像、视频、文案）
- 代码代理： 辅助软件开发（如代码生成、调试、代码库理解）
- 数据代理： 强化数据分析和洞察（如模式识别、预测、供应链优化、数字孪生）
- 安全代理： 增强安全防护（如威胁检测、欺诈预防、合规性）

  

相信对很多 AI 公司（尤其 To B）会有不少解决方案上的启发。

详细案例集在此：https://cloud.google.com/transform/101-real-world-generative-ai-use-cases-from-industry-leaders

  

---

### Ironwood TPU：Google 第 7 代 AI 芯片，专为推理而生

Google 即将推出他们的第 7 代 AI 芯片「Ironwood」，是他们迄今为止性能最高、可扩展性最强的定制 AI 加速器，也是首款专为推理而设计的加速器。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwQHCibTzr3FWcbDjUer4NibvY56Rwnlp27vuEZNYwXv4UbzAhpZnZyNYg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

官方公布 Ironwood 的峰值计算性能是上代 Trillium 的 5 倍，将大幅加速 AI 推理效率。

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwoB0rU3kibvYThKjtGshKTp48n8FfErhiaAmvPgm2RJnadHVv5HibmokEQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwMsbKsfiburn70WhbW4vVKuvjzOX32icmlk6ILX8rfF6ZYIPcJZIxftyQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![Image](https://mmbiz.qpic.cn/mmbiz_png/7ck8FnyVQnsgEe9GPc9oicibia0dUrVC5SwD9SJ53aAzzsXaapzWGNA96n58FwribmMOdlqg4FgvySZ343M4hzQXnQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

除了以上这些外，Google 还更新了不少其他的 AI 开发小套件、解决方案。

在这里看到 Google Cloud Next 2025 的完整官方公告：https://blog.google/products/google-cloud/next-2025/

  

---

差不多就是这些内容，我最期待 Gemini 2.5 Flash ，你最期待哪个更新？

你觉得 Google 又是否能借这次 Next 25，重新当回 AI 界老大哥呢？

---

## 📑 Ref

- 公告原文

- 【Google Cloud Next 25 官方原文大合集】：https://blog.google/products/google-cloud/next-2025
- Gemini 2.5 Flash：https://cloud.google.com/blog/products/ai-machine-learning/gemini-2-5-pro-flash-on-vertex-ai
- Vertex AI - Veo 2 / Chirp 3 / Lyria / Imagen 3：https://cloud.google.com/blog/products/ai-machine-learning/expanding-generative-media-for-enterprise-on-vertex-ai
- A2A：https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/
- Agent Development Kit：https://developers.googleblog.com/en/agent-development-kit-easy-to-build-multi-agent-applications/
- Google Workspace：https://blog.google/products/workspace/cloud-next-2025-workspace-gemini/
- Google AI 的 601 个落地案例：
    
    https://cloud.google.com/transform/101-real-world-generative-ai-use-cases-from-industry-leaders
    
- Ironwood TPU：https://blog.google/products/google-cloud/ironwood-tpu-age-of-inference/

- 文内提到的可体验内容

- Firebase Studio：https://idx.google.com/
- Google AI Studio：https://aistudio.google.com/
- Chirp 3：https://cloud.google.com/text-to-speech/docs/chirp3-hd
- Imagen 3：https://labs.google/fx/zh/tools/image-fx

- Waitlist 申请地址

- Veo 2：https://docs.google.com/forms/d/e/1FAIpQLSfdksQf4brbFzAx5l1geMx7DlBTjoZKjA4DuI3uTiETCB-0hg/viewform
- Lyria：https://docs.google.com/forms/d/1YktCIiIzyZe6TxfKnQ9PzybXGLzOeH0LJMUnhJubi1M/viewform