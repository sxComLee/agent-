---
标题: "Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训"
链接: "https://mp.weixin.qq.com/s/tMWaXAC1KYLeyXFl6LzSTQ"
作者: "[[王兆洋]]"
创建时间: 2025-07-28T10:24:40+08:00
摘要: "Manus团队分享了构建AI Agent过程中关于上下文工程的经验教训，包括KV缓存优化、动态动作空间管理以及利用文件系统作为扩展上下文的创新方法。"
tags:
  - "clippings"
  - "AI"
  - "上下文工程"
  - "KV缓存"
  - "Manus"
  - "季逸超"
字数: 617
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
原创 王兆洋 *2025年07月19日 10:25*

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/fe1536f0a482a4195d146fbf2e948a5d_MD5.webp]]

作者 *｜* 王兆洋  
邮箱 *｜* wangzhaoyang@pingwest.com

**Manus从诞生第一天起就是一款值得关注的产品。**

只不过在很长一段时间里，它的争议盖过了产品本身，团队本身也并未系统地分享过自己产品背后的技术。

**这逐渐造成一个有趣的矛盾：** Manus诞生到今天，它做出的交互方式创新，不只塑造了外界对“AI Agent”的印象，也在受到一众竞争对手乃至模型大厂的认可或跟随，这些关注的焦点并非在它炮制的“概念”，而是实打实来自它的技术方案和产品思路，先是Anthropic 官方把它作为最有代表性的应用案例，然后是多个AI应用明星团队在产品路线上让人看到它的影子，后是最近ChatGPT Agent的发布甚至被一些实打实在一线做Agent创业的人称为OpenAI的Manus时刻。

而另一方面，依然有很多人在好奇这款“套壳”产品的技术含量，加之技术和产品之外的各种争议不断，使得它对于今天AI Agent的技术和产品发展方向的严肃价值被进一步忽视。

**而最近Manus团队终于难得自己出来系统的分享了这个产品背后的思路，并十分直接的分享了踩过的一系列坑，和因此做出的各种技术方案的设计和产品路线的决定。**

这是一个对很多AI Agent领域的开发者和创业者都有价值的技术分享。 我们把这个用英文写的技术博客也交给Manus自己做了一个编译和备注版本。

**这个版本在翻译和解释上完成度很高。但在我跟Manus做prompt 的过程中，一个有意思的地方是，它死活写不对作者的名字。而这个问题反而正是这篇博客重点提到的KV Cache命中率对AI agent产品带来的挑战的一个体现。**

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/89a4f4b70f266fe9b7d87c86de1f5e7f_MD5.webp]]

多次提示后依然写错了名字

借用博客里的话，可能这个问题反而“讽刺地”指向了上下文工程方向的价值。

以下为Manus自己生成整理的版本：

**AI Agent的上下文工程：构建Manus的经验教训**

**发布日期：** 2025年7月18日

**作者：** 季逸超 'Peak' Ji

1

**编者按**

随着AI Agent技术的快速发展，如何高效构建和优化 Agent系统已成为业界关注的焦点。本文是对Manus联合创始人兼首席科学家季逸超（Yichao 'Peak' Ji）撰写的《Context Engineering for AI Agents: Lessons from Building Manus》一文的中文编译。并在一些关键信息位置做了必要背景补充，以括号内信息的形式呈现，在文末做了术语解释和参考资料信息汇总。

季逸超是中国AI领域的知名创业者，曾开发出"猛犸"系列浏览器和Magi知识图谱系统，拥有丰富的自然语言处理和AI产品开发经验。在本文中，他分享了Manus团队在构建AI Agent过程中关于上下文工程的宝贵经验，包括KV缓存优化、动态动作空间管理以及利用文件系统作为扩展上下文的创新方法。

这些经验不仅揭示了当前AI Agent开发的技术挑战和解决思路，也为未来 Agent技术的发展提供了重要参考。无论您是AI研究者、开发者还是产品经理，相信都能从中获得启发。

1

**文章亮点总结**

以下是《AI Agent的上下文工程：构建Manus的经验教训》一文的10个最重要的亮点：

