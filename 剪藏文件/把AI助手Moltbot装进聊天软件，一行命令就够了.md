---
标题: "把AI助手Moltbot装进聊天软件，一行命令就够了"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[有机大橘子]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "深度介绍Moltbot（原Clawdbot）的核心能力、安装配置、进阶用法和安全风险，从'被动AI'到'主动AI'的范式转变"
亮点:
  - "定义Moltbot的价值：把AI装进每天用的聊天软件，让AI主动为你工作而非被动等待"
  - "心跳机制（Heartbeat）：30分钟检查一次邮件/日程，有紧急情况主动通知你"
  - "本地优先设计：对话记录本地Markdown存储，Gateway运行在localhost，隐私有保障"
  - "完整进阶配置：Cron定时任务、心跳监控、MCP工具集成等"
重难点:
  - "安全边界的判断：什么场景下可以用，什么场景下绝对不能用"
  - "HEARTBEAT.md配置：控制AI主动行为的逻辑"
  - "Cron任务的语法和实际应用场景"
  - "不同平台（Telegram/Discord/WhatsApp）的配置差异"
tags:
  - "clippings"
  - "OpenClaw"
  - "Moltbot"
  - "主动AI"
  - "进阶配置"
字数: 4000
状态: "未开始"
---

# 把AI助手Moltbot装进聊天软件，一行命令就够了

> 作者：有机大橘子

## 为什么说Moltbot不一样

传统AI使用方式：
```
打开浏览器 → 输入问题 → 等回答 → 复制粘贴 → 关闭网页
```
→ 像每次想跟朋友说话都要先坐飞机去他家

Moltbot做的事：**把AI装进你每天都在用的聊天软件里。**

> 有机大橘子的评价：
> "ClawdBot/MoltBot 最大的意义在于把大众对通用Agent的想象进一步打开了。在这个赛道依然有巨大的想象空间和可能性。"

## 改名历程（"大蜕壳"事件）

2026年1月27日，Anthropic发律师函，"Clawdbot"与"Claude"太像。
创始人Peter Steinberger 2小时内组织社区投票，改名 **Moltbot**（取蜕壳之意）。

改名公告发出10秒后，骗子机器人抢注原Twitter账号发虚假加密货币地址，差点酿成1600万美元诈骗。

## 核心能力

| 场景 | 指令 | 实际操作 |
|------|------|----------|
| 文件整理 | "把Downloads的PDF按日期分类" | 创建文件夹，自动归类 |
| 收据处理 | "把这张购物小票录入表格" | OCR识别，生成Excel |
| 资料查询 | "React 19新特性有哪些" | 搜索、汇总、发给你 |
| 日程管理 | "提醒我明天3点开会" | 设置提醒，到点主动发消息 |
| 代码审查 | "检查今天的GitHub提交" | 拉取代码，输出审查意见 |

### 三大核心机制

1. **持久记忆**：记忆以Markdown文件存储在本地，随时可查看修改
2. **主动通知**：心跳（Heartbeat）每30分钟检查，主动发现并告知紧急情况
3. **真实执行**：能执行Shell命令、操作文件、控制浏览器，失败会自我反思重试

## 安装（一行命令）

macOS / Linux:
```bash
curl -fsSL https://molt.bot/install.sh | bash
```

Windows PowerShell:
```powershell
iwr -useb https://molt.bot/install.ps1 | iex
```

装完后：
```bash
moltbot onboard --install-daemon
```

## 配置向导三问

1. **本地用还是云端用？**
   - Local：装本机（注意安全）
   - Remote：云服务器（推荐）

2. **用哪家AI？**
   - 国内性价比选择：GLM 4.7、MiniMax m2.1、Kimi K2.5
   - 推荐理由：量大管饱，性价比远超Claude API

3. **在哪个聊天软件？**
   - Telegram（最简单）：@BotFather → /newbot → 获取Token
   - Discord：开发者后台 → 创建应用 → 获取Token
   - WhatsApp：`moltbot channels login whatsapp` → 扫码

## 进阶配置

### 设置每日早报（Cron任务）

```bash
# 每天早上7点发送简报
moltbot cron add --name "Morning brief" --cron "0 7 * * *" --message "天气、日程、重要邮件"

# 2小时后提醒回电
moltbot cron add --name "Call back" --at "2h" --message "给客户回电"
```

### 配置心跳监控

编辑 `~/clawd/HEARTBEAT.md`：
```markdown
# 心跳检查清单
- 检查是否有紧急邮件
- 查看未来2小时的日程
- 如果闲置超过8小时，发送问候
```

在配置文件设置：
```json
{
  "agents": {
    "defaults": {
      "heartbeat": {
        "every": "30m",
        "activeHours": { "start": "08:00", "end": "22:00" }
      }
    }
  }
}
```

## 安全建议

| ✅ 推荐做法 | ❌ 避免做法 |
|-----------|-----------|
| 装在云服务器（隔离环境） | 装在主力工作机 |
| 装在虚拟机里 | 处理敏感财务数据 |
| 用闲置旧电脑 | 给予不必要系统权限 |
| 定期备份重要数据 | 在公共网络暴露Gateway |

## 隐私设计

- 对话记录存在本地设备（Markdown格式）
- Gateway运行在localhost，不暴露公网
- AI调用时数据直接发给Anthropic/OpenAI，不经过第三方

## 实战案例

- **自动整理发票**：每月底扫描发票文件夹，分类生成支出汇总表，发到Slack
- **代码审查助手**：接入Discord，每天自动分析前一天GitHub PR，输出审查意见
- **智能购物比价**：发商品链接，自动在多平台比价，返回最低价和历史走势
- **语音笔记转录**：收到Telegram语音，自动转录，提取待办事项添加到Todoist
