---
标题: "手机上也能用满血Claude Code和Codex了，教你一步搞定！"
链接: "https://mp.weixin.qq.com/s/YuOcnHsl9EliHjRv21SCpg"
作者: "[[卡尔的AI沃茨]]"
阅读星级: 3
内容类型: "鎶€鏈暀绋�"
创建时间: 2026-02-08T12:20:56.378Z
摘要: |
  本文介绍如何通过开源项目Happy Coder实现Claude Code在手机端的便捷使用，突破设备、网络和打字限制，提升AI编程工具的可访问性和实用性。
tags:
  - "Claude Code"
  - "移动端开发"
  - "AI编程工具"
  - "开源项目"
  - "远程访问"
字数: 4887
状态: "未开始"
总结: |
  本文是Claude Code系列教程的第十五篇，主要讲解如何利用开源项目Happy Coder将Claude Code扩展到移动端使用。关键要点包括：
  1. **背景与痛点**：Skill迭代速度快，传统使用方式受限于电脑，外出时无法及时响应需求（如代码完成提醒、灵感即时复刻）。
  2. **解决方案**：通过Happy Coder实现手机与电脑Claude Code的连接，只需手机有网、电脑有电，支持跨网络远程访问，无需复杂配置。
  3. **安装与使用**：提供安装命令（`npm i -g happy-coder && happy`）和详细步骤，支持扫码连接，可同时管理多个Claude Code/Codex实例。
  4. **功能优势**：实时查看工具调用、代码修改差异和上下文余量，支持远程压缩上下文；兼容Codex的各种模式，回复速度快。
  5. **应用场景**：结合Skill实现移动端高效操作，例如将飞书文档转为Markdown并发布到X平台，或在路演中即时复刻开源项目。
  6. **历史对比**：相比十年前通过SSH连接终端的方案，Happy Coder解决了网络稳定性、界面交互和实时同步等问题，极大扩展了使用场景。
  7. **总结**：手机端使用Claude Code提升了工具的灵活性和效率，让用户随时随地调用AI编程助手。
---

# [[手机上也能用满血Claude Code和Codex了，教你一步搞定！]]
### 预读问题
**基于你的目标**：
- Q1:
- Q2:
- Q3:

### 关键图表/代码
![[提取的图表或代码片段]]
### 初步关联
- 已知：[[已掌握的相关热识]]
- 未知：`#\u5f85\u63a2\u7d22`

### 输出目标
- [ ]

# 内容
#flashcards

这是Claude Code系列教程的十五篇。

在动笔之前，我犹豫了一下，在这个时间点是继续分享更多好用的Skill，还是教大家一个更方便，把Claude Code能效拉满的玩法。

Skill的迭代速度太快了。比如最近收集到的做动态PPT、消除写作AI味以及将日常对话自动总结成技能的Skill。上周才刚推荐完我的十大好用Skill，估计再过两三周这个榜单就又要换一轮了。

所以这第十五篇，我们来点更原生态的，

如何最大限度地把Claude Code的额度，换句话说就是在手机上用Claude Code，不挑设备，不挑网络，不挑打字，还要免费。

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMgqicyiccfeWKvoeVsSxaicBJ9LSw3Gl5mPvaAS5JVIbuQpz2pKSIJ0gog/640?wx_fmt=jpeg)

用happy-coder在手机上也能用Claude Code和Codex

前面我已经介绍了如何用OpenRouter+cc-switch来管理几乎所有厂商的模型API。额度是完全用不完的。以我日常用Kimi K2 Thinking当栗子，100块就够我常态化天天高频使用Claude Code了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbM1DappKV36ibK5UHUwp3dM0RQagKyibFseibsfVUEM4hJHoe5jQepBQxDA/640?wx_fmt=png&from=appmsg)

我目前的编程模型组合，Claude，GPT，Kimi，Minimax，GLM

虽然 Claude Code 已经具备了通宵写代码（配合Ralph Wiggum skill）的能力，

但还是会遇到一些痛点，出差在外，要是电脑里代码跑完了我想要收到提醒，或者在刷小红书时看到一个很棒的页面设计，想立刻让Claude Code帮我复刻一个出来。

Claude Code就应该像豆包一样可以随时随地在手机上用，Anthropic不教，我来教。

很简单，只需要用到一个开源项目，Happy Coder

🔗 happy.engineering

同时支持移动端和网页端，不管是苹果、安卓还是其他系统。我已经测试过了，手机和电脑不需要连接在同一个Wi-Fi下。这意味着，你的手机是可以带着出门，随时随地调动家里的Claude Code。

![image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMbX6icDibqRicgREtEHUvrUictNibsM7GwFVTgqGgZpX5ENstbZevTg1uREA/640?wx_fmt=png&from=appmsg)

只需要保证两件事，手机有网，电脑有电。

至于如何让电脑二十四小时保持清醒，这里我就不教大家复杂的终端命令了，直接推荐一个我用了很久的小应用，它能保证你的电脑即便合上盖子，也能保持在线。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMiasZxH2C5HibqsoEplGxWfClUDT6x3QgJfoLoZOiatpWQdjedu5ASygow/640?wx_fmt=png&from=appmsg)

关于Claude Code和Codex的安装，我之前已经把豆包调成了CC安装助手，这次我也把Happy Coder的安装流程更新了进去。你只需要用口语化的方式告诉AI助手你的电脑系统，它就会为你生成对应的安装步骤，

这里也有一个直接安装的代码，可以先运行，有错误了再给豆包排除。

