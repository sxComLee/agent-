---
标题: "新模型亦是新 Agent，Kimi-Researcher 超大量一手实测！"
链接: "https://mp.weixin.qq.com/s/DtCACnnSGW-0avuptyukaw"
作者: "[[特工Alpha/彩虹糖]]"
创建时间: "2025-07-03T14:14:07+08:00"
摘要: "月之暗面发布新一代Agent模型Kimi-Researcher，通过端到端强化学习训练，在HLE和xbench上取得SOTA成绩，并展示了其在深度研究任务中的出色表现。"
tags:
  - "clippings"
  - "AI"
  - "深度研究"
  - "强化学习"
  - "月之暗面"
  - "Kimi-Researcher"
字数: "630"
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
原创 特工Alpha/彩虹糖 *2025年06月24日 18:35*

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NIohwLdkvYtSkfytbKHl5WqcKRZG38WUnxFNE1ZNTaEZfKQNejEzrjMCex9WWJK5mmwIzH2uHnhxg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

> 月之暗面正式发布新产品：Kimi-Researcher，是新模型，亦是新 Agent。

内容编辑丨特工阿尔法 特工彩虹糖

**内容审核丨特工少女**

被称之为 “ **Agent 元年** ”的 2025 已过半载， **“下半场”** 亦百花齐放。

但我们似乎有了些共同困惑，比如：

“Agent 产品频出，但好像都只是 Workflow，究竟哪个产品最实用？”

**“Paper 越来越多，且都说自己模型又 SOTA 了，如今 Benchmark 还有参考价值吗？”**

……

关于后者， **红杉中国** 用两年多的思考，构建出了 **xbench** 这份同时考验 AI 能力与产品力的实际基准测试。

而对于前者，沉淀已久的大模型独角兽 **月之暗面** ，终于交出了 “AI 下半场”的第一份答卷—— **端到端强化学习训练的新一代 Agent 模型：Kimi-Researcher** 。 更令人欣喜的是， **其基座居然还是尚未发布的自研新模型！**

---

**✍️ 特工帮你问：“** **端到端** **\+** **强化学习** **→** **Agent模型** **”究竟是个啥？和最近的 Agent 产品都有什么区别？**

**1\. 端到端训练 ：从用户的“输入端”到产品的“输出端”都是一个模型， 过程中的 workflow 是模型自己逐步生成的（让模型学会自主调用工具） ，不依靠人去预定义工作流（这与大部分 Agent 产品截然相反）。**

**2\. 强化学习： 和普通训练相比，新增了“奖励函数”，顾名思义就是，当模型做对了就给分 / 做错了就扣分——久而久之，模型可以学会什么是对的什么是错的。需给定一个空间，让模型在里面自由玩耍。**

**3\. Agent 模型：Agent = 模型 + 推理/规划 + 工具/行为+ 记忆...（还可加，认知，感知，情绪）；与之前训练大模型相比，Agent RL 更强调模型对其他组件（能力）调用的训练。阶段是“后训练”，常用策略有 SFT→RL→...**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NIohwLdkvYtSkfytbKHl5WqrP2m9vhMqkKW2ANpXy5XCmO1uypaT6dnwC7Q6U6QlIwaIUfVd7vbDw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1) ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKicUC6ia8tIxlVpID6fhib5lNTAp0fic5GSuclU48OcGmvuwQyN7NODuEdsWT20EzYTkBHFuGNHsQbeg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

## Agent 元年的逆行者？AGI 的坚定探索者？

## Kimi 做了第一个吃螃蟹的人

最近，各类的 Agent 层出不穷：前有 Manus 引领新风，后有 MiniMax 集大成者 。而可惜的是，迫于通用智能的难度与随之的压力，许多优秀的模型团队放弃了预训练或已转向垂域……

也因此， **大众用户能在国内“直连即用”的 Agent 产品其实一直寥寥无几** 。

而就在这个阶段， **Kimi 居然加注预训练的同时，坚定地选择了在自研模型的基础上探索** **通用** **智能体。**

**Kimi-Researcher** 从初始 8.6% 的 HLE 准确率， 几乎 **完全依靠端到端的强化学习训练** ，将成绩提升至 **26.9% HLE 实现登顶（Pass@4 准确率甚至达到了惊人的 40.17%）** ——打破了 OpenAI 和 Gemini 积累已久的 Deep Research 壁垒。

