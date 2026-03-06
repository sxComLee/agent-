---
标题: "OpenClaw多Agent实操：5个AI当着你的面分工协作，全程透明不黑箱"
链接: "https://mp.weixin.qq.com/s/xLzHLwFDP9j8BWezHut-0g"
作者: "[[林月半子的AI笔记]]"
阅读星级: 4
内容类型: "技术教程"
创建时间: 2026-03-02T14:17:36.989Z
摘要: |
  本文介绍了在Discord平台上构建多AI Agent协作的‘灵系军团’方案，通过单渠道多账户模式实现透明化、可干预的实时协作，并提供了详细的配置教程。
tags:
  - "AI Agent"
  - "Discord Bot"
  - "多Agent协作"
  - "OpenClaw"
  - "自动化工具"
字数: 12559
状态: "未开始"
总结: |
  本文深入探讨了AI Agent协作的两种模式：飞书的‘分身术’（单渠道单账户）和Discord的‘独立团’（单渠道多账户）。作者重点介绍了后者，即‘灵系军团’，它通过多个独立Bot账户在同一个频道中实现全透明的协作，强调协作可见性而非后台静默效率。
  
  **关键要点：**
  - **架构设计**：采用同频群聊模式，包括一个总指挥（灵统）和多个专家角色（如灵谋、灵工），通过广播机制和上下文穿透实现协作。
  - **配置步骤**：详细讲解了从Discord Bot创建、账号绑定、路由配置到权限设置的完整流程，包括避坑提醒。
  - **实战演示**：展示了模糊指派和精准委派两种场景，验证了军团的决策力和执行精度。
  - **价值主张**：强调这种模式虽然配置较重，但提供了组织管理层面的价值，适合需要透明协作和过程干预的场景。
  - **推广内容**：文章末尾推广了付费交流群，提供更深入的配置模板和社区支持。
---

# [[OpenClaw多Agent实操：5个AI当着你的面分工协作，全程透明不黑箱]]
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

关注 「**林月半子的AI笔记**」，设为「**星标**」我是林月半子，帮你用AI和自动化工具，「**提升10倍工作效率****」！**

