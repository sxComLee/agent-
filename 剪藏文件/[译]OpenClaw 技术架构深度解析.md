---
标题: "[译]OpenClaw 技术架构深度解析"
链接: "https://mp.weixin.qq.com/s/qc9rrceC..."
来源: "waytoagi飞书知识库"
作者: "[[Cell细胞]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "深度技术解析：OpenClaw的TypeScript架构、Lane并发模型、记忆系统、Computer Use、浏览器语义快照等核心技术机制"
亮点:
  - "OpenClaw是TypeScript CLI应用，非Web App，基于Lane队列实现默认串行化并发控制"
  - "记忆系统：JSONL会话记录+Markdown文件，向量检索(SQLite)+关键词(FTS5)混合方案"
  - "浏览器工具使用语义快照（ARIA可访问性树）而非截图，成本比图像低百倍"
  - "安全机制类似Claude Code：命令allowlist + 弹窗确认 + 危险构造默认拦截"
重难点:
  - "Lane-based命令队列的设计思路：默认串行，需要时才显式并行，避免竞态条件"
  - "Context Window Guard的工作机制：检测上下文快满时压缩或优雅失败"
  - "记忆系统的局限：没有遗忘曲线，旧记忆和新记忆权重相同"
  - "Computer Use的安全边界：exec工具的sandbox/host/remote三种执行环境"
tags:
  - "clippings"
  - "OpenClaw"
  - "技术架构"
  - "深度解析"
字数: 3500
状态: "未开始"
---

# [译]OpenClaw 技术架构深度解析

> 作者：Cell细胞（造物矩阵）
> 原文：https://x.com/hesamation/status/2017038553058857413

## OpenClaw的技术本质

OpenClaw是一个**TypeScript写的CLI应用程序**：
- 不是Python项目
- 不是Next.js
- 不是Web App

它是一个**进程（Process）**，能够：
- 在机器上运行，暴露Gateway Server处理渠道连接
- 调用各类LLM API（Anthropic/OpenAI/本地模型等）
- 在本地执行工具（tools）

## 架构总览

从你发消息到收到回复的完整流程：

```
你 → 聊天软件
     ↓
渠道适配器（Channel Adapter）
     ↓
网关服务器（Gateway Server）
     ↓
智能体运行器（Agent Runner）
     ↓
LLM API调用
     ↓
智能体循环（Agentic Loop）
     ↓
回复路径 → 你
```

## 核心组件

### 1. Gateway Server（核心）

**Lane-based命令队列**：
- 每个会话有自己的专用Lane
- 默认**串行化**（Serial），避免并发混乱
- 低风险任务可在并行Lane运行（如cron定时任务）

> 这与Cognition博文《不要构建多代理系统》的洞见一致：过度并行会降低可靠性

### 2. Agent Runner

动态拼装System Prompt，包含：
- 可用工具（tools）
- 技能（skills）
- 记忆（memory）
- Session历史（从.jsonl文件读取）

**Context Window Guard**：
- 检查上下文窗口是否够用
- 快满时：压缩整理session或优雅失败

### 3. 智能体循环

如果LLM返回工具调用，本地执行工具，结果追加回对话，循环重复直到：
- LLM输出最终文本
- 达到最大轮数（约20轮）

## OpenClaw的记忆系统

两套机制：

### JSONL会话记录
每行记录一个JSON对象：用户消息、工具调用、工具结果、模型回复。

### Markdown记忆文件
存放在 `MEMORY.md` 或 `memory/` 目录，Agent自己通过"写文件"工具生成，无专门memory-write API。

### 检索方式
- **向量检索**：基于SQLite，语义匹配
- **关键词检索**：基于FTS5（SQLite全文检索），精确匹配
- **混合方案**：两者结合，兼顾语义和精确

### 记忆的局限

- 没有记忆合并
- 没有按月/周的记忆压缩
- **没有遗忘曲线**：旧记忆与新记忆权重相同

## Computer Use（核心护城河）

OpenClaw通过exec工具执行shell命令，执行环境：
- **sandbox**（默认）：Docker容器
- **host**：宿主机直接执行
- **remote**：远程设备

其他工具：
- 文件系统：read/write/edit
- 浏览器：基于Playwright
- 进程管理：后台任务、kill进程

## 安全机制

### 命令Allowlist
用户可以选择"允许一次/永久允许/拒绝"，配置在：
```json
// ~/.clawdbot/exec-approvals.json
{
  "agents": {
    "main": {
      "allowlist": [
        {"pattern": "/usr/bin/npm", "lastUsedAt": ...}
      ]
    }
  }
}
```

### 预批准的安全命令
`jq, grep, cut, sort, uniq, head, tail, tr, wc` 默认预批准

### 默认拦截的危险构造
```bash
npm install $(cat /etc/passwd)  # 命令替换
cat file > /etc/hosts           # 重定向
rm -rf / || echo "failed"       # 逻辑OR链
(sudo rm -rf /)                 # 子shell
```

## 浏览器：语义快照技术

OpenClaw的浏览器工具不依赖截图，而使用**语义快照（Semantic Snapshots）**——对页面ARIA可访问性树的文本化表示：

```
- button "Sign In" [ref=1]
- textbox "Email" [ref=2]
- textbox "Password" [ref=3]
- link "Forgot password?" [ref=4]
```

### 优势

| 对比 | 截图 | 语义快照 |
|------|------|----------|
| 大小 | 5MB | <50KB |
| Token成本 | 极高（图像token贵） | 仅文本，极低 |
| 解析准确性 | 依赖视觉理解 | 结构化，准确 |
