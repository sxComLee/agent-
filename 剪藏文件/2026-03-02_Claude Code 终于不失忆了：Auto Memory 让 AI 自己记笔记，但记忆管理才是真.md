---
标题: "Claude Code 终于不失忆了：Auto Memory 让 AI 自己记笔记，但记忆管理才是真正的难题"
链接: "https://mp.weixin.qq.com/s/esRFayxpBipYanhWUPLuYg"
作者: "[[石臻说AI]]"
阅读星级: 4
内容类型: "深度科普"
创建时间: 2026-03-02T14:17:56.513Z
摘要: |
  本文介绍了Claude Code新上线的Auto Memory功能，该功能让AI编程助手能够自动记录项目结构、调试习惯和代码偏好，解决跨会话失忆问题，提升开发效率。
tags:
  - "AI编程助手"
  - "Claude Code"
  - "Auto Memory"
  - "开发者工具"
  - "技术分析"
字数: 5995
状态: "未开始"
总结: |
  本文详细分析了Claude Code的Auto Memory功能，包括以下关键要点：
  - **功能概述**：Auto Memory允许Claude自动将项目信息记录到本地MEMORY.md文件，每次新会话加载前200行上下文，无需手动配置。
  - **双层记忆体系**：区分CLAUDE.md（用户手动维护的指令文件，可共享）和MEMORY.md（Claude自动记录的笔记，仅本地存储），实现指令与记忆分离。
  - **层级结构**：记忆系统从组织到个人分为多个层级，优先级由高到低，支持团队协作与个人偏好管理。
  - **技术细节**：包括存储结构、加载策略（仅加载前200行）、读写时机和开关控制机制。
  - **社区反应**：开发者反应分为三类：兴奋于解决刚需、质疑记忆管理难题（如过时信息处理）和企业级担忧（如本地存储导致的治理问题）。
  - **竞品对比**：相比ChatGPT的对话级记忆，Claude Code的Auto Memory是项目级，更专注于代码层面，且从被动接收指令转向主动积累经验。
  - **使用建议**：建议用户先试用、定期审查MEMORY.md、配合CLAUDE.md使用，并注意200行限制以保持效率。
  - **趋势意义**：标志着AI编程工具从无状态问答向有记忆协作伙伴的进化，但记忆管理挑战仍需解决。
---

# [[Claude Code 终于不失忆了：Auto Memory 让 AI 自己记笔记，但记忆管理才是真正的难题]]
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

点击右上角,设为星标⭐ ,才能接收到实时推送哦

![封面图](https://mmbiz.qpic.cn/sz_mmbiz_jpg/TkWsojtosvRty3EKz4nbycr4TY9hJGfgC6XJ9eK2FMVZfQ1PhLz8euI9rM4KJh2kLJHDTrYRRZcBqlAWYn02uY9COGOTlj6HR40jfX0H58w/640?from=appmsg)

  
  
  

**  石臻说AI报道  **

编辑：石臻

**导读：** Claude Code 刚刚上线了一个让很多开发者等了很久的功能：Auto Memory。简单说，Claude 现在能自己记笔记了——你的项目结构、调试习惯、代码偏好，它会自动记下来，下次开新会话直接用，不用你再重复解释一遍。
## 先说清楚这是什么

Anthropic 的工程师 Thariq 在 X 上宣布了这个功能的全面上线：

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/TkWsojtosvSoEWHkMDNRN3Mib8jehMgZJjSNvuvibkcGG28VBHa4Ml5w8ZDicGABUmJDDrGibPqTdoBUKES8tvwwyeOHsUibEXSBBTUNZ4MTHzyA/640?from=appmsg)

用过 Claude Code 的人都知道，它最大的痛点之一就是"失忆"。每次开新 session，你得重新告诉它项目用什么框架、测试怎么跑、代码风格是什么。项目越复杂，这个重复解释的成本越高。

Auto Memory 要解决的就是这个问题。Claude 会在工作过程中自动把有用的信息记到一个本地文件里——`MEMORY.md`，存在 `~/.claude/projects/<项目名>/memory/` 目录下。每次启动新会话，它会自动加载这个文件的前 200 行作为上下文。

你不需要做任何配置，它默认就是开着的。

![image](https://mmbiz.qpic.cn/mmbiz_png/TkWsojtosvQWTCP6fCLqd1MEYVUwt4sNveyTnOyur3WNgzoY87UJCuzuibo84hfCziaCiaJNkl3y5xphSGJ7eT9G9EJUr9Re3ia7Xm3bO0licQRE/640?from=appmsg)

## 双层记忆体系：CLAUDE.md vs MEMORY.md

这里有个关键的设计区分，Thariq 在后续推文里专门解释了：

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/TkWsojtosvSgLHs4pROxvIzhvlTUkWWgnxvhYSGT8EgMXSW8uyETyVZwdtt0RgSv2f120k196x8G1KfDPHm7trG6J4qFqFPn5F8JpVPG9N8/640?from=appmsg)