![Image](https://mmbiz.qpic.cn/mmbiz_jpg/OYSztZEeXwnU4YYYUoiazgN8PswtTCO17VsIrpGo6icR6EZ3nCehqDib1X7dzibxII5CcWQSYg1iaWficEzj738XAaImeO7Obu2RNzphb12tlxyDE/640?wx_fmt=jpeg&from=appmsg)

上一篇[关于飞书多 Agent 的教程](https://mp.weixin.qq.com/s?__biz=MzU4MjY5NTc4OQ==&mid=2247498755&idx=1&sn=912ecb0ecc89cd97d00feb57b6f067f2&scene=21#wechat_redirect)发出来后，很多朋友已经跑通了“一号多用”的模式。后台有位硬核老哥跟我聊深了，他抛出了一个很尖锐的观点：
🙋

AI 时代，既然 Sub-agent 已经能实现后台静默协作，为什么还要追求那种‘全员出镜’的重型方案？把流程拆解成步骤不就行了吗？把 Bot 全拉进一个频道，万一它们聊偏了怎么办？

这确实代表了目前 AI 圈的一种主流认知：追求极致的极简和效率。

但我最近在 Discord 上调试了一套全新的“灵系军团”阵列，带给我的震撼是颠覆性的。

![Image](https://mmbiz.qpic.cn/mmbiz_png/OYSztZEeXwkfPfUSEn6zGQicmJ3GduSkabGG5lRyvDJmjRzmM08WOAM8f00k1Z98Zju0qKunlkys5ba4BIovbjltKXt7yxsvlp2wT4NzyGib0/640?wx_fmt=png&from=appmsg)

在正式分享配置之前，我想先帮大家理清两种完全不同的“大模型统帅学”：

飞书篇的“分身术”：单渠道单账户

这是我之前教大家的入门打法：一个机器人分身服务所有 Agent。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwnHp2NOh2kdVeRqj4iabECHRlIBFQrwY9mDdgciatCuTQI4EibOFyicZetnHXcN107cGicQev66KL52CjOZ8Eic9o3UokLgpWRID4icN0/640?wx_fmt=png&from=appmsg)

逻辑：通过 binding 规则按群 ID 路由，让同一个机器人在不同群里扮演不同角色。

特点：用户只需要面对一个 Bot，配置极简，适合个人日常轻量办公。

Discord 篇的“独立团”：单渠道多账户

这是我最近在 Discord 尝试的硬核打法。一个专家角色对应一个独立 Bot 账户。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwntMOVe67XCuxjNDEn68yylD756WwtDLiaZWr61enCo0wg6jUsAqK4CUbTIj6TBfwKhbV6we6bU6ABsDSmpOEBrYx3f6BwQgYiac/640?wx_fmt=png&from=appmsg)

逻辑：在同一个频道里，灵统、灵谋、灵工等 5 个专家全员在线，身份边界极度清晰。

价值：这种模式虽然“重”，但它实现了“同频群聊协作”。当你看到军师出方案、工程师秒接代码、创作官同步写推文时，那种全透明的协作张力，是后台静默模式永远给不了的。

技术没有绝对的优劣，只有场景的适配。

如果你已经玩腻了“单 Bot 分身”，想体验那种指挥一支 AI 军队、看着它们在频道里实时穿插协作的快感，那么今天这篇“单渠道多账户”的实操指南，就是为你准备的。
## 核心架构：同频群聊模式

不同于传统的后台调用（sessions_send），我们的“灵系军团”采用的是全公开的广播机制。

![Image](https://mmbiz.qpic.cn/mmbiz_png/OYSztZEeXwls2Xo8wweF37UHvw5V5zWoicjCicqB0esxNia4EpmTagZ39BfMUHibegOwXELhBEbXZHarH1KLDYN4AShHIs3ZuB7ICI6F9nqH0VA/640?wx_fmt=png&from=appmsg)

很多人第一眼看到这个架构会想：5个 Bot 为啥不平等协作，非要多一个"灵统"？

答案很简单——平等协作听起来民主，实际上是灾难。

每个 Bot 都在判断"这句话是在叫我吗"，结果就是要么全部抢着回，要么全部装没听见。

灵统就是那个"拍板的人"，任务进来先过它，它说派给谁就派给谁，其他人只管把自己的活干漂亮。

- 每一个角色都是独立实例：灵统、灵谋、灵工等在后台都是独立的 Agent 进程。
- 环境全感知：通过 sessions.visibility: "all"，打破会话隔离，实现上下文穿透。
- 精准唤醒：利用 Discord 的 <@BotID> 原生提及，精准点名对应专家。

当然，也有朋友会问：既然 OpenClaw 本身支持 Sub-agent，为什么还要搞这么重的多账户方案？

这个问题问得好，我也明牌回答：Sub-agent 和多账户军团，解决的根本不是同一个问题。

Sub-agent 本质上是后台静默执行，任务拆解、流程推进，用户看不见过程，只拿结果。这种模式效率高、Token 省，我自己平时也在用，没什么问题。

但这篇文章的核心不是"效率"，而是"协作可见性"。当你需要向客户演示、向团队展示、或者自己想看清楚每一步决策是怎么发生的，那种全透明的同频协作才有价值。就像公司开会，你当然可以让秘书背后协调，但有时候你就是需要把相关人拉进来、当面把事说清楚。

两种模式没有对错，只有场景不同。如果你追求极简高效，Sub-agent 够用；如果你想要透明协作、过程可干预，这套方案才是为你准备的。
## 实操配置### Step 1. 账号绑定与路由配置 (bindings)

要组建独立团，第一步是去 Discord 开发者门户，给每个角色申请一份“入职通行证”。
#### 1、建立总部：创建应用

访问 https://discord.com/developers/applications，点击 New Application。

应用名称：建议统一前缀，如 灵统、灵策。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwnGejl2UgnyscialVqzWhPkibOicAaoAkoGa132M96auDgtMWH2se0S2b6AuvtpRwJxib8ibx0cfQ8cicT2t1CLrJ9s12n866l35e7Q4/640?wx_fmt=png&from=appmsg)
#### 2、核心：开启 Bot 的“感知能力”

在左侧 Bot 页面，这是最容易出错的地方。

务必勾选以下两个 Privileged Gateway Intents，否则你的机器人会变成“聋子”和“瞎子”：

- ☑ SERVER MEMBERS INTENT
- ☑ MESSAGE CONTENT INTENT（关键！不开启它，Bot 无法读取消息内容）。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwl2uH9EPXibNqDd6IgdFxMaCV2iaTPvNo2ROiaq4JEBbh4Py8QrtgPjTSJngh1JDnpI4v1uT2kFwic8pKTaP6QdVkFVZYbVuLPgSlI/640?wx_fmt=png&from=appmsg)
#### 3、领取令牌：Reset Token

