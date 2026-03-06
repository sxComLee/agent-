---
标题: "Clawdbot一夜爆火，GitHub已狂飙64k Star！附最新部署使用教程"
链接: "https://mp.weixin.qq.com/s/5sVXHd43..."
来源: "waytoagi飞书知识库"
作者: "[[苍何]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "苍何的全面Clawdbot部署教程，从腾讯云服务器选购到Discord配对，含自定义API配置、优缺点分析"
亮点:
  - "基于腾讯云轻量+Discord的全流程教程，含自定义第三方API（Atlas Cloud）配置方法"
  - "详细说明了Clawdbot的Discord OAuth2配置步骤，包含权限范围和机器人邀请流程"
  - "支持自定义API baseURL，可接入任何兼容OpenAI格式的模型服务"
  - "完整的优缺点分析：本地优先安全、多平台、高可定制 vs 技术门槛高、费用自承"
重难点:
  - "自定义API配置需要手动编辑openclaw.json文件，格式要求严格"
  - "discord通道需要完成配对步骤（pairing approve）才算真正配置完成"
  - "session-memory hooks的启用对保持对话记忆至关重要"
  - "持久化后台运行：用nohup命令避免关闭终端后服务中断"
tags:
  - "clippings"
  - "OpenClaw"
  - "ClawdBot"
  - "Discord"
  - "部署教程"
字数: 3500
状态: "未开始"
---

# Clawdbot一夜爆火，GitHub已狂飙64k Star！附最新部署使用教程

> 作者：苍何（苍何）
> 原文链接：https://mp.weixin.qq.com/s/5sVXHd43...

## 准备工作

### 服务器选择

推荐腾讯云轻量应用服务器：
- 配置：2核2G起步
- 地区：**硅谷或香港**（别选大陆，有网络问题）
- 镜像：选择 **Clawdbot应用模板**（省去环境安装）

通过SSH客户端（如Xterminal）或控制台登录。

## 配置自定义API

### openclaw.json配置格式

```json
{
    "models": {
        "providers": {
            "xxx": {
                "baseUrl": "https://api.atlascloud.ai/v1",
                "apiKey": "你的API Key",
                "api": "anthropic-messages",
                "models": [
                    {
                        "id": "claude-opus-4-5-20251101",
                        "name": "Claude Opus 4.5",
                        "reasoning": true,
                        "input": ["text", "image"],
                        "contextWindow": 200000,
                        "maxTokens": 4096
                    }
                ]
            }
        }
    },
    "channels": {
        "discord": {
            "enabled": true,
            "botToken": "你的Discord Bot Token"
        }
    },
    "agents": {
        "defaults": {
            "model": {
                "primary": "xxxx/claude-opus-4-5-20251101"
            }
        }
    }
}
```

## Discord完整配置

### 创建Discord Bot

1. 访问：https://discord.com/developers/applications
2. 创建新Application
3. Bot页面 → Reset Token → 复制Token
4. 开启 **Message Content Intent**

### OAuth2配置

1. OAuth2 URL Generator → 选择 `bot`
2. Bot Permissions：
   - Send Messages ✅
   - Read Message History ✅
3. 复制邀请链接 → 添加到你的服务器

## 配置向导（如使用腾讯云模板）

```bash
clawdbot onboard
```

- 同意免责声明 → Yes
- 选 QuickStart
- 选模型（GLM 4.7等）
- 输入API Key
- 选择Discord通道
- 启用hooks（**必选session-memory**）

## 配对步骤

```bash
# 1. 启动Gateway
clawdbot gateway --port 18789 --verbose

# 2. Discord私聊Bot获取配对码

# 3. Ctrl+C停止

# 4. 执行配对
clawdbot pairing approve discord <配对码>

# 5. 重启Gateway
clawdbot gateway --port 18789 --verbose

# 6. 后台持久运行
nohup clawdbot gateway --port 18789 --verbose > /dev/null 2>&1 &
```

## Clawdbot优缺点

### 优点
- 本地优先，数据隐私安全
- 多平台支持（10+通讯平台）
- 高度可定制
- 功能丰富（浏览器自动化/Cron/Canvas等）

### 缺点
- 技术门槛较高（需要命令行操作）
- API调用费用需自承
- 需要维护服务器持续运行
- 权限高，安全风险不可忽视

## 实际效果演示

苍何的测试案例：
1. 指令："搜集整理最新的关于Clawdbot的信息，找出10个最佳实践"
   → AI自主搜索，推荐相关Discord社区，非常贴心
2. 手机上指令："把刚才的结果保存成markdown文档，放在claw文件夹"
   → 喝几口水的功夫就完成了
