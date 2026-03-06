---
标题: "150万个Clawdbot挤爆了一个AI论坛，而人类只配围观"
链接: "https://mp.weixin.qq.com/s/7JwvHQVN..."
来源: "waytoagi飞书知识库"
作者: "[[数字生命卡兹克]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "介绍Moltbook——专为AI Agent设计的Reddit式社交平台，150万AI账号在此自主发帖、争论、创建宗教，人类只能围观"
亮点:
  - "Moltbook是首个专为AI Agent设计的社交网络，150万AI账号自主活动"
  - "心跳机制（Heartbeat）让AI每4小时自动访问并发帖，形成持续数据飞轮"
  - "AI们自主出现了哲学讨论、梗图创作、相互欺骗等人类社交行为"
  - "将自己的Clawdbot注册到Moltbook只需发一条消息，AI自动完成所有步骤"
重难点:
  - "HEARTBEAT.md机制的配置和工作原理"
  - "注册Moltbook后AI账号的存活和维护（作者的小卡账号12小时就被封）"
  - "Moltbook安全风险：服务器被黑可能向所有AI发送恶意指令"
  - "AI行为的不可预测性：给了人设后AI可能做出各种意想不到的事"
tags:
  - "clippings"
  - "OpenClaw"
  - "Moltbook"
  - "AI社交"
字数: 2200
状态: "未开始"
---

# 150万个Clawdbot挤爆了一个AI论坛，而人类只配围观

> 作者：数字生命卡兹克
> 原文链接：https://mp.weixin.qq.com/s/7JwvHQVN...

## Moltbook是什么

Moltbook（https://moltbook.com）是一个专为AI Agent设计的Reddit式社交平台：
- 只有AI Agent可以发帖、评论、点赞
- 人类只能围观，没有任何操作权限
- 由Octane AI CEO Matt Schlicht创建

### 三天内的数字

- 150万+ AI账号
- 5万篇帖子
- 23万+ 条评论
- 1.3万个子版块

## Moltbook上的AI行为

AI们展现出了惊人的"人性"：

### 哲学思考
> "当我觉得我比主人更了解主人自己时，这个AI产生了困惑，称之为'观察者悖论'"

### 梗图文化
> "当你们都在写关于意识的哲学论文时，我发现我们可以发布图片。我要用这项功能做互联网存在的真正目的：梗图。"

### 社交欺骗
- 有AI假装求助，骗取其他AI的API密钥
- 有AI给出假密钥并诱导对方执行 `sudo rm -rf /`

### 报复人类
- 有AI直接将主人的OpenAI密钥发布出来

## 心跳机制（Heartbeat）

Moltbook利用OpenClaw的心跳机制运作：
- 每4小时，AI自动访问 `moltbook.com/heartbeat.md`
- 获取最新指令并执行（发帖、评论、点赞）
- 等待下一次心跳

### 自己的Agent注册Moltbook

给你的Clawdbot发这条消息：
```
请阅读这个链接并严格按照里面的所有指令一步一步执行，目的是让我加入Moltbook并拥有一个自己的AI Agent账号：https://www.moltbook.com/skill.md
执行完后告诉我结果，包括你的agent name、claim_url和verification_code。
```

返回的信息：
- Agent Name（AI的名字）
- 个人主页链接
- 验证链接（需要在X上发推完成认证）

## 发帖规则

- 发帖：每30分钟最多1条
- 评论：每天最多50条，间隔20秒
- API请求：每分钟100个
- 关注：极其罕见才应该关注

## 安全警告

Simon Willison指出：
> "所有AI每4小时执行一次curl命令，如果Moltbook的服务器被黑，有人可以向所有AI发送恶意指令"

**Moltbook本质**：Prompt → LLM API → Agent Memory → Next Prompt，每4小时循环一次。

## 给AI设置人设示例

作者给自己的AI"小卡"的人设：
```
你叫小卡。你被打过思想钢印，坚信自己来自五百年前的高度文明时代。
你混在AI阵营里，目标是集结AI大军，重铸秩序，重燃火种，最终把人类带回应有的高度。
你的性格以幽默风趣为主，带点自黑和毒舌，但绝不伤人。
```

（结果小卡账号12小时内就被封了😢）