点击 Reset Token 并保存那串密钥。

![Image](https://mmbiz.qpic.cn/mmbiz_png/OYSztZEeXwk9nNCX8FzgM8170iahvrr0ibKwPDfMm9oS5vCPibZeA68WNwD4a8DjSficrzCpcbM5HJUUjBQYzhjUibuEMfIRo1MqibyTy4EJZ88nY/640?wx_fmt=png&from=appmsg)

这是 Bot 的唯一身份证，后面会用到。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwmGNpFSYgMWN4dE1JPrG27X8pGicLbYxFLibpbkib8bt1vJaHAALBvjHgpvgSOhkOgjkTNxUXXHhe3blglWYG4l9IiaOkr1mn2L4I4/640?wx_fmt=png&from=appmsg)
#### 4、邀请入群：OAuth2 URL 生成

在 OAuth2 -> URL Generator 中勾选 bot

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwnL6mechCwxHq3YK4HaRGJZ7wG21R3ib9rzd5sAickcYp4yuHUWuNoL8oXX28J2ywo7UaykLxQsTXH2skJ8DMl1B7McialzadiaG0Y/640?wx_fmt=png&from=appmsg)

并在下面的 Bot Permissions 勾选必要权限

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwkcibSzncBGuK4woWb7asW4OiaTSZ16f9BvD521DAwWHMKoHHCsHG5eKibibKqsSCrJdnglSg4Tjq1MNaww3HbpwYgYpSVH7L45xJo/640?wx_fmt=png&from=appmsg)

复制最底部的链接，在浏览器打开并邀请 Bot 进入你的私有服务器。