1. **上下文工程的重要性** ：Manus选择押注上下文工程，而非从头训练模型，以实现快速迭代和产品与底层模型的正交性。
2. **KV缓存命中率是关键指标** ：对于生产阶段的AI Agent，KV缓存命中率直接影响延迟和成本，是优化性能的关键。
3. **保持提示前缀稳定** ：LLMs的自回归特性意味着即使单个token的差异也可能使缓存失效，因此保持提示前缀稳定至关重要。
4. **上下文仅追加原则** ：避免修改之前的动作或观察结果，确保序列化确定性，以维持KV缓存的有效性。
5. **明确标记缓存断点** ：在不支持自动增量前缀缓存的框架中，手动插入缓存断点有助于优化缓存利用。
6. **掩码而非移除工具** ：面对不断增长的工具数量，Manus通过掩码token logits来管理工具可用性，而非动态添加或移除工具，以避免缓存失效和模型混淆。
7. **避免动态增删工具** ：动态添加或移除工具会使KV缓存失效，并可能导致模型混淆和幻觉动作。
8. **上下文感知状态机** ：Manus使用上下文感知状态机来管理工具可用性，通过掩码token logits来约束动作选择。
9. **文件系统作为扩展上下文** ：将文件系统视为上下文窗口的扩展，可以克服固定大小上下文窗口的限制，处理更复杂、更长的任务。
10. **虚拟文件系统的优势** ：Manus的虚拟文件系统能够高效存储检索信息、分层组织信息、在 Agent间共享信息以及支持版本控制。

1

**正文**

**在Manus项目的最初阶段，我和我的团队面临一个关键决策：我们应该使用开源基础模型训练一个端到端的Agent模型，还是在前沿模型的上下文学习（in-context learning）能力之上构建Agent？**

回顾我在自然语言处理（NLP）领域的第一个十年（季逸超出生于1992年，高中时期便开始独立开发苹果应用程序，并在高三时推出了备受瞩目的"猛犸1"浏览器。大一时他推出"猛犸4"浏览器，并获得了Macworld Asia 2011的特等奖，在业界崭露头角），我们没有这种选择的奢侈。

遥想 **BERT** 时代（已是 7 年前）（注：BERT 2018 年发布，代表“预训练+微调”范式），模型必须先微调、再评估才能迁移到新任务；一次迭代常常要几周——尽管那些模型和今日 LLM 相比小得多。 **对于节奏很快、特别是仍在寻找 PMF（Product-Market Fit）的应用，这种缓慢反馈循环简直是“判死刑”。**

**这是我上一个创业公司的痛苦教训** （季逸超的创业之路始于Peak Labs，他获得了真格基金和红杉中国的早期投资，致力于打造创新产品。其中，Magi系统被称为"中文互联网最大通用知识图谱"，显示了他在知识图谱和语义搜索领域的积累）。 当时我从零开始训练开放信息抽取（open information extraction，从非结构化文本中自动提取结构化信息的技术）和语义搜索模型。然后GPT-3和Flan-T5（Google的指令微调T5模型）出现了，我的内部模型一夜之间变得无关紧要。具有讽刺意味的是，正是这些模型标志着上下文学习的开始——以及一条全新的前进道路。

那段来之不易的教训让方向变得清晰： **Manus 要押注 context engineering** （上下文工程：系统性设计、组织、操控 LLM 读取的上下文结构与内容以驱动行为）。 **这样我们能在“数小时”而不是“数周”里交付改进，并保持产品与底层模型“正交”。也就是，模型进步是“上涨潮水”，Manus 要做漂浮的船，而不是被钉在海床的柱子。**

然而，context engineering 并不简单。 它更像“实验科学”：我们重写（rebuild）了四次 Agent 框架——每次都是发现了更好的上下文塑造的方式。

我们把这种架构搜索、prompt 微调、经验猜测的手工过程（manual process）戏称为 “Stochastic Graduate Descent” **（注，这里是一个双关自嘲，Manus翻译的版本里，AI Agent没有get到这个意思，它影射 Stochastic Gradient Descent，随机梯度下降，而Graduate 暗指“靠研究生体力/脑力不断试”，把 Gradient梯度换成 Graduate研究生，讽刺地说明：它不是数学自动优化，而是一群工程师/研究生手动做大量、带噪声的小实验，逐步逼近更好的 Agent 架构）** 。

