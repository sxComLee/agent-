---
标题: "挑战用阿里版Claude Cowork跑通Clawdbot5个神级玩法，我Mac Mini可能白买了"
链接: "https://mp.weixin.qq.com/s/L-7mQcCxzLRujWSv_B3TBg"
作者: "[[卡尔的AI沃茨]]"
阅读星级: 3
内容类型: "缁忛獙鍒嗕享"
创建时间: 2026-02-08T12:21:17.591Z
摘要: |
  本文作者通过对比Clawdbot、Claude Cowork和QoderWork等AI工具，测试了QoderWork在邮件处理、日程管理、代码开发和文件整理等任务中的表现，强调现有工具的潜力，鼓励用户突破工具限制，探索AI的可能性。
tags:
  - "AI工具对比"
  - "自动化任务"
  - "邮件处理"
  - "文件管理"
  - "代码开发"
字数: 4166
状态: "未开始"
总结: |
  本文主要探讨了多种AI工具（如Clawdbot、Claude Cowork和QoderWork）在自动化任务中的应用。作者通过实际测试，验证了QoderWork在以下关键任务中的能力：
  - **邮件处理**：不仅限于阅读邮件，还能下载附件、识别紧急回复需求（如兑换余额）和处理续费提醒。
  - **日程管理**：根据邮件信息生成ICS文件，导入本地日历软件。
  - **代码开发**：调用Claude Code生成网页，但存在登录验证等小bug。
  - **文件整理与分析**：下载视频、按内容整理文件夹、生成文字记录和设计观看顺序。
  作者指出，Clawdbot因消耗token多而适合作为子智能体，而QoderWork等现有工具仍有很大潜力，鼓励用户不要给工具设限，应尝试用熟悉工具完成新挑战。
---

# [[挑战用阿里版Claude Cowork跑通Clawdbot5个神级玩法，我Mac Mini可能白买了]]
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

起因是这样的，

当我还在跟Mac Mini版满血版Clawdbot PK的时候，发现有人统计了排名前十的Clawdbot常见任务，分别是邮件处理，日历管理（日程提醒和会议安排），控制Claude Code开发，每日简报等，

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibUmoONNiaa17a5YkgibTFEMLwG4CYuzwNNZDliaMgUcO3JY9Rr2QIH6Gicw/640?wx_fmt=jpeg)

感觉这些任务桌面版Claude Cowork也能做啊，所以我反手又去收集了Claude Cowork在X上最火的十种玩法，它也可以控制Claude Code，解析WHOOP的数据做健身跟踪，文档管理更是Cowork舒适区，320份播客文件一次性分析出来了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibHqjDoxpXlW2TrXQM30t3pibuV05hecGOUodyts201twgPicjkzVowZJw/640?wx_fmt=png&from=appmsg)

按照我同时用Claude Code，Cowork和Clawdbot的频率来说，我更想在这篇文章验证Cowork对浏览器自动化，它对Mac系统上面其他工具的控制权限能够做到一个什么样的程度。又又又因为Claude Cowork只支持官方订阅，还不支持第三方 API，又贵又不稳定，

所以这次我跟阿里新推出的Claude Cwork，Qoderwork一拍即合，一起来完成这期的挑战。

先来试试看邮件处理，

我觉得邮件处理不能局限在只是打开一个网页、把未读邮件读一遍就完事了。

事实上，我希望Cowrk可以做到更多，它能够读取哪些邮件里的文件需要下载到本地，方便后续在本地做分析。识别哪些邮件需要及时回复。比如我这里有一个野卡的回复，前段时间被封了服务，最近一周就要去兑换余额，不兑换会过期。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibwV9vclaGYTwQD5MKG7JBz1u1BtKrwf37p4ewY9clsIRDHkQ97ozIag/640?wx_fmt=png&from=appmsg)

现在的AI服务续费真的太多了，我上个月在测试工具时开通了续费，后面也没常用，结果不知不觉又被扣了50刀，这也应该算在邮件处理范围内

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibj0uXdNfyJe2YmPhMFybzd2B0CvqTicicrVesI3qaWamzslS3ibpltNHaA/640?wx_fmt=png&from=appmsg)

邮件整理和阅读只是最初级的，我需要的是在确定邮件信息后，它能跳转到对应的网页去执行更细化的任务。目前来看，下载文件到本地，或者去卡片页面帮我兑换余额，都是可以完成的。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibpfqfbcwYtYABjgEZTWMjVqB4TVbI3AcQ5bVytBMDeJuUBiby1lt9F2w/640?wx_fmt=png&from=appmsg)