**CLAUDE.md 是你写给 Claude 的指令**——项目规范、编码标准、工作流程，相当于你给新同事写的 onboarding 文档。这个文件你手动维护，可以提交到 Git 跟团队共享。

**MEMORY.md 是 Claude 自己的笔记本**——它在工作中发现的项目模式、踩过的坑、你的偏好习惯。这个文件 Claude 自己读写，存在你本地，不进版本控制。

这个分离设计挺聪明的。指令和记忆是两回事：指令是确定性的规则（"我们用 pnpm 不用 npm"），记忆是经验性的积累（"上次那个 API 超时问题是因为连接池没释放"）。混在一起管理会很乱。

## 记忆的层级结构

Claude Code 的记忆系统其实不止两层，官方文档里列了一个完整的层级：

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/TkWsojtosvQbypk7TBKRL0DFrBkft71ebsC5K7f0iazksXQUG68ib69UGXgkqFmpXbpwicNHBjJFHoay2UyaJIGSlhBRy1eW1sVWB5F3ODyGRQ/640?from=appmsg)

层级位置用途共享范围  组织策略`/etc/claude-code/CLAUDE.md`全公司编码规范、安全策略组织内所有人 项目指令`./CLAUDE.md`项目架构、编码标准团队（Git） 项目规则`.claude/rules/*.md`按主题拆分的规则文件团队（Git） 用户指令`~/.claude/CLAUDE.md`个人偏好（全局）仅自己 项目本地`./CLAUDE.local.md`个人的项目特定配置仅自己 Auto Memory`~/.claude/projects/*/memory/`Claude 自动记录的笔记仅自己  从上到下，越具体的优先级越高。组织级别的规则是兜底，项目级别的覆盖组织级别，个人级别的再覆盖项目级别。

这个设计对团队协作很友好。团队共享的东西走 Git（CLAUDE.md + rules/），个人的东西留本地（CLAUDE.local.md + Auto Memory），互不干扰。

## 技术细节：它到底怎么记的？

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/TkWsojtosvRiaiaQoSuG5mHGpBQqFzEcXJIWDwiaFT8HiamBSVDAVFib9xAn9CtEgnNZgVDtnukjLQUjzJfkMmcUfsHADQug4Rr7ZjfLHhlqWwXY/640?from=appmsg)

几个关键机制：

**存储结构**：每个 Git 仓库对应一个独立的记忆目录。MEMORY.md 是入口文件，Claude 还会根据需要创建子文件（比如 `debugging.md`、`api-conventions.md`），MEMORY.md 充当索引。

**加载策略**：只有 MEMORY.md 的前 200 行会在启动时自动加载到系统提示词里。子文件不会自动加载，Claude 需要时才去读。这是个很务实的设计——200 行足够放核心信息，详细内容按需加载，不浪费上下文窗口。

**读写时机**：Claude 在会话过程中随时可能更新记忆文件。你会看到它在工作间隙写入 MEMORY.md，这不是后台偷偷做的，操作日志里看得到。

**开关控制**：用 `/memory` 命令可以切换开关，也可以在 `settings.json` 里设 `autoMemoryEnabled: false` 全局关闭，或者用环境变量 `CLAUDE_CODE_DISABLE_AUTO_MEMORY=1` 强制覆盖。

## 社区反应：兴奋、质疑、和一些真问题

这条推文发出后引发了大量讨论，社区反应大致分三类。

**第一类：终于等到了**

不少开发者之前一直在手动维护类似的记忆系统。有人用 CLAUDE.md 加日志文件手动记录，有人甚至自己搭了一套 JSON 文件追踪项目上下文、失败模式和有效方案：

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/TkWsojtosvQBDxt4xxZn5t6qQmSG7ibmmftiaBricIISAt7RcFJRzqOrDv6vSJqdFYDPnkeYQnxt0A6Jcb0zvCbpQ23grzNdJPqV1cA0ibXDeuM/640?from=appmsg)