**是的，它不优雅，但有效。**

这篇文章分享了我们通过自己的"SGD"达到的局部最优解。如果你正在构建自己的AI Agent，我希望这些原则能帮助你更快地收敛。

**设 计围绕KV缓存**

**如果我必须选择一个指标，我认为KV缓存命中率是生产阶段AI Agent最重要的单一指标** （KV-cache hit rate，键值缓存是Transformer模型中存储注意力计算结果的机制，命中率高意味着可以重用之前的计算结果）。它直接影响延迟和成本。为了理解原因，让我们看看典型 Agent是如何运作的：

收到用户输入后， Agent通过一系列工具使用来完成任务。在每次迭代中，模型根据当前上下文从预定义的动作空间中选择一个动作。然后在环境中执行该动作（例如，Manus的虚拟机沙盒环境，这是Manus提供的隔离执行环境，确保代码安全运行）以产生观察结果。动作和观察结果被附加到上下文中，形成下一次迭代的输入。这个循环持续到任务完成。

正如你可以想象的，上下文随着每一步而增长，而输出——通常是结构化的函数调用——保持相对较短。这使得 Agent中预填充（prefilling，将输入token一次性处理的阶段）和解码（decoding，逐个生成输出token的阶段）之间的比例与聊天机器人相比高度倾斜。 **例如，在Manus中，平均输入与输出token比例约为100:1。**

幸运的是，具有相同前缀的上下文可以利用KV缓存，这大大减少了首token时间（TTFT，Time-To-First-Token）和推理成本——无论你使用的是自托管模型还是调用推理API。 **我们谈论的不是小幅节省** ：例如，使用Claude Sonnet时，缓存的输入token成本为0.30美元/百万token，而未缓存的成本为3美元/百万token——相差10倍。

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/3690e5c0ab4e8a91e7d102e76b7489d1_MD5.webp]]

从上下文工程的角度来看，提高KV缓存命中率涉及几个关键实践：

1. **保持提示前缀稳定（Keep your prompt prefix stable）** 。由于LLMs的自回归（autoregressive，模型按顺序生成token，每个token的生成都依赖于之前的所有token）特性，即使是单个token的差异也可能使该token之后的缓存失效。一个常见错误是在系统提示的开头包含时间戳——特别是精确到秒的时间戳。当然，这让模型能告诉你当前时间，但也会杀死你的缓存命中率。
2. **使你的上下文仅追加（append-only）** 。避免修改之前的动作或观察结果。确保你的序列化是确定性的。许多编程语言和库在序列化JSON对象时不保证稳定的键排序，这可能会悄无声息地破坏缓存。
3. **在需要时明确标记缓存断点** 。一些模型提供商或推理框架不支持自动增量前缀缓存，而是需要在上下文中手动插入缓存断点。分配这些断点时，要考虑潜在的缓存过期，至少确保断点包含系统提示的结尾。

此外，如果你使用vLLM（一个高性能的LLM推理框架）等框架自托管模型，请确保启用前缀/提示缓存，并使用会话ID等技术在分布式工作节点间一致地路由请求。

**掩码，而非移除（Mask, Don't Remove）**

随着你的 Agent承担更多能力，其动作空间自然变得更加复杂——简单来说，工具数量爆炸式增长。 **MCP最近的流行只是火上浇油。** （Model Context Protocol，Anthropic提出的模型上下文协议，用于标准化AI模型与外部工具的交互）如果你允许用户可配置的工具，相信我：总会有人将数百个神秘工具插入你精心策划的动作空间。结果，模型更可能选择错误的动作或采取低效路径。简而言之，你高度武装的Agent变得更愚蠢了。