此外，其还 SOTA 了红杉 xbench，很好地体现了其解决现实需求能力。如愿成为了国内第一家验证大规模 E2E Agentic RL 可行性并完成产品化的团队。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKz8sNravYsa7l76e6JWovHel4QEtsJUgOhYWjicesb4697KNHbh7gIlytdE5viaWXTAXB0ALfiaQlaQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

Tech Blog 全文： https://moonshotai.github.io/Kimi-Researcher/

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKicUC6ia8tIxlVpID6fhib5lNmLcIpcssiaK8JDyyDiaibk3AfRllIXpotzfcJQqSHDdIblU3Wia1Vw3tmQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

## 当“通用智能”对齐“用户需求”

刚听闻喜讯，我们特工便努力争取到了内测资格，并连夜展开了大量实测和深入分析。毕竟， **解决用户需求才是检验产品价值的第一标准** 。

令人激动的是， **我们真的从 Kimi-Researcher 的思考过程中感受到了一定程度的智能。**

在详细分析 Case 之前，容我先为大家简单介绍一下 **Kimi-Researcher 的流程以及最终效果** ：

1\. 对于用户提出的每一个问题，他都会 **认真思考并提出精准的反问** ——与你一起拆解问题、厘清意图，确保真正理解你想解决的是什么；

2\. 经过对需求的深入理解，他会通过平均 23 步的推理步骤来解决问题，结合任务目标灵活规划行动路线 **，每一步都是不断** **根据** **环境的实时反馈** **调整** **而产生的：**

