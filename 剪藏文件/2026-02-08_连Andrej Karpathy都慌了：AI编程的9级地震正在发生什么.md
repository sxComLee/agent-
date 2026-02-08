---
标题: "连Andrej Karpathy都慌了：AI编程的9级地震正在发生什么"
链接: "https://mp.weixin.qq.com/s/4UL1kjGlWxiKrUINafAVYQ"
作者: "[[花叔]]"
阅读星级: 4
内容类型: "琛屼笟鍒嗘瀽"
创建时间: 2026-02-08T12:19:27.801Z
摘要: |
  本文讨论了AI编程时代带来的职业重构，通过分析Andrej Karpathy的推文和评论区反应，探讨了程序员如何应对新技术栈的挑战，并分享了个人的实践经验与建议。
tags:
  - "AI编程"
  - "职业重构"
  - "技术趋势"
  - "程序员技能"
  - "工具比较"
字数: 5424
状态: "未开始"
总结: |
  文章围绕Andrej Karpathy的推文展开，他表达了对AI编程时代感到落后的焦虑，提到了15个新概念如agents、prompts等，这些在18个月前大多不存在。评论区出现两极分化：一些人（如外行或前端边缘型）感到能力提升，而另一些人（如传统精英型）则难以跟上。作者结合自身每天12小时的AI编程经验，分析了不同AI工具（如Claude Opus 4.5、OpenAI Codex）的优缺点，并强调context管理、接受不确定性和组合使用工具的重要性。文章最后将程序员分为四类（外行、前端边缘型、传统精英型、固执抵抗型），并给出应对建议：保持好奇、学习编排而非仅写代码、避免抵抗新技术。核心观点是，AI编程正在引发职业地震，优势在于深度理解这个“没有说明书的外星工具”。
---

# [[连Andrej Karpathy都慌了：AI编程的9级地震正在发生什么]]
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

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHbjKd111LsPRbuEBfgHqgsKhYe1KRPWVZyuGibEk3IKGl9Z2aCyd3q2IeaGopUAlXaFj2nK5JGLeyQ/640?wx_fmt=png&from=appmsg)

9小时前，Andrej Karpathy发了条推文，说他"从没感觉自己这么落后过"。

就是那个Karpathy——OpenAI联合创始人、特斯拉前AI总监、Stanford CS231n的创建者、"vibe coding"这个词的发明人。

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHbjKd111LsPRbuEBfgHqgsKZj8RU5PdZqu9u3BYn7HAGCLH5eHtZ3ww8NHic18GFp8I5ibiaeIpmoghg/640?wx_fmt=png&from=appmsg)

他说的原话是：

> "I've never felt this much behind as a programmer."

我看到这条的时候，正好刚结束一天12小时的AI编程。说实话，第一反应是：连他都慌了？
## Karpathy到底说了什么
![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHbjKd111LsPRbuEBfgHqgsKuvRZzvPtUiaE9Y6r2jTFjYUY6FsSL8sGL5mGYm5bQtXq1Asibmtzov1Q/640?wx_fmt=png&from=appmsg)

他的完整推文是这样的：

> 作为程序员，我从没感觉自己这么落后过。这个职业正在被剧烈重构，程序员贡献的部分变得越来越稀疏。我有种感觉，如果能正确串联过去一年出现的这些东西，我能强10倍。而没能获得这个提升，明显是skill issue。现在有一个新的可编程抽象层需要掌握（在原有的那些层之上），涉及agents、subagents、prompts、contexts、memory、modes、permissions、tools、plugins、skills、hooks、MCP、LSP、slash commands、workflows、IDE integrations...还需要为这些本质上随机的、会出错的、不可理解的、不断变化的实体建立一个全面的心智模型——而这些东西突然和传统的工程混在了一起。显然，某个强大的外星工具被分发了出来，但它没有说明书，每个人都得自己摸索怎么拿、怎么用。与此同时，9级地震正在撼动这个职业。撸起袖子，别掉队。

数了一下，他提到了15个AI编程时代的新概念：agents、subagents、prompts、contexts、memory、modes、permissions、tools、plugins、skills、hooks、MCP、LSP、slash commands、workflows、IDE integrations。

这些东西，18个月前大部分还不存在。
## 评论区炸了

