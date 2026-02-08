---
标题: "Skills商店来了：5万人在用的Top 10热门Skills，我帮你试了一遍"
链接: "https://mp.weixin.qq.com/s/Cv2OtWDqnQg2thh4BqAIPw"
作者: "[[花叔]]"
阅读星级: 4
内容类型: "技术教程"
创建时间: 2026-02-08T12:35:07.029Z
摘要: |
  文章介绍了由Vercel创建的Skills社区市场skills.sh，拆解了Top 10 Skills的功能和适用人群，并推荐了额外实用的Skills，强调其对于开发者和非开发者的价值。
tags:
  - "AI工具"
  - "Claude Skills"
  - "技能市场"
  - "技术分享"
  - "自动化"
字数: 6499
状态: "未开始"
总结: |
  文章详细分析了skills.sh这个Skills社区市场，主要内容包括：
  - **skills.sh简介**：由Vercel创建的开放Skills索引和分发平台，提供一键安装功能，解决用户不知如何使用Skills的问题。
  - **Top 10 Skills拆解**：分为开发者专用（如vercel-react-best-practices、web-design-guidelines）和所有人都能用的Skills（如frontend-design、agent-browser、seo-audit），后者特别适合产品、运营、设计师等非技术用户。
  - **额外推荐**：包括23个营销Skills的仓库（coreyhaines31/marketingskills）、宝玉老师的中文友好Skills（jimliu/baoyu-skills）和Anthropic官方的文档处理四件套。
  - **实用建议**：根据岗位选择Skills、避免安装过多、注意来源安全、先试用再深入理解，并强调通过模仿热门Skills来学习创建自己的Skills。
  - **价值总结**：skills.sh降低了Skills使用门槛，社区筛选确保了质量，是学习和应用Skills的有效途径。
---

# [[Skills商店来了：5万人在用的Top 10热门Skills，我帮你试了一遍]]
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

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHYFcFzYwaexCYRrx6FuribpvBcAxz4CQfia7h76yKcrJqlRYiawnWcfkWXLv7gPYicaZEiboHwWHiaibdFpw/640?wx_fmt=png&from=appmsg)

> 发现了一个Skills社区市场，安装量最高的skill已经37000+。我把Top 10都装上了，给你拆解一下。

说起来，Skills这个话题我写过好几次了。

[【万字长文】Claude Skills完全指南：从概念到实战](https://mp.weixin.qq.com/s?__biz=Mzg2OTA1OTAxNA==&mid=2247487935&idx=1&sn=b687a77de3fc04720c8257fbd35a8510&scene=21#wechat_redirect)

[关于Claude Skills，我给你写了份82页的白皮书](https://mp.weixin.qq.com/s?__biz=Mzg2OTA1OTAxNA==&mid=2247487659&idx=1&sn=d5b420e923c494302e2898db7cfdc9a9&scene=21#wechat_redirect)

这两篇文章和对应的白皮书可以说从概念到实战讲了个遍。但始终偏方法论，讲的是"怎么理解、怎么自己创建"。

最近发现了一个新东西：**skills.sh**。

简单说，就是Skills的应用商店。别人把工作经验打包成Skill，你一键安装就能用。

我第一反应是：终于有靠谱的做这个了。

之前用Skills最麻烦的就是要自己写。虽然我说过"让AI帮你写"，但前提是你得知道自己要什么、能把需求说清楚。

但很多人压根不知道Skills能干嘛，也不知道有什么好用的可以参考。

skills.sh解决的就是这个：让你先用起来，再说。
## skills.sh是什么

skills.sh是一个开放的Skills索引和分发平台，**由Vercel创建**。

网站底部写着"Made with love by Vercel"。Vercel是硅谷知名的技术公司，很多大型网站都用他们的服务，我自己的静态网站部署也都是通过Vercel。他们愿意做这个平台，说明Skills这个方向被认可了。而且大厂出品，平台本身也靠谱。

当然，这也解释了为什么排行榜前几名都是Vercel自家的Skills——自家平台嘛，自然有先发优势。但内容确实可以。

界面很简单：一个排行榜，按安装量排序。点进去能看到每个Skill的描述、来源、安装命令。

安装方式是一行命令，复制粘贴到终端就行：

```
npx skills add vercel-labs/agent-skills
```

我花了几分钟，把排行榜前10的Skills全装上了。一共安装了55个Skill（因为有些仓库包含多个）。

下面我逐个拆解，**会特别说明哪些对非开发者也有用**。
## Top 10 Skills拆解

先说个整体情况：Top 10里7个是给开发者的，3个对产品、运营、设计师也有用。

我把值得详细说的挑出来讲，其他的列个表就行。
### 开发者专用的（7个）

这7个都是给写代码的人用的，非开发者可以直接跳到下一节。
排名Skill安装量干嘛用的1vercel-react-best-practices37600+React/Next.js性能优化，57条规则2web-design-guidelines28500+检查网页是否符合设计规范3remotion-best-practices18800+用代码做视频的最佳实践5skill-creator3700+官方出的，教你怎么创建Skill6building-native-ui2700+Expo手机App开发指南8better-auth-best-practices2300+登录认证系统最佳实践10upgrading-expo2200+Expo框架升级指南

这些Skills来自Vercel、Anthropic、Expo等官方团队，质量都不错。做前端的话，第1、2个基本必装。
### 所有人都能用的（3个）⭐

这3个是我觉得Top 10里最值得说的，不写代码也能用。

**frontend-design（7500+安装）**

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHYFcFzYwaexCYRrx6FuribpvYHicibZ2uJmmv1VtM7ml7zZ1WqGBCLI16AWZd3jV0raIWKq3bYiar8FUg/640?wx_fmt=png&from=appmsg)

来自Anthropic官方。目标很简单：让Claude做出来的东西别那么"AI味"。

你可能有过这种体验——让Claude帮忙做个网页或PPT，出来的东西能用，但没特色，一眼就知道是AI做的。这个Skill就是治这个的。

它明确告诉Claude**不要用什么**：

- 不要用Inter、Roboto、Arial这些"标准字体"（太没个性）
- 不要用紫色渐变配白底（AI最爱用，已经烂大街了）
- 不要用对称布局（打破常规才有设计感）

同时告诉Claude**应该怎么做**：

- 选择有个性的字体
- 配色要有主次，主色大胆、强调色锐利
- 动效要克制，一个精心设计的页面加载动画，比到处都在动更高级

这个Skill好在"反套路"。Claude其实懂什么是好设计，但它容易偷懒。这个Skill就是逼它动脑子。

**agent-browser（2700+安装）**

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHYFcFzYwaexCYRrx6FuribpvtysAPF0Nu9ia23ibPdMicH7HHdCxiaSA84m4icLjahgFJs84Uv98LFTagzA/640?wx_fmt=png&from=appmsg)

