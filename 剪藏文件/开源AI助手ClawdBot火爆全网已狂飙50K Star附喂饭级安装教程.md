---
标题: "开源AI助手ClawdBot火爆全网，已狂飙50K Star！附喂饭级安装使用教程"
链接: "https://mp.weixin.qq.com/s/nAC-Z-Bz..."
来源: "waytoagi飞书知识库"
作者: "[[袋鼠帝]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "袋鼠帝的保姆级Clawdbot安装教程，5步完成从购买云服务器到Telegram机器人对话的全流程，附真实使用评测"
亮点:
  - "AI从'被动'走向'主动'的范式转变：Clawdbot是真正主动帮你干活的数字员工"
  - "五步极速搭建教程：选服务器→一键安装→傻瓜配置→创建Telegram Bot→赋予人设"
  - "实测证明：Clawdbot爬取多个信息源生成早报的能力确实强大"
  - "相比Claude Code等CLI工具，Clawdbot工程化程度更高，普通人体验更好"
重难点:
  - "国内服务器Telegram无法联通问题：需要在配置文件中禁用Telegram，改用TUI模式"
  - "配置文件修改方式：/root/.clawdbot/clawdbot.json中将telegram的enabled改为false"
  - "向导中多选界面的操作方式：上下键+空格选中多个，回车提交"
  - "API Key的获取：GLM/Minimax等国内模型的coding plan是性价比选择"
tags:
  - "clippings"
  - "OpenClaw"
  - "Telegram"
  - "安装教程"
字数: 3000
状态: "未开始"
---

# 开源AI助手ClawdBot火爆全网，已狂飙50K Star！附喂饭级安装教程

> 作者：袋鼠帝（袋鼠帝AI客栈）
> 原文链接：https://mp.weixin.qq.com/s/nAC-Z-Bz...

## Clawdbot到底是什么？

生活在你聊天软件里的AI助手，不是"人找AI"，而是"AI主动找人"。

### 三大核心优势

1. **它是"活的"**：有永久记忆，昨天告诉它不吃香菜，下周它还记得
2. **它很主动**：不等你提问，主动通知你股票跌了、航班可能延误
3. **它是你的**：数据在自己服务器上，隐私更可控

### 真实案例

- 用户语音说"分析网站数据、写博客、更新元数据、发领英"→ 睡一觉醒来全搞定了
- 用户让它监控股票 → 开车时收到Telegram消息："老板，股票跌了，建议补仓"

## 30分钟极速搭建教程

### 第一步：购买服务器（5分钟）

推荐方案：
- **境外VPS**：新加坡/香港节点，2核4G
- 推荐：Evoxt、AWS免费套餐
- 七牛云也有海外服务器（东京/东南亚），约20元/月
- 腾讯云/阿里云也有Moltbot镜像，直接省去安装

### 第二步：一键安装（2分钟）

SSH连接服务器后执行：
```bash
curl -fsSL https://clawd.bot/install.sh | bash
```
（等待自动安装依赖，可以去泡杯咖啡）

### 第三步：傻瓜配置向导（10分钟）

```bash
clawdbot onboard
```

- 选择 "Quick Start"
- 配置模型（推荐GLM coding plan）
- 选择聊天渠道（推荐Telegram）

**多选界面操作**：上下键移动 + 空格选中 + 回车提交

### 第四步：创建Telegram机器人（3分钟）

1. 打开Telegram，搜索 `@BotFather`
2. 发送 `/newbot`，给机器人起名
3. 获取Token并粘贴到配置中

### 第五步：赋予灵魂（1分钟）

配置完成后，给Clawdbot设定人设：
```
你叫贾维斯，你的任务是帮我管理日程和整理信息。
```

## ⚠️ 国内服务器的坑

**问题**：国内服务器无法连通Telegram，启动报错。

**解决**：
1. 打开配置文件：`/root/.clawdbot/clawdbot.json`
2. 找到 `telegram` 字段
3. 将 `"enabled": true` 改为 `"enabled": false`

然后启动：
```bash
clawdbot gateway  # 开启网关
clawdbot tui      # 启动TUI界面，本地测试
```

## 使用评价

### 优点
- 交互自然，像和朋友聊天
- 能力强大（有权限可操控所有工具）
- 隐私安全（数据在自己服务器）
- 工程化程度高，比Claude Code对普通人更友好
- 成本低（软件免费开源）

### 缺点
- 仍有动手门槛（买服务器+配API Key）
- 稳定性依赖模型API（API宕机则大脑失灵）
- 复杂任务需要前期磨合调教

## 结语

> "Clawdbot的爆火，其实释放了一个强烈的信号：2026年，AI将从'被动'走向'主动'。"

拥有7x24小时AI助手和没有AI助手的人，效率差距会越来越大。
