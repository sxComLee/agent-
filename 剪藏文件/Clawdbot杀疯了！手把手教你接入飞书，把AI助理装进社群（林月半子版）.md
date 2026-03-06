---
标题: "Clawdbot杀疯了！手把手教你接入飞书，把AI助理装进社群"
链接: "https://mp.weixin.qq.com/s/qnDCqYtZr4xvGx1mgEDKVw"
来源: "waytoagi飞书知识库"
作者: "[[林月半子]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "林月半子的Clawdbot飞书接入完整教程，详解长连接配置方法，解决本地部署无公网IP时的飞书双向通信问题"
亮点:
  - "本地部署无公网IP时，通过WebSocket长连接实现飞书双向通信"
  - "飞书权限批量导入JSON的高效方法，一次性配置所有必要权限"
  - "两步验证法：先测单向（ClawdBot→飞书），再打通双向（飞书→ClawdBot）"
  - "配置文件中手动添加connectionMode:websocket和requireMention:true两个关键字段"
重难点:
  - "长连接配置是最关键的一步：在飞书后台选择'长连接'而非公网回调URL"
  - "本地配置文件~/.clawdbot/clawdbot.json需要手动补充connectionMode和requireMention字段"
  - "安装插件时需要确认安装最新版本（2026.1.24-3）而非旧版本"
  - "添加事件订阅（接收消息事件）必须配置，否则机器人听不到消息"
tags:
  - "clippings"
  - "OpenClaw"
  - "飞书"
  - "长连接"
  - "接入教程"
字数: 1800
状态: "未开始"
---

# Clawdbot杀疯了！手把手教你接入飞书，把AI助理装进社群

> 作者：林月半子（林月半子的AI笔记）
> 原文链接：https://mp.weixin.qq.com/s/qnDCqYtZr4xvGx1mgEDKVw

## 飞书接入的核心思路

官方没有飞书插件，但社区项目 `m1heng/clawdbot-feishu` 解决了这个问题。

本地部署没有公网IP，需要使用**WebSocket长连接**而非公网回调URL。

## 第一步：飞书开放平台准备

1. 登录飞书开放平台（https://open.feishu.cn/）
2. 新建企业自建应用
3. 启用机器人能力

### 批量导入权限（高效！）

直接粘贴以下JSON批量导入：
```json
{
  "scopes": {
    "tenant": [
      "im:message",
      "im:message.p2p_msg:readonly",
      "im:message.group_at_msg:readonly",
      "im:message:send_as_bot",
      "im:resource"
    ]
  }
}
```

## 第二步：安装飞书插件

```bash
clawdbot plugins install @m1heng-clawd/feishu
```

⚠️ **注意**：确认安装的是最新版本（2026.1.24-3），不是旧版本！

## 第三步：交互式配置

运行 `clawdbot config` 进入向导：

1. 运行环境：选本地（直接回车）
2. 选择渠道：选 `channels`
3. 添加配置：选 `Channels`
4. 选择 channel：选 `Feishu`
5. 填入飞书开放平台的 **AppID** 和 **AppSecret**
6. 飞书版本：选国内默认
7. 群聊策略：选 `Open`（方便测试）
8. 一路回车到finished
9. 最后询问是否直接发送信息：选 **Yes**

## 第四步：单向连通测试（ClawdBot → 飞书）

1. 在飞书建群，把机器人拉进去
2. 在群设置里复制**群组ID（会话ID）**
3. 在ClawdBot配置界面，往这个群发一条消息
4. 如果飞书群收到消息 → 说明AppID和Secret没问题 ✅

## 第五步：打通任督二脉（飞书 → ClawdBot）

这是最关键的一步！

### 飞书后台开启长连接

1. 进入**事件与回调**页面
2. 选择**长连接**模式
3. 点击保存

### 添加事件订阅

在**事件配置**中添加**接收消息事件**（`im.message.receive_v1`）

### 修改本地配置文件

打开 `~/.clawdbot/clawdbot.json`，在 `feishu` 字段下手动补充：

```json
{
  "channels": {
    "feishu": {
      "connectionMode": "websocket",
      "requireMention": true,
      // ... 其他已有配置
    }
  }
}
```

### 重启ClawdBot

```bash
clawdbot gateway restart
```

## 第六步：双向验收测试

在飞书群里 @机器人 发消息，如果收到AI的回复，说明双向通路打通！✅

## 使用体验

成功接入后：
- 私聊、群聊都可以使用
- 24小时待命，随时响应
- 手机飞书随时操控AI助手

## 总结

飞书接入的最关键点是**长连接配置**：
1. 飞书后台选长连接（非公网URL）
2. 本地配置文件加 `connectionMode: "websocket"`
3. 添加消息接收事件订阅
4. 发布版本

只要这四步做对，飞书接入就没有问题。
