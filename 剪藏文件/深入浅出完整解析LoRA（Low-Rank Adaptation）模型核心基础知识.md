---
标题: "深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识"
链接: "https://zhuanlan.zhihu.com/p/639229126?share_code=JtJfOf8qWbBe&utm_psn=1998742441361183222&utm_source=wechat_session&utm_medium=social&s_r=0"
作者: "[[Rocky Ding​北京科技大学 工学硕士]]"
创建时间: 2026-01-28T22:43:19+08:00
摘要:
tags:
  - "clippings"
字数: 226
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

![[_resources/深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识/225ab83d437e1bfc9f24ed0c98be47ac_MD5.jpg]]

深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识

目录

收起

1\. LoRA系列模型资源

2\. 零基础深入浅出理解LoRA模型核心基础知识（全网最详细讲解）

2.1 零基础深入浅出理解LoRA模型的核心原理

2.2 零基础深入浅出理解LoRA模型的优势

2.3 零基础深入浅出理解LoRA模型的三大特性（易用性、泛化性、还原度）

2.4 零基础深入浅出理解LoRA模型的高阶用法

2.5 零基础深入浅出理解DreamBooth LoRA模型

2.6 零基础深入浅出理解LoRA模型的融合和提取方法（Merge Block Weighted，MBW）

3\. 从0到1搭建使用LoRA模型进行AI绘画（全网最详细讲解）

3.1 零基础使用diffusers搭建LoRA推理流程

3.2 零基础使用Stable Diffusion WebUI搭建LoRA推理流程

3.3 零基础使用ComfyUI搭建LoRA推理流程

3.4 零基础使用SD.Next搭建LoRA推理流程

3.5 LoRA生成图像示例

4\. 从0到1上手训练自己的LoRA模型用于AI绘画（全网最详细讲解）

4.1 LoRA训练数据集制作

4.2 使用kohya-trainer框架训练LoRA模型

4.3 kohya-trainer框架中LoRA训练参数全解析（全网最详细）

4.4 使用diffusers框架训练LoRA模型

4.5 LoRA模型的关键训练超参数详解（全网最详细）

4.6 LoRA模型的训练技巧与经验分享

4.7 LoRA模型训练结果测试评估

5\. 主流LoRA变体模型深入浅出完整讲解

5.1 LoCon核心基础知识深入浅出完整讲解

5.2 LoHa核心基础知识深入浅出完整讲解

5.3 残差/差异化LoRA模型深入浅出完整讲解

5.4 LCM\_LORA模型深入浅出完整解析

5.5 Textual Inversion（embeddings模型）技术深入浅出完整讲解

6\. 深入浅出完整讲解MoE-LoRA（Mixture of Experts with LoRA）的核心基础知识

6.1 深入浅出完整讲解MoE框架下LoRA技术的核心原理

6.2 MoE思想与LoRA模型相结合

6.3 MoE-LoRA架构中专家选择(Expert-Choice)与token选择(Token-Choice)的核心基础知识讲解

6.4 深入浅出讲解Token-Choice (TC) 和Expert-Choice (EC) 的具体代码实现

7\. 优质LoRA模型推荐（持续更新）

7.1 人物LoRA模型推荐

7.2 风格LoRA模型推荐

7.3 Low-Level功能LoRA模型推荐（美颜、美肤、祛痘、磨皮、精修、画质增强、光影调整等）

8\. 推荐阅读

8.1 深入浅出完整解析扩散模型DDPM、DDIM、Classifier/Classifier-Free Guidance、Rectified Flow核心基础知识

8.2 深入浅出完整解析AI Agent（AI智能体）的核心基础知识

8.3 深入浅出完整解析FLUX.1 Kontext和FLUX.1 Krea核心基础知识

8.4 深入浅出完整解析DeepSeek系列核心基础知识

8.5 深入浅出完整解析Stable Diffusion 3（SD 3）和FLUX.1系列核心基础知识

8.6 深入浅出完整解析Stable Diffusion XL（SDXL）核心基础知识

8.7 深入浅出完整解析Stable Diffusion（SD）核心基础知识

8.8 深入浅出完整解析Stable Diffusion中U-Net的前世今生与核心知识

8.9 深入浅出完整解析ControlNet核心基础知识

8.10 深入浅出完整解析Sora等AI视频大模型核心基础知识

8.11 深入浅出完整解析AIGC时代Transformer核心基础知识

8.12 深入浅出完整解析主流AI绘画框架核心基础知识

8.13 手把手教你成为AIGC算法工程师，斩获AIGC算法offer！

