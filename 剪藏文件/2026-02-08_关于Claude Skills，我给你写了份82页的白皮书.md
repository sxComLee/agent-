---
标题: "关于Claude Skills，我给你写了份82页的白皮书"
链接: "https://mp.weixin.qq.com/s/ng64TXxCCHCKiDkbh1lj6w"
作者: "[[花叔]]"
阅读星级: 3
内容类型: "技术科普"
创建时间: 2026-02-08T10:58:19.952Z
摘要: |
  本文探讨了Claude Skills功能的核心价值，对比了Skills、MCP、Prompts和Sub-agents的区别，并分享了作者的使用经验和一份白皮书资源。
tags:
  - "Claude Skills"
  - "AI工具"
  - "Token优化"
  - "工作流自动化"
  - "技术对比"
字数: 2324
状态: "未开始"
总结: |
  - **Claude Skills功能**：让Claude按需加载规则，减少重复提示和Token消耗，降低AI Native门槛。
  - **关键概念对比**：
    - **MCP**：连接外部系统（如数据库、API）。
    - **Skills**：教Claude如何使用工具，按需加载以节省Token。
    - **Sub-agents**：派新会话处理复杂独立任务。
    - **Prompts**：用于单次临时任务。
  - **Skills的优势**：Token消耗低（仅加载元数据）、门槛低（只需写Markdown文档）、适合重复性工作流。
  - **适用人群**：有固定工作流、团队协作或Token消耗大的用户。
  - **白皮书资源**：作者与Claude Code合作编写了82页白皮书，涵盖技术架构、案例分析和未来展望，可通过公众号获取。
  - **实践建议**：从创建简单Skills开始，动手实践比单纯阅读更有效。
---

# [[关于Claude Skills，我给你写了份82页的白皮书]]
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

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHZTDhx4wLQeSheDayFyYaBOjewDpWqRVquAkQcyxuJehIPe3niahrJOEwuUjkia8IXVjO0ZCfK68eag/640?wx_fmt=png&from=appmsg)

说起来，Claude Skills这个功能我关注挺久了。

10月份刚发布的时候我就写过一篇，当时的判断是"AI Native的门槛又降低了"。这几个月用下来，判断没变，但理解更深了一层。

我在Claude Code里写了几十个Skills，主要用在写作和开发流程上。最大的感受是——**它让Claude学会了按需加载**。

以前每次开聊，都得重复一堆东西："帮我按XX格式""记得包含XX""别忘了XX"。烦，Token也烧得厉害。

现在不用了。规则提前写好，Claude平时只记住"有这么个手册"，大概100个tokens，真正用的时候才打开看。官方管这叫渐进式披露。
## Skills、MCP、Sub-agents到底啥区别？

这个问题被问过很多次。一开始我也晕，研究了一圈才理顺。

最简单的理解：

**MCP****让Claude能碰到外部系统。** 连数据库、调API、读文件，都是MCP的活儿。

**Skills告诉Claude碰到之后怎么用。** 拿到销售数据怎么算增长率，生成什么格式的报告，这是Skills的活儿。

MCP是发工具，Skills是教怎么用工具。**两个是配合关系。**

那Sub-agents呢？

Sub-agents是**派一个人出去干活**，新开一个会话，干完把结果带回来。Skills不一样，是在当前对话里给自己加能力。

简单说：Skills是装技能，Sub-agents是派人。

任务复杂、要跑很久的时候用Sub-agents。比如审查整个代码仓库，你总不能干等着。
## 为什么有人说Skills比MCP更重要？

Simon Willison写过一篇分析，说Skills可能比MCP更重要。

理由挺直接：**Token消耗差太多了。**

GitHub官方的MCP服务器，单独就要吃掉几万个tokens——因为要把所有能力描述预先加载进去。Skills呢，平时只加载一百来个tokens的元数据，需要的时候才加载详细内容。

而且Skills门槛更低。一个Markdown文件加上可选的脚本，就是一个Skill。不用跑服务器，不用配JSON。

会写文档就能写Skills。这个我觉得挺关键的。
## 对比表
PromptsSkillsMCPSub-agents复用性单次对话跨对话跨对话单次任务Token消耗每次全量按需加载预先全量独立会话门槛会写字会写文档要写代码要配置能访问外部数据❌❌✅❌

临时任务用Prompts，重复性工作流用Skills，需要连外部系统用MCP，复杂独立任务用Sub-agents。
## 谁比较需要这个？

三类人：有固定工作流的、团队协作的、Token烧得多的。

我自己主要用来跑写作流程——创作流程、风格指南、个人素材库，以前每次写文章都要手动加载，现在打包成Skills，自动按需调用。
## 白皮书里有什么？

为了帮大家更系统地理解这个东西，我和Claude Code合作写了一份**82页的白皮书**。

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHZTDhx4wLQeSheDayFyYaBOpMBwBQOYTh4SyMxKfRaI2zTJ0JfIGnQuuGGBBAdKm4icfczL5XSWRJw/640?wx_fmt=png&from=appmsg)

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHZTDhx4wLQeSheDayFyYaBOOThx9fojKCIc7CA7XfVsNZEibKOrdOgiblyV6xqRiayk8dUP2JIZ7drMg/640?wx_fmt=png&from=appmsg)

![图片](https://mmbiz.qpic.cn/mmbiz_png/HRdaeEmxNHZTDhx4wLQeSheDayFyYaBOd1wYdYSpxibstjE7ticasxwpVNicQibRG0cIx267VxlibiaZAsIhywsCyEsA/640?wx_fmt=png&from=appmsg)

涵盖了：

- 核心概念和技术架构
- Skills vs MCP vs Prompts vs Sub-agents的对比
- 在不同平台使用Skills
- 真实案例（Sionic AI怎么用Skills管理ML实验）
- 局限性和安全风险
- 未来展望

你可以按需查阅，也可以直接把PDF丢给Claude，让它给你做个性化解释。
## 不过话说回来

如果你还没太搞懂Skills，也别焦虑。像之前的MCP一样，风潮过去后，真正留下来常用的其实没几个。

技术迭代太快，谁也不好说下一个替代Skills的会是什么。保持学习、保持好奇就行。
## 最简单的开始

在 `~/.claude/skills/` 下创建一个文件夹，写个SKILL.md，重启Claude Code，就能用了。

白皮书里有完整的创建流程和模板，动手跑一遍，比看十遍文档都管用。

**如何获取白皮书？**

转发、点赞本文，在公众号后台发送「skills」，即可获取完整PDF文档。
