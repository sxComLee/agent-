---
标题: "OpenAI发布o3和o4mini，看图不过脑子的大模型开窍了"
链接: "https://mp.weixin.qq.com/s/_vt5f7U2Mg0Wd5AwjuLGQg"
作者: "[[AI沃茨]]"
创建时间: "2025-04-22T13:42:58+08:00"
摘要:
tags:
  - "clippings"
  - "openai"
  - "o3"
  - "o4mini"
  - "图像模型"
字数: "161"
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

![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXlHmpBHsDfV5DnJ0kFicNZYLymzDXesR87EI3ibdpAAe38QFMpdrG00BY2yNvpWjkmodGxCDia7vhfhg/0?wx_fmt=jpeg)

原创 AI沃茨 [卡尔的AI沃茨](https://mp.weixin.qq.com/s/)

2025-04-17 09:22:04

精确发文时间由壹伴提供

手机阅读

![图片](https://mmbiz.qpic.cn/mmbiz_gif/YEhakvKZjXnldP5j86gl7F0BX2wnsreS7y5dnqT3nNMR5E3blh98PEOVETviaQ0K7mXFibG9uzTIK2ruLXq1Eo9Q/640?wx_fmt=gif&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

来不及怀念月底即将消亡的GPT4了！

也来不及取笑价格最高，号称最强非推理模型的GPT4.5反而要被GPT4.1 API取代了！

现在迎面走来的是，取代 o1、o3-mini 和 o3-mini-high 的：

o3、o4-mini和o4-mini-high

说实话，我刚看到的时候是懵的，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXnldP5j86gl7F0BX2wnsreS7jeQ00SFGsmFtnsU5ygo31kzRaZ13Eo5NtIddpK8EAXGYdPPaOmfibg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

凭借着隔壁好邻居 Grok3，才算是整理出了这次更新的所有内容，先来说说结论：

- 推理模型首次能自主组合 GPT 里所有工具，包括网页搜索、Python 编程、图像分析、文件解析和图像生成。
- o3、o4-mini是首个能“思考”图像内容，将图像信息整合到思维链的模型
- 支持完整工具集的 o3-pro 将在几周后推出，不过o1-pro还活着，暂时不会被下架
- 目前 Plus、Pro、Team 用户可使用
![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSKSibzEuy8G1O1iaibTnjzkl6v63TibDqIzic6ddtqLsQctncUCXGKdEibFAw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

发布会里演示的“看图思考”就让o3在图里找出最大的船只、以及推测这首船最后会停靠在哪里。

按照官方技术报告， o3、o4-mini的具体能力是能识别图表、扫描页、截图、手绘图等复杂图像。还可以主动放大、旋转、裁剪图像，作为思考的一部分。

所以我尝试在一次对话让o3把所有工具都用一遍：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSSF84BWBjJsWRBgicsvYUamOO6KfPboMbeS8ia8x0VUw9tE7WPpKUp5Gw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
切割查看图里的每一个组件，结合联网搜索，解释它们的定义，并以代码形式告诉我如何最简单做一个mcp server，最后生成一张同样的图，但是解释的文字用中文
```

直接看看结果，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXnldP5j86gl7F0BX2wnsreS5OT1w66j7EFr8fzPnzCu51gazEgjNLYFAqobt7W1bXknJpug4dEJ7Q/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

o3 是真的可以在单轮对话里兼顾图像分析、生图、代码生成和联网搜索，我的评价是比 Deep Research好玩多了。

接下来我还给o3安排了一个看花眼的任务：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSunbhB22nIKbqfibGXKWrRF2RY7zrY6C7kGRVAghDHbjA16RKdGlFp7Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
找不同，并用红框框出来
```
![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSsjIKhIXM98KxcxzbTyC8IDeTGRAcaBddTXtqCear3RMhoPPgfOuQAw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这个输出就更离谱了，

从 o3 的思考过程看出，它能加载图像并将其分成两半（左侧图像将从 x=0 裁剪到 319，右侧图像从 x=320 裁剪到 639）。然后，通过Python代码将两半图像都转换为灰度图、应用阈值并使用形态学运算进行清理来查看它们之间的差异。

换句话来说，

以后我们应该都不需要上传图片后，

还自己手动给模型补充背景知识了。

那再来看看具体的数值表现：

1. o3 刷新 Codeforces、SWE‑bench 及多模态 MMMU 纪录
2. ![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSGRptuCjKBPheq6HziceSiaZwPu5Fwlo18r6vBedzWx4Sx78ePGobRSXw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
3. API 定价上，o3比o1便宜33%，o4‑mini跟o3-mini、o1-mini保持了一样的价格。
![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreS7BPHEXckwd7y0UibmRFiarSpcDE803Ar7PAygibNicSGFvQe0sFE6L5n5w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上面这幅定价图就是我跟o3对话生成的，

几轮对话体验后，个人感觉是思考动画质感有提升（跟 Grok3 有点像），能明显感到思考时间提升，以及搜索网页数量的增多。

BTW，这里有个小彩蛋，内部测试的管 o3 叫精简版 Deep Research。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSMwq3YtxSWicMvZakQeKsLtWoqM7PtZgKWBGjgPHaJd18vjiaaavCj9uw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

小遗憾的是，主打能将图片放入思考过程的 o3 和 o4-mini 目前在多模态能力平台上没打过 `Gemini 2.5 Pro`

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXnldP5j86gl7F0BX2wnsreS8DgDglkECHalUaKUibl2k0JEUewuoNPJapCqAtztpGqpIPIUkdYNCicQ/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

除了模型之外，OpenAI这次没有按照惯例追着 Gemini 打了。

反而是推出了一个叫开源的 `Codex CLI` 的 Agent，再加上前天发布，也是重点提升了编程能力的 GPT4.1，很难不临想到针对的是隔壁的编程之王 `Claude`.

![图片](https://mmbiz.qpic.cn/mmbiz_gif/YEhakvKZjXnldP5j86gl7F0BX2wnsreSWiaO2eJianlYpUHnSIibIg56ThtYwzibHdlZlzsbOYSm7cmX6glvC3TMlQ/640?wx_fmt=gif&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

简单来说， `Codex CLI` 可以运行在本地的终端上，并作为一个链接模型和本地代码的接口。

  

写在最后

o3、o4-mini 的登场，

像是给 GPT4 的离去献上了一场盛大烟花，

我一开始没写 GPT4.1，是因为觉得它的诞生是为了取代 GPT4.5 超高的成本。

GPT4 需要一个真正意义上，在 ChatGPT 这个页面上完全能取代它的新模型。

继承大家对它，对 AGI 的期待。

在模型更新迭代上，

我们告别了GPT3.5、GPT4，

见证了 OpenAI 从 GPT 系列转向以推理为核心的o系列，

甚至还将迎来第一个推理模型o1的离去。

有时候，我还是希望这些模型只是短暂沉睡在自己的权重文件里，

等待着我们重新唤醒TA，

再一次说声 `Hi,GPT`!

  

@ 作者 / 卡尔 @ 动手学AI知识库 / learnprompt.pro

---

最后，感谢你看到这里👏 如果喜欢这篇文章，不妨顺手给我们 *点赞👍｜在看👀｜转发📪｜评论📣* 更多的内容正在不断填坑中……

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSxxdj9KQzoibgBqHuRPanHRAagPCvmFkBda0gsHQ0ehJvqfROPhyLKUw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qlogo.cn/sz_mmbiz_jpg/9JPKQ6n4AVm2uVtTV3yR0sszrCKNP141voF1CaGSIMxAwVGlhrQM2qIZkmeHtibVtlQibVdDv3tQugMVqichjqeKQ/0?wx_fmt=jpeg)

谢谢你的无糖可乐😸

 [喜欢作者](https://mp.weixin.qq.com/s/)

AIGC教程 136

科技抢鲜看 129

ChatGPT 42

OpenAI研究追踪 21

继续滑动看下一个

卡尔的AI沃茨

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功