这个Skill不太一样，它不是"知识库"，而是"工具"。装上之后，Claude可以帮你操作浏览器：

- 自动打开网页、点击按钮、填写表单
- 批量截图
- 自动登录网站（保存登录状态，下次直接用）
- 录制操作过程

**举个例子**：你是运营，每天要登录5个平台查数据。以前要一个个打开、登录、截图。现在可以让Claude帮你自动完成，最后把截图整理好发给你。

**再比如**：你是产品经理，想看竞品的某个功能在不同页面的表现。Claude可以自动打开这些页面、截图、整理成文档。

这个Skill说明Skills不只是给程序员用的。自动化网页操作，运营、测试、产品都能用得上。

**seo-audit（2300+安装）**

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHYFcFzYwaexCYRrx6FuribpvunMMI8kde4GpxF3ZpiarDWC4P2stuwusPsCjOXQxxBoxIlibMGF0aKsQ/640?wx_fmt=png&from=appmsg)

终于来了一个纯运营向的Skill。

这是一个完整的SEO审计框架，让Claude帮你检查网站的SEO健康度：

1. 能被Google找到吗？（爬虫能不能访问、有没有被收录）
2. 网站快不快？（加载速度影响排名）
3. 内容优化了吗？（标题、描述、关键词布局）
4. 内容质量够不够？（是否值得被推荐）
5. 有没有可信度？（外链、权威性）

每个维度都有具体的检查清单。Claude会给出：问题是什么 → 影响多大 → 怎么修 → 优先级。

做网站的都能用。不需要懂技术，直接问Claude"帮我审一下SEO"就行。
## 额外收获：23个营销Skills

Top 10里大部分是开发向的，但别急。

我在安装过程中发现了一个宝藏仓库：**coreyhaines31/marketingskills**。

这个仓库有23个营销相关的Skill，从文案到定价到投放都有：

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHYFcFzYwaexCYRrx6FuribpvtGYV4miaocrrVWKjVLsSTbkt70H7MlOumwQ2Sao6l6yHfGaDao6OIpg/640?wx_fmt=png&from=appmsg)
Skill功能适合谁copywriting营销文案写作市场、运营copy-editing文案润色修改市场、运营pricing-strategy定价策略设计产品、创业者launch-strategy产品发布策略产品、市场seo-auditSEO诊断运营、独立开发者ab-test-setupA/B测试设计产品、运营page-cro落地页转化优化运营、增长signup-flow-cro注册流程优化产品、增长email-sequence邮件营销序列市场、运营social-content社交媒体内容市场、运营paid-ads付费广告投放市场referral-program推荐计划设计增长、产品marketing-psychology营销心理学市场、产品

安装命令：

```
npx skills add coreyhaines31/marketingskills --yes
```

一次性装23个。

