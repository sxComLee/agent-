---
标题: "「DeepSeek-V3 技术解析」：DeepSeek-V3-Base 预训练阶段解析"
链接: "https://mp.weixin.qq.com/s/_m4kk6zWUJE8KE2t1q67uw"
作者: "[[追求卓越的]]"
创建时间: "2025-04-22T13:43:52+08:00"
摘要: "本文详细解析了DeepSeek-V3-Base预训练阶段的关键技术，包括Document Packing、Fill-in-the-Middle（FIM）和基于YaRN的长上下文窗口扩展技术，并展示了其在训练效率和长文本理解能力上的卓越表现。"
tags:
  - "clippings"
  - "AI"
  - "编程"
  - "预训练技术"
  - "DeepSeek-V3"
  - "长上下文处理"
字数: "746"
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
原创 追求卓越的

2025-04-17 09:28:36

精确发文时间由壹伴提供

手机阅读

**编者按：** 这篇技术解析详细阐述了 DeepSeek-V3-Base 的预训练阶段所采用的关键技术。

文章重点介绍了三项核心技术：Document Packing 技术有效解决了输入序列长度差异导致的资源浪费问题；Fill-in-the-Middle（FIM）采用 PSM 框架和特殊 tokens，使模型具备上下文感知的中间内容生成能力；基于 YaRN 的长上下文窗口扩展技术则通过频率插值策略解决了位置编码的扩展挑战。

随后，文章详细描述了 DeepSeek-V3-Base 的预训练过程，包括数据构建、训练策略和评估结果。

评估显示，这些技术组合使 DeepSeek-V3 每训练 1T token 仅需 180K NVIDIA H800 GPU 小时数，并在“大海捞针”测试中展现卓越的长文本理解能力，为后续 RL 阶段奠定了优质基座。

**作者 |** **Shirley Li**

**编译 | 岳** **扬**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf4oThnn4sAeljcLlk4DlDB1eQ5uJKIjQD54MSM7HXKiaXqMkzIPvB4dYc8MibhdXXHwopnknkRR5Wrw/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1 "undefined")

  

  

  

  

这是 DeepSeek 系列文章的第五篇，也是首篇聚焦 DeepSeek-V3 <sup><span>[1, 2]</span></sup> 训练流程的文章。

如下图所示，DeepSeek-V3 的训练分为多个阶段：

- **产出 DeepSeek-V3-Base 基础模型的预训练阶段**
- **基于 DeepSeek-V3-Base，通过大规模强化学习（RL）分别训练出 DeepSeek-R1-Zero（无需监督式微调冷启动）和 DeepSeek-R1（含有监督式微调）**
- **利用 DeepSeek-R1 生成推理数据，用于 DeepSeek-V3 的监督式微调（SFT），接着是未在图中展示的 RL 阶段。**

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamLsLYwrYYn8bsfcL3z58fm5tuBSLSdjov8b39ViaoMdD2Xyj5NfLzMuA/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 1. DeepSeek-V3 训练流程示意图（由原文作者绘制）

本文将重点关注产出 DeepSeek-V3-Base 的预训练阶段，阐述该阶段实现高效预训练的关键技术。后续文章将涵盖：

- 群组相对策略优化（GRPO） <sup><span>[7]</span></sup>
- DeepSeek-R1-Zero 和 DeepSeek-R1 的训练细节
- DeepSeek-V3 的后训练阶段（监督式微调与 RL 阶段）

**目录**

- **技术背景** ：解析 DeepSeek-V3 预训练阶段的相关技术，包括 Document Packing，Fill-in-Middle 和 long context extension。
- **预训练阶段** ：详解如何构建预训练数据、强调一些关键的训练策略，并回顾评估结果。
- **总结**
- **参考文献**

  

01

  

## 技术背景

本节将介绍预训练 DeepSeek-V3 过程中使用的几种技术，包括 document packing、Fill-in-the-Middle（FIM）和基于 YaRN 的长上下文窗口扩展技术。

## 1.1 Document Packing

要理解为什么需要 document packing，我们首先需要回顾一下 Transformer 模型是如何构建输入序列 tokens 的。

