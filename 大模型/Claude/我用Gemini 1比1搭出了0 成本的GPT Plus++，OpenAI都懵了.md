---
标题: "我用Gemini 1比1搭出了0 成本的GPT Plus++，OpenAI都懵了"
链接: "https://mp.weixin.qq.com/s/r1SB5dPueKBq3-P586KiTQ"
作者: "[[AI沃茨]]"
创建时间: "2025-04-22T12:28:43+08:00"
摘要:
tags:
  - "clippings"
字数: "293"
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

原创 AI沃茨

2025-04-18 09:45:15

精确发文时间由壹伴提供

手机阅读

![图片](https://mmbiz.qpic.cn/mmbiz_gif/YEhakvKZjXnldP5j86gl7F0BX2wnsreS7y5dnqT3nNMR5E3blh98PEOVETviaQ0K7mXFibG9uzTIK2ruLXq1Eo9Q/640?wx_fmt=gif&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

我有 GPT 订阅焦虑症，

虽然已经有很多替代，编程用的 Claude 3.7、写作用的 DeepSeek R1、音视频理解用的 Gemini 2.5 pro。

但下不了决心取消，

因为 Plus、Pro 套餐除了基础的 GPT 和 o1、o3 等推理模型外，还有一大堆附加功能，4o 生图、深度研究 Deep Research、代码和写作画布 Canvas等等。

但是隐形降智太严重了，

模型会在你不知情的时候自动切换成较低版本，联网、图片生成、推理能力等通通无法用。新出的 o3 在网页版里用中文对话都变成傻子了。

再加上 Gemini 三、四月份不要钱的更新，我单方面宣布挑战零元搭出 `超 Plus 近 Pro` 的工作流，OpenAI 看了都懵，不需要东拼西凑，体验感不带差的。

![OAI 你头怎么尖尖的？](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXnldP5j86gl7F0BX2wnsreSdkepsr88RFBMvbTwgnPHzI0rDWZibduBI1ib5I7kVHvkN5RypT5Czpog/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

OAI 你头怎么尖尖的？

  

一、Pro、Plus 真的值吗？

我们先来扒扒 OpenAI 订阅套餐里的附加价值。免费版就不用看了，那点使用额度，不充还不如用 DeepSeek R1，直接上 Plus 和 Pro。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSN8rnrKuEPrdVUL8kwIozicnH5IRwicGsNB2qliccBmqbHLdDctNicyt5aA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

先来激情吐槽一波，

- 高级语音模式：练口语还行，但想要用对话完成复杂操作很难。中文语境下拿来用视频通话问些 `这个是什么` 的简单问题就是极限了。想要达到发布会上教你一步步冲咖啡的效果，抛开使用额度的限制外，GPT的回复都是高度概括的，做不到手把手，还不如看某书快。。。
- Sora 本来零人在用，4o生图拯救了一波
- Pro 专属的浏览器自动操控 Agent `Operator` 远不如 Manus，哪怕是用 OpenManus、OWL、Flowith2.0 等多 Agent 系统都比它好不少。
- GPTs、类知识库 Projects、定时任务执行这三个功能估计也就剩部分持续更新的三方 GPTs 还有一定流量
- 写作和代码画布 `Canvas` 也被 Gemini 实现了。

王牌功能深度研究 Deep Research 是好用的，就是 Plus 一个月只能用10次，有需求的不够用，轻需求的用 Gemini 免费的 Deep Search 就够了，还能转成播客。。。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreS3svM77DWPfKjUW1KZvtAAV59EfMpNibqFwWia7EBGNGJzleLlZTCXnWg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

或者上 Gemini Advanced 就能获取无限次数，效果更好的 2.5 pro 版 Deep Research。

虽然已经有不少人陆续输出 Gemini 的一些强功能，但好像很少搭成完整的，全功能的。所以我才想到这个有趣的挑战，

用免费的 `Gemini` 完全取代，甚至超越 GPT Plus 的所有功能，Here we go！

  

二、像素级复刻 GPT Plus

gemini 模型目前主要使用地址是两个，

- 🔗 aistudio.google.Com/prompts/new\_chat
- 🔗 gemini.google.Com/app

先从 GPT 都没有的开始，Gemini 的 `NotebookLM` 、 `Personalization` 和 `Apps` 。

`NotebookLM` 就是前段时间超火的 AI 播客，可以将一切内容转成两人播客，还可以中途加入他们一起讨论。这个功能现在已经在 Gemini 里上线了！

使用方式也简单，上传文件或者深度搜索后就会自动弹出 `生成音频概述` 。

`Personalization` ，简单来说就是Gemini 可以读取到我的搜索记录，我找了个超棒的应用场景：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreS79rhsGMm3GZndBCYrWOljSbzDxkaQI5A5datDvEADfJdhljXz3gP3A/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

让 Gemini 快速总结这周来我关注的知识点！这对我这种每日都大量记笔记的人来说很有诱惑力。毕竟谁不想用原始数据来查漏补缺啊，就是量太大了。

同样一个我很看好的应用领域就是 `Apps` 这个功能，体验上说像是 MCP 的原生版。盲猜是 Gemini 针对这几个 App 做了很全面的兼容：

我可以查询旅游最佳路线后订机票、直接写入日历，还可以直接搜索任意主题、播放量较高的视频，也可以检查重要的邮件。

接下来，就是 OpenAI 现在的王牌功能 `Deep Research` ，Gemini 的 Deep Search 目前的额度是每月10次，跟 GPT Plus 的额度保持一致。

2.0-Flash 版的 Deep Research 功能目前确实还没发跟 o1 比。比起一般的AI搜索，Gemini 搜索信息源数目足够多，一次搜索里平均还会反复补充几次网站，总体来说是一个相当不错的平替。

至于 2.5-Pro 版的完整 Deep Research 在技术报告上比 o1 版的强，但是刻意体验了两周后，我还是更喜欢o1做报告的思维模式

至于 OpenAI 脱胎于 Claude Artifacts 的 `Canvas` 功能，专注于用模型来写作和代码展示的功能，也已经被 Gemini Copy 完了。。。

代码展示效果没啥好挑的，中规中矩，不会出现 Claude Artifacts 初期生成代码后因为环境没有安装包而展示失败的情况。

拿来写作就有意思了，支持修改长度，语气和让模型自我发挥。好玩的是可以在完成生成后再要求模型补充上图片。可惜这个图片都是从联网搜索里爬到的，不是自己生成，所以有一部分都对不上。。。

接下来体验体验 Gemini 的 `语音模式` ，

我测了很多很多遍，可以确定的是目前语音模式下应该是支持联网的 Gemini 2.0 Flash，就是可以满足一些简单的问题，但即刻打断、中文发音要比豆包差点。

好笑的是现在安卓手机已经部分支持相机和屏幕共享功能了，苹果手机却被排除在外了。

现在应该到了聊聊 `Veo2` 了，作为跟 Sora 同时期出道的练习生，文生视频方面上在我心目中是稳超 Sora 的，缺点就是太贵太贵太贵了，哪怕是失败率很多，1秒X元的价格也是有点劝退。

```
一个广角慢摇镜头，捕捉一个巨大的冰川洞穴，笼罩在诡异的暮色中。淡青色的光线从上方倾泻而下，照亮了冰墙内冰冻的糖果人偶。两个身穿白色外骨骼的人影，头盔上的灯光投射出光束，在洞穴中心艰难前行。捕捉洞穴的规模与静谧。
```

不过 Gemini 还真支持上了，虽然额度有限，但是用到就是赚到！

至于 AI 图片方面的话，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXnldP5j86gl7F0BX2wnsreSppXDlAsrDO0SzzCicjIq3FusDQn0y948mECyicanqsGntUb7UiatOftxQ/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可惜的是这段时间爆火的 Gemini 2.0 的 `图片编辑功能` 还没有上线 Gemini App，只能在 ai studio 里用。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXnldP5j86gl7F0BX2wnsreScClNsdMwTyRiaVliajhichibpfuHJWG871qgEYVxWQLOVDkKEnguiaBveLg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Gemini App 自带的还是 Imagen3，在写实风格上只能说还能看，其他的风格就不多提了，懂的都懂。

最后的最后，我们来聊聊 `Gems` 吧，也算是 Gemini 版本的 GPTs 吧。

只能支持上传10个文件注定了目前 Gems 处于很尴尬的局面，拿到当知识库吧，存储空间太少，同时没有 GPTs 的灵活和其他三方公司的支持，一共就发了 6 个官方 GPTs。

我的建议是用 `Coding partner` 来辅助写写代码就行。

So，

你觉得这次我的复刻GPT订阅套餐成功了吗？

希望奥特曼别被我“追上了”（/狗头护体）

评论区和我一起讨论你的最爱使用搭配吧。

@ 作者 / 卡尔 & 阿汤 @ 动手学AI知识库 / learnprompt.pro

---

最后，感谢你看到这里👏 如果喜欢这篇文章，不妨顺手给我们 *点赞👍｜在看👀｜转发📪｜评论📣* 更多的内容正在不断填坑中……

![图片](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnldP5j86gl7F0BX2wnsreSxxdj9KQzoibgBqHuRPanHRAagPCvmFkBda0gsHQ0ehJvqfROPhyLKUw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

谢谢你的无糖可乐😸

继续滑动看下一个

卡尔的AI沃茨

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功