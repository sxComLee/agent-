---
标题: "Sim：moltbot超详细保姆级教程（原clawdbot）--discord版本"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[Sim]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "Sim的超详细保姆级教程，基于腾讯云+Discord，手把手完成moltbot从服务器购买到Discord配对的全过程"
亮点:
  - "全流程截图教程，每一步操作都有截图辅助，零基础可上手"
  - "腾讯云一键部署方案+Discord配置，是最快完成部署的路径之一"
  - "详细说明了智谱GLM-4.7等国内模型的接入方式，免翻墙"
  - "Skills安装完整列表及说明，帮助用户了解可扩展的能力"
重难点:
  - "Discord开发平台配置步骤较多，每步需按照教程操作不能跳步"
  - "服务器购买时需实名认证，对部分用户是额外障碍"
  - "nohup持久化运行命令需要在Discord完成配对后才能使用"
  - "Skills安装可跳过（Skip for now），避免因网络问题卡在安装环节"
tags:
  - "clippings"
  - "OpenClaw"
  - "Moltbot"
  - "Discord"
  - "保姆级教程"
字数: 2000
状态: "未开始"
---

# Sim：moltbot超详细保姆级教程（原clawdbot）--discord版本

## 教程适用场景

- 使用腾讯云轻量服务器（推荐新加坡/香港节点）
- 通过Discord与moltbot交互
- 使用国内模型（智谱GLM系列）

## 完整流程

### 第一步：购买腾讯云服务器

1. 访问腾讯云轻量应用服务器
2. 配置：**至少2核2G**
3. 地区：**新加坡或香港**（非常重要！大陆节点有网络问题）
4. 镜像：找到并选择 **moltbot镜像**
5. 实名认证（如未认证）

### 第二步：登录服务器

1. 进入控制台 → 轻量应用服务器
2. 点击登录按钮，扫码进入
3. 等待命令行界面出现

### 第三步：配置moltbot

```bash
clawdbot onboard
```

#### 配置细节

- **免责声明**：选 Yes（了解高权限风险）
- **启动模式**：选 QuickStart
- **模型选择**：推荐选 Z.AI（智谱）
- **API Key**：粘贴智谱API密钥（从open.bigmodel.cn获取）
- **二次模型确认**：保持当前选择（Keep current）
- **通道选择**：选 Discord

### 第四步：Discord配置

#### 4.1 创建Discord应用

1. 访问：https://discord.com/developers/applications
2. 点击右上角 **New Application**
3. 填写应用名称

#### 4.2 获取Bot Token

1. 进入应用 → Bot页面
2. 点击 **Reset Token**
3. 复制Token并保存

#### 4.3 开启必要权限

1. 找到 **Message Content Intent**
2. 开启此选项
3. 点击页面最下方 **Save Changes**

#### 4.4 配置OAuth2

1. 进入 **OAuth2** 页面
2. Scopes中选择 `bot`
3. Bot Permissions中选择：
   - `Manage Messages`
   - `Read Message History`
4. 复制底部生成的邀请链接

#### 4.5 创建Discord服务器并添加Bot

1. 在Discord客户端点击左侧 `+` 创建服务器
2. 在浏览器中打开之前复制的邀请链接
3. 选择刚创建的服务器，添加Bot

### 第五步：完成配置

1. 将Discord Token粘贴到腾讯云配置界面
2. Discord频道权限：选第二个选项（更安全）
3. Skills安装：可选 **Skip for now** 跳过
4. Hooks安装：建议全选（boot-md, command-logger, session-memory）
5. 等待配置完成

### 第六步：配对Discord

1. 启动Gateway：
   ```bash
   clawdbot gateway --port 18789 --verbose
   ```
2. 在Discord中找到Bot，点击名称进入私聊
3. 发送任意消息，Bot返回配对码
4. 回到服务器，按 Ctrl+C 停止Gateway
5. 执行配对：
   ```bash
   clawdbot pairing approve discord <配对码>
   ```
6. 重新启动：
   ```bash
   clawdbot gateway --port 18789 --verbose
   ```
7. 在Discord私聊窗口发消息，正常回复即成功！🎉

## Skills说明

主要的可安装Skills：
- `session-memory`：保存对话记忆
- `command-logger`：操作日志记录
- `boot-md`：启动时加载偏好设置
- `obsidian`：Obsidian笔记集成
- `summarize`：网页/视频内容摘要
- `nano-pdf`：PDF处理工具
- `weather`：天气查询

## 持久化运行

```bash
nohup clawdbot gateway --port 18789 --verbose > /tmp/clawdbot-gateway.out 2>&1 & disown
```
关机后需重新执行此命令。