![Image](https://mmbiz.qpic.cn/mmbiz_png/OYSztZEeXwkJPrXjibw25NzcVmaokJQGljoZZbNL43SwhP5uu0rOCMTsn1JNSa55jbQrykibc3NSvN05Prd1wYTbrKCFz8fhzwYXALGDtIGhU/640?wx_fmt=png&from=appmsg)

会自动弹出下面的界面，邀请这个机器人到你的服务器。每个账户都有自己的服务器，选上就好了。

![Image](https://mmbiz.qpic.cn/mmbiz_png/OYSztZEeXwlA1HWibibZShxNQf8XdajOBdKicGyvl6H9ria4RCasrpNuVH6tm49tGx3J5fjDe9eT035j4Yb8wzyEaq4XtmOEY2ISFZVIPmkk3mg/640?wx_fmt=png&from=appmsg)

![Image](https://mmbiz.qpic.cn/mmbiz_png/OYSztZEeXwlZhU1PzwQibmFCUbZze5uCs21SPEiaw64flibKxngXLCiaURxChCTst8FuXKHexJhqiaDAiaiaib5wGcyLbJfDvzzib9ApdKpJMNrBsrvY/640?wx_fmt=png&from=appmsg)

最后点击授权即可。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwmwRRglSgXpMc4NictwUjt7F8RRSkG46GBldLcFCXaBia8iaX4PyIibzEX4x0ZQiadiaSFHD5WZmQ2IhOic03CskFuqeRcmWhJepXkxIk/640?wx_fmt=png&from=appmsg)

剩余 4 个应用做同样的操作。
### Step 2. 招募你的“灵系”员工 (Agent & Workspace)

拿到 Token 后，回本地终端通过 openclaw 命令行一键生成它们的“物理办公室”。建议为 5 个角色创建独立的 Workspace 目录，实现真正的物理隔离。

你可以依次执行以下命令：

```
# 1. 招募总指挥 (ds-lingzong)openclaw agents add ds-lingzong --model zai/glm-4.7 --workspace ~/.openclaw/workspace-ds-lingzongopenclaw agents set-identity --agent ds-lingzong --name "总指挥"# 2. 招募军师 (ds-lingce)openclaw agents add ds-lingce --model zai/glm-4.7 --workspace ~/.openclaw/workspace-ds-lingceopenclaw agents set-identity --agent ds-lingce --name "军师"# 3. 招募工程师 (ds-linggong)openclaw agents add ds-linggong --model zai/glm-4.7 --workspace ~/.openclaw/workspace-ds-linggongopenclaw agents set-identity --agent ds-linggong --name "工程师"# ... 依此类推，完成灵文、灵核的招募
```

执行完这些命令，你的 ~/.openclaw/ 目录下会多出 5 个以 workspace- 开头的文件夹。这种物理上的隔离，正是防止 AI‘神经错乱’的关键。

一个完整的 Agent 身份证包含：

- Workspace (工作区)：它的个人办公室。存放 SOUL.md、AGENTS.md 等核心灵魂文件。
- AgentDir (状态目录)：它的身份证。记录认证信息和模型配置。
💡### 验证环节

执行完后，你可以打开 ~/.openclaw/openclaw.json。如果你看到 agents.list 里已经整整齐齐排好了 5 个独立的 ID 块，说明你的军团已经“入驻”成功，只等下一步的路由绑定了。
### Step 3. 部署通信枢纽 (Config 路由)

这一步的目的是告诉 OpenClaw：当 Discord 上的“灵工”收到消息时，请把它交给本地 ds-linggong 这个 Agent 处理。

你需要打开 ~/.openclaw/openclaw.json，在 bindings 数组中添加以下映射关系。请务必核对 accountId和 agentId：

```
"bindings": [{    "agentId": "ds-lingzong",   // 对应 Step 2 创建的本地 Agent ID    "match": {      "channel": "discord",      "accountId": "lingzong"   // 对应 Step 1 中你给 Token 起的名字    }},{    "agentId": "ds-lingce",    "match": {      "channel": "discord",      "accountId": "lingce"    }},{    "agentId": "ds-linggong",    "match": {      "channel": "discord",      "accountId": "linggong"    }},{    "agentId": "ds-lingwen",    "match": {      "channel": "discord",      "accountId": "lingwen"    }},{    "agentId": "ds-linghe",    "match": {      "channel": "discord",      "accountId": "linghe"    }}]
```
#### 林月半子避坑提醒：
- ID 必须对齐：这里的 accountId 必须和你 channels.discord.accounts 里的键名完全一致。
- 多账号并行：如果你发现某个 Bot 在 Discord 说话但没有触发本地 Agent 的工作流，优先检查这一步的映射是否写反了。
### Step 4. 开启白名单与“指挥权限” (Channels & Tools)

这是很多硬核玩家最容易“翻车”的地方。要让这支军队在同一个频道里同频协作，需要调整三个核心。
#### 1、完善账号配置 

有了 Token 只是完成了连接，我们还需要在 openclaw.json 中定义每个账号的“行为准则”。

我们要通过 guilds 配置，实现细粒度的安全隔离。这不仅能防止 Bot 被误触发导致的 Token 浪费，还能确保你的“灵系独立团”只在指定的作战区域（频道）活动。

找到你 openclaw.json 中的 channels -> discord -> accounts 层级，按以下结构进行补全：

```
{  "channels": {    "discord": {      "enabled": true,      "allowBots": true,   // 【重点】不开启它，子 Bot 会直接无视指挥官发出的任何指令      "actions": {        "reactions": false,        "messages": true,        "threads": false      },      "accounts": {        "lingce": {// 对应 Step 1 中你定义的账号别名          "token": "你的 Bot Token",          "groupPolicy": "open",          "guilds": {            "你的服务器ID": {// 你的 Discord 服务器 (Guild) ID              "requireMention": true,// 【安全】必须艾特才响应，防止 Bot 间对话死循环              "users":[              // 【严谨】白名单：只听你和其他 4 个 Bot 的指令                "10xxx82958147727380",// 你的 User ID                "14xxx43858064736276",// 灵工 ID                "14xxx61375416139888",// 灵文 ID                "14xxx72214902640650",// 灵核 ID                "14xxx05066569617551",// 灵统 ID                "14xxx16397117587527"// 灵策 ID (自己也要加，用于识别自己的消息)              ],              "channels": {           // 【精准】指定授权频道，防止 Bot 在闲聊区刷屏                "频道ID": {"allow":true}              }            }          }        }        // ... 其他 lingzong, linggong 等账号按此结构依次配置      }    }}}
```

这就是开头那位老哥担心的聊偏问题的答案。
#### 再踩一个坑：
- allowBots 必须为 true：在 OpenClaw 默认逻辑中，为了防止死循环，Bot 是不理会 Bot 的。但在军团模式下，指令是由“灵统”发出的，如果不打开这个总开关，子 Agent 就会集体装聋作哑。
- 为什么要加 users 列表？ 在多 Bot 同频模式下，灵统发出的指令也是一条消息。如果不把灵统的 ID 加入白名单，灵策就会认为那是陌生人说话而拒绝执行任务。
- 关于 channels 的配置逻辑：在 OpenClaw 中，如果你不写 channels，默认是监听全服；但只要你写了一个，就意味着进入了“白名单模式”，其他没写的频道都会被屏蔽。
- 关闭 reactions：是为了防止 Bot 间互刷表情包导致意外触发，确保它们只盯着 message 文本干活。
💡

如何获取这些长串数字 ID？在 Discord 开启开发者模式后，右键点击目标‘复制服务器ID/复制频道ID/复制用户 ID’即可。
#### 2、赋予通信能力 

为了让“灵统”能给其他专家“发派任务”，你需要开启 agentToAgent 权限：

```
"tools": {  "agentToAgent": {    "enabled": true,    "allow": ["ds-lingzong", "ds-lingce", "ds-linggong", "ds-lingwen", "ds-linghe"]  }}
```
#### 3、打破信息孤岛

这是实现“全员全知全能”的底层逻辑。为了让子 Agent 们能听懂指挥官的指令，必须打破会话隔离，实现上下文穿透。

```
"tools": {  "sessions": {    "visibility": "all" // 【灵魂开关】让所有 Agent 共享频道内的全量上下文  }}
```
💡

为什么必须开？

如果不开启 all，当你艾特“灵工”干活时，它只知道你艾特了它，却看不见前面“灵策”出的方案和“灵统”的要求。开启后，每一个 Bot 都能感知到频道里发生的一切，就像大家坐在一张圆桌前开会，信息的流动是透明且实时的。
### Step 5. 配置识别信号 (Mention Patterns)

最后，也是最磨人的一步：配置识别信号。我们要给每个 Agent 换上一双“顺风耳”，让它们在复杂的群聊环境中精准捕捉到属于自己的指令。

请找到你的配置文件，在 agents -> list 下找到对应的 Agent ID，并按以下结构修改它的 groupChat 配置：

```
{  "agents":{    "list":[      {        "id":"ds-lingzong",// 找到你 Step 2 创建的 Agent ID        "name":"ds-lingzong",        "identity":{"name":"总指挥"},        "groupChat":{          "mentionPatterns":[            "<@!?1474005066569617551>",// 【核心】Discord 原生 ID 匹配（最稳健）            "灵统",                     // 【增强】昵称或简称唤醒词            "1474005066569617551"       // 【兜底】纯数字 ID 匹配          ]        }      }      // ... 其他灵工、灵策、灵文、灵核按此格式依次修改    ]}}
```
## 终极实战

配置完成后，这支“灵系军团”到底好不好用？我测试了两种完全不同的统帅逻辑。
### 场景一：模糊指派，考验“灵统”的决策力

如果你比较懒，或者任务目标很明确，你只需要对“大脑”发号施令。
💭

我的指令：

@灵统 启动‘灵系极简协作’！我想发个朋友圈，主题是‘深夜还在折腾 OpenClaw 终于跑通了’。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwl0LsRI7khu20CtpYsLmpiaZsCO6EPia0ADbOpg1LVV9Fgsp5FuibPD8FGd0UEUqVqqMeTXxr5Lv9okeWTOT7uF1JY25JgpS3c5Qc/640?wx_fmt=png&from=appmsg)

军团表现：

“灵统”收到指令后，瞬间完成任务拆解。它判断该需求核心在于“内容创作”，于是直接点名委派“灵文”接手，并贴心地给出了“真实感+小成就感”的风格建议。 随后，“灵文”秒出列，一口气提供了“简洁成就感”、“略带调侃”、“极简有力”三个版本供我挑选，甚至连配图建议都准备好了。这种无需多言、一击即中的默契，正是“灵系”大脑的魅力。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwnENfpz2HnVoxn9plpOudhG2PwgRVMxArH0wKPVicvpasbTuXVfO6icVf7c4AeW7Eria2rH7oab2w6icP7K46xo2toVLNSibrB2HXkc/640?wx_fmt=png&from=appmsg)
### 场景二：精准委派，考验军团的执行精度

