---
标题: "Claude Opus 4.6和GPT 5.3 Codex同时更新，这波贪了，应该留到春晚再看的"
链接: "https://mp.weixin.qq.com/s/USIxq6xU28aJU2q0z-dpMw"
作者: "[[卡尔的AI沃茨]]"
创建时间: 2026-02-08T10:22:34.277Z
摘要: |
  文章分析了Anthropic发布的Claude Opus 4.6和OpenAI发布的GPT-5.3-Codex两款AI模型，重点比较了它们在性能测试、应用更新和安全方面的特点。
tags:
  - "AI模型"
  - "性能对比"
  - "应用更新"
  - "安全防护"
  - "技术分析"
字数: 4973
状态: "未开始"
总结: |
  本文详细对比了Claude Opus 4.6和GPT-5.3-Codex的发布情况：
  - **性能测试**：Claude Opus 4.6在MRCRv2和GDPval-AA测试中表现优异，提升了记忆和知识任务能力；GPT-5.3-Codex在编程和视觉桌面操作（如OSWorld-Verified）上大幅提升，融合了编码和推理优势。
  - **应用更新**：Anthropic更新了Claude产品线，包括Claude Code的agent teams、Excel的规划模式和PPT的research preview；OpenAI展示了GPT-5.3-Codex构建的游戏案例，但未提供API。
  - **安全措施**：两家公司都加强了安全防护，Anthropic采用可解释性方法和网络安全探针，OpenAI则通过话术识别规则降低滥用风险。
  - **其他方面**：文章还提到了定价、API更新（如Claude的自适应思考功能）和用户对模型迭代的期望变化。
---

# [[Claude Opus 4.6和GPT 5.3 Codex同时更新，这波贪了，应该留到春晚再看的]]
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

AI圈迎来了新年的第一个双响炮啊，

Anthropic刚发了Claude Opus 4.6，OpenAI也发了GPT‑5.3-Codex，在Codex app里已经能用了。我这稿子写一半直接重新写啊。马上来看看这两模型的评分，它们强化了那些点，以及除了模型本身，还带来了什么更新。

先看跑分。

Anthropic是第一次给Opus系列模型上100万tokens的上下文窗口，在MRCRv2八针1M （大海捞针）测试里，比Sonnet 4.5高了57个点，我第一反应就是我一定要在clawdbot体验一把Opus 4.6。

除了记忆好，Opus 4.6在GDPval-AA（44个不同岗位的知识工作任务）上也超了GPT5.2 200多分，感觉Cowork又可以升级一波了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/VNz1x8bH8FxMsz4WuJfUibiav8AoOYicgrf81TxIjREHBCkulu1RN0KyEDbMcgWzYXN2LwIGwu0cXh6Xk4fp36ymlE3N8icNgEzTwRgw9gvRfEY/640?wx_fmt=png&from=appmsg)

隔壁的GPT‑5.3-Codex定位是个编程模型，融合了GPT-5.2-Codex的编码性能和GPT-5.2的推理能力及专业知识，速度提升了 25%（codex有救了），离谱的是OSWorld-Verified（视觉桌面操作）上提升了快30个点，

夯爆了。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/VNz1x8bH8Fw8YDZKtzicBw90UHz2G9SeR3ic6iaqAceaGypMkPibvbiauzU4YvEibVbExcTGd4lLp2Hib3QiaGLd7emdFZicS9bMr86aI5YCd0WVl0YY/640?wx_fmt=png&from=appmsg)

我仔细对比了一下两张官方表，发现它们重合的数据集只有一个，Terminal-Bench 2.0，是在终端命令行里进行编程的测试。光看这个评分，GPT-5.3-Codex可以说是把Claude Opus 4.6给拉爆了，高了12个点。

其他展示出来的数据不能直接拿来硬比，

SWE-Bench（Agent编程）数据集人OpenAI用的是Pro版本，包含了四种语言。Claude Opus 4.6测评的SWE-Bench Verified只测试Python。

