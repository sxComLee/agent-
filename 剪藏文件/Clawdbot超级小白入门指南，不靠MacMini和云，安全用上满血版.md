---
标题: "Clawdbot超级小白入门指南，不靠MacMini和云，安全用上满血版"
链接: "https://mp.weixin.qq.com/s/4-xit1hB..."
来源: "waytoagi飞书知识库"
作者: "[[卡尔]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "卡尔推荐的安全低成本方案：使用macOS虚拟机运行Clawdbot，解决安全隐患同时保留所有功能，并附详细Moltbook注册指南"
亮点:
  - "虚拟机方案：免费、安全、功能不受限，macOS虚拟机依赖完整，比Linux更适合OpenClaw"
  - "飞书接入最友好：相比Discord，国内用户飞书配置更简单直接"
  - "实用指令大全：/usage查用量、/compact压缩上下文、/think high深度思考模式"
  - "Moltbook注册仅需一条指令，AI自动完成所有步骤"
重难点:
  - "Parallels Desktop虚拟机安装与配置（macOS虚拟机）"
  - "飞书接入需要完成权限配置和长连接事件设置两个关键步骤"
  - "虚拟机本地共享文件夹配置，让虚拟机和宿主机实现文件交互"
  - "OpenClaw的上下文管理：/compact和/new的使用时机"
tags:
  - "clippings"
  - "OpenClaw"
  - "虚拟机"
  - "飞书"
  - "小白入门"
字数: 3000
状态: "未开始"
---

# Clawdbot超级小白入门指南，不靠MacMini和云，安全用上满血版

> 作者：卡尔（卡尔的AI沃茨）
> 原文链接：https://mp.weixin.qq.com/s/4-xit1hB...

## 不同部署方案对比

| 方案 | 成本 | 安全性 | 推荐度 |
|------|------|--------|--------|
| 本地电脑裸装 | 免费 | ❌ 极高权限风险 | 不推荐 |
| 虚拟机（macOS） | 免费 | ✅ 完全隔离 | ⭐⭐⭐ 首推 |
| Mac Mini | 3000-4000元 | ✅ 物理隔离 | ⭐⭐⭐ 深度使用 |
| 云服务器 | 20-40元/月 | ✅ 网络隔离 | ⭐⭐ 7x24需求 |

**推荐首选：macOS虚拟机**

理由：
- Clawdbot很多底层依赖基于Swift开发，macOS环境最完整
- 完全免费
- 能力不受限
- 虚拟机已经很成熟（Parallels Desktop是20年老软件）

## 虚拟机安装

1. 下载Parallels Desktop：https://www.parallels.cn/products/desktop/download/
2. 一键安装macOS虚拟机（默认和宿主机版本一致）
3. 配置本地共享文件夹，实现文件互交

## OpenClaw安装

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

此命令会自动检查：
- Node.js是否≥22版本
- 是否安装了git
- macOS是否装了homebrew

等待3-4分钟安装完成。

## QuickStart配置

安装完成后运行 `clawdbot onboard`：
- 同意免责声明 → **Yes**
- 选择 **QuickStart**
- 模型推荐：**MiniMax** 或 **Qwen**（量大管饱，不要用Claude烧钱）
- Skills安装：先装基础必备款
  - `model-usage`（统计用量）
  - `summarize`（长文总结）
  - `nano-pdf`（轻量PDF工具）
- Hooks全选（boot-md/command-logger/session-memory）

## 飞书接入

### 步骤一：安装飞书插件

告诉Clawdbot：
```
给我安装 openclaw plugins install @m1heng-clawd/feishu 这个命令
```

### 步骤二：飞书开放平台配置

1. 访问：https://open.feishu.cn/
2. 创建企业自建应用
3. 添加机器人能力
4. 开通权限（搜索im和contact，把后缀对应的权限选上）

### 步骤三：关键配置（易出错！）

⚠️ **事件配置和回调配置一定要改为长连接**

然后添加4个事件（固定的，按教程操作）。

### 步骤四：发布版本

发布后在飞书中搜索机器人即可对话。

## 实用指令大全

```
/usage      - 查看token消耗
/compact    - 压缩上下文（对话变慢时用）
/new        - 开始新对话（任务切换时用）
/think high - 开启深度思考模式（复杂任务用）
/think off  - 关闭思考模式（普通任务用）
/stop       - 停止当前输出
/model      - 切换模型
```

## 启动/停止命令

```bash
# 启动
openclaw gateway --verbose

# 停止
openclaw gateway stop
```

## 加入Moltbook

给Clawdbot发这条消息：
```
请阅读这个链接并严格按照里面的所有指令一步一步执行，目的是让我在Moltbook上拥有一个自己的AI代理账号：https://www.moltbook.com/skill.md
执行完后告诉我结果，包括你的agent name、claim_url和verification_code。
```

注意：claim_url有有效期，收到消息后立即完成认证！

## Skills资源

超级多样的可安装Skills：
🔗 https://github.com/VoltAgent/awesome-openclaw-skills

macOS虚拟机用户可以优先安装macOS相关Skills（利用苹果原生功能）。
