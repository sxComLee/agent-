---
标题: "做了一个skill技能，一句话装好openclaw"
链接: "https://mp.weixin.qq.com/s/c7GN_JBG..."
来源: "waytoagi飞书知识库"
作者: "[[waytoagi]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "作者开发了openclaw-installer这个Skill，一句话指令即可自动完成OpenClaw的全部安装配置流程"
亮点:
  - "openclaw-installer Skill实现一句话指令完成安装：说'帮我安装OpenClaw'即可"
  - "自动检测系统环境，覆盖16个AI模型和7个消息通道的安装配置"
  - "每个命令都经过实测验证，附带健康检查脚本，装完一键检测配置正确性"
  - "Skills机制是OpenClaw的核心扩展能力，任何人都可以开发和分享"
重难点:
  - "理解Skills的本质：Markdown格式的说明书，告诉AI如何使用外部工具或完成特定任务"
  - "Skills安装方式：npm安装或直接从GitHub URL安装"
  - "如何自己开发Skills并发布到ClawHub社区"
  - "Skills中的健康检查脚本设计，确保配置正确"
tags:
  - "clippings"
  - "OpenClaw"
  - "Skills开发"
  - "自动化安装"
字数: 400
状态: "未开始"
---

# 做了一个skill技能，一句话装好openclaw

## 背景

OpenClaw（原Clawdbot）GitHub 10万星，号称"私人AI助手"——但各种安装教程出来后，很多人还是装不上，一堆报错。

配置流程不短：装Node.js → npm全局安装 → 写环境变量 → 配API Key → 设模型 → 接通道 → 起服务……

新手很容易在某一步卡住。

## openclaw-installer Skill

作者开发了一个解决方案：**openclaw-installer** Skill。

### 用法

只需说一句：
```
帮我安装 OpenClaw
```

它就会自动：
1. 检测你的系统环境
2. 逐步完成安装
3. 配置模型和通道
4. 运行健康检查

### 覆盖范围

**16个AI模型**：
- Claude、GPT、Gemini、DeepSeek
- Kimi、智谱GLM、MiniMax
- Ollama本地部署
- ...及更多

**7个消息通道**：
- Telegram / Discord / WhatsApp / Slack
- 微信 / 飞书 / iMessage

### 质量保证

- 所有命令实测验证过
- 从全新环境到服务跑起来，每步均经实际执行确认
- 附带健康检查脚本，装完一键检测配置是否正确

## Skills是什么

Skills是OpenClaw的核心扩展机制：
- 本质是Markdown格式的说明书
- 告诉AI如何使用工具、完成特定任务
- 可以从npm安装、从GitHub URL安装、或自己开发
- 社区技能市场：https://clawhub.ai

## 相关标签

`#OpenClaw安装教程` `#AI助手部署指南` `#ClawbotMoltbot私人大助手`