自然的反应是设计动态动作空间——也许使用类似RAG（Retrieval-Augmented Generation，检索增强生成，通过检索相关信息来增强模型生成能力的技术）的方式按需加载工具。 **我们在Manus中也尝试过这种方法。但我们的实验表明一个明确的规则：除非绝对必要，避免在迭代中动态添加或移除工具。**

主要有两个原因：

1. 在大多数LLMs中，工具定义在序列化后位于上下文的前部，通常在系统提示之前或之后。因此任何更改都会使所有后续动作和观察的KV缓存失效。
2. 当之前的动作和观察仍然引用当前上下文中不再定义的工具时，模型会感到困惑。没有约束解码（constrained decoding，限制模型输出必须符合特定格式或规则的技术），这通常导致模式违规或幻觉动作。

为了解决这个问题同时仍然改进动作选择，Manus使用上下文感知状态机（state machine，根据当前状态和输入确定下一个状态的计算模型）来管理工具可用性。它不是移除工具，而是在解码过程中掩码token logits（模型输出的原始概率分布）以防止（或强制）基于当前上下文选择某些动作。

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/b2d1416c7e505b578e2c17a88bd7cd91_MD5.webp]]

实际上，大多数模型提供商和推理框架都支持某种形式的响应预填充，这允许你在不修改工具定义的情况下约束动作空间。通常有三种函数调用模式（我们将使用NousResearch的Hermes格式作为示例）：

• **自动** – 模型可以选择调用函数或不调用。通过仅预填充回复前缀实现：<|im\_start|>assistant

• **必需** – 模型必须调用函数，但选择不受约束。通过预填充到工具调用token实现：<|im\_start|>assistant<tool\_call>

• **指定** – 模型必须从特定子集调用函数。通过预填充到函数名开头实现：<|im\_start|>assistant<tool\_call>{"name": "browser\_

使用这种方法，我们通过直接掩码token logits来约束动作选择。例如，当用户提供新输入时，Manus必须立即回复而不是采取动作。我们还故意设计了具有一致前缀的动作名称——例如，所有浏览器相关工具都以browser\_开头，命令行工具以shell\_开头。这使我们能够轻松强制 Agent在给定状态下只从某组工具中选择，而无需使用有状态的logits处理器。

这些设计有助于确保Manus Agent循环保持稳定——即使在模型驱动的架构下。

**将文件系统用作上下文（Use the File System as Context）**

现代的前沿大语言模型（LLM）现在提供 128K 甚至更多的 token 上下文窗口。但在真实的 Agent（agentic）场景中，这通常是不够的，有时甚至是一种负担。这里有三个常见的痛点：

观测（Observations）可能非常庞大，特别是当 Agent与网页或 PDF 等非结构化数据交互时，很容易就会超出上下文限制。

模型性能在超过一定上下文长度后会下降，即使其上下文窗口在技术上支持更长的长度。

长输入（Long inputs）的成本很高，即使有前缀缓存（prefix caching，一种技术，通过缓存已处理过的前缀 token 来加速后续请求的处理），你仍然需要为传输和预填充（prefill）每个 token 付费。

为了解决这个问题，许多 Agent系统采用了上下文截断（truncation）或压缩（compression）策略。但过于激进的压缩不可避免地会导致信息丢失。 **这个问题是根本性的： Agent的天性决定了它必须基于所有先前的状态来预测下一步行动——而你无法可靠地预测哪个观测（observation）在十步之后可能会变得至关重要。从逻辑上讲，任何不可逆的压缩都带有风险。**

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/55a0374b5e5a4f39c05d2b672d408652_MD5.webp]]

**这就是为什么我们将文件系统视为 Manus 中最终极的上下文：它的大小无限，本质上是持久的，并且可以由 Agent自己直接操作。模型学会了按需读写文件——将文件系统不仅用作存储，还用作结构化的、外部化的记忆。**

我们的压缩策略始终被设计为可恢复的。例如，只要保留了 URL，网页的内容就可以从上下文中丢弃；只要其路径在沙箱（sandbox，一个隔离的计算环境）中仍然可用，文档的内容就可以被省略。这使得 Manus 可以在不永久丢失信息的情况下缩减上下文长度。