**我的看法**：做产品、运营、市场的，这个仓库比Top 10更值得装。
## 熟悉的名字：宝玉老师的Skills
![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHYFcFzYwaexCYRrx6Furibpv5NnGeOW5jfrDiccRr1Qp30h91TZWOUonyTHcLMJCejzB1xTX4GTD7jg/640?wx_fmt=png&from=appmsg)

翻Top 100的时候，发现了一些熟悉的名字——**宝玉老师**（@dotey）的Skills。

宝玉老师是X上的AI大V，经常分享Claude Code的使用心得。他把自己的工作流打包成了一堆Skills，放在 `jimliu/baoyu-skills` 仓库：
Skill功能安装量baoyu-slide-deck幻灯片生成972baoyu-article-illustrator文章配图938baoyu-cover-image封面图生成868baoyu-xhs-images小红书图片841baoyu-comic漫画生成822baoyu-post-to-wechat发布到微信752baoyu-post-to-x发布到X725baoyu-infographic信息图生成480

这些Skills对中文用户特别友好——小红书图片、发微信、文章配图，都是我们平时会用到的。

安装命令：

```
npx skills add jimliu/baoyu-skills --yes
```

**额外建议**：装了之后，可以去X上翻翻宝玉老师的分享。他经常讲这些Skills为什么这么设计、踩过什么坑、怎么改的。想自己做Skill的话，看他的分享挺有帮助。
## 还有一个：文档处理四件套

Anthropic官方仓库（anthropics/skills）里有4个文档处理Skill：

- pdf —— PDF读取、提取、合并
- docx —— Word文档处理
- pptx —— PPT生成和编辑
- xlsx —— Excel处理

这几个所有人都能用。装上之后让Claude帮你处理文档，会顺手很多。

安装命令：

```
npx skills add anthropics/skills --yes
```
## 为什么你应该去看看skills.sh

说两个实际的好处。

**第一，这些Skill确实有用**。

skills.sh上排名靠前的，都是被大量vibe coder实际装过、用过的。37000+安装不是刷的，是真有人在用。

这些人天天用Claude Code写代码、做产品，他们愿意装，说明确实有用。

跟着装就行。不用自己判断"这玩意到底行不行"，社区已经帮你筛过一遍了。

**第二，这是学习Skills最好的方式**。

很多人看了我之前的文章，知道Skills是啥了，但还是不知道怎么下手——自己的Skill该怎么写？

最好的学习方式不是啃文档，是**看别人怎么写的**。

装几个热门Skill之后，让Claude Code帮你解读：

> "帮我读取并解释 ~/.agents/skills/seo-audit/SKILL.md 的实现逻辑"

Claude会告诉你：

- 这个Skill的触发条件是怎么写的
- 指令是怎么组织的
- 为什么要这样分层
- 哪些设计可以借鉴

看3-5个写得好的，你就知道了：

- Skill该怎么组织
- 好的Skill长啥样
- 自己的工作流怎么打包

**从模仿开始，比从零开始容易多了。**

所以我建议：先装、先用、先看，再想自己要不要做。
## 几个实际建议

**1. 根据你的岗位选择**

- 开发者：vercel-react-best-practices、anthropics/skills
- 产品经理：seo-audit、marketingskills仓库、agent-browser
- 设计师：frontend-design、web-design-guidelines
- 运营/市场：marketingskills仓库（23个全装上）

**2. 别贪多**

我装了55个是为了写这篇文章。平时用的话，选3-5个高频的就够了。

装太多，Claude启动时要加载的东西多，还是会影响上下文的。

**3. 注意来源**

Skills可以包含可执行脚本，所以要看谁发的：

- ✅ anthropics/skills（Anthropic官方）
- ✅ vercel-labs（Vercel官方）
- ✅ 框架官方（expo/skills等）
- ⚠️ 个人仓库谨慎点

**4. 先用再说**

不用完全搞懂原理，先装一两个用起来。

用过才知道好不好。
## 最后

skills.sh出来之后，用Skills变简单了。

以前得自己写，现在直接装别人的就行。而且不只是程序员能用——营销、产品、运营，都有对应的Skills。

去skills.sh看看，找一两个和你工作相关的装上试试。

比如你是运营，装个seo-audit，然后问Claude："帮我审计一下我们的官网SEO"。

比如你是产品，装个pricing-strategy，然后问Claude："帮我分析一下我们产品的定价策略"。

试过就知道好不好使了。

哦对，虽然上面给了你怎么安装这些skills的代码，但其实最佳实践还是你直接把这篇文章，以及把skills.sh的网址丢给Claude Code，用自然语言让他帮你选择及安装就好了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHYFcFzYwaexCYRrx6FuribpvEmKibhDg5FRTomwibqichEr8xI9icLlibOknpMk7icOXWtNBHJZkw676oQ6Q/640?wx_fmt=png&from=appmsg)

enjoy～