![image](https://mmbiz.qpic.cn/mmbiz_png/TkWsojtosvRZRhcFc5gMftOzOwgU0glIWbtzU4jgXOqYhNibO3iceCrwtYjmw030QsDfCJrQVQwvFlZJoqZZicZdwAbY0d1HQpmhnwdEEA9g78/640?from=appmsg)

这说明跨会话记忆确实是个刚需。之前社区里还出现过 Claude-Mem 这样的第三方插件，用向量数据库做持久化记忆，在 GitHub 上很受欢迎。现在官方把这个能力内置了，第三方方案的生存空间会被压缩。

**第二类：记忆管理的难题**

好几个开发者提出了同一个问题：**Claude 知道什么时候该忘记吗？**

这其实是记忆系统最难的部分。三周前的项目上下文如果还在记忆里，被错误地应用到今天的代码上，比没有记忆还糟糕。有人问有没有"衰减机制"来自动清理过时信息，目前看来官方没有提供自动过期功能——MEMORY.md 就是个纯文本文件，Claude 自己决定什么时候更新或删除内容。

这意味着记忆的质量很大程度上取决于 Claude 自己的判断力。用久了之后，MEMORY.md 会不会变成一个臃肿的垃圾场？这个问题目前没有答案。

**第三类：企业级的担忧**

有开发者指出了一个更深层的问题：

![image](https://mmbiz.qpic.cn/mmbiz_png/TkWsojtosvTHyGIsW5Lx9hoDm1icFYcwh9QCE2brJgD2bpD3uwD4ajBhEWtD1sIWGp3FJZrzd8rsdgufdVqfN4FcJE6C94uolhg6u7ZYDTO4/640?from=appmsg)

Auto Memory 是用户级别的，存在每个开发者的本地机器上，没法用 Git 追踪。对个人开发者来说这没问题，但对企业来说，成千上万个开发者的笔记本电脑上散落着自动更新的 .md 文件，这是个治理噩梦。

还有人提出了 Git 追踪的问题：

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/TkWsojtosvTdglpHWQSJsaRCaIUzlYZjTe4ficvI8fpUaXnMmxMSENaDJUqgev1I6jvICL3CZWKAoESEZHYwN9p4XYhJ0MnjiapSm6ZLQtqyA/640?from=appmsg)

CLAUDE.md 可以进 Git，团队共享；但 MEMORY.md 是个人的，不进 Git。那团队成员之间的知识怎么同步？如果 Claude 在 A 的机器上学到了一个关键的调试技巧，B 完全不知道。

说实话，这个问题短期内不好解决。Anthropic 目前的方案是把共享知识放 CLAUDE.md（手动维护），个人经验放 MEMORY.md（自动积累），但两者之间缺少一个桥梁。

## 跟竞品比，这算什么水平？

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/TkWsojtosvTMGFibVia152uZOaQDkwafMefMoy0LYcvaZvr4cnvy9a2pNUDjjlgef72E0Vol6uoFGqUD4eVRxv3WEHhdLzF1VMa93UoSADPDg/640?from=appmsg)

ChatGPT 很早就有了 Memory 功能，但那是对话级别的——记住你喜欢什么风格的回答、你的职业背景之类的。Claude Code 的 Auto Memory 是项目级别的，记的是代码层面的东西：构建命令、测试规范、架构模式、调试经验。

Cursor 有 `.cursorrules` 文件，Windsurf 有类似的配置机制，但这些更接近 CLAUDE.md 的定位——是你写给 AI 的指令，不是 AI 自己积累的经验。

Auto Memory 的独特之处在于：它不是你告诉 AI 该记什么，而是 AI 自己决定什么值得记。这个从"被动接收指令"到"主动积累经验"的转变，是 AI 编程工具进化的一个重要信号。

## 实际使用建议

![image](https://mmbiz.qpic.cn/mmbiz_png/TkWsojtosvRzsZ7tRFt8YVIpIqNia4ZNDxqMsQmxXJ0zQibV8RLPtZuibnTPickQvI0PHsqfK26cjVyldMD3u3Mrjo09vNvLqytXSvccMIPN5vE/640?from=appmsg)

如果你已经在用 Claude Code，几个建议：

1. **别急着关掉它**。先让它跑几天，看看 MEMORY.md 里记了什么。大部分情况下，它记的东西是有用的。

1. **定期审查 MEMORY.md**。用 /memory 命令可以直接打开编辑。删掉过时的信息，补充它遗漏的重要上下文。把它当成你和 Claude 共同维护的项目笔记。

1. **CLAUDE.md 和 MEMORY.md 配合使用**。确定性的规则写 CLAUDE.md（"所有 API 必须有错误处理"），经验性的东西让 Claude 自己记到 MEMORY.md（"上次 Redis 连接超时是因为没设 maxRetries"）。

1. **200 行限制要注意**。MEMORY.md 只加载前 200 行，所以要保持精简。详细内容让 Claude 拆到子文件里去。

Auto Memory 不是什么革命性的功能，它解决的是一个很朴素的问题：让 AI 编程助手不再每次都从零开始。

但它背后的趋势值得关注。AI 工具正在从"无状态的问答机器"变成"有记忆的协作伙伴"。当 AI 能记住你的项目上下文、你的编码习惯、你踩过的坑，它就不再只是一个高级补全工具，而是一个真正在跟你一起成长的搭档。

当然，记忆是把双刃剑。记得越多，出错的可能性也越大。如何平衡"记住有用的"和"忘掉过时的"，这个问题不光是 Claude 要解决的，也是所有 AI 编程工具都要面对的。
## 参考链接

- Claude Code 官方记忆文档：https://code.claude.com/docs/en/memory

  
  

— **完** —

**围观朋友圈查看每日最前沿AI资讯**

![二维码](https://mmbiz.qpic.cn/mmbiz_jpg/kmWVxLDDVAUIIacP7klkMlRmmOaT3TnlIuS57YkwUT0s5ItIDjYaCGSrG8fnYYKrsIx6pyKpsFVibib0vx2ic5Ttg/640?wx_fmt=jpeg)

**一键关注 👇 点亮星标**

**每日科技资讯和提效工具分享**
