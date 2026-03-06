---
标题: "在MoltBot/ClawdBot，火山方舟模型服务"
链接: ""
来源: "waytoagi飞书知识库"
作者: "[[waytoagi]]"
创建时间: 2026-03-06T23:05:00+08:00
摘要: "介绍如何在MoltBot/ClawdBot（OpenClaw）中接入字节跳动火山引擎方舟模型服务，使用国内大模型"
亮点:
  - "火山方舟提供字节系豆包等大模型API，国内访问速度快、稳定性高"
  - "支持在OpenClaw中配置自定义API，灵活替换底层大模型"
  - "通过修改openclaw.json的baseURL即可切换到火山方舟接口"
  - "国内模型服务费率更低，适合高频使用场景"
重难点:
  - "火山方舟API格式与OpenAI兼容，需要正确填写baseURL和模型名称"
  - "需要在火山引擎控制台开通对应模型权限并获取API Key"
  - "模型ID命名规则与官方文档一致，填写错误会导致调用失败"
tags:
  - "clippings"
  - "OpenClaw"
  - "火山方舟"
  - "模型配置"
字数: 500
状态: "未开始"
---

# 在MoltBot/ClawdBot，火山方舟模型服务

## 火山方舟是什么

字节跳动旗下的大模型API服务平台，提供：
- 豆包系列模型
- 其他字节系AI能力
- 国内节点，访问稳定

## 接入步骤

### 步骤一：获取API Key

1. 访问火山引擎控制台：https://console.volcengine.com/ark
2. 创建API Key
3. 开通对应模型的访问权限

### 步骤二：修改OpenClaw配置

编辑 `~/.openclaw/openclaw.json`：

```json
{
  "models": {
    "providers": {
      "volc": {
        "baseUrl": "https://ark.cn-beijing.volces.com/api/v3",
        "apiKey": "你的火山方舟API Key",
        "api": "openai",
        "models": [
          {
            "id": "doubao-pro-32k-241215",
            "name": "豆包Pro 32K",
            "input": ["text"],
            "contextWindow": 32000,
            "maxTokens": 4096
          }
        ]
      }
    }
  }
}
```

### 步骤三：切换到火山方舟模型

在TUI界面输入 `/model`，搜索并选择火山方舟模型。

## 使用建议

- 适合：日常对话、文本处理、内容创作
- 火山方舟按token计费，价格实惠
- 国内用户延迟低，响应快
- 与其他模型并行配置，根据任务选择最优模型