- **优质搜索** ：每个任务，他会平均检索 74 个关键词，找到 206 个网址，再自主筛选出质量最高的一批信息；
- **调用工具** ：配合搜索，他总会自主调用浏览器以及代码等工具，可以处理原始数据、自动生成分析结论。
![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/0v4p9yzE7NKz8sNravYsa7l76e6JWovHS1bicmu2OVFu3hS2s70VTicKyiba1SbbDiaXp0niaN37fVT8hE6zqK7e63g/640?wx_fmt=gif&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

3\. 交付结果：

首先你会获得 **一份 1w 字以上的报告** ，每份平均会 有 **26 处引用** 。

如果你想查找模型 insight 的来源，你还可以点击句子对应的 icon 来直接 **溯源（高亮版）。**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/0v4p9yzE7NKz8sNravYsa7l76e6JWovH9Ubu8icVj0n3LDTpsaaGpDNrzBrcqoaDLiaAHbcqBFKiayqZC9rf375dA/640?wx_fmt=gif&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

除了文字报告之外，你还会收到一份 **简约且美观的可视化网页** ，用于梳理自己的理解与加深印象，可读性 Up！Up！

https://www.kimi.com/pr eview/d19p79os8jdm2ikr99b0?blockId=108

**以下是我们随手节选的一些实测 Case，赏心悦目的环节！数据分析，思维导图，插图排版，元素配色……样样精通。**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/0v4p9yzE7NKz8sNravYsa7l76e6JWovH49VziaItGMC0mtAibOBXY7IXVNuBt6wibqVnLALDiawcehQvXnsq11NVyg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

Case Gallery

总的来说，Kimi-Researcher 不只是简单的信息汇总工具，他会与你一起梳理需求，拆解问题本质， **确保** **其** **任务目标真正对焦。**

他能灵活调用搜索&浏览器、运行代码、处理数据，动态适应实时环境并对齐用户目标。

**最终产出包括** ：一份万字级报告（每段引用都可追溯），以及一份结构清晰的网页版本（见上图），真正满足从信息检索到知识构建的全流程需求（真的超赞！）

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKicUC6ia8tIxlVpID6fhib5lNxEchnkSVVQI7ZCDCU3OrWta33JbicPsU4mIYNKc18icMWoYDdBV0YnjQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

## 实测 20 个案例（文末附链接）

## 两分钟带你看懂 Kimi-Researcher

Kimi 已在其技术博客中给出了很不错的 5 个 Use Case，场景包括：学术研究、法律监管、金融分析、临床医学、信息挖掘……

所以这次特工会节选实测中发现一些的 「Aha」现象，并且更聚焦于中文的日常需求。

我们将问题一并给了 **Kimi-Researcher** 与 **OpenAI Deep Research** 「$200 每月」，并针对他们的回答进行了模块对应与对比分析。

而且附测了近期对 Multi-Agent 路线非常有见解的 Anthropic 之 **Claude 4 with Advanced Research** 「$200 每月」的结果，供大家思考与讨论。

**Case 1. 硬件产品分析**

> “对 OP PO Find X8 Ultra、XIAOMI 15 ultra和Vivo X200 Ultra进行深入的对比分析，涵盖所有关键方面。”

A: Kim i-Researcher： https://www.kimi.com/share/d1c6o8anae76ql6qt5c0

B: OpenAI Deep Research： https://chatgpt.com/share/68585ba0-2b3c-8003-a231-cd938efc13d4

> Claude Advanced Research: https://claude.ai/public/artifacts/996edb0d-07fc-45f4-9545-f996dd4d1a4f

硬件产品是考验 **深度研究** 能力最好的场景之一，不仅产品本身的技术指标与特性很多，还需要从多个信息源来对技术、商业、用户、生态等进行全面的调研分析。

**这一次，Kimi 可以说是非常惊艳。**

在列表分析手机的影像系统时，Kimi-Researcher 不但考虑了基本的摄像头参数，还将中焦、潜望、前置、光学变焦和数字变焦纳入了分析维度。（OpenAI 只在文字描述时部分提及）。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKz8sNravYsa7l76e6JWovHY33U1ucHEnvc6cic8fdoE6YhHv51uiahsPrx2G3nFcia9uIjKGTec7XSg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

除了基本参数之外， **Kimi-Researcher 还悉心考虑了影像系统在“夜景拍摄”的能力，以及“视频录制”的各种表现，这些都是 OpenAI Deep Research 完全没有考虑的维度。**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/0v4p9yzE7NKz8sNravYsa7l76e6JWovH9j6C45fFickXJCDoHrc5ESflGZYbQR4YN6g15PPqGVfsoadqoo2ibsPA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

**Kimi-Researcher 的悉心考虑**

**Case 2. 近期 GitHub 热门开源项目**

> “请对开源项目 Browser-Use 进行全面的解读和分析”

A: Kimi-Research er:https://www.kimi.com/share/d1cc2rii59732pb02lkg

B: OpenAI Deep Research： https://chatgpt.com/share/6858bbd7-4864-8003-b196-7fa76fed9247

> Claude Advanced Research: https://claude.ai/public/artifacts/70e98682-d0f1-4576-9b15-bd27358d573a

当 Kimi-Researcher 遇到复杂的代码项目时，我们发现他在 report 阶段居然 **涌现** 出了： **自主通过 Mermaid 代码画图，梳理知识架构的能力** 。 反之 OpenAI Deep Research 更习惯在某一个信源里深挖，擅长纯文字表达。

（我们也问了 Kimi 负责这部分算法的同学，大家都表示意料之外的惊喜，因为没有对此进行过任何的训练）

但对 GitHub 仓库的解读深度，暂时不及 OpenAI，期待后续能迭代 ：）

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/0v4p9yzE7NKz8sNravYsa7l76e6JWovHlOGz60WSj1wnGDgUwvfRhTLBQPg5vDW53we4g0GicRyC3vU2Siamzg1w/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

****Case 3. 热点&行业分析****

> “帮我分析一下全球爆火的labubu，从诞生到最近破圈的全过程”

A: Kimi-Research er: https://www.kimi.com/share/d1c6ogpg6i8l5gnvct00

B: OpenAI Deep Research： h ttps://chatgpt.com/share/685866c0-38fc-8003-8920-39c34bb975ed

> Claude Advanced Research: https://claude.ai/public/artifacts/03698a21-de62-4588-b2ac-c1fcdb9203a4

Labubu 是最近大家都在热议的话题。从两者的 Clarification 环节就可以看出， **Kimi-Researcher 的思考逻辑注重结构化表达与逻辑闭环，通过时间线梳理、数据验证与跨界反馈，注重还原现象全貌并进行深度归因** ；相比之下，OpenAI Deep Research 更侧重故事化叙述与感性观察，虽单一视角更加深入，但整体结构相对松散。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKz8sNravYsa7l76e6JWovHnliasvWMdI1x7C1aTy7pauuXUM9f1Lyc0ryo0DBujIdAlLXezr2MXvg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

在时间线梳理上， **Kimi-Researcher 的结构更清晰、节奏更紧凑** ， 通过阶段划分配合表格呈现，不仅标出了每个关键节点，还结合了对应的触发机制与市场反应，用户能快速看懂全貌。

但是 **OpenAI 的内容更偏向段落式铺陈** ， 缺乏明确的时间轴与阶段划分，信息呈现偏散，且它过于重视设计者背景的介绍，这个点对本问题的重要性有限。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKz8sNravYsa7l76e6JWovHqTbrcibID5UibAanSn4edCt4kCoOzcV0r15jrY8tqjzqdMzYbcA3u9Tg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

在分析 Labubu 的成功因素时， **Kimi-Researcher 从产品设计、营销策略、明星效应到社交传播构建了四个核心维度** ， 逻辑完整、结构清晰；而 **OpenAI Deep Research 的内容则更聚焦，重点围绕社交媒体传播与二级市场溢价展开** ，虽然分析范围相对较窄，但在某些关键点上挖掘得更深入。

**Kimi 也分析了二级市场的炒作行为** ，更偏向把它作为“营销策略放大效应”的影响和结果来处理，放在整体链路中去看，显得有体系感。但 **OpenAI** 在这一点的分析还是更加 insightful，并将溢价产品做成了表格对比，对于关注产品价格的用户实用性更强。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKz8sNravYsa7l76e6JWovHzYN3iaoGWCCaFibsvDB1Um65ialicK8zJLibN4uSvziaCIx9e69QK6c2YvEQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1) ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NLVkQGVRNdEAGa32xs0aJQN0T3AEI6RktEkw58Ibn9p59OzZPcuyfz82jiczM2yQpcFlroUCw2iaJdQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

