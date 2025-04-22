---
标题: "这个开源真tm牛！一键将FastAPI转换成MCP服务器，以后API=MCP。"
链接: "https://mp.weixin.qq.com/s/CLJMzAv3GYTwb9owgAQEwQ"
作者: "[[开源AI]]"
创建时间: "2025-04-22T12:20:28+08:00"
摘要:
tags:
  - "clippings"
  - "mcp"
  - "fastApi"
字数: "149"
状态: "未开始"
---
# [[学习方法/预读法介绍]]
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
#flashcards

![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/l2VB7h1M5Nb69coNJjYwLrdDicA1kP6DUhlXhePTVYrhoZAuibXQhPthJOnFxIiaZvibmjL3GjGytM1LVUhBq7tJDg/0?wx_fmt=jpeg)

原创 开源AI [开源AI项目落地](https://mp.weixin.qq.com/s/)

2025-04-18 19:06:59

精确发文时间由壹伴提供

手机阅读

这是我这个月看过的最有价值的开源项目了。

  

MCP发布之后，很多粉丝朋友都有疑问，MCP跟API有什么区别呢？

  

简单来说， **MCP就是规定格式的API** ，这样才可以被AI模型来调用。

  

现在有海量的API，但都没有做成MCP，如果你想调用的话还要重新去写一遍，很麻烦！

  

**FastAPI-MCP的出现，解决了这个问题，它能把FastAPI转换成MCP。**

  

**而且非常简单，只需要复制一段代码加进去就能用了。**

  

这就是他牛的地方。

  

FastAPI都实现了，其他的像是Gin、Spring Boot这些还会远吗？

  

**以后就可以认为，API=MCP了。**

  

**扫码加入AI交流群**

**获得更多技术支持和交流**

**（请注明自己的职业）**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/l2VB7h1M5Nb69coNJjYwLrdDicA1kP6DU8pNAjlfngd92np8ntrQytZdd0I0rpLnOWEC2mExibn3val3j2OIbNAg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

**项目简介**

  

FastAPI-MCP能自动把FastAPI端点转化为MCP工具。它可直接集成到 FastAPI 应用中，无需复杂配置，自动发现并转换所有端点，还能保留请求和响应模型的架构以及端点文档。支持 Python 3.10+，采用 MIT 许可协议，让开发者轻松实现 FastAPI 与 MCP 的高效对接。

  

**DEMO**

  

  

**功能特点**

  

**集成与配置特性**

  

- **直接集成：** 可直接将 MCP 服务器挂载到 FastAPI 应用中。
- **零配置：** 只需指向 FastAPI 应用即可工作，无需复杂配置。
- **灵活部署：** 既可以将 MCP 服务器挂载到同一应用，也能单独部署。

  

**端点处理特性**

  

- **自动发现：** 能够自动发现所有 FastAPI 端点，并将其转换为 MCP 工具。
- **工具命名：** 使用 FastAPI 路由中的 operation\_id 作为 MCP 工具名称，建议显式指定以获得更清晰直观的工具名。

  

**模式与文档特性**

  

- **保留模式：** 保留请求模型和响应模型的模式。
- **保留文档：** 保留所有端点的文档，如同在 Swagger 中一样。

  

**高级配置特性**

  

- **自定义模式描述：** 可以在工具描述中包含所有可能的响应模式以及完整的 JSON 模式。
- **自定义暴露端点：** 可通过 include\_operations、exclude\_operations、include\_tags、exclude\_tags 等参数对暴露的端点进行筛选。

  

**使用方法**

  

简单的离谱。。。小学生都能操作。

  

首先，你需要安装一个python包。

  

然后复制下面这段代码放到FastAPI里就行了。。。

  

```python
from fastapi import FastAPIfrom fastapi_mcp import FastApiMCPapp = FastAPI()mcp = FastApiMCP(    app,    # Optional parameters    name="My API MCP",    description="My API description",    base_url="http://localhost:8000",)# Mount the MCP server directly to your FastAPI appmcp.mount()
```

  

虽然但是，就这么容易。

  

**项目链接**

  

https://github.com/tadata-org/fastapi\_mcp

  

  

关注「 **开源AI项目落地** 」公众号

与AI时代更靠近一点  

github 193

开源项目 206

人工智能 264

MCP 3

API 2

继续滑动看下一个

开源AI项目落地

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功