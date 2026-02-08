---
标题: "我把新版Claude Code的上手门槛降到小学二年级，有豆包就行"
链接: "https://mp.weixin.qq.com/s/kKU8otnN0l9kbaAj7pC24g"
作者: "[[卡尔的AI沃茨]]"
阅读星级: 3
内容类型: "技术教程"
创建时间: 2026-02-08T12:20:40.568Z
摘要: |
  本文介绍了一种利用AI助手豆包简化Claude Code和OpenCode安装配置的方法，旨在解决传统安装教程复杂、API不稳定等痛点，提供稳定使用一年的解决方案。
tags:
  - "AI编程助手"
  - "Claude Code"
  - "OpenCode"
  - "API管理"
  - "技能库"
字数: 6995
状态: "未开始"
总结: |
  文章主要内容包括：
  1. **安装痛点分析**：指出现有安装教程众多但复杂，强调利用AI（豆包）简化流程，实现“小学二年级都能装”的低门槛目标。
  2. **核心工具推荐**：
     - **OpenRouter**：作为API模型市场，支持支付宝支付，价格透明，可集成现有API Key，提供免费模型（如小米、DeepSeek等）。
     - **Claude Code与CC-Switch**：通过豆包辅助安装，CC-Switch用于可视化管理多模型API（如GPT、Gemini、Claude等）。
     - **Skills管理**：介绍如何为Claude Code添加技能库（如GitHub社区技能），支持自定义Skill创建（使用skill-creator工具）。
     - **Cursor IDE**：作为补充工具，支持支付宝订阅，用于文件调整和开发记录。
     - **OpenCode**：作为开源版Claude Code，提供安装命令和插件（oh-my-opencode）配置，但警告避免使用反代等不稳定方法。
  3. **工作流整合**：推荐组合使用Claude Code（项目代码）、Cursor（单个文件）和OpenCode（模块修bug），实现稳定高效的开发环境。
  4. **未来展望**：预告将分享如何将链接转化为可迭代的提示语，并鼓励读者参与Skills需求讨论。
---

# [[我把新版Claude Code的上手门槛降到小学二年级，有豆包就行]]
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

现在搜Claude Code，OpenCode的安装教程，

没个八万也得有个七千篇，

为什么还要来写一篇主打稳定用一年的教程呢？

我觉得都有AI了，复杂大段的安装指令就应该让AI去跑，所以这次我把官方的安装指南都打包给豆包了，不管你是什么系统，不管你安装遇到什么问题，都可以彻底跳过复制粘贴，拍照为难豆包。

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxLwanBz5ibTycHicxrgxYsTlTZibmVc0qhlsUp5PnYZDH7tVicHJp3Rw1nQ/640?wx_fmt=jpeg&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxaSdaj4jibIt2HlsicicwXuocY6oHwagySmxRZRWpe8jCR0jnvbZd4UHqw/640?wx_fmt=jpeg&from=appmsg)

🔗 https://doubao.com/bot/stIy6xcY

我想要解决的是平时遇到的痛点，包括支付，切换不同模型和skills，新版本更新等，而且要做到没有门槛，小学二年级能可以装，不担心Claude会不会抽风封号，也不需要担心用不上最新版。

我还有点贪心，稳定版Claude Code和备选版OpenCode都想要，大家如果对更加详细的操作感兴趣的，不妨给在评论区吐槽吐槽安装遇到的痛点。我看到的话，应该会做一个长视频出来。

先来说说常规四件套Claude Code，cc-switch，OpenRouter，Cursor，很多人卡手的第一步甚至都不是安装Claude Code，而是没有稳定的API

我用的是OpenRouter，它是一个API模型市场，更像一个把一堆模型供应商的API统一起来的入口。这跟那些中转API有本质区别，那些中转更像是替你绕路，拼车，代刷的灰色通道。

很多人到现在都不知道，OpenRouter的API是可以用支付宝买的，完全不需要国外的银行卡。

OpenRouter的价格逻辑非常透明，不会在模型本身的价上加价，底层模型供应商怎么定价，它就按那个价走。它赚的是你充值时候的平台手续费，用信用卡之类的会收5.5%的手续。

它还有一个对工作流特别友好的玩法，就是我可以把已有的API Key，比方说OpenAI、Anthropic的Key存到OpenRouter里用，所以我才有信心说配置一次用一年。

而且OpenRouter上面有大量的免费模型，像小米，DeepSeek，GLM，还有Qwen，在里面都有免费版本。它每周还会更新模型的使用排行榜。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxiabbqx8Gds9Qauz3W7fvmzsRumGH0GOqhNndsDXWH82xRVicJ3yzUH7w/640?wx_fmt=png&from=appmsg)

很多时候我用中转API的痛点在于波动太大，为了便宜，开了很多1:10，1:20的中转，在很多不同的网站上都充了，结果年底发现利用率只有30%。

