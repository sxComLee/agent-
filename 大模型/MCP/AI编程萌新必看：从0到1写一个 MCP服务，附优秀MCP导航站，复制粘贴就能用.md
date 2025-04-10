---
标题: "-AI编程萌新必看：从0到1写一个 MCP服务，附优秀MCP导航站，复制粘贴就能用"
链接: "https://mp.weixin.qq.com/s/y4f-TiK7kOe_vK2sh7It8A"
作者: "[[向阳乔木]]"
创建时间: "2025-04-10T18:37:10+08:00"
摘要:
tags:
  - "clippings"
字数: "449"
状态: "未开始"
---
# [[预读法介绍]]
### 预读问题  
**基于你的目标**：
- Q1: 
- Q2: 
- Q3:   

### 关键图表/代码  
![[提取的图表或代码片段]]
### 初步关联  
- 已知：[[已掌握的相关知识]]  
- 未知：`#待探索`  

### 输出目标
- [ ] 

### 总结
- 是什么
- 为什么
- 怎么用

# 内容
原创 向阳乔木 *2025年03月10日 18:40* *天津*

> 字数 1503，阅读大约需 8 分钟

**看再多MCP教程，都不如直接上手写一个。**

Deepseek等模型训练经验告诉我们：

**“干中学” 效率最高。**


本文推荐一些常用AI编程工具，然后一步步教你写一个 MCP 服务器。

最后，再推荐一些好用的 MCP 应用市场。

MCP 是未来让 AI Agent变得更简单易用的关键，趋势已非常明显，值得持续跟进学习。

## 工欲善其事必先利器

Claude Sonnet 3.5问世后，带动用这个模型的 AI编程工具大火。

下面是常见的 AI 辅助编程工具，付费的有Cursor、Windsurf，免费的可选Trae（字节出品）。

喜欢自定义和DIY的，推荐Visual Studio Code + Cline，再配置各种免费薅的 API key。

比如 Gemini 或者 火山方舟Deepseek V3，一定可以达到可用程度。

关于如何免费获取API key，之前写有教程：

[https://mp.weixin.qq.com/s/YiWFmq1j4xGlplM8cV1p3g?payreadticket=HCIiJXFQDeQJ0qTKy26ny\_9jDnXERx2o8HevkvLovUT2pcQ9YiwPI3HPOqibfueux6fGYzA](https://mp.weixin.qq.com/s?__biz=MzAwODIyOTQ4Mw==&mid=2649441962&idx=1&sn=3f0cfe780b813bd41002787d737f9b91&payreadticket=HCIiJXFQDeQJ0qTKy26ny_9jDnXERx2o8HevkvLovUT2pcQ9YiwPI3HPOqibfueux6fGYzA&scene=21#wechat_redirect "https://mp.weixin.qq.com/s?__biz=MzAwODIyOTQ4Mw==&mid=2649441962&idx=1&sn=3f0cfe780b813bd41002787d737f9b91&payreadticket=HCIiJXFQDeQJ0qTKy26ny_9jDnXERx2o8HevkvLovUT2pcQ9YiwPI3HPOqibfueux6fGYzA&scene=21#wechat_redirect")

### Cursor

https://www.cursor.com/ <sup><span>[1]</span></sup>

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib08WBODW1yL38jTA6d7zqiceAr02fFibMatRKAlibPBMATMUQDoM2Co2Yvw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### Windsurf：

https://codeium.com/windsurf <sup><span>[2]</span></sup>

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0pKEUibFibEVzRiafaxoibiaiazsXG6rT1ibJFMaRm2vvMbzw4rlS4f0k1eCkQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### Trae：

https://www.trae.ai/ <sup><span>[3]</span></sup>

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0kIFlZVIfkicVxu93kKWhuRS5SKJFu8xKRpIt4h8gQVF3nGxvH0EL9bQ/640?wx_fmt=png&from=appmsg)

### Visual Code + Cline