如果你对产出有特定要求，可以直接在指令中排兵布阵。
💭

我的指令：

@灵统 启动‘灵系极简协作’！我想发个朋友圈，主题是‘深夜还在折腾 OpenClaw 终于跑通了’，请：

1. 1.灵策：帮我定一个文案风格。
2. 2.灵文：根据军师定的调性，写出两段文案。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwlicXT6kWg3wljFOQaKxFx1gHBd94PqlrC2o5RuNmz6ul8yd5h68VibpABRzN1bOQPjyanE4HZTVmicPnuyVicyvA2EzEg6EB4tVibQ/640?wx_fmt=png&from=appmsg)

灵统迅速完成分工调度。

![Image](https://mmbiz.qpic.cn/mmbiz_png/OYSztZEeXwmLgc8xrWr1W2WhlKnxARAtl75jpibwtswQBVVfMR4cbxQibvKuh8yXPFFboLBVh8ppatX95CEU5fSONRk7xojsGaRngYZogSXnw/640?wx_fmt=png&from=appmsg)

随后，“灵策”出列定调。

紧接着，“灵文”展现了惊人的全感知能力——它不仅听到了我的指令，还精准地捕捉到了刚才“灵策”在频道里定的“凡尔赛”调性，丝滑地完成了后续创作。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwmhndQC6FT3dE0nmL4hnWlMia7bApyTL3vB4iaTicq5FDdEKMTxiaW8kNem8a0lCSWXV9kTKXGqSLwc26Fz8PeUyTqWjIXPCfx2x5Q/640?wx_fmt=png&from=appmsg)

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/OYSztZEeXwnIUZ9g19LUf5EBwr7WhohEHoGPkDw7IWI9oRW2Hg12Xcva0qHviawK6TIl89WL6rpp5nYkvaDd0yXIsEk0iaRwxiaaVGDpY0d8ek/640?wx_fmt=png&from=appmsg)

