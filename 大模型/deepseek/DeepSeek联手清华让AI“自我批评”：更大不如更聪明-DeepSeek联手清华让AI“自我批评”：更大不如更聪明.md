---
标题: "DeepSeek联手清华让AI“自我批评”：更大不如更聪明-DeepSeek联手清华让AI“自我批评”：更大不如更聪明"
链接: "https://mp.weixin.qq.com/s/G8YCwoo8OH-FYVujL1ukZw"
作者: "[[北茗]]"
创建时间: "2025-04-11T10:36:37+08:00"
摘要: "清华大学与DeepSeek联合提出自我原则点评调优技术，让AI在推理阶段具备自我校对能力，显著提升小模型性能。"
tags:
  - "clippings"
  - "AI"
  - "深度学习"
  - "模型优化"
  - "清华大学"
  - "推理成本"
字数: "140"
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
原创 北茗 *2025年04月09日 17:13* *广东*

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/ib9XNH4XHSaXWicESvLByCiaj38NlEnhap4RtwSgWR78Py6Mrp73JHuR9yVQlJEO7ljeibE7P4YdlDvopvfM7U8mjA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在大模型越做越大的今天，另一个问题正悄然浮现： 模型越大，推理成本越高，表现却未必更加稳定 。尤其是在处理开放性、复杂性任务时，模型 缺乏清晰判断标准 ， 反馈机制过于单一 ，这个问题正成为AI发展的瓶颈。

而最近，清华大学与DeepSeek联合提出了 一种新的解决路径： **自我原则点评调优（Self-Principled Critique Tuning，简称SPCT）** 。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/ib9XNH4XHSaXDW72wkbia1IZRZKTwMAfepdvu7tbWD6e84x68xsN4iappaHYgCLsnzGxcBmIDamKSotj9UzRAJliaw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这项技术的出发点很明确——不是再去“堆数据”“堆算力”，而是让AI在生成答案的同时，也生成判断标准，并以此标准自行评估答案是否合理。换句话说， **让模型在推理阶段拥有“自我校对”的能力** ，而不再完全依赖训练阶段的人类反馈 。

🔗 论文网址：

https://arxiv.org/abs/2504.02495

1

  

模型训练需要“裁判”

传统AI的训练逻辑其实很直给：想让它变聪明？那就堆数据、堆参数、堆算力、堆反馈，一层一层往上怼。

但现实中，很多复杂问题根本没有标准答案，比如“什么是好文案？”“哪个答案更合适？”等等。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/ib9XNH4XHSaXDW72wkbia1IZRZKTwMAfep1tqePc8kcqeIibtJD0iaDmBBf32zlibvubbayBpUBIAKicQ1qIbAVybmPw/640?wx_fmt=other&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

于是，模型开始需要 “奖励模型”（Reward Models, RMs） ，作为那位站在一边打分的“裁判”。

可现在的裁判，多半还只会在简单问题上判个输赢。一旦遇到模糊的情绪、主观的偏好、多样的场景，就会立刻懵圈。

2

  

**“拒绝学习+规则微调”，练拳又练心**

为了训练出这个“能思考的裁判”，DeepSeek设计了两个关键步骤：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/ib9XNH4XHSaXDW72wkbia1IZRZKTwMAfep29DS4H7ZGguibbqRrTXwbJboTkUJeB61ZjCvdToMatfBszOmwfDISYw/640?wx_fmt=other&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 第一阶段：拒绝式微调（Rejective Fine-Tuning）

模型要先 学习怎么写出合格的评价。如果输出的批判逻辑混乱、结论偏颇，统统 **拒绝采纳、拒绝学习** 。只有那些判断跟“真实好答案”一致的案例，才会被保留下来喂给模型。

这个阶段就像模型训练数据的“审稿人”，取其精华，弃其糟粕。

### 第二阶段：基于规则的强化学习（Rule-based RL）

接下来就是实际应用：给模型一个问题，它自己写评价规则、自己写点评，然后再根据事先设定的简单规则（比如“有没有选对答案？”）来打分。

这个过程像是在反 复教会AI： **“原则不是拿来背的，是要你用来审判世界的。”**

3

  

小小身体大大能量

这个过程最大的魅力在于三个字 —— “扩展性” 。

DeepSeek在实验中发现，哪怕只用Gemma-2-27B这样的小模型作为基础， 通过SPCT微调后生成的DeepSeek-GRM-27B模型，居然能在多项推理测试中 **吊打比它大十几倍的对手** 。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/ib9XNH4XHSaXDW72wkbia1IZRZKTwMAfepPQTicv93ZZmjotXkslsIHNlKtR0uCs0D6kz8R2VibWnfHCLmeygOWicPA/640?wx_fmt=other&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

比如：

✨ 超过 **GPT-4o** 、 **Nemotron-4-340B-Reward**

✨ 在32次采样下， **性能追平甚至超越671B级别模型**

✨ 延迟仅 **1.4秒** ，但训练成本比GPT-4o少了 **99%**

✨ 在多个主观领域上 **表现更稳、偏见更少**

一个270亿参数的模型，靠着自我批评，可以以小博大。

而且，在可解释性上也更好： 不仅能知道模型给出多少分，还能知道 **为什么打这个分** 。

4

  

走出科研，进入现实

这个技术不仅是学术 炫技，它对实际产业也充满想象力：

✅ 在 **客服系统** 中，它可以根据不同场景、客户情绪，实时调整服务语言风格。

✅ 在 **金融、医疗等高风险领域** ，它可以生成结构清晰、逻辑自洽的判断报告，并提供“依据链条”。

✅ 在 **创意内容生成** 中，它可以判断创意是否“情绪到位”“节奏自然”，甚至可以辅助剪辑、编剧。

更重要的是，它极大地 **降低了门槛** 。DeepSeek测试显示： SPCT训练所需 **人工标注减少90%，能耗减少73%** 。

5

  

更大不如更聪明

SPCT带来了一种范式的转变。

SPCT所代表的，是一种全新的思维方式： **不再靠堆资源去压倒对手，而是靠结构设计去理解复杂、适应多样。**

未来，这项技术可能成为大模型推理的标配技术，也可能成为判断内容“是否合格”的强大裁判，甚至成为企业部署AI时的必备中枢。

DeepSeek团队表示，这项技术将开放开源。

而他们的下一代R2模型，也有可能在不久后正式登场。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/ib9XNH4XHSaWFgLTSAfRpZiawibzib8HtHITc0DCiaqlzoicu75YB3HCXSHia0kPDQIwssLrHQibDgPedNKM12zYzhL9ew/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/ib9XNH4XHSaXDW72wkbia1IZRZKTwMAfepMyLn3q44TCyfVPWdeEq67OmtMaQEWFrb6ZvCCQ5MtNibGd0LxRSw8sA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过