在开发这个功能时，我发现自己开始想象，要让一个状态空间模型（SSM）（State Space Model，一种与 Transformer 不同的序列模型架构，以其高效处理长序列而闻名）在 Agent场景中有效工作需要什么。

**与 Transformer 不同，SSM 缺乏完全的注意力机制，并且难以处理长距离的反向依赖关系。 但如果它们能够掌握基于文件的记忆——将长期状态外部化，而不是保存在上下文中——那么它们的速度和效率可能会开启一类新的 Agent。 Agent化的 SSM（Agentic SSMs）可能成为神经图灵机（Neural Turing Machines，一种早期的尝试，旨在通过外部记忆来增强神经网络能力的模型）的真正继承者。**

**通过“复述”来操控注意力（Manipulate Attention Through Recitation）**

如果你使用过 Manus，你可能已经注意到一个有趣的现象：在处理复杂任务时，它倾向于创建一个 todo.md 文件，并随着任务的进展逐步更新它，勾掉已完成的项目。

这不仅仅是一种可爱的行为——它是一种有意操控注意力的机制。

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/0c1d27f35d76e675054f68a609f164ce_MD5.webp]]

在 Manus 中，一个典型的任务平均需要大约 50 次工具调用。这是一个很长的循环——而且由于 Manus 依赖大语言模型进行决策，它很容易偏离主题或忘记早期的目标，尤其是在长上下文或复杂任务中。

通过不断重写待办事项列表，Manus 正在将其目标“复述”到上下文的末尾。这将全局计划推入模型的近期注意力范围，避免了“迷失在中间”（lost-in-the-middle，指大模型在处理长上下文时，容易忽略中间部分信息的现象）的问题，并减少了目标偏离。实际上，它是在使用自然语言来引导自己的注意力偏向任务目标——而无需特殊的架构更改。

**保留错误的内容（Keep the Wrong Stuff In）**

Agent会犯错。这不是一个 bug——这是现实。语言模型会产生幻觉，环境会返回错误，外部工具会行为异常，意想不到的边缘情况（edge cases）也时常出现。 **在多步骤任务中，失败不是例外，而是循环的一部分** 。

然而，一种常见的冲动是隐藏这些错误：清理痕迹（trace），重试操作，或者重置模型的状态，然后把它交给神奇的“温度参数”（temperature，一个控制模型输出随机性的参数）。 **这感觉更安全、更可控。但这是有代价的：抹去失败就移除了证据。没有证据，模型就无法适应。**

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/76ced3867bf4ef602fcd644bed005550_MD5.webp]]

根据我们的经验，改进 Agent行为最有效的方法之一简单得令人意外：将走错的弯路保留在上下文中。 当模型看到一个失败的操作——以及由此产生的观测或堆栈跟踪（stack trace，一种显示程序出错时函数调用序列的报告）——它会含蓄地更新其内部信念。这会使其先验（prior，指模型在看到新证据之前的既有信念）偏离类似的操作，从而减少重复同样错误的机会。

事实上，我们相信错误恢复是真正 Agent行为最清晰的指标之一。然而，在大多数学术工作和公开基准测试中，它仍然没有得到充分的体现，这些工作和测试通常关注在理想条件下的任务成功率。

**不要被“少样本”所困（Don't Get Few-Shotted）**

少样本提示（Few-shot prompting）是改进大语言模型输出的常用技术。但在 Agent系统中，它可能会以微妙的方式适得其反。

语言模型是出色的模仿者；它们会模仿上下文中的行为模式。如果你的上下文中充满了相似的过往“行动-观测”对，模型将倾向于遵循这种模式，即使它已不再是最佳选择。

**在涉及重复性决策或行动的任务中，这可能很危险。** 例如，当使用 Manus 帮助审查一批 20 份简历时， Agent常常会陷入一种节奏——仅仅因为它在上下文中看到了这些行为，就重复类似的操作。这会导致偏离（drift）、过度泛化（overgeneralization），有时还会产生幻觉。

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/6b1e90730b7be3d67229fe362900f709_MD5.webp]]