OpenAI测试OSWorld-Verified比Claude Opus 4.6测的OSWorld测评出来的分数会更加可信，因为Verified修复了300多个数据问题。

还是来看看它们单个都更新了啥，

Claude Opus 4.6还在高难度Agent 搜索（DeepSearchQA / BrowseComp）上单 Agent比GPT-5.2 Pro多6个点，在多学科推理（Humanity's Last Exam / ARC AGI 2）上，同样是工具配置拉满的状态下，比GPT5.2Pro多了3个点。

![Image](https://mmbiz.qpic.cn/mmbiz_png/VNz1x8bH8FygiaQ2Fjl5ovDsbmoicbxRNfXO3BKDKskEx7NoHkXaDn3TZiaGcicn7rF5ZSJJzTXNBEZjO6yYlc4Qw9gHxAr0bibhSGl42Ay9Qe1Q/640?wx_fmt=png&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_png/VNz1x8bH8FxicK1vB2iaNhwWab7Sq9u23pewGa9h9paibejEPrq1CwufnCetRGYSRwoc8ib386fMgU5jsGRJhQGCrr5tFtCsGT29ckibHvzop9DA/640?wx_fmt=png&from=appmsg)

GPT-5.3-Codex有个指标高到离谱，

OSWorld-Verified（视觉桌面操作），

用人话说就是让AI看截图换成各种电脑任务，人类基准是72%，GPT-5.2-Codex是38.2%，GPT-5.2是37.9%，

融合这个两个模型的优势的GPT-5.3-Codex直接干到64.7%，跟这个比起来，其他的SWE-Bench Pro（Agent编程），Cybersecurity Capture The Flag Challenges（Agent安全攻防）和SWE-Lancer IC Diamond（修bug赚100万挑战）的5，6个点的提升都是常规操作了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/VNz1x8bH8FwZCYqkH7ZWsianzLsLzCBO3GqXADetzIPOVYDwRqibJR27uSy9nCicGPCR5vPfricJVakib7aVOrrHoDxq7iaEfRibZgVjE4A6iajkQiao/640?wx_fmt=png&from=appmsg)

再来看看应用案例。

Anthropic这次都没有放出Claude Opus 4.6跑的case，而且选择把自家产品线更新了，

Claude Code新功能agent teams（智能体团队），可以让多个Agent并行工作，适合用在像大规模代码检查之类可以被拆成很多个独立子任务的场景。

Claude in Excel也更新了，更新了规划模式，还能给乱七八糟的非结构化数据，自动做一个合适的表格结构。

还给PPT新出了 research preview，Claude能识别公司品牌的ppt模版，保证布局，字体，颜色都不会变，能针对单张幻灯片简化文本和添加图表，也可以一次性生成10张幻灯片再微调。

![Image](https://mmbiz.qpic.cn/mmbiz_png/VNz1x8bH8FxMhb2w2cZZhnKzsZj5z0upLcuicVbrUaAtibLHQibxCvxTLeIrrLRART2icXDvnrrAE0op0EBeesPfWIhO82wx4HSJJTkYRJHnzP4/640?wx_fmt=png&from=appmsg)

OpenAI把更多时间放在showcase上，

他们放了两个用GPT-5.3-Codex构建的新游戏，但没有像GPT-5.2-Codex那样把完整提示语放出来。

🔗 https://cdn.openai.com/gpt-examples/7fc9a6cb-887c-4db6-98ff-df3fd1612c78/racing_v2.html

两个游戏我都完整打了一把，这个赛车真的不是抄马里奥赛车的吗，道具箱里还有泡泡和香蕉。

🔗 https://cdn.openai.com/gpt-examples/7fc9a6cb-887c-4db6-98ff-df3fd1612c78/diving_game.html

潜水我也玩了，本来是想当个超人，一口气潜到最底的，但是潜到一半就体验到为什么神秘园会说，那些专业人士潜进去就出不来了。。。

他们还放出来一个我觉得很蠢的网页case，理由是GPT-5.3-Codex做这个价格页面的时候，会把年费展示成打个折的月费，而不是总金额。。。

奥特曼没活了可以去咬个打火机

关于API和定价，Anthropic这次给API加了Adaptive thinking（自适应思考），由Claude 来判断什么时候打开thinking模式。

还有四档Effort（努力程度）可选，默认是high（高），还有low（低），medium（中）和max（最大）。

还有一个beta功能，当长期对话或者Agent任务快到打到上下文上限的时候，会自动把上下文压缩成摘要，用摘要替换上下文。价格我做成表格了，

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/VNz1x8bH8FxgTPTeRx758YsNKxsLzcicMIq78moseIYm1wyFg2LrNeUVQbjnwRFyicr8NNXqfXQeDQhw1NibQ4Rjsxt3dvTq7QcnUtoyhO1JtY/640?wx_fmt=png&from=appmsg)