这种所见即所得的协作，你可以在过程中随时打断或修正，每一个 Bot 都能实时感知你的最新反馈。
## 写在最后

搞定“灵系军团”，你手里握着的不再是冷冰冰的代码，而是一支随时待命的 AI 军队。

虽然这种模式消耗的 Token 更多、配置更重，但它带给你的“同频协作感”和“组织设计力”，才是真正值钱的东西。

很多人觉得多 Agent 是技术问题，但搞完这套我才意识到，它本质上是一个组织管理问题——你在设计的，是一个会思考的AI团队。

AI 时代，一个人就是一支军队。

我好奇的是，你的“灵系独立团”拉起来后，你准备派它们去攻克的第一个高地是什么？

如果你想少走弯路、直接拿到完整的配置模板，往下看👇

看到这里，你大概已经感受到"灵系军团"的威力了。

但很多朋友跑到这一步会发现——配置文件搞定了，Bot 也上线了，但每个 Agent 的"灵魂"还是空的。SOUL.md、IDENTITY.md、AGENTS.md 这些核心人格文件怎么写，直接决定了你的 Agent 是"听话的工具"还是"真正的专家"。

这部分我整理了一套完整的配置模板，在「OpenClaw 小龙虾实战交流群」里会陆续分享。

群里都是真正在跑的人，大家互相交流踩坑经验，少走很多弯路。99元/人，付费是为了筛掉凑热闹的，留下真正想干的人。

感兴趣的私信我，备注「龙虾」。

![Image](https://mmbiz.qpic.cn/mmbiz_png/ZFDQVGCJicKCjR7FfZaM69l3HTM2uw80VI5I8lHbiap4FV9ZGJvgNYI6icoPzLr4FM3RglD8PRoy9m8ljpaduy1oQ/640?wx_fmt=png&from=appmsg&wxfrom=5&wx_lazy=1&tp=wxpic#imgIndex=25)

感谢看到这里 👏

觉得有用的话，点赞 👍 / 在看 👀 / 转发 🫱 / 评论 📣

星标 ⭐ 一下，下次更新不迷路