**解决方法是增加多样性。 Manus 在行动和观测中引入了少量结构化的变体——不同的序列化模板、替代性的措辞、顺序或格式上的微小噪音。这种受控的随机性有助于打破模式，并调整模型的注意力。**

换句话说，不要让自己陷入“少样本”的窠臼。你的上下文越统一，你的 Agent就越脆弱。

**结论**

上下文工程（Context engineering）仍然是一门新兴的科学——但对于 Agent系统来说，它已经至关重要。模型可能正在变得更强、更快、更便宜，但再强的原始能力也无法取代对记忆、环境和反馈的需求。你如何塑造上下文，最终定义了你的 Agent的行为方式：它的运行速度、恢复能力以及扩展的程度。

**在 Manus，我们通过反复的重写、走过的死胡同以及对数百万用户的真实世界测试，学到了这些教训。我们在此分享的一切都不是普适的真理——但这些是为我们奏效的模式。如果它们能帮助你哪怕避免一次痛苦的迭代，那么这篇文章就完成了它的使命。**

Agent的未来将由一个个上下文构建而成。请精心设计它们。

1

**引用文章介绍**

在原文中，作者引用了一些重要的概念和技术，以下是对这些引用的简要介绍：

- **Manus** ：Manus是一个基于AI的自主 Agent平台，旨在执行复杂的多步骤任务。它能够模拟人类操作计算机，通过一系列工具使用来完成从信息收集到数据分析，再到内容创作等多种任务。Manus的核心理念是"交付成果"，而非仅仅提供想法，旨在成为人机协作的下一代范式。
- **in-context learning** ：上下文学习（In-context learning）是指大型语言模型（LLMs）在推理时，通过在输入中提供少量示例（few-shot examples）来学习新任务的能力，而无需进行模型参数的更新或重新训练。这种能力极大地提高了LLMs的灵活性和适应性，使其能够快速适应新的任务和领域。
- **BERT** ：BERT（Bidirectional Encoder Representations from Transformers）是Google在2018年发布的一种预训练语言模型。它通过双向训练Transformer编码器来学习语言的上下文表示，极大地推动了自然语言处理领域的发展，并在多项NLP任务中取得了突破性进展。BERT的出现标志着预训练模型时代的到来，但其应用仍需进行微调。
- **open information extraction** ：开放信息抽取（Open Information Extraction, Open IE）是一种从非结构化文本中自动提取结构化信息（如实体、关系和事件）的技术。与传统的需要预定义模式的信息抽取不同，Open IE旨在发现文本中所有可能的、自包含的事实，而无需人工干预或预先构建的本体。
- **GPT-3** ：GPT-3（Generative Pre-trained Transformer 3）是OpenAI在2020年发布的一款大型语言模型。它拥有1750亿个参数，是当时最大的语言模型之一。GPT-3在生成高质量文本、完成各种语言任务方面表现出色，其强大的上下文学习能力更是引发了广泛关注，被认为是AI发展史上的一个里程碑。
- **Flan-T5** ：Flan-T5是Google在T5模型基础上进行指令微调（instruction tuning）的系列模型。通过在大量不同任务的指令格式数据上进行训练，Flan-T5展现出更强的零样本（zero-shot）和少样本（few-shot）泛化能力，能够更好地理解和遵循用户指令，从而在多种NLP任务中取得优异表现。
- **KV-cache** ：KV缓存（Key-Value Cache）是Transformer模型中用于优化推理速度的一种机制。在自回归生成过程中，模型会重复计算注意力机制中的键（Key）和值（Value）矩阵。KV缓存通过存储这些计算结果，避免了在生成每个新token时重复计算，从而显著减少了推理时间和计算成本，尤其是在处理长序列时。
- **autoregressive** ：自回归（Autoregressive）是指模型在生成序列时，当前时间步的输出依赖于之前所有时间步的输出。在大型语言模型中，这意味着模型会逐个生成token，每个新生成的token都基于其前面已生成的所有token。这种特性使得模型能够生成连贯且有逻辑的文本，但也意味着对序列前部的任何修改都可能影响后续的生成和缓存效率。
- **vLLM** ：vLLM是一个用于大型语言模型推理的高吞吐量和服务框架。它通过PagedAttention等创新技术，显著提高了LLM的服务吞吐量和效率，并降低了延迟。vLLM支持多种模型和推理优化，是自托管LLM推理的流行选择。
- **prefix/prompt caching** ：前缀/提示缓存（Prefix/Prompt Caching）是vLLM等推理框架中的一项优化技术，它允许模型缓存输入提示（prompt）的KV值。当后续请求具有相同的前缀时，可以直接从缓存中加载这些KV值，从而避免重复计算，显著提高推理速度和效率，尤其适用于 Agent等场景中重复使用相同系统提示的情况。
- **MCP** ：MCP（Model Context Protocol，模型上下文协议）是Anthropic提出的一种标准化AI模型与外部工具交互的协议。它旨在为AI模型提供一种统一的方式来理解和使用工具，从而简化 Agent系统的开发和集成。MCP的流行反映了AI Agent对外部工具调用能力日益增长的需求。
- **RAG** ：检索增强生成（Retrieval-Augmented Generation, RAG）是一种结合了信息检索和文本生成的技术。它允许大型语言模型在生成回答之前，从外部知识库中检索相关信息，然后利用这些信息来生成更准确、更丰富、更少幻觉的回答。RAG在处理需要最新信息或特定领域知识的任务时尤其有效。
- **constrained decoding** ：约束解码（Constrained Decoding）是一种在大型语言模型生成文本时，强制其输出符合特定格式、语法规则或预定义模式的技术。通过在解码过程中限制模型可以选择的token，可以确保生成的文本满足特定的结构化要求，例如生成有效的JSON、代码或函数调用。
- **state machine** ：状态机（State Machine），或有限状态机（Finite-State Machine, FSM），是一种数学模型，用于描述系统在不同状态之间转换的行为。它根据当前状态和接收到的输入，决定下一个状态以及可能执行的动作。在AI Agent中，状态机可以用于管理工具的可用性，根据 Agent的当前任务和上下文来动态调整其行为。
- **Hermes format** ：Hermes格式通常指的是NousResearch开发的Hermes系列模型所使用的指令遵循和函数调用格式。这些模型经过特殊训练，能够理解并执行复杂的指令，包括结构化的函数调用。在本文中，它被用作演示不同函数调用模式的示例。
- **Neural Turing Machines** ：神经图灵机（Neural Turing Machines, NTMs）是DeepMind在2014年提出的一种神经网络架构，它结合了神经网络的学习能力和图灵机的外部记忆能力。NTMs旨在解决传统神经网络在处理长序列和需要外部记忆的任务时的局限性，为构建更通用、更强大的AI系统提供了新的思路。
- **temperature** ：在大型语言模型中，temperature是一个用于控制生成文本随机性和创造性的参数。较高的temperature值会使模型输出更具多样性和随机性，可能产生更具创造性但有时不那么连贯的文本；较低的值则会使模型输出更具确定性和保守性，更倾向于选择概率最高的token。在 Agent错误恢复中，有时会通过调整temperature来影响模型的行为。
- **Few-shot prompting** ：少样本提示（Few-shot prompting）是一种提示工程技术，通过在给模型的问题中提供少量完成任务的示例，来引导模型生成符合期望的输出。这种方法利用了大型语言模型的上下文学习能力，使其能够在没有额外训练的情况下，快速适应新的任务。

