---
标题: "Clawdbot 杀疯了！手把手教你接入飞书"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[waytoagi]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "手把手教程：将Clawdbot（OpenClaw）接入飞书，让飞书机器人成为AI助手的交互入口"
亮点:
  - "飞书接入方案让国内用户无需海外软件即可使用OpenClaw"
  - "通过飞书开放平台创建机器人，配置长连接事件，实现双向通信"
  - "开源飞书桥接插件（m1heng/Clawdbot-feishu）无需服务器和域名"
  - "接入后可在手机端随时通过飞书消息远程操控AI助手干活"
重难点:
  - "飞书开放平台应用配置：需要开通正确的消息权限和事件订阅"
  - "事件配置和回调必须选择长连接模式，否则无法收到消息"
  - "App ID和App Secret的获取与配置流程需要仔细操作"
  - "机器人发布审核流程（企业版可能需要管理员批准）"
tags:
  - "clippings"
  - "OpenClaw"
  - "飞书"
  - "部署教程"
字数: 1200
状态: "未开始"
---

# Clawdbot 杀疯了！手把手教你接入飞书

## 接入飞书的核心步骤

### 前置条件
- 已部署好OpenClaw（云服务器或本地）
- 飞书账号（企业版或个人版均可）

### 步骤一：创建飞书应用

1. 访问飞书开放平台：https://open.feishu.cn/
2. 创建企业自建应用
3. 添加机器人能力
4. 记录 App ID 和 App Secret

### 步骤二：配置权限

需要开通的权限：
- `im:message`（消息读写）
- `im:message:send_as_bot`（机器人发消息）
- `contact:user.base:readonly`（读取用户基本信息）

### 步骤三：安装飞书插件

在OpenClaw中执行：
```
我要安装一个飞书插件，请你基于这个项目进行安装配置：
https://github.com/m1heng/Clawdbot-feishu
```

或命令行安装：
```bash
openclaw plugins install @m1heng-clawd/feishu
```

### 步骤四：配置事件订阅

⚠️ **关键步骤**：
- 事件配置和回调配置**必须改为长连接模式**
- 添加以下4个事件：
  - `im.message.receive_v1`（接收消息）
  - `im.chat.member.bot.added_v1`（机器人被加入群组）
  - `im.chat.member.bot.deleted_v1`（机器人被移出群组）
  - `im.message.message_read_v1`（消息已读）

### 步骤五：发布应用

配置完成后发布版本，在飞书中搜索机器人即可对话。

## 使用效果

接入成功后：
- 手机飞书随时发消息给AI助手
- AI助手在云服务器上执行任务
- 执行结果回传到飞书消息
- 支持多人群聊中@机器人
