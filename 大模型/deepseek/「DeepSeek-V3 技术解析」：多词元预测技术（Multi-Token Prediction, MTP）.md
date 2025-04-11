---
标题: "「DeepSeek-V3 技术解析」：多词元预测技术（Multi-Token Prediction, MTP）"
链接: "https://mp.weixin.qq.com/s/si6YAHoxrDDx42fZpmJu6g"
作者: "[[追求卓越的]]"
创建时间: "2025-04-11T11:29:58+08:00"
摘要: "本文深入解析DeepSeek-V3模型的多词元预测技术（MTP），探讨其如何通过模块间表征依赖关系提升文本生成效率与质量，并与推测解码结合实现1.8倍推理加速。"
tags:
  - "clippings"
  - "AI"
  - "多词元预测技术"
  - "DeepSeek-V3"
  - "大语言模型"
  - "效率"
字数: "632"
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
原创 追求卓越的 *2025年04月08日 09:25* *湖南*

**编者按：** 在实时人工智能应用场景中，大语言模型的推理速度直接影响用户体验。传统模型通过逐词元预测（next-token prediction）生成文本，每次仅预测一个词元的方式导致长文本生成耗时较长。这种延迟在对话系统和内容创作平台中尤为明显，已成为阻碍用户沉浸体验的主要障碍。

本文深入探讨了 DeepSeek-V3 模型的多词元预测技术（Multi-Token Prediction, MTP）。与现有方法（如独立预测多个词元导致逻辑断裂）不同，DeepSeek 创新性地通过模块间的表征依赖关系，在训练时保持词元预测的完整因果链，从而生成高质量连贯文本。此外，该技术可与推测解码（speculative decoding）结合，在推理时，MTP module 并行生成草稿词元，main model 通过单次前向传播验证并修正，凭借 85%-90% 的高接受率实现 1.8 倍的推理加速。

**作者 |** **Shirley Li**

**编译 | 岳** **扬**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7FIXGz6P7FncUL1f3RBYKI9ibaMZCs0a1sia6xmwsG479fd5YNicATUibtI1GfntiastFbMu4pABVXqHQ/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1 "undefined")

  

  

  

  

这是 DeepSeek-V3 系列的第四篇文章，将解释 DeepSeek <sup><span>[1,2]</span></sup> 模型的最后一个重要架构创新：多词元预测（multi-token prediction）。

在前几篇文章中，我们阐述了 DeepSeek 如何通过巧妙的设计，在矛盾的优化目标之间找到折中方案，既不过度偏向某一目标，又能保持整体效果：