OK，当搞定充值并新建了一个API Key后，你就已经成功了99%，剩下1%就是当一个无情的复制黏贴机器了。

我们现在就来安装Claude Code和cc switch（这个用来管理不同模型的）。

不用搜任何安装教程，直接在豆包助手里提问，并说明你的电脑系统即可，毕竟我们要做到小学二年级的难度，可以参考一下我这段话，
🌅

我的电脑是苹果，要安装Claude Code和CC switch，还要把openrouter api key配置到cc swich，然后用上gpt gemini claude glm kimi minimax 六家模型！

还有很多朋友不知道在自己的电脑上怎么打开终端并运行这些命令，这些也是可以为难豆包的。

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxhEQlqrqI4682MHGYZWwicwPEs6BPwvgfapcDBGJqLUP6Sr99omFfvVg/640?wx_fmt=jpeg&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxWPuGVqrvSicMgs8yCqAtwyupnbbls8lERI7WWkicAXBo01dPibuJoyY2Q/640?wx_fmt=png&from=appmsg)
CC-Switch可以管理模型，Skills和MCP，属于是一鱼多吃，

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwx87Iyr3KgMPxjYRfVJspVWa4QNXEDVr0aQVFGeoCrUEPrCuic1KACzicA/640?wx_fmt=png&from=appmsg)

使用方法非常符合直觉，还是可视化界面，

同时支持Claude Code、CodeX和Gemini CLI的API管理。你只需要像我那样，每次启动之前选择想要的API供应商，这样当你启动Claude Code的时候，配置的模型就已经顺便切换过去了。

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxP2TKMufPPuGRgRljH9JuByGnr2DJdYPAgEKmbfSKmW26csy89qOEZA/640?wx_fmt=jpeg)

这时候我们就可以接入Skills了。

人话说就是给Claude Code用的技能书，

不同于普通提示语只是文本，Skills像一个知识库文件夹，里面可以放规范，脚本，模板，参考资料等等，Agent会在需要的时候自己去翻阅。那Skills有没有小学二年级都能学会的用法呢？

当然有！你可以直接让Claude Code读取下面这两个链接里所有的Skills，然后告诉它你的需求，让它帮你看看社区里有没有已经造好的轮子。
⚽

读取下面网页里面所有的 Skills，当我给你提出我的需求之后，匹配最合适的，并且返回它的链接。https://github.com/anthropics/skills

https://github.com/ComposioHQ/awesome-claude-skills

如果喜欢在GUI页面上选的，时不时给自己的CC找一门技能书学学的话，也可以到这里，

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxWTI5kR6a7jFQ5KxUu0YUby164453mXKe3nbA0BdCjaKACkjHuJghDA/640?wx_fmt=png&from=appmsg)

🔗 https://skillsmp.com/

有4911页。。。

所以更多时候我是自己新建一个 Skill。新建Skill不需要从零开始，可以先安装一个叫skill-creator的技能，它是来帮助我们设计新技能的，在Claude Code上运行，

`安装这个skill，skill项目地址为: https://github.com/anthropics/skills/tree/main/skills/skill-creator`

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxUKqDgUJ7TNVF6Cvyrt8KdaY9W6ZSUMbhunuEPUgIFRqSuH0BibZ6GMg/640?wx_fmt=png&from=appmsg)

比方说我复刻一下目前社区热度第一的前端设计的 Skills，我就可以对它说，

使用skill-creator帮我设计一个Skill。这个Skill在我创建前端页面的时候，能够保留复杂度和美学，设计出一个非常有创造力、以文字表达和渐变色为主体的网页。我还需要加上一些纯CSS和HTML实现的动画，增加一些点缀色，使用更加出人意料的字体，并且实现一些简单的鼠标悬停交互效果。

（纯语言输入就是要为难claude code）

中间是不是会弹出选择，默认选yes就行。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxAzbUkTicDz2R24iaOIw3kSaHBEjpG7WsiafkYFxxHfqfD0w4ibYicwkRvJw/640?wx_fmt=png&from=appmsg)

而且现在 ClaudeCode 有热加载模式，也就是说生成完Skills后，直接就能使用都不需要重启。

把API，Claude Code，CC-Switch和Skills都配置好了后，我还是会推荐你装一个Cursor。

Cursor作为一个IDE可以补充Claude Code的不足，比方说调整单一文件，或者做一个开发进度的记录等等，

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxdH5SqFfouc1jmoHaZdgbFW0ia4o7HiaE0AC2IxyIiavVchDTTmzQwHo2w/640?wx_fmt=png&from=appmsg)

当然还有一个大点，Cursor同样可以用支付宝订阅。在支付界面选择美元，就会出现支付宝选项，还是免税的，比直接用银行卡还便宜。。。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwx3vAF1wG78FiaUhCkZNkUiar35DoazLzcM7ibZGpiciaYaWDgId7ib27mJicZA/640?wx_fmt=png&from=appmsg)

