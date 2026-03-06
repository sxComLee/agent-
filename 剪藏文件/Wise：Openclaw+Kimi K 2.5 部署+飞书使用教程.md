---
标题: "Wise：Openclaw+Kimi K 2.5 部署+飞书使用手把手教程"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[Wise]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "Wise用Kimi Code + Claude Code（GLM）全程调研、部署Clawdbot，并扩展了生图、联网搜索、私有代码仓库连接等高级能力"
亮点:
  - "用AI来部署AI的创新做法：全程让Kimi Code提供部署指导，连服务器操作都让AI协助"
  - "飞书机器人配置中遇到问题直接问飞书智能助手，零摩擦排障"
  - "将OpenClaw当分发入口+Claude Agent执行的分层架构，充分利用两者优势"
  - "成功接入联网搜索（无需信用卡的免费MCP：exa.ai和tavily）"
重难点:
  - "Kimi code不肯直接登录服务器的问题（需要转用Claude Code解决）"
  - "飞书机器人配置权限繁多，建议直接问飞书智能助手排障"
  - "国内API的editing coding plan使用限制（实测GLM和火山可用，Kimi coding plan当时不行）"
  - "生图能力的开发需要额外扩展，不是开箱即用"
tags:
  - "clippings"
  - "OpenClaw"
  - "Kimi K2.5"
  - "飞书"
  - "进阶教程"
字数: 2500
状态: "未开始"
---

# Wise：Openclaw+Kimi K 2.5 部署+飞书使用手把手教程

> 作者：Wise

## 核心理念

**用AI来部署AI**：全程让Kimi Code做调研和部署指导，遇到问题让AI排错。

> "最近有很多朋友问我，为什么我的Token消耗量那么大，其实答案只有一个，我把编程CLI代替了所有的事。"

## Clawdbot是什么（AI调研结论）

简言之：Moltbot是一个**真正能干活的Agent**，不是只会聊天的废物。

- 操控电脑生成代码
- 整理文件
- 生图、创作
- 可以通过WhatsApp/Telegram操控
- 云厂商接入后通过钉钉/企微/飞书操作

与编程助手的区别：**不再需要打开编程工具**来完成任务。

## 飞书接入实操

### 关键步骤

1. 购买云服务器（新加坡节点）
2. 运行 `clawdbot onboard`配置
3. 访问飞书开放平台：https://open.feishu.cn/
4. 创建应用 → 添加机器人 → 开通权限
5. 发布版本

### 遇到问题

直接问飞书智能助手：
- 访问：https://open.feishu.cn/app/ai/playground?from=nav
- 把截图和错误描述发给它

### 模型选择建议（实测结论）

| 模型 | 是否可用于Coding Plan |
|------|---------------------|
| GLM | ✅ 可用 |
| 火山（豆包） | ✅ 可用 |
| Kimi coding plan | ❌ 当时不行（可能已更新） |

## 能力扩展实测

### 能力1：生图+发送图片消息

让Kimi给OpenClaw添加生图和发送飞书图片消息的能力 → 开发时间较长（飞书场景未充分训练）。

### 能力2：私有代码仓库连接

```
配置GitHub Personal Access Token后，可访问私有仓库
通过git协作，在电脑前用电脑打代码，不在就用手机打
```

### 能力3：联网搜索

需要绑定Brave API Key，但也有**免费无需信用卡**的MCP替代方案：
- **Exa**: https://mcp.exa.ai/mcp
- **Tavily**: https://app.tavily.com/home

### 能力4：使用Claude Code的Skills

**玩法1**：让OpenClaw模拟Skills工作
```
告诉它你可以模拟我的skills操作
```

**玩法2**：调用Claude Code使用Skills
- 先安装Claude Code
- 让OpenClaw下载你的Skills
- 把OpenClaw当分发入口，Claude Agent负责执行

## 架构心得

> "我会更倾向于把Openclawd当做分发入口，然后选择相信Claude的Agent，毕竟一天迭代N个版本的Coding工具，业界不多了。"

```
飞书消息 → OpenClaw（分发入口）→ Claude Code（执行）→ 结果回飞书
```

## 最后的感悟

> "写到最后忽然发现，也许我们离AGI的距离是到底把权限交出去多少。"

ClawdBot是联通软件的AI产品，以后会有联通硬件的，以后会全部都联通的。