https://cline.bot/ <sup><span>[4]</span></sup>

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0yMDPa3icYAcDkYrTShdTIeiaBicSxl5PrK9WlOlc0DnhFW0k4IHCMbhmg/640?wx_fmt=png&from=appmsg)

## 手把手创建第一个MCP Server

有编程工具，接下来，手把手教完成第一个MCP server

### 第一步：打开系统终端或安装第三方工具

强推Warp，AI时代的 Terminal，有LLM加持，真的好用，且全平台支持（Linux、Windows、Mac）。

虽然要求注册账号登录有点怪，但也能理解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0tBeaEHjibybEXhBVKUykialTgicJTqceiceRUuZrMzUbvdoQLc9icYjcYrw/640?wx_fmt=png&from=appmsg)

官网下载：  
https://www.warp.dev/ <sup><span>[5]</span></sup>

### 第二步：创建MCP项目

终端中输入命令： `mkdir mcp-demo` ，敲回车

> 命令作用：创建一个文件夹，叫 mcp-demo

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0a9HTk7iaTHyN1MibiavPnmDe53jR4F4ZLyAniceKxcwSm0OCLhdMmezsiag/640?wx_fmt=png&from=appmsg)

输入: `cd mcp-demo` 进入文件夹

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0mqsDgXo5XLH8xcqb7dEBcA0icUVrY8nDmpdD7arUAZeLYPwiaAujNCDA/640?wx_fmt=png&from=appmsg)

输入: `touch main.py` 创建一个叫main.py的文件。

然后输入 `python -m venv myenv` 创建一个叫“myenv”的虚拟环境，避免Python库版本冲突。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib07RGjckI6Okvibic97xPfRjfomVq4ibYCQvuhiaKCaaCzWzQAGyNjx8ibNxg/640?wx_fmt=png&from=appmsg)

激活虚拟环境

- • macOS/Linux下输入： `⁠source myenv/bin/activate`
- • Windows 输入： `⁠myenv\Scripts\activate`
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0e6KibDx0IxCJTMthRdSibx4dyGyAA9BNicW6rvWdep0picSDE08JhsaQBQ/640?wx_fmt=png&from=appmsg)

### 第三步：安装SDK，输入代码

安装MCP的Python SDK，命令： `pip install mcp`

> 其他安装方法和介绍见：  
> https://github.com/modelcontextprotocol/python-sdk <sup><span>[6]</span></sup>

接着，用任意代码编辑器打开 main.py，输入以下内容：

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import httpx
from mcp.server.fastmcp import FastMCP

# 创建MCP服务器
mcp = FastMCP("Demo")

# 简单加法工具
@mcp.tool()
def add(a: int, b: int) -> int:
    """两数相加"""
    return a + b

# 直接运行时的入口点
if __name__ == "__main__":
    print("服务已启动")
```

创建一个最简单的MCP服务器，只提供一个工具：两个数字的加法。

## 使用 MCP 服务器

### Cursor 为例

首选项->Cursor Settings，打开如下图，点击“Add new MCP server”

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0SW8aq5ib0h8A8z3qo4BSo28JmkHicMiaywMmRH4iaQ0nS43XpVM0xfjfiaQ/640?wx_fmt=png&from=appmsg)

Name：随便起名  
Command： `mcp run /创建文件的完整目录/mcp-test/main.py`

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0Zx1ibE9LhhMQnErR0KonhvtSWY7uqUm98xe3MVONbgIFb76tm9SHWKg/640?wx_fmt=png&from=appmsg)

过一会，MCP服务器会启动，指示器会变绿色。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0xBCuOCiaH6tpicLbeMcuYIhQb6ORgok9WIpQVB8fl6Fdx3VbBavMen6Q/640?wx_fmt=png&from=appmsg)

Cursor右侧对话，输入 `add 6,88` ，调用MCP中的add完成计算。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0WxzibJxEzKNgwsG0gusNZhLsNibiaOssZ5YpsncSyGLuHs9oHFbgT9O9A/640?wx_fmt=png&from=appmsg)

### Cline 为例

打开Cline插件，按图示顺序点击

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0icKJrQdaHQYWj5bMzFYfw2q6r335qzy1DNOyrevicFTDCfsHVuCXWIOw/640?wx_fmt=png&from=appmsg)

打开MCP servers ->installed->Configure MCP Servers

编辑配置文件，添加一条：

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0yHeo7JRrHDNiajvA0QL6Ue5cfczeAWedr2DwTibOgDHY8PgPcnlytrmw/640?wx_fmt=png&from=appmsg)

```
"mcp-test": {
      "command": "mcp",
      "args": [
        "run",
        "/创建文件的完整目录/mcp-test/main.py"
      ],
      "disabled": false,
      "autoApprove": [
        "add"
      ]
    }