Transformer 模型默认情况下需要固定长度的 token 序列作为输入，然而同一 batch 的文本输入往往长度不同。为了适应这种情况，文本输入通常需要经过以下预处理步骤：

- **将所有原始文本输入分词为 token 序列**
- **将 token 序列截断或填充到预定义的固定长度（max\_seq\_len）：若原始序列过长则截断，否则用特殊 \[PAD\] token 进行填充**
- **生成掩码 IDs 使模型在训练时能忽略填充的 token**

为了更清晰地展示这个过程，以下这个示例我们将使用 GPT-2 <sup><span>[10]</span></sup> 的分词器处理两个句子：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2Tbnam9duxOQbLkB06kCth0DwRo7fUJFg5IfpEZUR4WYxloXAeBqcQ8ibSNGg/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

运行上述脚本后，会得到如下输出，其中：

- 第一句话被填充了 4 个额外的 padding token，体现在 input\_ids 和 mask\_ids 中；
- 第二句被截断，因此无需添加 padding token。

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamnB3sfrJtEkLJduuPsNhey5CoXR5pIHw2eVkXZ9TG1qhvd6l4f8kG4w/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 2. 填充操作示例（此图由作者绘制）

上述截断和填充方法虽然能让模型处理不同长度的输入，但当输入序列长度差异过大时（这在 LLM 训练中非常常见）会引发一系列问题：

- **对超长序列，截断可能导致有用信息丢失**
- **对较短的序列，填充过多 token 会造成计算资源浪费**

因此，LLM 训练通常采用 document packing 技术来处理输入序列。

更具体地说，如果给定若干长度不同的文档，我们首先将其分割为较小的块（chunk），如下图所示（用不同颜色代表不同文档）：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2Tbnamk9sVJ9lubRbL1Np5s7DAzib8ib7rU9icXicb1Zod1PNNHLjJ2V4fUS8Gng/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 3. 文档分割（图片改编自文献\[3\]）

随后，我们将不同文档的块（chunk）进行拼接，以避免对长文档进行截断和对短文档进行填充：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamNIR0DKk2l07bwicT8wCgEgC8aiblL3uSqtKRibMC06J9WYf5aE74DewzA/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 4. 传统拼接方式（图片改编自文献\[3\]）

在上例中：

- 第一个输入 （译者注：图 4 第一行） 仅包含文档 1 的 tokens
- 第二个输入 （译者注：图 4 第二行） 拼接自文档 1 和文档 2 的 tokens
- 第三个输入 （译者注：图 4 第三行） 拼接自文档 2 和文档 3 的 tokens
- 第四个输入 （译者注：图 4 第四行） 拼接自文档3、4、5 的 tokens

**这种方法虽能在一定程度上避免进行填充和截断，但由于仅按数据中的相对顺序拼接来自不同文档的块（chunks），无法控制最终输入序列的构建方式。** 例如：文档 3（紫色）被不必要地分割为两部分，尽管其实际长度小于 max\_seq\_len，可以完整放入。

为了解决这个问题，文献 \[3\] 提出了 Best-fit Packing 技术，通过两个步骤完全消除不必要的分割：

- Step 1：将每个文档分割为更小的块。
- Step 2：以一种智能的方式将这些块（chunks）分组为训练序列，确保在不进一步分割任何块（chunks）的前提下生成最少量的序列。

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamHyF3q3WTDkCcXjZvdr8OflrtJDxaDA4CytR4G1gLiaYDb3ULff5w4Qg/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 5. Best-fit packing技术（此图改编自文献\[3\]）

## 1.2 Fill-in-the-Middle（FIM）

在传统的自回归生成中，只能以从左到右的方式训练模型，即模型只能根据前面的 tokens 预测下一个 token。 **然而在实际应用中，模型常需根据上下文生成中间缺失的内容。** 尤其在代码生成场景中 —— 我们常会给定输入/输出和部分代码片段，要求模型填充中间逻辑，如下例所示：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamA4hNkfoLkYsF50ol7ELEGgolicct99Rtgp78ibrHsnicfnicO76NbmZyyA/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

为了适配此类需求，文献 \[4\] 提出了一种简单有效的方法，称为 “fill-in-the-middle”：即将文档随机切分为 prefix、middle 和 suffix 三部分，然后将 middle 部分移至末尾：