QoderWork右侧有一个任务监控。他在每一次完成任务后会做一个任务进度的回顾，这时候会输出一大串指令再执行下一个。但我希望在下一个版本中，能把这种回顾信息折叠到一个单独的block里面。

当然，在这个基础上做日程管理也是有解法的。

QoderWork可以根据邮件里的信息，生成ICS文件。这时候可以导入到苹果本地的日历软件中

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibmVO0LN9uKfibLRwB6D3KyYhpeuI3RLUCqnTQkTVD0ncjSACteSPA63Q/640?wx_fmt=png&from=appmsg)

这样我们就完成了邮件读取，分类管理，紧急事项处理，代办事项日程录入，社区最火的Clawdbot的前两个使用案例，我们已经完成了。

接下来是一个我最近学到Claude Code新玩法，

如何只靠安装两个skill，就能让你的前端设计达到 80 分，还可以搜索Figma上合适的模版来复刻互动效果。

需要用到的 skill 是这两个，ui-ux-pro-max-skill和frontend-design

```
帮我在claude code上安装两个新skills，命令是npx skills add https://github.com/nextlevelbuilder/ui-ux-pro-max-skill --skill ui-ux-pro-maxnpx skills add https://github.com/anthropics/skills --skill frontend-design
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibecEebJiaypy5RxMNep4cSVzZ4iaqnsqiaFtw4AA4NVfN0E52GaXg79G6w/640?wx_fmt=png&from=appmsg)

好消息是QoderWork确实可以调用Claude Code来生成网页，上面的图片素材是 QoderWork 直接生成好的，不需要额外去找，做出来的网页没有讨厌的蓝紫配色，也能做出鼠标互动。

但是目前来说，直接用QoderWork去调用Claude Code会出现一些小 bug。比方说我本地已经配置好完整配置的 Claude Code，但它会需要我再次登录验证。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCibGIwHJq5pDIkHZEtTeLZ9XlwCdIibkc79TP3VoMyWTI5sKK6icConRhcQ/640?wx_fmt=png&from=appmsg)

PS，我个人认为，之所以强调在Clawdbot上远程使用Claude Code，而不是直接用它去做代码开发，主要是因为Clawdbot消耗的token太多了。这个操作相当于让Claude Code成为了它的一个sub agent，专门负责开发的子智能体。

然后前十的玩法就剩下一个大类，文件整理。

我直接把它跟文件分析（也就是健康追踪）一起来说吧，主要的三步就是

整理文件，搜索文件，文件内容分析

我把它放在一个case里面搞定，
🏆

帮我下载 Tina Huang 最近 10 个视频到本地，下载的视频按照里面介绍的产品来整理到对应文件夹。然后给每个视频生成带有时间轴的文字记录的doc文件，最后给我设计一个合理的观看顺序

QoderWork识别到我本地已经安装了yt-dlp（视频下载）的skills，它就这样kukuku完成了任务，

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCib8ttgwiaYW9HlbybcCC6pdjicotoXujAszpSmVUwUaeqL5ls2y5Xvj4cg/640?wx_fmt=png&from=appmsg)

做出来的文字总结和学习路线也分别存在各自的文件夹了，桌面Agent能跟本地目录交互的优势还是很大的。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXnJibu74ceOqib989YkiaB1jCiba4KcOZqgibfuZOP4DPysIAPux47sh5uXsiah4ELek5OthOF5RU5A2g7Q/640?wx_fmt=png&from=appmsg)

这两天高频率地使用Clawdbot和QoderWork，

也理解了为什么Clawdbot会突然爆火。

我们都希望有这样一类Agent帮我们完成更多的事情：

它不只限于代码。

它能拥有我们的账号权限。

它活得就像我们真正意义上的替身。

但我觉得其实可以不纠结于工具本身。

我身边有很多朋友一直在催我做Clawdbot的各种安装教程，有的买了Mac mini，有的装了云服务器，装了总觉得有点不知道问啥。

今天我挑战用QoderWork去完成ClwadBot的任务，是想告诉大家，

我们之前接触到的Claude Code和CoWork依然有很大的潜力，

不要给工具设限，

尝试先用现有的，熟悉的东西去完成未知挑战

相信AI的潜力，

相信我们自己。

@ 作者 / 卡尔

最后，感谢你看到这里👏如果喜欢这篇文章，不妨顺手给我们*点赞｜在看｜转发｜评论 📣*

如果想要第一时间收到推送，不妨给我个星标🌟

如果你有更有趣的玩法，欢迎在评论区和我聊聊🤝

更多的内容正在不断填坑中……

![image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXmCDLEEW1wClZOVGFURjmibJmciaYLNhp0N55Y6mPiaCj01eV8yzACqDvWDhicbPm07Wu7bboATuKgAbA/640?wx_fmt=jpeg)
