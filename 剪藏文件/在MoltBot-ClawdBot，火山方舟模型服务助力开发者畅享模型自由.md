---
标题: "在MoltBot/ClawdBot，火山方舟模型服务助力开发者畅享模型自由"
链接: "https://mp.weixin.qq.com/s/4083wLHH..."
来源: "waytoagi飞书知识库"
作者: "[[火山引擎]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "火山引擎官方介绍如何在MoltBot中接入火山方舟模型，提供Coding Plan套餐配置和企业客户详细配置流程"
亮点:
  - "火山方舟已全面适配Moltbot：豆包Seed/Code、GLM-4.7、DeepSeek-V3.2、Kimi-K2-Thinking等模型"
  - "Coding Plan套餐：新用户首月9.9元（原40元），解决Token消耗大的成本问题"
  - "Auto模式：火山方舟根据任务场景自动选择最优模型，减少手动选择负担"
  - "支持飞书文档+飞书消息+豆包语音输入法全套集成，打通国内办公生态"
重难点:
  - "Coding Plan和普通API的baseURL不同（coding/v3 vs api/v3），配置时注意区分"
  - "需要在开通管理页面选择目标模型，而非在Moltbot工具内修改"
  - "企业客户需要手动修改三处配置：主要模型配置、模型供应商配置、认证配置"
  - "修改配置后需先Save再点Update才能生效"
tags:
  - "clippings"
  - "OpenClaw"
  - "火山方舟"
  - "豆包"
  - "模型配置"
字数: 1500
状态: "未开始"
---

# 在MoltBot/ClawdBot，火山方舟模型服务

> 作者：火山引擎（面向AI时代的）
> 原文：https://mp.weixin.qq.com/s/4083wLHH...

## 火山方舟已全面适配Moltbot

支持的模型：
- **Doubao-Seed-Code**（代码能力强）
- **GLM-4.7**
- **DeepSeek-V3.2**
- **Kimi-K2-Thinking**
- **Auto模式**（根据场景自动选择最优模型）

## Coding Plan方案

| 套餐 | 价格 |
|------|------|
| 新用户首月 | 9.9元（原40元） |
| 首季 | 60元（原120元） |
| 推荐好友优惠 | 额外9折，最低8.9元 |

## 个人开发者接入（Coding Plan）

Coding Plan的配置信息：
```json
{
  "baseUrl": "https://ark.cn-beijing.volces.com/api/coding/v3",
  "apiKey": "YOUR_API_KEY",
  "api": "openai-completions"
}
```

主要模型配置：
```json
"model": {
  "primary": "doubao/ark-code-latest"
},
"models": {
  "doubao/ark-code-latest": { "alias": "doubao" }
}
```

## 企业客户接入（普通API）

### 第一步：查看当前配置

方式一：Web UI中 Settings-Config-Authentication → 选Raw
方式二：终端查看
```bash
cat ~/.clawd/config.json
```

### 第二步：修改三处配置

**1. 主要模型配置**（以豆包1.8为例）
```json
"model": {
  "primary": "doubao/doubao-seed-1-8-251228"
},
"models": {
  "doubao/doubao-seed-1-8-251228": { "alias": "doubao" }
}
```

**2. 模型供应商配置**
```json
"models": {
  "providers": {
    "doubao": {
      "baseUrl": "https://ark.cn-beijing.volces.com/api/v3",
      "apiKey": "YOUR_API_KEY",
      "api": "openai-completions"
    }
  }
}
```

**3. 认证配置**
```json
"auth": {
  "profiles": {
    "doubao:default": { "provider": "doubao", "mode": "api_key" }
  }
}
```

### 第三步：保存并重启

先点击 **Save**，再点击 **Update**。

## 使用效果

火山引擎实测案例：
> 豆包大模型 + 飞书消息 + 飞书文档接入Moltbot，配合豆包语音输入法，打开手机就能指挥MoltBot查资料、写文档，爽感满格！

## 安全提醒

- Moltbot可访问设备所有数据和数字账户，存在安全隐患
- 建议在专用设备（而非含敏感信息的设备）上部署
- 定期检查权限设置
- 为API密钥设置访问限制
