---
标题: "把AI助手Moltbot装进聊天软件"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[waytoagi]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "介绍如何将Moltbot（OpenClaw）与各类聊天软件集成，让AI助手通过熟悉的IM工具进行交互"
亮点:
  - "支持10+聊天平台：Telegram、Discord、WhatsApp、飞书、企微、钉钉、iMessage等"
  - "通过熟悉的聊天软件操控AI，极大降低使用门槛和操作摩擦"
  - "多通道同时配置，同一个AI助手可以在不同IM上响应"
  - "手机端随时通过IM远程操控家里/服务器上的AI执行任务"
重难点:
  - "每个平台的Bot创建流程不同，需要分别获取Token/AppID/AppSecret"
  - "国内平台（飞书/企微/钉钉）需要额外配置长连接或公网回调URL"
  - "Discord需要配置正确的权限范围（Scopes和Bot Permissions）"
  - "配对（Pairing）步骤容易遗漏，需要执行approve命令才算配对成功"
tags:
  - "clippings"
  - "OpenClaw"
  - "Moltbot"
  - "IM集成"
字数: 900
状态: "未开始"
---

# 把AI助手Moltbot装进聊天软件

## 支持的聊天平台

| 平台 | 类型 | 适合人群 |
|------|------|----------|
| Telegram | 国际 | 最稳定，推荐首选 |
| Discord | 国际 | 开发者社区 |
| WhatsApp | 国际 | 海外用户 |
| 飞书 | 国内 | 企业/个人均可 |
| 钉钉 | 国内 | 企业用户 |
| 企微 | 国内 | 企业用户（需公网） |
| iMessage | macOS专属 | Mac用户 |
| Slack | 国际 | 团队协作 |

## 配置通用流程

### 方法一：命令行配置向导
```bash
clawdbot onboard
# 或
openclaw configure
```
按向导选择对应渠道

### 方法二：直接告诉AI助手安装
在WebUI或TUI中输入：
```
我要安装一个[平台]插件，请你基于这个项目进行安装配置：[GitHub地址]
```

## Discord配置详细步骤

1. 进入 Discord Developer Portal：https://discord.com/developers/applications
2. 创建新Application
3. 找到Bot，点击 **Reset Token**，复制Token
4. 开启 **Message Content Intent**
5. OAuth2页面选择Scopes: `bot`，Bot Permissions: `Send Messages` + `Read Message History`
6. 复制邀请链接，添加Bot到服务器
7. 将Token粘贴到配置中

## 配对步骤（关键！）

配置通道后，需要完成配对：
1. 在聊天软件中私聊机器人，发任意消息
2. 机器人返回配对码（Pairing Code）
3. 终止Gateway（Ctrl+C）
4. 执行配对命令：
   ```bash
   clawdbot pairing approve discord <配对码>
   ```
5. 重新启动Gateway

## 使用体验

配置成功后：
- 手机随时发消息 → AI在服务器上执行
- 结果直接回到聊天窗口
- 支持文件、图片等多媒体交互
- 多渠道同时在线，随时响应