这条推文下面的评论特别有意思，两种截然不同的声音：

**一边是"从没觉得自己这么强"：**

Ian Patrick Hines，一个做前端的政治技术顾问说：

> "作为一个一直在代码边缘的人（会前端不会后端），我从没觉得自己这么有能力追上。我感觉自己什么都能做，唯一的限制是想象力。太刺激了。"

更夸张的是一个叫RidgetopAi的地板销售：

> "我是个地板销售，10个月前我连Windows终端都打不开，更不知道ls -la是什么。现在太好玩了！感觉自己内心有什么东西被解锁了。"

**另一边是"根本追不上"：**

有人说："everyone has to come to terms with the fact that there is no catching up, in the long run"（长远来看，每个人都得接受一个事实：没有追上这回事）。

还有人说："man if even andrej karpathy is feeling this way how are the rest of us supposed to keep up"（连Karpathy都这样，我们普通人怎么跟得上）。

**最有意思的是Aakash Gupta的分析**：

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHbjKd111LsPRbuEBfgHqgsKicicrcXYVE5NlcQjhcgJCSPIpaI032QpPHkqLgMk3neNNOpaHxdyZmyQ/640?wx_fmt=png&from=appmsg)

他是Product Growth领域的专家，有20多万订阅者的newsletter作者。他说：

> "Karpathy真的建造了跑在编程助手里的那些神经网络。他在Stanford教会了全世界深度学习。他领导过特斯拉的AI。如果他都觉得自己'明显落后'...这说明了一切。这条推文的confession是：原始智力和深厚的技术知识不再保证精通。新的技术栈不是关于理解transformer或写优雅的算法，而是关于编排一堆没人能完全控制的随机系统。"

他总结得很到位：**新规则变了，旧精英不一定还是精英。**
## 我的真实体感：每天12小时后的结论

说回我自己。最近三天又在疯狂用AI编程工具，每天12小时以上，大幅迭代了2个产品，开发完了一个接近上万行代码的app。

几个真实感受：

**1、Claude Opus 4.5确实是目前最强的**

Karpathy说要为"fundamentally stochastic, fallible, unintelligible"（本质上随机的、会出错的、不可理解的）的系统建立心智模型。这话没错，但不同模型的"随机程度"差很多。

Opus 4.5稳得一批，在Claude Code和Cursor里都好用。它的"随机性"是可控的——你大概能预期它会做什么，不会突然给你整一堆莫名其妙的东西。

**2、OpenAI Codex情况特殊**

内置的gpt-5.2-codex模型，选high及以上的思考模式时，后端开发能力巨好。能跑的时间无比长，经常一个任务跑一个多小时，然后完全没有bug。

但速度也是真的慢，思考时间过久。以及审美是真的差，不适合做前端。

**3、Claude Code比Cursor划算很多**

同样用Opus 4.5的话，Cursor跑起来很容易一个项目就花完整个月的用量。Claude Code的计费方式友好很多。

去年大家都在卷AI IDE，今年突然又都在卷终端工具。Claude Code能起来，很大程度上是因为Anthropic有模型优势——他们可以更"无所畏惧"地给模型投喂代码上下文，不用担心成本。

**4、Codex的上下文工程确实更好**

Karpathy提到的15个新原语里，"contexts"可能是最关键的一个。

Codex会很好地进行自动化compact，所以基本上可以在一个窗口下不停布置任务，不用担心任务间干扰或者上下文撑爆。能更沉浸地vibe coding。

Claude Code更适合每个独立任务都新开窗口执行。

**5、多任务并行完全可行**

在Cursor内开多个终端，分别执行Claude Code和Codex，没问题。我有过同时跑5个不同任务，相互没造成任何干扰的情况。前提是任务之间做的内容比较独立。

说实话，我平时写代码时，经常是多个AI工具一起开着。不是哪个最强就只用哪个，而是不同任务用不同模型。

**6、国产模型也能用了**

glm-4.7挺不错的，肯定不如前面说的几个，但也能连续执行一个小时以上的任务。而且它在Claude Code中也能管理多个子agent执行任务。

在这个情况下，很多批量写作之类的任务你甚至不需要写脚本调用API，让glm-4.7+Claude Code去调用子agent批量执行即可，很省事。
## 那个"没有说明书的外星工具"

