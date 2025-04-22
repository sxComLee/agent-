---
标题: "腾讯开源全新角色定制生图框架InstantCharacter"
链接: "https://mp.weixin.qq.com/s/mbScuNfOCL_qKCQu88T3UA"
作者: "[[弹贝斯的鱼]]"
创建时间: "2025-04-22T13:24:27+08:00"
摘要:
tags:
  - "clippings"
字数: "49"
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

![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/o5laVv7SiaeKfOcQApVky5iaiawezBJhjsYibKRKnxswtiaJJfZU1h5OxOTjGAhlQsAbvAJQNrjCx84tkGKoOZQibKyA/0?wx_fmt=jpeg)

原创 弹贝斯的鱼 [带你学AI](https://mp.weixin.qq.com/s/)

2025-04-19 23:01:11

精确发文时间由壹伴提供

手机阅读

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/o5laVv7SiaeKfOcQApVky5iaiawezBJhjsYa5TpdA2yBUBibHDxbLyTgT7H1kYS45mBZ6TqefoaTyrX0icpMZN9hhXg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

好消息！ 好消息～ 欢迎科研团队供稿 免费分享学术、项目成果

当前基于学习的主题定制方法，主要依赖于U-Net架构，存在泛化能力有限和图像质量降低的问题。与此同时，基于优化的方法需要针对特定主题进行微调，这不可避免地会削弱文本控制能力。为了解决这些挑战，腾讯提出了InstantCharacter—一个基于扩散变压器（diffusion transformer）的可扩展角色定制框架。 （链接在文章底部，可在线体验）

InstantCharacter能够实现跨多样角色外观、姿势和风格的开放域个性化，同时保持高保真度的结果。 InstantCharacter基于强大的FLUX1.0-dev模型实现，具有三大优势：一是实现了跨多种角色外观、姿势和风格的开放域个性化，同时保持高保真度；二是开发了可扩展的适配器架构，能有效处理角色特征并与扩散变压器潜在空间交互；三是通过三阶段训练方法，结合千万级数据集，优化角色一致性和文本控制。

![图片](https://mmbiz.qpic.cn/mmbiz_png/o5laVv7SiaeKfOcQApVky5iaiawezBJhjsYy4m1dZAMXD1L7cyHGQtJWyxNTsRCmJ6qEibkcVCvwMzxZZpxvVkO2QA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

01 技术原理

—  

现代扩散变压器（DiTs）相比传统的基于UNet的架构，展现了前所未有的保真度和能力，为生成和编辑任务提供了更强大的基础。然而，现有方法主要基于UNet，在角色一致性和图像保真度之间存在基本的权衡，限制了其在开放域角色中的泛化能力。此外，先前的研究尚未成功验证在大规模扩散变压器（例如120亿参数）上的角色定制，导致该领域存在显著空白。通过灵活的适配器设计和阶段性学习策略的协同作用，增强了通用角色定制能力，同时最大限度地保留了基础DiT模型的生成先验。

![Teaser Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Teaser Image

InstantCharacter 框架将可扩展的适配器与预训练的DiT模型无缝集成。适配器由多个堆叠的变压器编码器组成，逐步优化角色表示，能够有效地与DiT的潜在空间进行交互。训练过程采用三阶段渐进策略，首先进行未配对的低分辨率预训练，最终进行配对的高分辨率微调。

![Teaser Image](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Teaser Image

02 对比与演示效果

—  

InstantCharacter与最先进的基于FLUX的方法进行了定性比较：OminiControl、EasyControl、ACE+ 和 UNO；以及大型多模态模型GPT4o。为了评估，收集了一组训练数据中未出现的开放域角色图像。分析表明，现有方法存在局限性：OminiControl和EasyControl未能保持角色身份特征，ACE++仅在简单场景中保持部分特征，而在处理动作导向的提示时表现不佳。UNO过度保持一致性，导致行动和背景的可编辑性降低。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

值得注意的是，与当前的SoTA方法GPT4o取得了相当的结果，尽管GPT4o并未开源。相比之下，InstantCharacter始终表现最佳。具体而言，InstantCharacter在高保真度的同时，能够优越地保持角色细节，并精确地控制文本，即使在复杂的动作提示下也是如此。

```perl
https://github.com/Tencent/InstantCharacterhttps://arxiv.org/abs/2504.12395https://huggingface.co/spaces/InstantX/InstantCharacter
```

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

欢迎交流～，带你学习AI，了解AI

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

继续滑动看下一个

带你学AI

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功