```

### 持续迭代MCP功能

如果觉得上面的例子太简单。

你可以在这个main.py 代码 基础上迭代，给MCP增加更多Tool，甚至还可以看官方文档，增加Resource或Prompt调用。

举个例子，再增加一个叫call\_llm的工具，让它调用火山方舟的Deepseek V3回答问题。

迭代后代码如下：

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import httpx
from mcp.server.fastmcp import FastMCP

# 创建MCP服务器
mcp = FastMCP("Demo")

# 简单加法工具
@mcp.tool()
def add(a: int, b: int) -> int:
    """两数相加"""
    return a + b

# LLM API调用工具
@mcp.tool()
def call_llm(prompt: str, system_prompt: str = "你是人工智能助手.") -> str:
    """调用LLM API获取回答"""
    # API配置
    url = "https://ark.cn-beijing.volces.com/api/v3/chat/completions"
    headers = {
        "Content-Type": "application/json",
        "Authorization": "Bearer API key"
    }
    data = {
        "model": "ep-20250222222029-sx6sd",
        "messages": [
            {"role": "system", "content": system_prompt},
            {"role": "user", "content": prompt}
        ]
    }
    
    try:
        # 发送请求
        response = httpx.post(url, headers=headers, json=data, timeout=30.0)
        response.raise_for_status()
        result = response.json()
        
        # 提取回答
        if "choices" in result and len(result["choices"]) > 0:
            return "回答：" + result["choices"][0]["message"]["content"]
        else:
            return "回答：未获得有效回答"
    except Exception as e:
        return f"回答：发生错误: {str(e)}"

# 直接运行时的入口点
if __name__ == "__main__":
    print("服务已启动")
```

输入Tool名称，发给AI： call\_llm “李白是谁”，输出如下：

### Cursor结果

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib047KWf7RxZCzwCUnL8dYtNzpN3iacB6L03DFguicCxepQSSMk4oJPQ6Ng/640?wx_fmt=png&from=appmsg)

### Cline结果

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0oucLuY9GChXiclFibA9oiak2KT4NWGNdFO5CcSibbqMWib9aO4CAPdqqaCA/640?wx_fmt=png&from=appmsg)

## 好用的 MCP 市场

### Smithery.ai

华裔青年Henry Mao打造的产品。  
https://smithery.ai/ <sup><span>[7]</span></sup>

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib09WicVbA6nibaVeBdv02fFa5jXHicEpcwuLpNeu2XtSSoWtMgiaJbvGPqCg/640?wx_fmt=png&from=appmsg)

目前发现交互体验最好的MCP导航网站，每个MCP Server都搭配或生成使用代码：

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0J5QqSvAZpRzehE1eT5yI1BpOMm8r12ymr7yTic0ibQdXS7ImibGKwpticQ/640?wx_fmt=png&from=appmsg)

### MCP.so

著名独立开发者idoubi开发的 MCP.so 导航，收录了2k多个Server，数量庞大。

作者 X 账号：