8.14 AIGC产业的深度思考与分析

8.15 算法工程师的独孤九剑秘籍

8.16 深入浅出完整解析AIGC时代中GAN系列模型的前世今生与核心知识

![[_resources/深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识/43ea073fc2c79a10bd7efc382ce96c51_MD5.jpg]]

SD模型+LoRA模型组合生成图像示例

1 人已送礼物

[所属专栏 · 2025-11-10 19:35 更新](https://zhuanlan.zhihu.com/c_1646154470676168704)

[![[_resources/深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识/acb28f15a59666edc9165465700b4066_MD5.jpg]]](https://zhuanlan.zhihu.com/c_1646154470676168704)

[Rocky Ding的AI算法兵器谱](https://zhuanlan.zhihu.com/c_1646154470676168704)

[

Rocky Ding

北京科技大学 工学硕士

16 篇内容 · 8605 赞同

](https://zhuanlan.zhihu.com/c_1646154470676168704)

[

最热内容 ·

深入浅出完整解析Stable Diffusion（SD）核心基础知识

](https://zhuanlan.zhihu.com/c_1646154470676168704)

编辑于 2026-01-25 12:00・浙江[AI绘画](https://www.zhihu.com/topic/25477934)[Stable Diffusion](https://www.zhihu.com/topic/26072993)[AIGC](https://www.zhihu.com/topic/26215901)

[![[_resources/深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识/4eb729fcda6d9cc19140cfdc6ee7546c_MD5.webp]]](https://www.qianwen.com/?ch=webtongyi@gp_zhztzhihugpwebty01_normal2_10&spu=biz%3D0%26ci%3D3649135%26si%3D7557c4b0-7fee-49ef-9a69-33dd3f466780%26ts%3D1769413977%26zid%3D1629)

[官方AI助手，写作有温度更有逻辑](https://www.qianwen.com/?ch=webtongyi@gp_zhztzhihugpwebty01_normal2_10&spu=biz%3D0%26ci%3D3649135%26si%3D7557c4b0-7fee-49ef-9a69-33dd3f466780%26ts%3D1769413977%26zid%3D1629)

[

作为官方AI助手，千问不仅会写，更懂写作逻辑。自动分段、加小标题、埋关键词，产出即用型内容，省去反复修改。 查看详情

千问 的广告

](https://www.qianwen.com/?ch=webtongyi@gp_zhztzhihugpwebty01_normal2_10&spu=biz%3D0%26ci%3D3649135%26si%3D7557c4b0-7fee-49ef-9a69-33dd3f466780%26ts%3D1769413977%26zid%3D1629)

![[_resources/深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识/26725aa9602db156eaafd2cb68a4a816_MD5.jpg]]

理性发言，友善互动

101 条评论

默认

最新

[Rocky Ding](https://www.zhihu.com/people/ca54c41c7dad1e7525b48f4a1312254a)

作者

关于LoRA系列模型的问题，疑惑，见解或者建议，都可以在评论区留言，Rocky会持续优化本文，希望能给大家带来帮助。也希望我们一起参与到AIGC的生态共建中去，让AIGC的生态持续繁荣！

![[_resources/深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识/08d6fefe4a035a290e37d3274b3a4f08_MD5.gif]]

2023-12-27 · 浙江 · 作者置顶

[编程Cookbook](https://www.zhihu.com/people/086a6d94009c1e533ee78dd2de9f7361)

dreambooth\_lora 技术 是同时使用lora和dreambooth两种微调手段微调sd模型吗？数据集和lora微调时候数据集有没有差异？ 以及 两种方法同时微调的原理哪里有参考资料

2024-09-14 · 山西

[Rocky Ding](https://www.zhihu.com/people/ca54c41c7dad1e7525b48f4a1312254a)

作者

有一些差异的，dreambooth技术需要设置一些正则集

2024-09-14 · 浙江

[cenyl1996](https://www.zhihu.com/people/e560914a8344df46ed9ae55751747e54)

diffusers跑那个宝可梦数据集训练lora， 一定要把.txt删掉，只留下.png和metadata.jsonl，不然会报错的ValueError: --image\_column' value 'image' needs to be one of: text

2025-02-05 · 广东

[Rocky Ding](https://www.zhihu.com/people/ca54c41c7dad1e7525b48f4a1312254a)

作者

2025-02-05 · 浙江

点击查看全部评论

![[_resources/深入浅出完整解析LoRA（Low-Rank Adaptation）模型核心基础知识/26725aa9602db156eaafd2cb68a4a816_MD5.jpg]]

理性发言，友善互动