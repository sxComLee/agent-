---
标题: "OpenAI o3&o4mini 短评：Model is Agent？"
链接: "https://mp.weixin.qq.com/s/MIwh2UZVbY3jhN3QGfgMIw"
作者: "[[张海庚]]"
创建时间: "2025-04-22T13:17:27+08:00"
摘要:
tags:
  - "clippings"
  - "agent"
  - "openAi"
  - "model"
字数: "158"
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

![cover_image](https://mmbiz.qpic.cn/sz_mmbiz_jpg/Vx299gEHPV7KBLNYDH8Uf4ciaOEemE86qoH1pghibbJGsVyUYBuicFz41XEk8C9dicZNB7gbNnXQHibdFRr9rzFZWNg/0?wx_fmt=jpeg)

原创 张海庚 [张无常](https://mp.weixin.qq.com/s/)

2025-04-17 17:32:24

精确发文时间由壹伴提供

手机阅读

记录下今天看发布会&官方Blog、第一时间体验的感受。欢迎评论、指正。

总结：

1、 Model is Agent，o3可能要进一步革 Agent 的命了

2、 o3的工具调用能力又好又快，可能是极速版的 Deep Research

3、 作为第一个多模态思维链模型，o3多模态结合工具的推理能力极强

  

**一、Model is Agent**

**o3** **思维链** **支持调用工具了，** 而且推测是内置工具，如web search、file search、code interpreter。  

根据OpenAI的官方说明去推测， 应该是在端到端训练时，通过强化学习把调用工具的能力内置到了Reasoning思维链里面 ，让模型把工具调用作为推理的一部分，因此不仅知道如何调用工具，也知道调用时机。

比如对于最常用的搜索，o3在搜索时机和结合对搜索结果的反思并进行多轮搜索等方面有更好的效果。

可以 类比一下普通 LLM + Search 搜索和 Deep Research ——有意思的是，Deep Research是基于o3强化微调的，而正式版o3可能把这种微调能力训到模型里了。

可能的影响：

1、效果：相比 **Agent「让模型使用外置工具」** ，思维链内置工具的效果应该会更好，OpenAI说是通过强化学习让模型“不但知道如何如何使用工具，更知道什么时候使用”

2、速度：思维链内置工具的速度明显更快了（下面有case）

3、也许意味着： **现在大量 Agent 做的教模型调用web search、反思并进行多轮搜索、调用code interpreter……不管是workflow还是Agentic的方法，在** **思维链** **内置** **方式面前，可能都要没用了** ？（因为效果更差、速度更慢）

——继4o冲击生图Workflow后，苦涩的教训（The Bitter Lesson）又要冲击Agent了吗？值得关注。

外置工具 vs 内置工具的UI表现：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/Vx299gEHPV7KBLNYDH8Uf4ciaOEemE86qribf3dxzBPtzDGLB0WnqGqrIrgJngsbnKD0icvcuc5nUexoxUpfLIOvA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)  

OpenAI API中提供web search、code interpreter等内置工具

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

**二、 o3的工具调用能力又好又快，可能是极速版的 Deep Research**

o3的指令遵循能力在o1的基础上进一步提升，值得一提的是BrowseComp，这是OpenAI最近推出的一个Benchmark，衡量Agent通过浏览互联网查找难以找到的信息的能力。

在这个评测集下， **o3 with** **python** **\+ browsing 准确率基本持平（基于o3做了强化** **微调** **的）Deep Research** ，效果持平，而 **o3速度上会比Deep Research快非常多** ，可以说是极速版Deep Research了。

也就意味着： **你不再需要等待Deep Research漫长的思考就可以得到几乎一样好的内容** ，应该会解锁更多场景了（想想Claude Research还在打“快速响应”的差异化）

Benchmark

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

实测确实多轮搜索速度挺快的

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这个问题的结果也是ok的

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

完整回答：

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

**三、第一个** **多模态** **思维链** **模型，多模态结合工具推理能力很强**

**多模态** **可能是最能让人感受到o3能力的点，结合搜索等工具推理，感觉像人一样聪明了。强烈建议看看官网给的case，感觉解锁了很多新场景。**

OpenAI官方的解读：o3可以将图像直接融入思维链中， 不仅能看到图像，还能 **用图像进行思考** 。开启了一种 融合视觉和文字推理的新的解决问题的方式 ——非常惊艳，可以看下面的实测case。  

********你可以上传白板、教科书图表或手绘草图的照片，而模型可以对其进行解读——即使 **图像模糊、颠倒或质量不高 。** 通过使用 工具 ，模型可以在推理过程中对图片进行 **旋转** 、 **缩放** 或 **变换** 等操作。********

下面放一些我测试的case：

能自己调用工具截图：

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

能放大图片

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

结合多模态理解、搜索、模型知识来综合推理

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

综合各种方法调整图片，调整对比度、放大，甚至用上了 锐化滤镜 ……太强了。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)  

以上，o3&o4mini 模型短评，第一天浅浅研究体验了一下，确实很强，可能会改变现有 Agent 和多模态理解的格局，值得继续深入体验探索。

  

---

  

我是无常，喜欢码字的AI产品经理，欢迎关注：

  

![](https://mmbiz.qlogo.cn/mmbiz_jpg/ib7Cbc6MhGsibRDFm8fVic73ageMicyt2BnXdmvMsx2cUS633ceCMvLQle9RhhetdkamCZmdvd3udcm0sCh828ObCQ/0?wx_fmt=jpeg)

为热爱投票

 [喜欢作者](https://mp.weixin.qq.com/s/)

AI 48

ChatGPT 36

LLM 42

OpenAI 4

继续滑动看下一个

张无常

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功