回到Karpathy说的核心问题：这是一个"没有说明书的外星工具"。

其实没有说明书是好事，比如我从去年开始就做了我的知识星球「AI编程：从入门到精通」，我一个压根不会写代码，没有经过科班工程师训练的人，凭什么还去教别人用AI编程呢？

其实事实情况就是，因为这个产品没有说明书，所以它有丰富的可能性，它的说明书需要最早期的信任者和探索者去建立，而我恰巧信任这正在发生的一切。

所以我拿AI编程工具开发过各种各样的东西，我估计很少有任何工程师比我做得更多了，大致列一列的话，我大概： 上线过几十个网站，开发上架过7个iOS app、微信小程序、鸿蒙app、Chrome插件、VSCode插件，等等等等

AI编程模型在写代码上已经很强了，无论是GPT、Claude还是GLM。真正的差距在于：处理边界情况、理解复杂需求的能力，以及你怎么跟它协作。

评论区有人说得好：

> "The skill now is orchestration not typing faster knowing what to wire together and when."（现在的技能是编排，不是打字更快，而是知道什么时候把什么连在一起。）

还有人说：

> "I've seen several stubborn engineers who think they're too good for LLMs fall drastically behind their peers."（我见过好几个自认为高人一等、不屑用LLM的固执工程师，被同事远远甩在后面。）
## 两种人，两种命运

看完评论区，我觉得现在的程序员可以分成几类：

**第一类：外行**

10个月前不会开终端，现在玩得很开心。他们没有"传统工程"的包袱，直接进入新范式。AI对他们来说就是理所当然的工具，不需要"转变心态"。

**第二类：前端边缘型**

像Ian Patrick Hines那样，一直在技术边缘，现在突然觉得什么都能做。AI补上了他们原来欠缺的能力，让他们第一次觉得"完整"了。

**第三类：传统精英型**

深厚的技术功底，对确定性系统有深刻理解。但现在面对"随机的、会出错的、不可理解的"新系统，原有的心智模型失效了。这是Karpathy自己的位置，也是很多资深工程师的位置。

**第四类：固执抵抗型**

"I'm too good for LLMs"。然后被同事远远甩开。

有意思的是，第一类和第二类反而可能适应得最快。因为他们没有"正确的工程应该是怎样的"这个框架要打破。
## 所以该怎么办

Karpathy的建议是"Roll up your sleeves to not fall behind"（撸起袖子，别掉队）。

具体怎么撸？

评论区有人给了个框架：

> "accept pace of creation > my learning pace"（接受创造的速度大于我学习的速度）"stay curious"（保持好奇）"coding is not where the edge is"（优势不在写代码本身）"half of it will be dead, obsolete or abstracted away"（一半的东西会死掉、过时或被抽象掉）"80/20 still applies"（二八定律仍然适用）

我的补充：

**1、别只用一个工具**

不是找到"最强的"然后只用它。而是理解每个工具的特点，组合使用。我现在经常同时开着CodeX、Claude Code和Cursor，不同任务用不同的。

**2、Context是关键**

Karpathy列的15个原语里，contexts可能是最重要的。怎么给AI足够的上下文，怎么管理上下文不爆掉，怎么让多个任务的上下文不互相污染——这些是真正的skill。

**3、接受不确定性**

传统工程追求确定性：你写了什么代码，它就执行什么。现在不一样了，你得学会和"有时候能行有时候不行"的系统打交道。

这不是"容忍低质量"，而是换一种心态：与其追求一次搞定，不如快速迭代验证。

**4、别抵抗**

那些"I'm too good for LLMs"的人，已经在掉队了。

这一年我写了很多AI编程的文章，也看到AI编程切切实实在距离普通人越来越近了。我在想一个问题：当所有人都能用AI编程，你的优势在哪？

现在看来，答案可能是：**你对这个"没有说明书的外星工具"理解得有多深。**

Karpathy说9级地震正在发生。我觉得他说得对。但地震之后，总有人会建起新的城市。

可以的话，成为这个新城市的建造者。

或至少，成为这个新城市的居民，别让自己停滞在地震倒塌的废墟之中。
