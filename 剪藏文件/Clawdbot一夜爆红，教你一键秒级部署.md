---
标题: "Clawdbot一夜爆红，教你一键秒级部署"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[waytoagi]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "Clawdbot爆红背景及一键秒级云端部署方法，利用腾讯云/阿里云镜像模板实现极速上手"
亮点:
  - "腾讯云轻量应用服务器提供Moltbot一键部署镜像，5分钟内完成部署"
  - "无需手动安装Node.js等依赖，镜像内已预配置好运行环境"
  - "选择境外服务器节点（新加坡/香港）解决API访问限制问题"
  - "云端部署24小时不间断运行，手机随时指挥AI完成任务"
重难点:
  - "服务器购买和配置的费用规划（推荐从最低配置起步）"
  - "Clawdbot onboard配置时的键盘操作方式（方向键+回车，非鼠标）"
  - "Discord/飞书通道配对步骤易出错，需要仔细执行配对命令"
  - "nohup后台运行命令的正确使用，避免关闭终端后服务停止"
tags:
  - "clippings"
  - "OpenClaw"
  - "云部署"
  - "腾讯云"
字数: 900
状态: "未开始"
---

# Clawdbot一夜爆红，教你一键秒级部署

## 爆红背景

Clawdbot（现改名OpenClaw）一夜之间成为GitHub上增长最快的开源项目：
- 72小时内：9000 → 6万 Star
- 一周后：突破18万 Star
- Mac Mini因此缺货

## 一键部署方案

### 腾讯云方案（推荐）

1. **选择服务器**
   - 访问腾讯云轻量应用服务器
   - 配置：2核2G起步
   - 地区：**新加坡或香港**（关键！避免API访问问题）
   - 镜像：选择 **Moltbot/Clawdbot** 应用模板

2. **登录服务器**
   - 控制台扫码登录，或SSH连接
   
3. **配置OpenClaw**
   ```bash
   clawdbot onboard
   ```
   操作说明：
   - ⬆️⬇️ 方向键：切换选项
   - 回车：确认选择
   - 空格：多选（skills选择时）

4. **配置向导**
   - 同意免责声明 → Yes
   - 选择 QuickStart
   - 模型选择（建议国内用户选智谱GLM或Kimi）
   - 输入API Key
   - 选择通道（Discord/飞书/Telegram等）

5. **启动服务**
   ```bash
   # 临时启动
   clawdbot gateway --port 18789 --verbose
   
   # 持久运行（关机需重启）
   nohup clawdbot gateway --port 18789 --verbose > /tmp/clawdbot-gateway.out 2>&1 & disown
   ```

## Discord配对完整流程

1. 启动Gateway
2. 在Discord中私聊你的Bot
3. 记录配对码
4. Ctrl+C 停止Gateway
5. 执行：`clawdbot pairing approve discord <配对码>`
6. 重新启动Gateway
7. 返回Discord，正常聊天即表示成功！

## 常用运维命令

```bash
# 查看版本
clawdbot --version

# 重新配置
clawdbot onboard

# 查看日志
tail -f /tmp/clawdbot-gateway.out
```