GPT-5.3-Codex还没有API，不过在app，CLI，IDE插件and网页版都能用了，上线就全量，这很不openai。

说句题外话，api形式的gpt4o一周后就没了，这波属于是时代的眼泪了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/VNz1x8bH8FwcAHl5RibEsMLCB1npIB0m455CyqLcfNdxa9gzNeJ1r8CxTMl3REicicb95iaurKYhYxibAuNb4JdNuA7vFibJ0WIxhwyxb1UHXaiciaM/640?wx_fmt=png&from=appmsg)

最后说说安全。

这次两家都花了不小的篇幅来谈安全问题。我们还是用人话来解读一下。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/VNz1x8bH8FzcxcShiaT1zNURGcnwE8cibHKejJicY0ZkuGfEmKyWMC2bvRVc2eZQmibzlb3TXISs2TgcNQ5CrwCXEOry6Q8l8kT9hJc2WMEIln0/640?wx_fmt=png&from=appmsg)

Anthropic上来先亮了个图，说这次升级没有影响我们模型的安全性，这段时间我们做了两件事。

第一件事，努力搞清楚模型脑子里到底在想什么。

他们在做一种可解释性的新方法，目标是让研究人员能看见模型为什么会在某些情况下给出某种回答。这样做的好处是，很多问题在标准测评里不一定暴露，但当你能追到原因，就更容易提前发现风险，比如模型在某些边缘场景会突然变得很会误导人。

第二件事，在模型擅长的领域加了更严的防护。

他们发现 Opus 4.6 在网络安全上能力更强，能修bug，也能拿去攻击。所以他们做了六个新的网络安全探针，用来检测模型有没有在输出可能被滥用的内容。

隔壁OpenAI在安全上也下了苦功夫，

他们现在给开源项目免费做体验，把一些熟悉的坏套路整理成话术识别规则，当我们给gpt发的问题跟某个套路很像的时候，模型就会自动降低问答的详细程度。

这次模型更新后，

明显感觉我的预期值变高了，以前更新模型我通常还会去测一下文本，代码，3D的表现，

但现在随着Claude Code，Cowork，Clawdbot三连击，我对于模型的表现处于薛定谔的猫状态。

太简单的测起来没意思，

我们现在用Claude Code加一些模型，

也能够做到这样的上限。

太复杂的，我想以Agent的形式，

放到我们已有的工作流里长时间来评估它的差异。

说不定后面模型的更新会成为一种日常的迭代，

发布会也不开了，

开始卷Agent形态了，

我就一个愿望，

别光跟整理桌面较劲了，

我桌面都快没文件了。

@ 作者 / 卡尔

最后，感谢你看到这里👏如果喜欢这篇文章，不妨顺手给我们*点赞｜在看｜转发｜评论 📣*

如果想要第一时间收到推送，不妨给我个星标🌟

如果你有更有趣的玩法，欢迎在评论区和我聊聊🤝

更多的内容正在不断填坑中……

![image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXmCDLEEW1wClZOVGFURjmibJmciaYLNhp0N55Y6mPiaCj01eV8yzACqDvWDhicbPm07Wu7bboATuKgAbA/640?wx_fmt=jpeg)
