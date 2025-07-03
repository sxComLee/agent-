---
标题: "Anthropic 官方：Genspark 是如何构建 Agents 的？"
链接: "https://mp.weixin.qq.com/s/gGfJS-5fZD-6eyjbzTnJKA"
作者: "[[宇宙编辑部]]"
创建时间: "2025-07-03T09:59:27+08:00"
摘要: "Anthropic官方介绍了Genspark如何利用Claude构建自适应AI Agents，改变用户研究和内容创建的方式，显著提升效率和规模。"
tags:
  - "clippings"
  - "AI"
  - "自适应智能"
  - "Genspark"
  - "Claude"
  - "效率"
字数: "174"
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
![cover_image](https://mmbiz.qpic.cn/sz_mmbiz_jpg/0v4p9yzE7NIWHHlu9ViaDxTgPpPISbRmWXZMRj4LVIfylEYtkPXZpybLY6ic4bOfWbjMs5mGZxX9SQ12zTWD2ia9w/0?wx_fmt=jpeg)

宇宙编辑部 [特工宇宙](https://mp.weixin.qq.com/s/) *2025年05月29日 22:03*

![Genspark + Anthropic logo lockup](https://mmbiz.qpic.cn/sz_mmbiz_jpg/0v4p9yzE7NIWHHlu9ViaDxTgPpPISbRmWDhsxm5hvXicrH5TnyYEVlbldjUpPiagUGCyDcRvLShtm3PDAIr6hTLOQ/640?wx_fmt=other&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)


  

Genspark 借助 Claude 打造自适应的 AI Agents，改变了人们研究和创建内容的新姿势，为复杂的工作流提供了极大的效率和规模。

Genspark 的关键成果：

1\. 推出 Super Agent 后 45 天内实现 3600 万美元年度经常性收入；

2\. 为超过 500 万用户提供动态的、自适应的 AI 工作流；

3\. 在大语言模型评审中获得高质量评分；

4\. 通过自动幻灯片创建和多步骤推理为用户节省大量研究时间。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKicUC6ia8tIxlVpID6fhib5lNTAp0fic5GSuclU48OcGmvuwQyN7NODuEdsWT20EzYTkBHFuGNHsQbeg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

突破固有的搜索工作流的限制

传统 AI 搜索产品对每个查询都遵循相同的流程：分析关键词、检索网络结果，然后将它们总结成一个答案。

虽然这对简单问题有效，但当用户需要复杂研究、详细比较或多步骤分析时，这种方法就显得力不从心。

Genspark 最初使用相同方法构建搜索引擎，并添加了**专业数据源和验证的 Agents 等改进**。尽管吸引了 500 万用户，他们仍然遇到了根本性限制。

“我们意识到我们仍然受困于传统设计—一个固定的、预定义的工作流，” Genspark 联合创始人兼 CTO Kay Zhu（朱凯华）表示，“要实现真正自适应、能解决上下文长度问题的 Agents，我们必须完全打破这一框架。”

团队认识到，不管怎么优化细节，都解决不了一个根本问题：**无论问题多复杂，需求多不同，每次提问的请求都是按照一套标准的固定流程来处理。**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKicUC6ia8tIxlVpID6fhib5lNmLcIpcssiaK8JDyyDiaibk3AfRllIXpotzfcJQqSHDdIblU3Wia1Vw3tmQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

选择 Claude 实现自适应智能

为构建 Super Agent，Genspark 需要一个**能够处理复杂推理并协调多个专业系统协同工作**的 AI 模型。经过测试各种选项后，他们选择了 Claude 作为新架构的基础。

Claude 的规划和推理能力使其成为协调 Genspark 混合 Agents 方法的理想选择，不同 AI 模型相互验证输出以减少错误和幻觉。“对于 Super Agent，我们利用 Claude 的**规划和推理能力**来驱动整个 Agent 流程。”朱凯华说。

Genspark 发现 Claude 在对其产品至关重要的特定任务上表现出色。对于 AI 幻灯片功能，Claude 的编程能力对生成交互式演示至关重要。

“Claude 处理创建幻灯片时的大部分繁重工作，我们发现它具有出色的视觉设计感。” 朱凯华说。这种技术能力与设计感性的结合使 Claude 在多个功能中都不可或缺。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKicUC6ia8tIxlVpID6fhib5lNxEchnkSVVQI7ZCDCU3OrWta33JbicPsU4mIYNKc18icMWoYDdBV0YnjQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

由 Claude 驱动的动态协调

Genspark 的 Super Agent 打破了限制传统搜索引擎的刻板工作流。它不是对每个查询遵循相同的预定步骤，而是根据每个问题的实际需求调整其方法。Claude 作为主协调者，分析请求、规划步骤、选择合适的工具，并根据新出现的信息调整策略。

这个自适应系统依赖三项核心创新：

1\. **动态协调**，Claude 协调八个专业 AI 模型，通过交叉验证确保质量。

2\. **专业工具和子 Agents**，可以处理从创建演示到执行 Python 代码到拨打电话的各种任务。

3\. **精选的高质量数据集**，负责验证的 Agents 持续审核以维持准确性。

结果是一个根据任务进行匹配的智能系统。简单问题得到快速、直接的答案，无需不必要的复杂性。

复杂研究项目可以通过多种方法迭代，从各种来源收集信息，并不断完善结果，直到它们全面而准确。

根据用户需求，Super Agent 可以提供从简单答案到完整演示、交互式网页，或协调电话通话的各种服务，所有这些都由 Claude 无缝协调。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NLVkQGVRNdEAGa32xs0aJQN0T3AEI6RktEkw58Ibn9p59OzZPcuyfz82jiczM2yQpcFlroUCw2iaJdQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

变革 用户创造和研究方式

对 Genspark 用户而言，影响主要体现在节省时间和增强功能上。以前需要数小时手动研究、复制信息和格式化的任务现在只需几分钟。

5 分钟自动化工作相当于 3 小时人工努力。“我们使人们能够进行复杂研究、从网络收集信息并将其编译成美观的幻灯片，” 朱凯华说。

用户现在可以处理手动难以完成的复杂度和范围的研究项目。AI 幻灯片功能自动从多个来源收集信息，分析其相关性，并将所有内容编译成可供分享和协作的专业演示。

这改变了用户处理复杂信息任务的方式，让他们能够专注于更高层次的分析和决策，而不是手动的进行数据收集。

商业影响同样显著。迅速的市场采用和大幅的收入增长验证了 Genspark 的押注，即自适应 AI 是人们将来与信息交互方式的未来。

用户持续给予正反馈：速度、准确性和创造力的结合以他们未曾想到的方式改变了研究的工作流程。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NLVkQGVRNdEAGa32xs0aJQNPibuicNHvJ3fjkXBqEBPmhT0bQGdpe2AYTwIydpWnpfhTam819FwDbibQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

构建自适应 AI 的未来

Genspark 从传统搜索到自适应智能的转变，揭示了 AI 开发的一个基本真理：当你给予 Agents 灵活性而非约束时，最强大的系统就会出现。

“我们发现了一个基本原则： **更少 控 制，更多工具** ，” Genspark 团队解释道，“**过度结构化的工作流限制了创造力和深度，而允许多个专业 Agents 处理问题的不同方面，并赋予它们选择和切换工具的自由，则释放了更大的能力。**”

---
注释：更多工具=更多上下文，更多控制=更多延时。模型遵循指令会更加不确定且更耗时

---

这一理念现在推动着 Genspark 的发展，他们正在准备下一个功能发布。每一项新功能都代表着 AI 创造性解决问题的另一种方式。

对 Genspark 而言，这代表着新时代的曙光，AI 成为真正的思考伙伴。不仅执行命令，还与人类协作解决我们尚未想象到的问题。

原文链接：https://www.anthropic.com/customers/genspark

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NI5L7L0avRsRQLbjXkLKCjGfAxFGrstS3SOdUDbvh6O4rRSZ9zZTL0QNrNDq3tCiah9fgc0VjicL5Cw/640?wx_fmt=png&from=appmsg&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NJgmVXkX5SOF9K6Q6Rhl3BVDnlQic4h78NOjU6tMpodse12I3ZxvibEZO6M02kr2fTVUmf9cKrQBGDw/640?wx_fmt=other&from=appmsg&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NLYCFULKZMW4HQDhVPpdyRZTpPaicMJYZBmuF6THYS950Em2u6YSAu2y4Bbicg7dlDZZTwrw6YIveEw/640?wx_fmt=png&from=appmsg&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

继续滑动看下一个

特工宇宙

向上滑动看下一个

特工宇宙