https://x.com/idoubicc <sup><span>[8]</span></sup>

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0qiab2ania2pPLP9r2bcAUefNT9j7VVib4CzoPuPMw5SlY30bu1QibU8aCQ/640?wx_fmt=png&from=appmsg)

### MCPs.live 搜索

好友最近研究几个MCP客户端实现，顺手借助AI开发了一个MCP搜索站。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0TibhnbFGEXLQRk14wzxCxfaCO6ibbFeZ9Z0k8NE6k5ia4kF9gGzoZuDicQ/640?wx_fmt=png&from=appmsg)

### Composio MCP

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0OeFuFyicEX9Ryt1k9N4Wbh9ibicx7s625XAEes65pyPMkRIo4LJMDE5Eg/640?wx_fmt=png&from=appmsg)

https://mcp.composio.dev/ <sup><span>[9]</span></sup>

这个站点特别的地方是，每个MCP都可以生成一个SSE URL，开发者技能在自己应用中集成这个MCP的能力，无需从0开发。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0s3Nts5sBbzlw1e5QFlQnGMIL02G88BQZhlSP7abUY47qibjOmACMumg/640?wx_fmt=png&from=appmsg)

### Pulse MCP

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0ELGZh5IUuc4icQ0vd9l8nLZlRst6g0ib262FibDYW3PbvX4dZDwOSCZPg/640?wx_fmt=png&from=appmsg)

也是设计很棒的MCP站，收录了1500多个Server。

比较特别的是，网站提供了很多Use Case，让人更直观了解怎么用。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib0CooHrKPK9b32yRmlnnXBQ6YQ5qFFWK70YozQia0I3DO03rRvcDMCUcA/640?wx_fmt=png&from=appmsg)

### 更多说明

MCP 导航和市场在飞速扩张，但质量稂莠不齐，注意甄别。

预计，未来会出现很多付费MCP Server，也会出大量支持 MCP的客户端软件，不仅仅是现在的 AI编程工具。

比如群友 Vaayne 正在开发的著名 AI 聊天客户端 Cherry Studio，目前在紧锣密鼓测试 MCP功能，估计很快能上线。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib01O2Nyvtrzbfe6S3SXGOMr9uedUMb4Nb4uWicMViaINYEicfiajvphuFvYQ/640?wx_fmt=png&from=appmsg)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/jibL99tg2bCWMEIxY1oo5ERKCSfnycdib05oX8YQVXZS1xwgUHAJkkLRQ4ibLYBbAknlsIdl0PLdLJT3e2g99KcRw/640?wx_fmt=jpeg&from=appmsg)

如果想了解更多MCP相关知识，可参考

https://xiangyangqiaomu.feishu.cn/wiki/PXAKwEgLQir9rkkV1zjcGnMHntg?fromScene=spaceOverview <sup><span>[10]</span></sup>

如想进群学习，加我微信： vista8

## 后记

这两天看了一些MCP教程，很多只有例子，没说怎么配置环境、怎么在Cursor、Cline等编辑器中配置。

看完教程，还是知道怎么搞，也不知道怎么开发自己的MCP Server。

索性写个教程，一方面是自己的学习总结，另一方面帮助和我一困惑的人。

#### 引用链接

`[1]` https://www.cursor.com/:  
`[2]` https://codeium.com/windsurf:  
`[3]` https://www.trae.ai/:  
`[4]` https://cline.bot/:  
`[5]` https://www.warp.dev/:  
`[6]` https://github.com/modelcontextprotocol/python-sdk:  
`[7]` https://smithery.ai/:  
`[8]` https://x.com/idoubicc:  
`[9]` https://mcp.composio.dev/:  
`[10]` https://xiangyangqiaomu.feishu.cn/wiki/PXAKwEgLQir9rkkV1zjcGnMHntg?fromScene=spaceOverview:  

  

向阳乔木

干货满满，一杯咖啡的鼓励！

 **微信扫一扫赞赏作者**

修改于 2025年03月10日

修改于 2025年03月10日 继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过