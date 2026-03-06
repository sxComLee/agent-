---
标题: "Clawdbot免费极简安装教程"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[waytoagi]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "最简洁的Clawdbot（OpenClaw）安装教程，一条命令完成安装，支持国内外多种AI模型"
亮点:
  - "一条命令完成安装，macOS/Windows/Linux均支持"
  - "支持国内模型：GLM、Kimi、MiniMax、DeepSeek等，无需OpenAI"
  - "QuickStart向导式配置，通过键盘方向键和回车即可完成所有配置"
  - "国内外版本URL区别是最大坑点，配置失败多数因此"
重难点:
  - "国内外版本的baseURL区分（如MiniMax国内api.minimax.com vs 海外api.minimax.io）"
  - "首次配置需要通过终端命令行操作，对非技术用户有一定门槛"
  - "安装后需单独配置通道（Channel），才能通过聊天软件控制"
tags:
  - "clippings"
  - "OpenClaw"
  - "安装教程"
字数: 600
状态: "未开始"
---

# Clawdbot免费极简安装教程

## 一键安装命令

### macOS
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

### Windows PowerShell
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

### Windows CMD
```cmd
curl -fsSL https://openclaw.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

## 安装后配置

安装完成后运行：
```bash
openclaw configure
```
或
```bash
clawdbot onboard
```

### 配置步骤（QuickStart模式）

1. 选择 **Yes** 接受免责声明
2. 选择 **QuickStart**
3. 选择模型供应商（推荐国内用户选 Z.AI/智谱 或 Kimi）
4. 输入对应的 API Key
5. 选择通道（飞书/Discord/Telegram等）
6. 完成配置

## 常见坑点

### 国内外版本URL区别

| 模型 | 国内版URL | 海外版URL |
|------|-----------|-----------|
| MiniMax | api.minimax.com | api.minimax.io |
| Kimi | 选coding plan专项 | 选moonshot |

### 配置失败排查

1. 检查 `~/.openclaw/openclaw.json` 中的 `baseURL`
2. 确认选择了正确的国内/海外版本
3. 看到 `no output` 不要慌——去其他配置过的渠道看

## 启动命令

```bash
# 临时启动（关闭终端会停止）
openclaw gateway --verbose

# 后台持久运行
nohup openclaw gateway --verbose > /tmp/openclaw-gateway.out 2>&1 & disown
```