```
npm i -g happy-coder && happy
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbM3MDNSk0cP9icOxibo0opaXVsEovuIzRetoicwCa2Ylnj0zDPqicHSib4SBQ/640?wx_fmt=png&from=appmsg)

🔗 https://doubao.com/bot/stIy6xcY

安装完成后，在终端里运行命令happy-coder，屏幕上就会出现一个二维码，然后就可以在手机上选择用浏览器访问，或者直接下载App来扫码连接。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMibkD08lfS8ssZYaOTiaAtoL4vibuncYOomQtbwBt1G3hjZd4RrRjZb5MA/640?wx_fmt=png&from=appmsg)

iOS🔗 apps.apple.com/us/app/happy-claude-code-client/id6748571505

安卓🔗 play.google.com/store/apps/details?id=com.ex3ndr.happy

连接成功后，一个全新的体验就开始了。

我可以在手机上实时看到Claude Code正在调用的工具，待办事项，前后代码的修改差异，以及当前对话的上下文余量。当上下文长度告急时，我可以直接远程让CC压缩一下。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMtWGyhp4oIqLNn9VF2tSlJDb1h3E3gqnSc29ib8OKmNQyDHVZDicBvS0g/640?wx_fmt=png&from=appmsg)

经过两天的深度使用，我还发现了一个隐藏的用法。Happy Coder的App支持新建多个对话，这意味着你可以在电脑上打开多个终端窗口，分别运行不同的Claude Code和Codex实例，

然后用一台手机同时与它们进行对话，互不干扰。

这里有一个大前提，一开始我们连接的是Claude Code，没有连上电脑的CodeX，

这时候就需要在电脑的终端上新建一个窗口，输入happy codex完成手机跟电脑的 Codex 连接，不需要重新扫码

只需要设置一次就好了，所以也是简简单单！

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMCicCz1Ntib2YuzkibzGZqEMRpODw1Tdr2bKiassIRhk9GlZclTKgMCibjDQ/640?wx_fmt=png&from=appmsg)

这个App对Codex兼容性非常好，无论是安全模式还是YOLO模式，无论是调用GPT-5的哪个版本，

回复速度都很快。

当Claude Code拥有了移动端入口，再配合我之前介绍过的各种Skill，我就能实现很多过去难以想象的秀儿操作。

比如，我可以把在飞书上写好的文章链接直接从手机上丢给Claude Code，

让它利用feishu2md（电脑才有的指令），帮我把文档转化为包含排版和图片的markdown版本。

然后，我再调用Claude Code的x-article-publisher-skill，就能直接把这篇文章发送到我的X上。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMZTUSjh2RyEFugyXrWnQBp84TKMecblt4Z7IWYKpjkoRhkoaJIrOsSw/640?wx_fmt=png&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbMLVRf6eiarVvYGsibcmdkYn46l9VIzByOmZb9yOf4vPqNvh9O8twhMiccQ/640?wx_fmt=png&from=appmsg)

大家感兴趣的我单开一篇新的来讲讲

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXn4sjrqBvCd6Y59egWW5hbM7Tl3JcbFf5oicGcvvQX5tEtL0nNrXfInQ8fYoqSLFTlsCvMkJO7kic7A/640?wx_fmt=jpeg&from=appmsg)

这篇文章发布的同时我就完成X的同步了。

整个过程，我都不需要打开电脑。

手机，

极大地延伸了我使用Claude Code的场景和形式。

在路演过程看到一个有趣的开源项目，

我就直接打开Happy Coder，在手机上语音输入，把项目下载，解读，复刻出来。

只要手机在手，我就拥有了一个随时待命，不会浪费我充的钱的开发Agent。

理论上实现这个方法还有很多。

通过 SSH 连接，

十年前我们就可以把终端连接到手机上了。

我记得自己刚学代码的时候，

非常执着于把iPad改成可以远程连接电脑终端，这样我出门就只需要带个 iPad就能够完成所有的编程任务。

但我印象中当时有两个头大的缺点，

首先无法稳定远程，两台设备必须处在同一个网络环境下才能连接，更复杂的网络配置有是有，但需要我额外负担一台服务器，

消息同步的速度也远没有到现在那样几乎是实时的对话体验，

其次是界面太小，当时还不支持纯对话式的交互，

在手机那块小屏幕上敲代码，

效率反而更低了。

现在靠着Happy Coder+Claude Code，

我终于实现了这个当时看起来有点瞎折腾的配置，

要是有重生文的话，

把Claude Code带回去十年前，

是不是直接就龙王归位了，

Claude Code写C# 和C++

应该能hold住吧。

[我把新版Claude Code的上手门槛降到小学二年级，有豆包就行](https://mp.weixin.qq.com/s?__biz=Mzg3MTk3NzYzNw==&mid=2247504014&idx=1&sn=707d2bc299e71b7d409e324a23570706&scene=21#wechat_redirect)

[我至今用到最好的Claude Code ...](https://mp.weixin.qq.com/s?__biz=Mzg3MTk3NzYzNw==&mid=2247504075&idx=1&sn=a90d14bba89744951ed5060bdc6860f9&scene=21#wechat_redirect)

@ 作者 / 卡尔

最后，感谢你看到这里👏如果喜欢这篇文章，不妨顺手给我们*点赞｜在看｜转发｜评论 📣*

如果想要第一时间收到推送，不妨给我个星标🌟

如果你有更有趣的玩法，欢迎在评论区和我聊聊🤝

更多的内容正在不断填坑中……

![image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXmCDLEEW1wClZOVGFURjmibJmciaYLNhp0N55Y6mPiaCj01eV8yzACqDvWDhicbPm07Wu7bboATuKgAbA/640?wx_fmt=jpeg)
