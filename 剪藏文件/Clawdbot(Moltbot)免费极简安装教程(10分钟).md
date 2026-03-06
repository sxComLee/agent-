---
标题: "Clawdbot(Moltbot)免费极简安装教程(10分钟)持续更新"
链接: "https://mp.weixin.qq.com/s/15T8bzs64RUA9VsMiqFxQw"
来源: "waytoagi飞书知识库"
作者: "[[Kevin涛]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "Kevin涛的极简安装教程：基于AWS免费EC2服务器，10分钟完成Clawdbot安装+Telegram接入，附Exa MCP集成和常见问题解决"
亮点:
  - "AWS免费套餐Ubuntu服务器全流程图文：从注册到SSH连接，零成本上手"
  - "安装仅需一行命令，后续跟着配置向导操作，全程不需要写代码"
  - "Exa MCP集成：通过让AI创建skill封装Exa接口，获得联网搜索+公司调研+LinkedIn搜索等能力"
  - "常见问题解决：Telegram配对方法和clawdbot command not found的PATH问题"
重难点:
  - "AWS免费EC2实例需要8GB内存规格才能稳定运行，创建密钥对步骤容易跳过"
  - "Telegram配对步骤：需要执行 clawdbot pairing approve telegram <code> 命令"
  - "clawdbot command not found解决：需要将npm全局bin目录加入PATH"
  - "推荐模型：Gemini最便宜，GLM性价比高，不建议Claude API（贵）"
tags:
  - "clippings"
  - "OpenClaw"
  - "AWS"
  - "Telegram"
  - "MCP集成"
字数: 1500
状态: "未开始"
---

# Clawdbot(Moltbot)免费极简安装教程(10分钟)

> 作者：Kevin涛（Kevin的学堂）
> 原文：https://mp.weixin.qq.com/s/15T8bzs64RUA9VsMiqFxQw

## 前置条件

- 北美地区（AWS有免费层）
- Telegram账号

## 第一步：准备AWS免费服务器（5分钟）

1. 访问 https://aws.amazon.com 注册/登录
2. 搜索 **EC2**，点击 Launch instance
3. 系统选 **Ubuntu**
4. 实例类型搜索 "free"，选 **8GB内存** 那个（重要！）
5. 创建密钥对（记住密钥文件位置）
6. Launch instance
7. 实例创建后，点击实例ID → Connect → Connect

## 第二步：一行命令安装（2分钟）

```bash
curl -fsSL https://molt.bot/install.sh | bash
```

⚠️ **安全提示：强烈建议在云服务器等安全隔离环境中运行，不建议在本机运行！**

## 第三步：跟着配置向导（10分钟）

- 继续安装：选 **Yes**
- 选 **Quick Start**
- 模型推荐：选 **Gemini**（最便宜），选 Token paste setup
- 通道：选 **Telegram Bot**

## 第四步：创建Telegram Bot（5分钟）

1. 在Telegram搜索 `@BotFather`
2. 发送 `/newbot`，创建机器人
3. 复制 Bot Token，粘回向导
4. Skills：只装recommended的，其他选Skip
5. 设置AI名字和性格（Hatch in TUI）

## 给AI设置人设（示例）

```
1. My name — TaoX
2. My nature — A sharp, reliable assistant to Kevin
3. My vibe — Professional yet approachable
4. My emoji — ✌️
```

## 进阶：接入Exa MCP

Exa提供联网搜索、公司调研、LinkedIn搜索等能力。

在Telegram对话框发送：
```
create a skill by wrapping this MCP:
https://mcp.exa.ai/mcp?
tools=web_search_exa,web_search_advanced_exa,get_code_context_exa,
deep_search_exa,crawling_exa,company_research_exa,linkedin_search_exa,
deep_researcher_start,deep_researcher_check
```

## 常见问题

### 问题一：Telegram配对失败（需要所有者批准）

解决方案：
```bash
clawdbot pairing approve telegram <配对码>
```

### 问题二：clawdbot command not found

原因：npm全局bin目录未加入PATH

解决方案（bash）：
```bash
echo 'export PATH="$(npm prefix -g)/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

解决方案（zsh）：
```bash
echo 'export PATH="$(npm prefix -g)/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```
