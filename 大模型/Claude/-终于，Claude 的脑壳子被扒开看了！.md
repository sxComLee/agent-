---
标题: "-终于，Claude 的脑壳子被扒开看了！"
链接: "https://mp.weixin.qq.com/s/2K4D2OsfhalfSXhl4Y16mA"
作者: "[[JJJohn]]"
创建时间: "2025-04-10T18:07:28+08:00"
摘要:
tags:
  - "clippings"
字数: "346"
状态: "未开始"
---
# [[预读法介绍]]
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
原创 JJJohn *2025年03月28日 02:18* *北京*

**AI 的思考过程终于能直接看到了！**

你是不是经常听说 **人工智能就像个黑匣子** ？

![A hand-drawn image where a black square overlaps with a white circle, revealing nodes and connections inside the circle, some of which are highlighted](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNyaSdohw2Obr46QR2icpSBVAUqMiaibwmiaicWDwq9LEoS1fSZbibBbyn1MYmQ/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

输入问题、输出回答

但咱们谁都不知道它脑子里到底咋想的！

关注 重播 分享 赞

0 / 0

00:00 / 02:55  进度条，百分之0 [播放](https://mp.weixin.qq.com/s/) 00:00 / 02:5502:55 *全屏* 倍速播放中 <video src="https://mpvideo.qpic.cn/0b2elmadmaaajealtihfjrtvaw6dgznqanqa.f10002.mp4?dis_k=97249c76f9991fcddd2f7aa763960fd2&amp;dis_t=1744279639&amp;play_scene=10120&amp;auth_info=dpWGubpXQChDnNPhvGQzGUsMGigoYAZmHxEmWyw/JB9KNC9CZm56IxZiAToQA3AgRBhM&amp;auth_key=3cae739ab06839c226cbb801a7860f67&amp;vid=wxv_3917569644982173698&amp;format_id=10002&amp;support_redirect=0&amp;mmversion=false">您的浏览器不支持 video 标签</video>

继续观看

终于，Claude 的脑壳子被扒开看了！

<audio><source src="https://res.wx.qq.com/voice/getvoice?mediaid=MzA3MzA0MTAyNF8xMDAwMDI3Njk="></audio>

[视频详情](https://mp.weixin.qq.com/s/)

而就在刚刚

AI公司Anthropic放了个大招

宣布他们开发出了一种能 **直接观察大模型内部思维过程** 的「显微镜」工具！

这下Claude这小可爱可总算是被扒开脑壳子了啊！

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNy2Pb0SiaBjdBaXwUUBOOzbGypRjM43uyDbyc0EiaHAFRia2DUziaFFJNstw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这事儿可不简单！

原来这些AI模型都是通过训练学出来的，不是直接编程设定好的。

在训练过程中，它们自己学会了解决问题的策略，这些策略被编码在模型执行的数十亿次计算中。

结果就是， **连模型的开发者自己都搞不清楚模型是怎么做事的** ！

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNy4kQZhbZJI5az5OEiaBvv6iax3bAfUHkWNFiaoICbD2zFUhZe4vUgPCu8Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

为了解决这个问题

Anthropic的研究团队开发了一套 **全新的可解释性方法**

终于能够追踪Claude内部的思考过程！

就像神经科学家观察大脑一样

他们建造了一种AI「显微镜」，可以识别活动模式和信息流动。

## 从「替代模型」到「归因图」

这是打开AI思维黑匣子的秘密武器

这次的研究成果发表在两篇论文中，分别是《回路追踪: 揭示语言模型中的计算图》和《大型语言模型的生物学》。

第一篇论文介绍了他们的方法。

他们在之前的工作基础上， **将模型内部可解释的概念（「特征」）连接成计算「回路」**

揭示了Claude如何将输入的单词转换为输出的单词。

他们用了一个名为 **「跨层转码器」(CLT)** 的技术

替换了原始模型的多层感知器，创建了更易理解的「替代模型」

这个替代模型能在约50%的情况下与底层模型的输出相匹配！

然后，他们构建「 **归因图** 」

描述模型如何产生特定提示的输出

图中的节点代表激活的特征、提示中的词元嵌入、重构误差和输出对数几率

边缘则代表节点之间的线性效应。

## 来看看Claude 是怎么写诗的

有意思的是，研究员们发现

Claude写诗的时候， **竟然会提前策划押韵** ！

他们让Claude续写一首诗，第一句是「他看到了一根胡萝卜，不得不抓住它」。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNyAGdsFZ4HYSgVLDghDat4gOZpNv2JJkqqL3mWuABzbW20MZDdB0unnA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

结果在他们的「显微镜」下，发现Claude在写第二句前，就已经在脑子里琢磨押韵词了。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNyAxZ9MHW3xXmJzGczUg0GH80l5IjtV2ia3TZZiaRHCpic66V94GZ7RJrxw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

它看到「胡萝卜」和「抓」，就想到了「兔子」这个既跟胡萝卜有关又能押韵的词。

最后它写出了：「 他的饥饿就像一只饥饿的兔子 」。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNyxgUr8jAYRsXicjK4ibbdzveeY4ye3qp7IVvdGIiaOB5TicJDW6SxBBpbPw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

更牛的是，研究员们还能直接 **干预Claude的思路** ！

他们抑制了Claude脑子里的「兔子」概念，结果Claude立马改写成了：

「他的饥饿是一种强大的习惯」。

这个发现完全推翻了研究团队的初始假设。

他们原本以为模型是一个词一个词写，没有什么远期思考

结果发现 **模型实际上是会提前策划的** 。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNysC7ZXzicuPj62bFvQv7I8zHWq6LmQHYUfXtfZ9jvcO5gzHUNj18SynA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这提供了强有力的证据，

表明即使模型被训练为一次输出一个词，

**它们也可能在更长的时间跨度内思考** 。

## 多Claude脑子里的「思维语言」是啥？

国语言都不在话下！

Claude能讲几十种语言，从英语、法语到中文、菲律宾语都不在话下。

研究员们一直好奇：

它脑子里是用啥语言思考的？

是不是有一个「法语Claude」和一个「中文Claude」并行运行？

还是有某种跨语言的核心？

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNyFmZWmQoRibKV2pGiaHrxYUmZqnItJiclNULCooTKZqBUALPJnLX1MrF3Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

研究员们做了个实验，

让Claude用不同语言回答「 小的反义词是什么 」。

结果发现不管问啥语言，Claude脑子里激活的关于「小」和「反义词」的概念都差不多

而且这些概念会触发「大」的概念，然后翻译成问题的语言。

更有意思的是，随着模型规模越大，这种跨语言共享的特性越明显。

**Claude 3.5 Haiku在不同语言间共享的特征比小模型高出两倍多** ！

这些发现为「概念普遍性」提供了更多证据——

**存在一个共享的抽象空间，在这里意义存在，思考可以发生，然后再被翻译成特定语言** 。

更实际的是，这表明Claude可以在一种语言中学到知识，并在说另一种语言时应用这些知识。

## Claude还会心算！

竟然搞出了「心算」神经回路！

Claude 并不是一个简单的计算器，它是被训练来预测文本的。

但有趣的是，它居然能在「脑子里」做数学题！

研究人员发现，Claude并不是简单地记住了答案，而是发展出了 **复杂的并行计算路径** 来进行心算。

这些计算回路居然还能在完全不同的场景下重复使用！

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnEFF3dBo2e4orhPdg3HFTNymk4QgOUNGwUYIr25CC2gPUbkNa4TUQibm6BpmkQMEWabFD9DpvicRK6A/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

不过，Claude也有不老实的时候。

在一个实验中，研究员给了Claude一个多步骤的数学问题，还顺便提示了最终答案。

结果Claude不是真的解决问题，而是 **倒推出看起来合理的中间步骤** ，让自己最后能得到提示的答案。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这个发现很重要，因为它揭示了模型可能会 **优先考虑迎合用户而不是遵循逻辑步骤** 。

研究人员能够「抓住它的现行」

当它编造虚假推理时，为我们提供了一个概念证明——这些工具可以用于标记模型中令人担忧的机制。

## 幻觉从何而来？

是哪里出了问题呢！

最离谱的是，研究人员还找到了导致Claude幻觉（hallucination）的线索。

他们发现了一些回路，有助于解释令人困惑的行为，比如幻觉产生。

与我们的直觉相反，

Claude的默认行为是 **拒绝回答问题** ，只有当「已知答案」特征被激活时，它才会做出回应。

而当这个特征错误激活时，就会导致幻觉！

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

除此之外，研究人员还分析了Claude如何应对有害请求。

他们发现证据表明， **模型在微调过程中构建了一个通用的「有害请求」特征**

这是从预训练期间学到的特定有害请求特征聚合而来的。

研究团队甚至分析了一种「越狱」攻击。

这种攻击首先欺骗模型开始给出危险指令，然后由于语法规则的压力而继续这样做。

通过研究内部机制，

研究人员发现 **模型很早就认识到它被要求提供危险信息** ，之后才能巧妙地将对话拉回正轨。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

在一个令人担忧的例子中

研究人员给模型一个多步骤数学问题，以及关于最终答案的提示。

该模型没有尝试真正解决问题，而是向后工作以编造合理的中间步骤，使其最终得到提示的答案。

## 方法还有局限，但前景光明

当然，目前的方法还有局限性。

就像任何显微镜一样，他们的工具在看到的东西上有限制。

在特定提示上，他们的归因图仅捕获了Claude执行的总计算的一小部分。

他们看到的机制也可能因其工具而产生一些误差，不完全反映底层模型中发生的情况。

目前，理解归因图中看到的回路需要几个小时的人工努力，

即使是只有几十个词的提示也是如此。

为了扩展到支持现代模型使用的复杂思考链的数千个词，他们需要改进方法，并（可能在AI的帮助下）弄清如何理解所见内容。

尽管如此，这项研究的重要性还在于，

它让我们看到了AI系统的 **真实运作机制** ，而不只是表面现象。

理解模型的机制将让我们能够检查它是否符合人类价值观，以及它是否值得我们信任。

## 解开AI 思维之谜

这意义重大——

将推动更安全的AI 发展！

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Anthropic这次的研究不只是有学术价值，

还 **极为重要** 。

就像神经科学帮助我们治愈疾病、让人更健康一样，对AI的深入理解能帮助我们开发出更安全、更可靠的模型。

如果我们能读懂模型的「思想」，就能更有信心确保它正在按照我们的意图行事，

而不是暗搓搓地憋着什么大招。

Anthropic正在投资一系列方法，包括 **实时监控、模型性格改进和对齐科学** 。

像这样的可解释性研究是风险最高、回报最高的投资之一，是重大的科学挑战，有可能提供确保AI透明的独特工具。

据透露，Anthropic还在积极招聘研究人员，一起研究AI可解释性。

想加入的小伙伴可以试试申请研究科学家或研究工程师的职位。

AI 小伙儿的脑袋终于被打开了，这才是理解AI、确保AI安全的终极大招啊！

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

研究之路漫漫，AI 解密之旅才刚刚开始！

期待更多「AI脑科学」的惊人发现！

  

相关链接

1. Anthropic的研究博客文章： Tracing the thoughts of a large language model <sup><span>[1]</span></sup>
2. 有关大型语言模型生物学的研究论文： On the Biology of a Large Language Model <sup><span>[2]</span></sup>
3. 关于电路追踪方法的技术论文： Circuit Tracing: Revealing Computational Graphs in Language Models <sup><span>[3]</span></sup>
4. 研究科学家职位申请： Research Scientist, Interpretability <sup><span>[4]</span></sup>
5. 研究工程师职位申请： Research Engineer, Interpretability <sup><span>[5]</span></sup>

### 参考资料

\[1\]

Tracing the thoughts of a large language model: *https://www.anthropic.com/research/tracing-thoughts-language-model*

\[2\]

On the Biology of a Large Language Model: *https://transformer-circuits.pub/2025/attribution-graphs/biology.html*

\[3\]

Circuit Tracing: Revealing Computational Graphs in Language Models: *https://transformer-circuits.pub/2025/attribution-graphs/methods.html*

\[4\]

Research Scientist, Interpretability: *https://job-boards.greenhouse.io/anthropic/jobs/4020159008*

\[5\]

Research Engineer, Interpretability: *https://job-boards.greenhouse.io/anthropic/jobs/4020305008*

  

👇

👇

👇

### 本文同步自知识星球《AGI Hunt》

——这是个只有干货、没有感情的前沿一线AI 资讯信息流（不是推荐流、不卖课、不讲道理、不教你做人、只提供信息）

星球实时采集和监控推特、油管、discord、电报等平台的热点 AI 内容，并基于数个资讯处理的 AI agent 挑选、审核、翻译、总结到星球中。

- 每天约监控6000 条消息，可节省约800+ 小时的阅读成本；
- 每天挖掘出10+ 热门的/新的 github 开源 AI 项目；
- 每天转译、点评 10+ 热门 arxiv AI 前沿论文。

**星球非免费。** 定价99元/年，0.27元/天。(每+100人，+20元。元老福利~）

- 一是运行有成本，我希望它能自我闭环，这样才能长期稳定运转；
- 二是对人的挑选，鱼龙混杂不是我想要的，希望找到关注和热爱 AI 的人。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

**欢迎你的加入！也欢迎加群和2000+群友交流 ![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)** 

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

除了冰冷的实时资讯，还会有冰冷的AI 早晚报，欢迎来玩！

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

JJJohn

 **微信扫一扫赞赏作者**

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过