由于数据组织形式为 "Prefix-Suffix-Middle"，该方法常被称为 PSM 框架。实际实现时通过添加特殊 token 来标记各部分的边界：

其中：

- <|fim\_begin|>和<|fim\_hole|>标记 prefix 部分
- <|fim\_hole|>和<|fim\_end|>标记 suffix 部分
- <|fim\_end|>和<|eos\_token|>标记 middle 部分

以如下输入为例：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamCoPsKxb986UkJHdg6IY5K04lFV7ic0QrC0pFXmf8RaPkbK1T34flXoA/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

若需模型预测第二行代码，可将该行作为 middle 部分，并构造 FIM 输入如下：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamPBkaNWY6zB9EpgxerWnm5V2iczyW0c12qsvrCU4G3jCUbd7g7YiauIrQ/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 6. PSM 框架示意图（此图由作者绘制）

此时模型的预期输出应为：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamQup8AZPshvKYWltKWKic8EfQVdAFPiak1AE6icXzHREVnPbuibsorAWBiaw/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 1.3 基于 YaRN 的长上下文窗口扩展技术

现代 LLM 常需处理极长的提示词（如整个代码仓库），但直接使用 128K 等长上下文窗口进行预训练并不现实。多数 LLM 采用分阶段渐进式扩展策略：先在较小的上下文窗口进行预训练，再分多个阶段逐步扩展到更长的上下文窗口，从而大大降低训练成本。

例如，在 DeepSeek-V3 中，模型首先使用 4K 的上下文窗口完成预训练，然后再分两阶段扩展到 128K：

- **第一阶段：从 4K 到 32K（1000 steps）**
- **第二阶段：从 32K 到 128K（再 1000 steps）**

需特别指出的是，这种扩展不能通过简单调大上下文窗口实现，而需借助基于旋转位置编码（RoPE）改进的 YaRN（Yet another RoPE extensioN）技术对位置编码进行修改。

