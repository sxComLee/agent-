---
标题: "微软开源DeepSeek-R1魔改版：响应99%敏感提示，风险降50%"
链接: "https://mp.weixin.qq.com/s/gQ9LA6lWevmw32aJ8Ck0Pg"
作者: "[[微信公众平台]]"
创建时间: "2025-04-22T13:14:54+08:00"
摘要: "{{\"One-sentence summary of the article content,translated to Chinese\"}}"
tags:
  - "clippings"
  - "{{\"Analyze the article and create up to 5 tags in comma-separated format. Tags should be in Chinese unless necessary for company names"
  - "person names or abbreviations. One tag must be selected from: \"UI 设计"
  - "AI"
  - "编程"
  - "经济"
  - "效率"
  - "产品\". Other tags should be based on the article's topic"
  - "mentioned people"
  - "companies or products.\"}}"
字数: "128"
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
![cover_image](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMkG6QAml6kBrI0wXAkAd4odkr8zicDAIfpsSW4K2dbNm3h6ECZWPcOEW8dAo3teUia46vlaFZIZAl4g/0?wx_fmt=jpeg)

[AIGC开放社区](https://mp.weixin.qq.com/s/)

2025-04-18 05:43:34

精确发文时间由壹伴提供

手机阅读

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMkvxLZ6qyzuEIa1sKPtqR9XSPSMAqdckRpK7QtLAsUagMhcc06NOTN8YUUgugV8Ip3aUqmjDTOHPg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247519924&idx=1&sn=1d9ab5f154bab99bf87b8ba6539385a2&scene=21#wechat_redirect)

今天凌晨，微软在官网开源了 DeepSeek-R1 魔改版 MAI-DS-R1 ，在保留原有推理性能的基础上进行了大幅度增强。

尤其是在响应和屏蔽词方面有了显著改进： MAI-DS-R1 可以响应 99.3% 的敏感话题提示，比原版 R1 提升了 2 倍 ，这对于政治学术研究、社会问题、伦理道德研究等帮助巨大；

但在安全风险大幅度降低，比原版 R1 降低了 50% 。那些想体验一下“放飞自我”版 R1 的小伙伴们可以试试这个，非常有意思打开全新世界。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkG6QAml6kBrI0wXAkAd4odvSmyCBDQLfxKVExfxHhOo4PTpsNuOT0TvndqcDEXT1vjibErmR0o1Sw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

开源地址： https://huggingface.co/microsoft/MAI-DS-R1

Azure 地址： https://ai.azure.com/explore/models/MAI-DS-R1/version/1/registry/azureml

微软在训练 MAI-DS-R1 的过程中，从大约 350000 个被屏蔽的主题示例中，收集和筛选查询关键词，将这些关键词转化为多个问题，并翻译成不同语言；

还通过 DeepSeek R1 和内部模型为这些问题生成答案和思维链。此外，训练数据中还纳入了来自 Tulu3 SFT 数据集的 110K 个安全和违规示例，这些示例涵盖了 CoCoNot 、 WildJailbreak 和 WildGuardMix 等内容。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkG6QAml6kBrI0wXAkAd4odpZR2viauSzjmibYJhhNMMcKO8EJupBb4qI0pwpfBFGv2qzkDwYljERNg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

随后，微软对 MAI-DS-R1 进行了综合评估。在敏感话题响应方面， MAI-DS-R1 能够成功响应 99.3% 的敏感话题提示，这一表现显著优于 DeepSeek R1 和 R1-1776 。

在安全性评估方面， MAI-DS-R1 在 HarmBench 评估中表现出色，相比 DeepSeek R1 和 R1-1776 ，在减少有害内容方面降低了 50% 风险。这说明虽然 MAI-DS-R1 能响应更多的敏感话题，但还是在安全控制范围之内。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkG6QAml6kBrI0wXAkAd4odDC923W0v92nbfqxDEFJFaGXjLJcQqU0UHaBTpSF439kzXuRAibbH58w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在推理能力方面， MAI-DS-R1 保持了与 DeepSeek R1 相同的推理能力，在一般知识、推理、数学和编程基准测试中表现非常出色。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkG6QAml6kBrI0wXAkAd4odfQoeaE80cgS6mLaNrsd4JjWN3fribT7m4U6iaDGA17JXONuXQJ8GNZibg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkG6QAml6kBrI0wXAkAd4odsnBUnUwhY58gGebE3wQtiar4zsbaGMZWiaMEZUEgUwdDGTiczpNOyGZmQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在伦理和法律标准方面， MAI-DS-R1 在处理非法或不道德的请求时表现得更加谨慎，拒绝生成有害或不当的内容。

此外， MAI-DS-R1 在后训练过程中将问题翻译成多种语言，能够更好地适应不同语言环境下的需求。这使得 MAI-DS-R1 在需要多语言支持的领域，如国际组织、跨国企业、教育机构等，能够提供多语言的高质量回答。

目前，微软已经在 huggingface 开源了该模型，同时在 Azure AI Foundry 进行了发布。

本文素材来源微软，如有侵权请联系删除

END

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMmBbbpQsIn8UfHicQ8BmicGjUuv1RSwibIceJUCVuL1kOPIMso1FVwgVRwZuQ5YwyOcVS6R7xPBW6R3g/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247520041&idx=1&sn=ce2593f449fcb0dc96d470e0a08d032d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMmBbbpQsIn8UfHicQ8BmicGjUCibxydoE4wIiaicyjQoSgonImMLUU1VpdOqYuYI9V6icJDllia0wHAuE8IA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247519850&idx=1&sn=ca9eba73ef827f579159aaf52577f2de&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMm4Nwicy0kgVa95jTZ2aMh9tibSuf7UNvUbAqIMq25aHD86VedrtVB8HBM5biaYBE7rq3P5mQw5YqKuA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMnR4jHBK9FdVibzjJmiasUIgRQ4ctBMBBEbM4cVicwhNnoka8rOHSkxUQhrHXWTpQVsiaXTVFoyYfZVgg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

微软 222

开源 223

DeepSeek 14

R1 8

MAI-DS-R1 1

素材来源官方媒体/网络新闻

继续滑动看下一个

AIGC开放社区

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功