## 特工之问 & 特工之思

**✍️ Q：Deep Research 为什么这么重要？为什么 OpenAI 和 Kimi 都把它当作为第一个 Agent 产品？**

A：从智能角度出发， **Deep Research 要同时考验模型的各种底层能力** ，包括但不限于：分析与推理能力、深度搜索能力、长文本能力、记忆管理能力、各种工具调用能力。

这些能力正是构建通用 Agent 所必须的关键模块，也恰好对齐了当前主流模型研发的重点方向。

因此， **De ep R esearch 是一个天然的“试金石”任务，用于推动并验证 Agent 系统的综合智能表现。**

---

**这么一看，Kimi 于此的每一点都非常吻合：**

**出色的 K1.5 系列模型，积累已久的搜索沉淀（以及各种信源合作），最早的长文本，内测中的 Memory 功能，正在高度重视的工具学习……**

**我想，其实这也是 Kimi-Researcher 为什么如此出色的原因。**

---

**✍️** **Q** **：Kimi** **\-Researcher** **和其他 Agent** **应用产品有什么区别？**

A： **大部分 Agent 产品都是通过调用 Claude** 等 API ，结合各种精细的 Prompt，再结合人工编排的 Workflow 包装而成。这类产品 **依赖大量人为规则与预设逻辑** 。

而 **Kimi-Researcher 是完全基于 Kimi 自研的 K 系列模型，通过纯粹的端到端 Agentic RL** **后训练而成的 Agent** 。 其解决用户需求的每一步，都是 Agent 自己不断根据环境的实时反馈调整而产生的。

这使得 Kimi-Researcher 更具泛化能力，相较人工编排的工作流有更高的上限，也更接近我们理想中的 General Agent 形态。

---

这带给了我两个思考：

**1\. 这次 Kimi-Researcher 的成功，给我们同行先验了Agent RL 的显著效果，给未来真正的“自主智能体”指引了很好的探索方向。** 我深刻地意识到，这已是业界与学界高度对齐的时代，我们或许即将迎来一场「 模型即 Agent 」的盛世。

2\. 对于我们国内创业者和开发者来说，目前最大的痛点之一就是，我们缺少比较好的国内模型的 API 来构建好的 AI 应用。好消息是， Kimi 声明了即将开源基模的安排， **可能在不久的将来，我们有机会从 Buil d with Claude 变成 Build with Kimi** 。也意味着，国内的大众也能在不久后，能真正地享受到现在 AI Agent 的百花齐放，而不是一直听个响，看不见摸不着……

---

✍️ **Q** **：Kimi-Researcher 还有哪些不足之处？**

A：目前作为研究助手已经很不错了，但还有一些值得优化的：

**1\. 关于功能：** 感觉信息索引非常好，所以希望可以支持指定文件/链接的上传，以及关联 GitHub 等知识库（或许可以参考 DeepWiki）

**2\. 关于搜索：** 目前主要依靠线性搜索（感觉比较慢），或许可以参考 Claude 的 multi-agent 的思路，去用一些 sub-agent 来并行搜索。以及可以继续优化信源，中文信源可以增加一些公众号的比例