关于 RoPE 的详细介绍，请参阅我们之前的文章 [《「DeepSeek-V3 技术解析」：多头潜在注意力机制（MLA）》](https://mp.weixin.qq.com/s?__biz=MzkzMTI3MTg5MQ==&mid=2247487383&idx=1&sn=8736660165bfb2f3e4bc945fbe08e77b&scene=21#wechat_redirect) 。

RoPE 是一种相对位置编码方法，其核心思想是通过使用复杂的旋转嵌入修改 Query 和 Key，使得二者的内积 依赖于它们的 相对位置：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamqdI8wwVOiaPunaNxyAJkqphuOgCWvtdN1U7j4dpDqiaLtkzpiczPGCiauA/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然而，由于余弦函数和正弦函数是周期性的，(pos\_i, pos\_j) 之间的内积可能看起来与 (pos\_i, pos\_k) 之间的内积相似，因此在固定 θ 的情况下，仅使用 1K tokens（即位置索引 1~1000） 进行预训练的模型在测试时可能会混淆，因为测试时遇到的位置索引（如 5K 或 10K）可能远远超出了预训练时的上下文窗口。

下图展示了这种现象： **当 32K 上下文窗口的预训练模型在超出该窗口的位置测试时，困惑度（Perplexity）急剧上升** ：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamyAlZUhXd7JtcA0VSXe5Ct1okhUP8NK5x4SdzbWTNnZk9PRsPqUIaFg/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 7. 困惑度与上下文窗口的关系（此图由作者绘制）

那么，YaRN 是如何应对这一挑战的呢？

**既然外推法（extrapolate）效果欠佳，YaRN 转而采用插值频率（interpolate the frequency）的策略。**

假设我们有一个在 4 个 token 长度的输入上训练的模型，希望将其扩展到 8 个 token，且基础频率 θ=0.5。

对于原始 RoPE，直接使用 cos(θ×pos) 和 sin(θ×pos) 对 Query 和 Key 进行旋转即可。

而对于 YaRN：

- 首先，计算扩展后的上下文长度与原始长度的比值作为缩放因子，本例中为 2。
- 然后，生成新频率 θ' = θ / 2 = 0.25。
- 再使用新频率对 Query 和 Key 进行旋转，即 cos(θ'×pos) 和 sin(θ'×pos)。

下图对比了 RoPE 与 YaRN 的 cos 和 sin 值：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnambR8KHypfvApLqWCMjZibFrTOcYEUic9KYvFia1fupfqLC3fxj0nVge51A/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 8. YaRN 工作原理示意图（此图由作者绘制）

通过该图可观察到：

- 在 RoPE 中，cos 和 sin 值会随位置索引的增加而快速振荡，导致扩展到更长的上下文时出现问题。
- 而在 YaRN 中，原始的余弦和正弦函数通过频率缩放被插值到扩展后的上下文长度（如蓝色高亮区域所示），实现了更平滑的过渡，使得模型能够更有效地处理长序列。

下图展示了 DeepSeek-V3 在"大海捞针"（Needle In A Haystack，NIAH）测试中的表现，表明其在 128K 以下的上下文窗口长度中均表现出色：

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2Tbnamf1AUo4JRW7UaibYiak8b2xPzwa7xbGcpXQ54pMQlknYDqYkCXzbRr5VQ/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图 9. DeepSeek-V3 的"大海捞针"测试结果（引自文献\[2\]）

  

02

  

## 预训练阶段

本节将介绍 DeepSeek-V3-Base 的训练方法，重点解析数据构建流程，并强调预训练阶段中的一些关键策略。

## 2.1 数据构建

数据规模与质量对 LLM 训练至关重要。DeepSeek-V3 的预训练语料库通过持续优化策略构建，具体优化路径如下：

- 在 DeepSeek 67B <sup><span>[8]</span></sup> 中， **训练语料采用去重-过滤-再混合策略构建。** 首先对 Common Crawl 语料进行去重，随后通过严格的文档质量评估标准进行过滤，最后通过数据再混合阶段解决数据不平衡问题。
- 在 DeepSeek-V2 <sup><span>[9]</span></sup> 中，通过以下方式扩展训练语料：1) **增加更多中文数据及来自不同来源的高质量数据** ；2) **通过优化数据清洗流程，恢复大量此前在文献 \[8\] 的策略中被删除的数据。同时，通过改进基于质量的过滤算法提升数据质量。**
- 在 DeepSeek-V3 <sup><span>[2]</span></sup> 中， **预训练语料进一步扩充，加入更多数学与编程样本，以及除中英文之外的多语言样本。**

收集的预训练语料会通过前文提出的 Prefix-Suffix-Middle（PSM）框架结合 FIM（Fill-in-Middle）策略进行预处理，并应用 document-packing 技术。

## 2.2 训练策略

原论文 <sup><span>[2]</span></sup> 对预训练参数进行了详细描述，此处我们仅强调几个关键点：