- [多头潜在注意力（Multi-head Latent Attention）在解码过程中优化内存效率，同时保持模型性能。](https://mp.weixin.qq.com/s?__biz=MzkzMTI3MTg5MQ==&mid=2247487383&idx=1&sn=8736660165bfb2f3e4bc945fbe08e77b&scene=21#wechat_redirect)
- [DeepSeekMoE 在混合专家模型（MoE）架构中平衡 knowledge sharing 与 expert specialization。](https://mp.weixin.qq.com/s?__biz=MzkzMTI3MTg5MQ==&mid=2247487388&idx=1&sn=2f5dd3553fa9bdf6e58e7da5911a1fbe&scene=21#wechat_redirect)
- [无辅助损失函数的负载均衡（Auxiliary-Loss-Free Load Balancing）在不影响主要训练目标的情况下实现有效的负载均衡。](https://mp.weixin.qq.com/s?__biz=MzkzMTI3MTg5MQ==&mid=2247487408&idx=1&sn=12d9064487b7af001edd3919abf2f292&scene=21#wechat_redirect)

本文将探讨 DeepSeek 如何在文本生成的效率与质量之间实现又一重要平衡。

本文目录：

- **技术背景** ：介绍大语言模型解码过程的基本原理，特别是 next-token prediction 机制及其局限性。同时回顾多词元预测（MTP）的相关研究，探讨其设计选择与优劣。
- **DeepSeek 的多词元预测** ：解释其工作原理，并重点讨论与先前研究不同的设计选择。此外还将介绍如何将 DeepSeek 的 MTP 策略与推测解码（speculative decoding）结合以加快推理速度。
- **评估** ：分析 MTP 对训练性能和推理效率的双重影响。
- **总结**
- **参考文献**

  

01

  

## 技术背景

要理解 DeepSeek 的多词元预测（multi-token prediction），我们首先需要仔细了解大语言模型（LLMs）如何生成文本。

## 1.1 Next-Token Prediction

**LLMs 通常通过自回归（autoregressive）的方式生成文本，即在给定历史 tokens 序列的前提下，通过逐 token 预测下一个最可能的 token 来生成文本。**

例如，给定文本 "The cat sat"，其分词结果可能为：

```
"The cat sat"->["The","cat","sat"]
```

每个 token 都有一个与它在词汇表中的索引相对应的 token id，并将通过该索引在嵌入矩阵（embedding matrix）中查询对应的稠密向量，并与位置编码（positional encoding）相加后输入模型：

```
Emb("The") = vector("The") + PositionalEncoding(1)
Emb("cat") = vector("cat") + PositionalEncoding(2)
Emb("sat") = vector("sat") + PositionalEncoding(3)
```

经过 LLM 的 Transformer 层处理后，最后一层通过线性投影将嵌入向量映射回词汇表空间，再通过 Softmax 输出词汇的概率分布。以上述简单示例为例，最高概率的 token 可能是：

```
P("on") = 0.7
P("under") = 0.3
...
```

因此，模型会选择最有可能的 token "on"，生成结果变为：

```
"The cat sat on"
```

**这一逐词元生成的过程将持续至达到最大生成长度或遇到终止符（EOS）为止。** 由于每一步仅生成单个 token，该机制被称为 next-token prediction，其定义为：

其中：

- t 表示第 t 个时间步
- x\_{t:1} 表示历史词元序列 x\_1 至 x\_t3
- x\_{t+1} 是未来的下一个词元（token）

从建模的角度看，Next-token prediction 似乎很自然，但存在以下局限：

- 无法并行化：需按序列逐词元处理，无法并行计算。
- 计算效率低：每次预测都需要一次完整的前向传播，导致训练和推理效率低下（尤其是实时长文本生成场景）。

为解决这些问题，多词元预测（multi-token prediction） 应运而生。

## 1.2 先前的多词元预测方法

在文献\[3\]中，作者将 next-token prediction 扩展为一种多词元预测机制：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

其中，给定相同的输入序列，模型将通过单次前向传播生成从 x\_{t+1} 到 x\_{t+n} 的 n 个 tokens。

请注意，这并不意味着在单个 Softmax 输出的概率分布上同时选择 n 个 tokens，因为 Softmax 不支持从单个概率分布中同时选择多个 tokens。

这是因为 Softmax 是为分类分布（categorical distributions）设计的，其建模的是多个互斥选项中单个离散事件的概率。因此，Softmax 在每个时间步（time step）只能生成单个 token，要预测多个 tokens 需要多个 Softmax 层，每层专门负责生成独立的 token。

因此，上述多词元预测的损失函数将首先被分解为多个单词元（token）预测操作头，然后每个单词元（token）预测头会运行独立的 Softmax 来选择对应词元。

更具体地说，我们引入了中间潜在表征（intermediate latent representation）z\_{t:1} 来表示大语言模型中的隐藏表征，如下列公式所示：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

作者根据文献 \[3\] 中的公式创建的图像

这种方式将输入序列 x\_{t:1} 与输出序列解耦，使模型能够通过单次前向传播将 x\_{t:1} 编码为 z\_{t:1}，并在后续所有生成过程中重复使用该表征。

随后，x\_{t+n:t+1} 与 z\_{t:1} 之间的条件概率会被进一步分解为 n 个独立的单步条件概率（如用蓝色标注的内容所示），每个条件概率代表一个单词元生成步骤：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

作者根据文献 \[3\] 中的公式创建的图像

在文献\[3\]中，这一过程通过以下公式实现：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

作者根据文献 \[3\] 中的公式创建的图像

其架构如下图所示，包含：

- **一个共享的 Transformer f\_s** ，通过单次前向传播将 x\_{t:1} 编码为 z\_{t:1}。
- **n 个独立的输出头 f\_{h\_i}** （以 Transformer 层实现），将中间隐藏表征 z\_{t:1} 映射到 x\_{t+i}。特别是，第一个头（当 i==1 时）的输出可视为下一词元预测头。
- **一个共享的解嵌入矩阵 f\_u** ，用于将 x 映射到词表大小的维度，最后通过应用 Softmax 获得各个词元的概率。

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

图 1. 文献\[3\]中的多词元预测架构。该图来自文献\[3\]

现在，让我们来深入了解这一架构，特别是共享组件与独立组件背后的设计考量：

- 共享的 f\_s：如前文所述，这种方式只需单次前向传播即可获得 z\_{t:1}，从而生成 n 个词元， **相比传统的 next-token prediction 具有更高的计算效率。**
- 共享的解嵌入矩阵 f\_u：由于解嵌入矩阵非常大，维度数量为 d×V（d 为隐藏层维度，V 为词表大小，通常为 5 万~ 20 万）， **共享参数能大大减少参数量且对性能的影响有限。**
- 独立的输出头： **这是这一架构中唯一独立的部分。** 如前文所述，每个词元都需要一个独立 Softmax，因此无法共享所有组件。

使用独立的输出头能够使得 n 个词元的生成过程相互解耦。一方面，这种设计支持并行生成词元，可以提升训练效率；但另一方面，独立生成词元可能导致输出缺乏连贯性或一致性。此外，模型可能会出现模式奔溃（mode collapse），倾向于生成通用的、高频的词汇，而非细致的响应，从而降低输出的多样性和丰富性。

在下一节，我们将看到 DeepSeek 的多词元预测技术如何解决这个问题。

  

02

  

## DeepSeek 的多词元预测技术

**如前文所述，文献\[3\]中的多词元预测方法会独立生成 n 个词元，可能导致输出不连贯甚至模式崩溃（mode collapse）。** 为了解决这个问题，DeepSeek 通过保持每个词元预测的完整因果链来实现多词元预测，如下图所示：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

图 2. DeepSeek 中的多词元预测架构。图片来自文献\[2\]

上图展示了三个生成步骤，分别称为 main model、MTP module 1 和 MTP module 2。

main model 的架构与我们在文献\[3\]中看到的架构高度相似，同样包含三个核心组件：

- **一个共享的嵌入层（embedding layer）**
- **一个独立的 Transformer block**
- **一个共享的线性输出头（shared linear output head）** ，其功能类似于文献\[3\]中的解嵌入矩阵（unembedding matrix）

但从 MTP module 1 开始，差异就变得明显了：因为 Transformer block 的输入依赖于前一个词元的表征。

更具体地说，第 i 个 token 的 Transformer 输入如下：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

其中：

- k 是 MTP module 的索引。
- h^{k-1}\_{i} 是来自上一步的表征。
- Emb(t\_{i+k}) 是第 (i+k) 个词元（token）的嵌入层输出。
- RMSNorm 算子对两个表征向量进行归一化处理，使它们的数值更具可比性，并允许将它们拼接起来。随后通过拼接算子\[·;·\]生成 2d 维度的表征。
- 最终通过线性投影矩阵 M\_k 将维度从 2d 映射回 d，供 Transformer block 使用。

在 MTP modules 间引入依赖关系破坏了文献\[3\]中的并行性，但也使文本生成更加连贯，更适合对话和推理等场景。

DeepSeek 模型中，多词元预测主要用于训练阶段，每个 MTP module 均应用交叉熵损失函数，如下图所示：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

其中 t\_{i} 表示第 i 个位置的真实词元（ground-truth token），而 p^{k}\_{i}\[t\_i\] 则是第 k 个 MTP module 对 t\_i 的预测概率。

然后，所有 MTP module 的损失值会被整合为一个额外附加的训练目标：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

在推理阶段，所有 MTP module 都会被丢弃，仅保留 main model 进行词元预测。但文献\[2\]的作者也提到他们的 MTP 技术可与推测解码（speculative decoding）结合，以加快推理速度。

那么，这是如何实现的呢？

## 2.1 推测解码（speculative decoding）

推测解码（speculative decoding）是一种通过先打草稿后验证的范式加速自回归生成过程的技术 <sup><span>[4, 5]</span></sup> ： **首先并行生成多个候选词元，然后用原始自回归（AR）模型验证或修正这些词元** ，如下图所示：

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

图 3. 推测解码技术的先打草稿后验证流程。图片来自文献\[5\]

具体而言，推测解码包含两个阶段：

- **并行生成草稿（Parallel drafting）** ：不再使用原始 AR 模型逐词元（token）生成，而是通过推测解码并行生成候选词元。
- **批量进行验证（Batch verification）** ：通过单次前向传播，用原始 AR 模型验证草稿词元，并根据需要接受或修正它们。

由于草稿词元可能被接受，也可能被拒绝，因此实际的加速效果主要取决于接受率：

- 理想情况下，所有草稿词元（K 个）均被接受，模型可通过单次前向传播前进 K 步，实现 K 倍加速。
- 如果部分草稿词元被拒绝，生成过程仍然可以从部分加速效果中收益，因为仅需重新生成被拒绝的词元，而非整个序列。

换言之，更高的接受率可带来更明显的加速效果。下一节我们将深入探讨 DeepSeek 如何在推理中应用此技术。

  

03  

  

## Evaluation

在文献\[2\]中，作者评估了其多词元预测策略对训练和推理阶段的影响。

## 3.1 训练性能影响

为验证多词元预测策略是否能提升模型训练效果，文献\[2\]的作者在两个不同规模的 MoE 模型上进行了实验：

- 15.7B 的较小规模模型（激活参数 2.4B，下表中用蓝色标注）
- 228.7B 的较大规模模型（激活参数 20.9B，下表中用绿色标注）

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

图 4. 多词元预测对训练性能的影响。作者基于文献\[2\]中的表格绘制

在这两种模型上，作者对比了原始模型与添加 MTP module 的变体模型的性能（其余配置保持一致）。在本实验中，MTP module 在推理时被完全丢弃，因此推理时间无差异。

**根据上表结果，两种规模的模型加入 MTP module 后，在多项任务上均表现更优，证明了该策略的有效性。**

## 3.2 推理效率影响

如前文所述，MTP module 在推理阶段可与推测解码（speculative decoding）结合，以加速推理过程，而非在推理时完全丢弃它们。

在文献 \[2\] 中，作者尝试通过 MTP 技术预测未来的 2 个词元（token），并将其与推测解码相结合，结果发现第二个词元预测的接受率约为 85%~90%，这表明其 MTP 策略的生成质量稳定可靠。

更重要的是， **凭借高接受率，MTP 与推测解码相结合可实现每秒生成词元数（TPS）1.8 倍的推理加速。**

  

04  

  

## Summary

本文探讨了 DeepSeek 的另一项关键架构创新——多词元预测（multi-token prediction），解析其如何在文本生成中平衡生成效率与生成质量。

MTP 和以下这些架构创新共同构成了 DeepSeek 模型的基础，使其既高效又强大：

- 多头潜在注意力（Multi-head Latent Attention）在解码过程中优化内存效率，同时保持模型性能。
- DeepSeekMoE 在混合专家模型（MoE）架构中平衡 knowledge sharing 与 expert specialization。
- 无辅助损失函数的负载均衡（Auxiliary-Loss-Free Load Balancing）在不影响主要训练目标的情况下实现有效的负载均衡。

核心启示：

- **大语言模型的训练仍存在诸多未决问题，新技术的引入常伴随非预期的副作用**
- **要应对这些挑战，既需要对现象进行透彻分析，也需要对内部机制有深刻理解。**
- **解决方案不必复杂 —— 简单的策略有时能带来惊人的效果**

至此，我们已完成对 DeepSeek 架构创新的探讨。下一篇文章将深入其训练策略，解析预训练、微调与对齐阶段的关键设计选择。

## 参考文献

\[1\] DeepSeek（https://www.deepseek.com/）

\[2\] DeepSeek-V3 Technical Report（https://github.com/deepseek-ai/DeepSeek-V3/blob/main/DeepSeek\_V3.pdf）

\[3\] Better & Faster Large Language Models via Multi-token Prediction（https://arxiv.org/abs/2404.19737）

\[4\] Fast Inference from Transformers via Speculative Decoding（https://arxiv.org/pdf/2211.17192）

\[5\] Speculative Decoding: Exploiting Speculative Execution for Accelerating Seq2seq Generation（https://arxiv.org/pdf/2203.16487）

*Thanks for reading!*  

*Hope you have enjoyed and learned new things from this blog!*

***About the author***

***Shirley Li***

I am a Machine Learning Engineer working on building multi-modality models to solve real-world problems.

**END**

**本期互动内容 🍻**

❓ **你在使用 AI 工具时，最在意的是响应速度还是输出质量？为什么？**

  

**原文链接：**  

https://medium.com/data-science-collective/deepseek-explained-4-multi-token-prediction-33f11fe2b868

![微信图片_20240716175748.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E "undefined")

**AI及大模型技术分享交流群**

**干货分享，联系小助手入群**

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

如果觉得有帮助，就点点 **『在看』** 哦！

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过