OK，那我们已经有了最稳定的方案了，我还想再贪心一点，把OpenCode也加进来。mac有三种不同类型的安装命令，我目前测下来这个最稳定。

curl -fsSL https://opencode.ai/install | bash

第一次用的时候输入/model，就可以选上免费的模型了，用免费的模型安装最后一个插件，

oh-my-opencode

少了它opencode都不能叫开源版Claude Code

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxsMecv3IRuN5Oy9dfbicqjth2PrxQZf81Ih54kcSEN3YZoCPhuSJMlcQ/640?wx_fmt=png&from=appmsg)

直接在OpenCode 的界面运行这一行命令就行了，模型会给你安排妥妥的。
🌅

按照这里的说明进行安装和配置 https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/refs/heads/master/README.md

中间会问你三个问题，

有没有Claude Pro/Max的订阅？有没有GPT订阅？会用Gemini 模型吗？

按照实际回答就是，我就是No，Yes，Yes

安装的时间比较长，可以先玩着claude code再等opencode安装。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxxoaBGGia2MvOF7ibpLSHGAgZPPR4ahdrFhWRLbpLZzfQbPP71hym6rOg/640?wx_fmt=png&from=appmsg)

看到这个界面的话，你就剩最后一步，登录GPT

运行opencode auth login，这里不能在opencode界面上运行，要打开一个新的命令行窗口，如果没有自动打开浏览器窗口的话，也可以点开下图左侧界面你看到的链接，照样可以成功登陆。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwx8SMXn7CBS3bY510pS8lgWOmIIwufKJdEVNV4t2wnZSEcYVOyiaGoe3A/640?wx_fmt=png&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxPw9pxtGZ2CVNwibGaxX3TLiclm4F5kanLLzC9AiaknsOqmAJ8qSHT0d3Q/640?wx_fmt=png&from=appmsg)

如果你是Gemini Pro的话，需要装一个插件opencode-antigravity-auth，把Antigravity（Google IDE）里面的Gemini 3 Pro和Claude Opus 4.5的额度薅来用。

但最近失败的人太多了，也太多被封号了，这种在opencode登陆后使用原本账号额度的技术实现就叫反代，我真心不建议用。

稳定方法的话我还是推荐openrouter用gemini，毕竟OpenAI的Codex是直接宣布支持OpenCode的，Google的态度没摸不清，万一给我封了，我的notebooklm里的项目不就全白弄了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwx02AF70lrricFQRK1uT4vyGy1BRRO68HBMAflvOfzLWMONDdsNiazU0EA/640?wx_fmt=png&from=appmsg)

全程豆包辅助下，这套也就花半个小时，就已经有稳定版Claude Code和开源版Claude Code了，

也解锁了终极形态，项目代码用Claude Code，单个文件用Cursor，项目模块和修bug用opencode，四舍五入就是codex，相当舒适，基本不会有三个使用入口都同时挂的情况。

![Image](https://mmbiz.qpic.cn/mmbiz_png/YEhakvKZjXkpqbdoOanrbs1lRhKIjFwxCRpQKPNgIqhgy2LfoibCRvPV8EtXzaFrOJ5vN27rPlSoURRdpblqicdA/640?wx_fmt=png&from=appmsg)

最后的最后，

我做出的豆包CC版还可以帮你省点API的费用，开发项目之前先把idea口述出来放给它，它可以做一个类似Claude Code Plan模式的提示语出来，

打磨完这一篇的话，

我终于可以跟大家分享一下怎么把平时保存后就再也不会打开的链接们通通转成能流动的提示语，

这套提示语是可以根据喂给它的知识库和对话记录迭代的，而且因为有本地文件兜底，就算超出上下文或者Claude Code项目损坏了也不影响，

更不会出现网页版用GPT的时候对话记录过去比较久，文件失效的情况，

属于是又给自己挖一个大大大大的坑，

凌晨两点继续开写，

希望有燃起大家玩Agent的热情，

快来催更！

有什么想要的skills都可以！

@ 作者 / 卡尔

最后，感谢你看到这里👏如果喜欢这篇文章，不妨顺手给我们*点赞｜在看｜转发｜评论 📣*

如果想要第一时间收到推送，不妨给我个星标🌟

如果你有更有趣的玩法，欢迎在评论区和我聊聊🤝

更多的内容正在不断填坑中……

![image](https://mmbiz.qpic.cn/mmbiz_jpg/YEhakvKZjXmCDLEEW1wClZOVGFURjmibJmciaYLNhp0N55Y6mPiaCj01eV8yzACqDvWDhicbPm07Wu7bboATuKgAbA/640?wx_fmt=jpeg)