1

**参考文献**

向下滑动查看更多

\[1\] Manus Blog. Context Engineering for AI Agents: Lessons from Building Manus. https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus  

\[2\] Wikipedia. KV cache.https://en.wikipedia.org/wiki/KV\_cache  

\[3\] 百度百科. 季逸超.https://baike.baidu.com/item/%E5%AD%A3%E9%80%B8%E8%B6%85/3787689  

\[4\] Wikipedia. In-context learning.https://en.wikipedia.org/wiki/In-context\_learning  

\[5\] Wikipedia. BERT (language model).https://en.wikipedia.org/wiki/BERT\_(language\_model)  

\[6\] Wikipedia. Open information extraction.https://en.wikipedia.org/wiki/Open\_information\_extraction  

\[7\] Wikipedia. GPT-3.https://en.wikipedia.org/wiki/GPT-3  

\[8\] arXiv. Flan-T5.https://arxiv.org/abs/2210.11416  

\[9\] YouTube. Introducing Manus: The General AI Agent.https://www.youtube.com/watch?v=K27diMbCsuw  

\[10\] Gamigion. China's AI Revolution: Manus, the Game-Changer.https://www.gamigion.com/chinas-ai-revolution-manus-the-game-changer/  

\[11\] Pandayoo. China's Revolutionary AI Agent Set to Disrupt Global Industries.https://pandayoo.com/post/manus-ai-chinas-revolutionary-ai-agent-set-to-disrupt-global-industries/  

