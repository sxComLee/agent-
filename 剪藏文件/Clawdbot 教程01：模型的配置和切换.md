---
标题: "Clawdbot 教程01：模型的配置和切换"
链接: "https://mp.weixin.qq.com/s/qlbCkX2P..."
来源: "waytoagi飞书知识库"
作者: "[[歸藏]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "歸藏分享配置国产模型时的坑点和解决方案，核心是国内外版本URL区别以及openclaw configure命令的正确用法"
亮点:
  - "openclaw configure命令是配置模型的首选方式，能解决大部分配置问题"
  - "国内外版本URL是最大坑（如Minimax国内api.minimax.com vs 海外api.minimax.io）"
  - "三大国产模型（Kimi/Minimax/GLM）均已验证可用，均通过测试"
  - "看到no output不要慌，去其他配置的渠道检查，可能只是输出位置不对"
重难点:
  - "Minimax国内版(minimax-cn)和海外版(minimax)的选择与对应URL区别"
  - "模型选择界面找到正确选项（需要用方向键往下找高亮项）"
  - "openclaw.json中的agents.defaults.fallbacks字段需要同步更新"
  - "切换模型建议先用/new开新对话再切换，避免上下文混乱"
tags:
  - "clippings"
  - "OpenClaw"
  - "模型配置"
  - "国产模型"
字数: 1100
状态: "未开始"
---

# Clawdbot 教程01：模型的配置和切换

> 作者：歸藏（歸藏的AI工具箱）
> 原文链接：https://mp.weixin.qq.com/s/qlbCkX2P...

## 核心问题

配置模型时到处报错的核心就两个问题：**命令行配置** 和 **URL修正**。

## 方法一：优先使用命令配置

```bash
openclaw configure
```

这是最省事的方法，能解决大部分配置问题。

### 操作步骤

1. 运行命令
2. 选择"本地"还是"远程"→ 选本地
3. 选择"配置什么"→ 选模型
4. 选择模型供应商
5. 输入API Key

### 模型选择坑点

| 要配置的模型 | 应该选择的选项 |
|------------|-------------|
| Minimax M2.1 | Minimax |
| Kimi K2.5 | moonshot AI |
| Kimi Coding Plan | Kimi for coding（有单独选项） |

⚠️ **注意**：Minimax没有coding plan选项，即使买了也选Minimax本身

选完后一大堆选项会出现，不用慌，用方向键向下找到已高亮的那项，回车即可。

## 方法二：手动修改配置文件

配置文件位置：
```
/Users/你的用户名/.openclaw/openclaw.json
```

找到 `baseURL` 这一行进行修改。

### 国内外URL对照表

| 模型 | 国内版 | 海外版 |
|------|--------|--------|
| Minimax | `api.minimax.com` | `api.minimax.io` |

**选错了会导致API调用失败！**

### 额外注意

`openclaw.json` 中的 `agents.defaults.fallbacks` 字段也需要更新为新模型，否则切换不生效。

## 模型切换

配置好后切换模型：

```
# 在TUI界面
/model
# 搜索模型名（如"Kimi"）并选择

# 启动TUI
openclaw tui
```

**建议**：切换前先用 `/new` 开新对话，避免上下文混乱。

## no output 问题解析

切换模型后发送消息返回 `no output`？

**不要慌**：这不是配置失败，意思是**输出在其他渠道里**。

可能输出到了：
- Web环境（claude.ai）
- Telegram Bot
- 其他配置过的渠道

→ 去其他渠道试试，如果能用，配置是成功的。

## 总结三步法

1. 用 `openclaw configure` 命令配置
2. 如果不行，手动改 `openclaw.json` 里的 `baseURL`
3. 切换模型用 `/model` 命令
4. 看到 `no output` 去其他渠道试