**3\. 关于分享：** 希望有针对于 Report 的分享功能，甚至做个类似公众号推文的指定语句的转发。

**4\. 关于交互：** 希望生成的 report 以及可视化报告可以像 OpenAI Canvas 一样交互与编辑……

---

总得来说，作为 OpenAI Deep Research 的深度用户 （每个月能把 $200 的 Pro 额度用完）， 目前的 Kimi-Researcher 的各种能力和产出质量，已经非常满足甚至超出我的预期了。  

至少在信息收集和汇总报告的能力上，并不亚于 OpenAI。但在一些高质量 insight 的推理生成上，值得继续探索（感觉 OpenAI 在这点上已经进行了一些优化）。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NLVkQGVRNdEAGa32xs0aJQNPibuicNHvJ3fjkXBqEBPmhT0bQGdpe2AYTwIydpWnpfhTam819FwDbibQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

**其他实测不错的案例**

**动漫娱乐：**

**1\. 宫崎骏： https://www.kimi.com/preview/d19qfcl4335e5l363f7g?blockId=46**

**2\. Nintendo Switch： https://www.kimi.com/preview/d19rf7s5rbsds6sqkkc0?blockId=30**

**健康：**

1\. 减脂指南： https://www.kimi.com/preview/d1ciums268gg176j0m90?blockId=108

2\. 体态康复： https://www.kimi.com/preview/d1ciu7c268gg176iu600?blockId=108

3\. 科学锻炼： https://www.kimi.com/preview/d1civntjqed30ec9279g?blockId=82

**商业分析：**

1\. 影石 Insta： https://www.kimi.com/share/d19v3e8nnlr1nd3psl70

2\. 英伟达： https://www.kimi.com/share/d19urcpl51j0a24ghpjg

3\. 无印良品： https://www.kimi.com/preview/d19s78e1bb2urkuu18eg?blockId=100

4\. 商分： https://www.kimi.com/share/d1aio34nvj4j1f3u5pd0

5\. 创业： https://www.kimi.com/preview/d1ciqs9kotdbg2j39k5g?blockId=108

6\. Labubu： https://www.kimi.com/preview/d1d56oeruqkovfdk7i60?blockId=32

**金融：**

1\. 炒股： https://www.kimi.com/preview/d18nc21l51jd29rf0fq0?blockId=19

2\. 财报： https://www.kimi.com/share/d1ce1mrmtofaqtgglqo0

**文化类：**

1\. 中国风游戏： https://www.kimi.com/preview/d19qb861bb2urkungckg?blockId=40

2\. 中国传统文化IP： https://www.kimi.com/preview/d19p79os8jdm2ikr99b0?blockId=108

3\. 中西乐器： https://www.kimi.com/preview/d19qk9vf2en38qtri6t0?blockId=66

4\. 茶道： https://www.kimi.com/preview/d19rnrvf2en38qtuqs50?blockId=108

5\. 书影音： https://www.kimi.com/share/d19tts5eik6ulj8q4b9g

**6\. 法律：** https://www.kimi.com/preview/d1cusv3odd0khd9qb000?blockId=28

**日常：**

1\. 攻略： https://www.kimi.com/preview/d1d5283lmiu5culg8clg?blockId=56

2\. 手机： https://www.kimi.com/preview/d1d577s2sn14bf180tn0?blockId=48

**3\. 代码** ： https://www.kimi.com/preview/d1d567uc8f25j4e2mri0?blockId=108

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/0v4p9yzE7NKGsCkic8Q7fIRWMRLibyQmwoBeiahVkGicTcy1aCqLXqA2BDDqFOa8ibHv5ry1UgQol7ISLcZS0COHaog/640?wx_fmt=jpeg&from=appmsg&wxfrom=5&wx_lazy=1&tp=webp) ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKz8sNravYsa7l76e6JWovHPKap8eHOWrAyvu14Teic6EZQgg0Q3ALbdkUHn8uIyAap7icGyzzfmOkw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1) ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NKz8sNravYsa7l76e6JWovHsAZCAGRjeUDnNDZVOOLkgiaUCSbq0cZmk4VRxytF37w3RVtg9DG19uQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/0v4p9yzE7NLYCFULKZMW4HQDhVPpdyRZTpPaicMJYZBmuF6THYS950Em2u6YSAu2y4Bbicg7dlDZZTwrw6YIveEw/640?wx_fmt=png&from=appmsg&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

继续滑动看下一个

特工宇宙

向上滑动看下一个