\[12\] Fortune. China's Manus follows DeepSeek in challenging U.S. AI lead.https://fortune.com/asia/2025/03/11/china-manus-follows-deepseek-ai/  

\[13\] MSN. Manus AI: China's second DeepSeek moment.https://www.msn.com/en-in/money/news/manus-ai-china-s-second-deepseek-moment/ar-AA1AAsSN  

\[14\] ChinaZ. Manus创始人季逸超：Manus产品基于阿里千问大模型开发.https://www.chinaz.com/ainews/16140.shtml  

\[15\] Facebook. Ji Yichao, co-founder of Manus, disclosed that the...https://www.facebook.com/nbdnews/videos/ji-yichao-co-founder-of-manus-disclosed-that-the-manus-product-employs-various-f/1229904471997770/  

\[16\] AInvest. Manus responds to the freeze of his X account: He claims...https://www.ainvest.com/news/manus-responds-freeze-account-claims-involved-cryptocurrency-projects-2503/  

\[17\] Hugging Face. Nous-Hermes-2-Mixtral-8x7B-SFT.https://huggingface.co/NousResearch/Nous-Hermes-2-Mixtral-8x7B-SFT  

\[18\] Yicai Global. The AI agent concept plate is up and down! Netizens left a message...https://www.yicaiglobal.com/star50news/2025\_03\_066801167325711040518  

\[19\] AI Magazine. Manus AI is Here. But What's Behind the Hype?https://aimagazine.com/articles/manus-ai-is-here-but-whats-behind-the-hype  

\[20\] Wikipedia. Autoregressive model.https://en.wikipedia.org/wiki/Autoregressive\_model  

\[21\] vLLM. vLLM GitHub.https://github.com/vllm-project/vllm  

\[22\] vLLM. Prefix/Prompt Caching.https://vllm.ai/docs/concepts/prefix\_caching.html  

\[23\] Anthropic. Model Context Protocol.https://www.anthropic.com/news/model-context-protocol  

\[24\] Wikipedia. Retrieval-augmented generation.https://en.wikipedia.org/wiki/Retrieval-augmented\_generation  

\[25\] Hugging Face. Constrained Decoding.https://huggingface.co/blog/constrained-decoding  

\[26\] Wikipedia. Finite-state machine.https://en.wikipedia.org/wiki/Finite-state\_machine  

\[27\] Wikipedia. Neural Turing machine.https://en.wikipedia.org/wiki/Neural\_Turing\_machine  

\[28\] Hugging Face. GenerationConfig.temperature.https://huggingface.co/docs/transformers/main\_classes/text\_generation#transformers.GenerationConfig.temperature  

\[29\] Prompting Guide. Few-shot prompting. https://www.promptingguide.ai/techniques/fewshot

![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/37a9cccb1d357ab05b990d6bb6a5b1a9_MD5.webp]]![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/ac9cdf86c498ac074fae5e3d2d55a6d5_MD5.webp]]

**![[_resources/Manus揭秘自己的技术：“手搓”上下文工程，推翻多个“共识”，一堆血泪教训/f42c09c9830e5d48d9c0b2d3a639d892_MD5.webp]]** 点个 **“ 爱心 ”** ，再走 吧

[阅读原文](https://mp.weixin.qq.com/s/)

继续滑动看下一个

硅星人Pro

向上滑动看下一个