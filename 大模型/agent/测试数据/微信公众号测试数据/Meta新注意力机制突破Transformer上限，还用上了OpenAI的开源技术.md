---
标题: "Meta新注意力机制突破Transformer上限，还用上了OpenAI的开源技术"
链接: "https://mp.weixin.qq.com/s/s1a2pTlWBV1nuCzjWrvoEw"
作者: "[[关注前沿科技]]"
创建时间: "2025-07-08T14:45:14+08:00"
摘要:
tags:
  - "clippings"
字数: "115"
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

![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtACnoeCszYZw4C41YqtjK2miaLaXvSr3n9M3B0d2vEEKpZc7Jxbrk15AwGQSjxhvibic319hBOKYKxzg/0?wx_fmt=jpeg)

关注前沿科技 [量子位](https://mp.weixin.qq.com/s/) *2025年07月07日 17:35*

##### 鱼羊 发自 凹非寺量子位 | 公众号 QbitAI

Meta挖走OpenAI大批员工后，又用OpenAI的技术搞出新突破。

这是什么杀人又诛心 （doge） ？

新架构名为 **2-Simplicial Transformer** ，重点是通过修改标准注意力，让Transformer能更高效地利用训练数据，以突破当前大模型发展的数据瓶颈。

而核心方法，就是基于OpenAI提出的Triton，将标准点积注意力推广到三线性函数。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mYnh5cibshXfso9lF5e3ictx23fLDFQo8OYqkZprcDvaArEichXobBn8yw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

实验结果显示，在同等参数量和数据量下，相较于传统Transformer，新架构在数学、编程、推理等任务上均有更好的表现。

并且，2-Simplicial Transformer的缩放指数高于传统Transformer——这意味着 **随着参数增加，新架构加持下的模型性能提升更快，更适用于有限数据的场景** 。

## 三元线性注意力

传统Transformer的核心机制是点积注意力，其计算复杂度较低，但对复杂任务 （如逻辑推理、数学运算等） 表达能力有限。

针对于此，Meta的这项研究，重点放在将点积注意力从二元线性操作扩展到三元线性操作。

简单来说，就是在计算注意力时引入第三个向量，来增加模型对复杂模式的表达能力。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2m5VTJibv37uGAPVZvDzUaQXyEP2Y7ZQuiayYSo4fY1oF7icBvFVwbia0ZUw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

这第三个向量，是一个新的Key，写为 **K’** ，通过三元线性函数计算得到。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mUziamhSdAQRCzM6ktnMFbV6pOpic73ZOzQdVZGcv6Mw0ibf9TuibWj3Vjw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

K’引入了额外的维度，使得注意力机制能够捕获更加丰富的关系。

举个例子，在处理推理任务时，可以用查询向量 **Q** 表示当前问题，用键向量 **K** 表示第一个参考信息，用 **K’** 表示第二个参考信息。

其中关键的一点在于，相比于点积，三元计算更为复杂。为此，这项研究引入了 **Triton** 来实现核心运算。

Triton是一种高效的GPU编程框架，最早由OpenAI提出。它旨在让研究人员无需CUDA经验，就能用较少的代码实现接近于手写CUDA的性能。

研究人员通过Triton实现了520TFLOPS （每秒万亿次浮点运算） 的性能。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mIGD4Z4vQaG6woZ38HmIX1FKGnnMvzib2d0gABNcd4Euictth720S7TFA/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

另外，论文还引入了滑动窗口 *（Sliding Window）* 机制，通过限制注意力的计算范围，来降低计算成本，同时保持较好的性能。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mUGlSCQQyXN0bUiaTVR9dzDKEDayNSwEib6R9ZBAGbLQX1dlZfSkhibA3w/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

## 缩放指数更优

研究人员训练了一系列MoE模型来验证2-Simplicial Transformer的有效性。

模型规模从活跃参数10亿、总参数570亿，到活跃参数35亿、总参数1760亿不等。

在不同任务和模型规模上对比2-Simplicial Transformer和传统Transformer的负对数似然 *（值越小，说明模型对数据的预测越准确）* ，结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mY5bQsckQPQBRM2MN3O9jeJljmQ5DHiaiay8KfrcsibT0dzRbuibqZYhjcg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

可以看到，在小模型 （1B） 上，2-Simplicial Transformer改进有限，在GSM8k、MBPP等任务中甚至出现了较为明显的性能下降。

但在较大模型上，2-Simplicial Transformer表现显著优于传统Transformer。

论文还分析了缩放指数的变化。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mtVzNmiadwd3L8c24LSgHu2G0WW6hLAFtjYmhM1XiaJX67vpmduuOePtA/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

2-Simplicial Transformer的缩放指数α明显高于传统Transformer，说明模型性能随参数量、数据量的增加，变强速度更快。这也意味着，2-Simplicial Transformer在数据有限场景下优势会更加明显。

不过，研究人员也提到，目前，2-Simplicial Transformer的计算复杂度和延迟仍然较高，Triton虽然高效，但仍需进一步优化以适配生产环境。

## One More Thing

新注意力机制引发讨论，而背后的Triton这次也牢牢吸引住了网友们的目光。

> 用Triton实现三元线性注意力机制？这就像给了模型一把瑞士军刀。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mgCVthiaHX6p4LSxicic70nBrGYyUhVxXJM7X7iapwtbE9Lfj8UVFpJr7Lg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

> 整个Triton库就是一本关于如何不编程的教科书。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2m1gMmoRR9nnyLFSyM7akjLPa4JTDniafhBW3OBvwLKYrUVdlosevKbiag/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

合着Meta的论文，这次算是给OpenAI的技术做了宣传了 （doge） 。

不过反过来也可以说，Meta这波不仅挖走了OpenAI的人，也玩转了OpenAI的技术。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mV76CtITJian0EgFicnDjhnbVY1ib39ia0HYaibsvYPE9qQp6piau7dPGg93w/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

论文地址：  
https://arxiv.org/abs/2507.02754

  

**一键三连** **「点赞」「转发」「小心心」**

**欢迎在评论区留下你的想法！**

— **完** —

  

专属AI产品从业者的 **实名社群** ，只聊AI产品 **最落地的真问题** 扫码添加小助手，发送 **「姓名+公司+职位」** 申请入群～

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACXBaAPKiaAiavjgaxpA5e6VSqNT3LDEKTjblKVdC8bRlDFW4AuHtyibCs12QibQ86hD59XE8VadvouQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

进群后，你将直接获得：

👉 最新最专业的AI产品信息及分析 🔍

👉 不定期发放的热门产品内测码 🔥

👉 内部专属内容与专业讨论 👂

  

**🌟 点亮星标 🌟**

**科技前沿进展每日见**

  

继续滑动看下一个

量子位

向上滑动看下一个

量子位