- **长上下文窗口扩展** ：首先在 14.8T token 上以 4K 上下文窗口进行预训练，随后通过 1000 steps 扩展到 32K 上下文，最终再通过 1000 steps 扩展到 128K 上下文。
- **多词元预测** ：如我们本系列前一篇文章 [《「DeepSeek-V3 技术解析」：多词元预测技术（Multi-Token Prediction, MTP）》](https://mp.weixin.qq.com/s?__biz=MzkzMTI3MTg5MQ==&mid=2247487419&idx=1&sn=8b36ecb46317ee03815ebc246dbdd73e&scene=21#wechat_redirect) 所述，DeepSeek-V3 采用了优化版的多词元预测机制，允许模型同时解码多个词元（tokens），以加速训练中的解码过程。
- **以 FP8 精度进行训练** ：DeepSeek-V3 采用混合精度计算提升效率，对部分计算使用低精度格式（如 8-bit 浮点数），在不过度影响精度的前提下减少内存占用并加速计算。
- **学习率的调度** ：在前 2K steps 中，学习率（learning rate）从 0 线性增长至 2.2e–4，并在 10T token 的训练过程中保持恒定；随后在 4.3T token 的训练过程中按照余弦曲线下降至 2.2e-5；在最后 500B token 的训练过程中，前 333B token 保持恒定的学习率，剩余 167B token 进一步降至 7.3e-6。
- **Batch size 的调度** ：在前 469B token 的训练过程中，Batch size 从 3072 逐步提升至 15360，后续训练中保持恒定。

## 2.3 评估结果

下表对比了 DeepSeek-V3 与其他开源基座模型在不同任务上的表现。 **其中 DeepSeek-V3 在多数数据集上都取得了最佳性能，尤其是在数学与代码相关的任务中表现突出。**

需特别说明，得益于本系列文章中介绍的各项创新技术，DeepSeek-V3 的优异性能是在极高的训练效率下实现的。具体而言， **DeepSeek-V3 每训练 1T token 仅需 180K H800 GPU hours，远低于训练 72B 或 405B 稠密模型的成本。**

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7jFfWRrYia2WnuJLE2TbnamYjRl2Junb1fM8UEHYfYNthpDCylhTkqZLXOZ4IqJ4JuP3fVugeDEqg/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

文献\[2\]中的表 3

文献 \[2\] 还通过全面的消融实验验证了无辅助损失函数的负载均衡、多词元预测等关键技术。由于我们已在前文中讨论过相关内容，此处不再赘述。

  

03  

  

## 总结

本文探讨了 DeepSeek-V3 预训练策略中的关键创新，旨在提升效率、可扩展性与性能。由此产生的 DeepSeek-V3-Base 模型成为更高级推理模型（如 DeepSeek-R1-Zero 和 DeepSeek-R1）的基础，而这些模型又通过知识蒸馏反哺优化 DeepSeek-V3。

除此前讨论的架构创新 —— 多头潜在注意力（Multi-head Latent Attention）、DeepSeekMoE、无辅助损失函数的负载均衡及多词元预测（Multi-token Prediction）外，本文还引入了包括 document packing、Fill-in-the-Middle（FIM）和基于 YaRN 的长上下文窗口扩展在内的多项技术。

这些技术共同推动了大语言模型效率与可扩展性边界的突破，为高性能 AI 模型设立了新标杆。

## 参考文献

\[1\] DeepSeek（https://www.deepseek.com/）

\[2\] DeepSeek-V3 Technical Report（https://github.com/deepseek-ai/DeepSeek-V3/blob/main/DeepSeek\_V3.pdf）

\[3\] Fewer Truncations Improve Language Modeling（https://arxiv.org/abs/2404.10830）

\[4\] Efficient Training of Language Models to Fill in the Middle（https://arxiv.org/abs/2207.14255）

\[4\] DeepSeek-Coder: When the Large Language Model Meets Programming — The Rise of Code Intelligence（https://arxiv.org/abs/2401.14196）

\[5\] DeepSeek-Coder-V2: Breaking the Barrier of Closed-Source Models in Code Intelligence（https://arxiv.org/abs/2406.11931）

\[6\] YaRN: Efficient Context Window Extension of Large Language Models（https://arxiv.org/abs/2309.00071）

\[7\] DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models（https://arxiv.org/abs/2402.03300）

\[8\] DeepSeek LLM: Scaling Open-Source Language Models with Longtermism（https://arxiv.org/pdf/2401.02954）

\[9\] DeepSeek-V2: A Strong, Economical, and Efficient Mixture-of-Experts Language Model（https://arxiv.org/abs/2405.04434）

\[10\] Language Models are Unsupervised Multitask Learners（https://cdn.openai.com/better-language-models/language\_models\_are\_unsupervised\_multitask\_learners.pdf）

*Thanks for reading!*  

*Hope you have enjoyed and learned new things from this blog!*

***About the author***

***Shirley Li***

I am a Machine Learning Engineer working on building multi-modality models to solve real-world problems.

**END**

**本期互动内容 🍻**

❓ **当前位置编码方案（RoPE/YaRN）已支持 128K 上下文，但人类书籍平均长度约 200K tokens。要实现真正无损的长文档理解，您认为下一代位置编码需要突破哪些理论瓶颈？**

  

**原文链接：**  

https://medium.com/data-science-collective/deepseek-explained-5-deepseek-v3-base-86c078ed5504

![微信图片_20240716175748.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E "undefined")

**AI及大模型技术分享交流群**

**干货分享，联系小助手入群**

  

继续滑动看下一个

Baihai IDP

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功