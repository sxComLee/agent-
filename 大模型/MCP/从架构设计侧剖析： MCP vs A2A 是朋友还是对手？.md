---
标题: "从架构设计侧剖析： MCP vs A2A 是朋友还是对手？"
链接: "https://mp.weixin.qq.com/s/GLjDJFW4UiTZ1va1yZvgAw?clicktime=1744782777&enterid=1744782777&scene=90&subscene=236"
作者: "[[玄姐]]"
创建时间: "2025-04-22T12:19:05+08:00"
摘要:
tags:
  - "clippings"
  - "mcp"
  - "a2a"
  - "架构"
字数: "730"
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

原创 玄姐

2025-04-16 08:03:10

精确发文时间由壹伴提供

手机阅读

大家好，我是玄姐。  

Anthropic 推出的 MCP（模型上下文协议）取得了成功，这显然激发了 AI 行业里的其他参与者，大家都想来定义一些开放协议，好用在 AI Agent 系统（Agentic Systems）的集成里。

上周周，谷歌公开发布了一个叫 A2A（Agent2Agent）的开放协议，目标是规范多 AI Agent 系统通信的实现方式。很多人（可能有点误解）说这两种协议是竞争关系，而不是互补关系。

谷歌公开说 A2A 和 MCP 是互补的 。这话挺合理的。但会不会有隐藏的长期竞争目标呢？我们会不会很快看到协议之间的竞争开始呢？

很多人都问我，我觉得这两种协议未来会不会变得有竞争？本文从架构设计来剖析 MCP vs A2A 是朋友有还是对手？

本文重点剖析：

- A2A 架构设计
	- MCP 架构设计
	- A2A 如何与 MCP 互补，反之亦然？
	- 长期来看，A2A 是否会在长期内取代 MCP？

下文详细剖析之。

  

****—* 1*** *—*

**A2A 架构设计**

第一、为什么会有 A2A？

现在越来越清楚，未来的 AI Agent 系统（Agentic Systems）将是多 AI Agent 的。而且，这些 AI Agent 会在彼此之间远程协作，每个 AI Agent 都可能使用不同的 AI Agent 框架（比如：LangGraph、AutoGen、CrewAI、Agent Development Kit 等）来实现。

这里面有 3个固有的问题 ：

1 、不同框架实现的 AI Agent 系统之间，不支持系统状态的转移和交换。

2 、远程 AI Agent 之间也无法转移系统状态。

3 、离线的 AI Agent 不共享工具、上下文和内存（包括系统状态）。

第二、A2A 解决方案

A2A 是一个开放协议，它为 AI Agent 之间提供了一种标准方式，无论底层开发框架或供应商如何，都可以进行协作。

![图片](https://mmbiz.qpic.cn/mmbiz_png/9TPn66HT9325qUbUw8Vuy5b9t4bY32K2qNYibWHHOVEoRUUvcAfVlgZSiaCZ4EFskI4T6jrSeSzy2NibxbptpTiatg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

根据谷歌的官方文档： A2A 协议促进了“客户端”和“远程” AI Agent 之间的通信。

简单来说，“客户端” AI Agent 创建任务并与“远程” AI Agent 沟通，期望执行某些工作或返回数据。

第三、A2A 架构设计

1、能力发现 ：所有实现 A2A 的 AI Agent 都通过“ Agent Card ”公开其能力目录。这有助于其他 AI Agent 发现给定 AI Agent 实现的潜在有用功能。

2、任务管理 ：通信协议，时代短期和长期任务变得更容易。它帮助通信中的 AI Agent 保持同步，直到请求的任务完成并返回答案。这很重要，因为有些 AI Agent 可能需要很长时间来执行工作，而且目前没有统一标准如何等待这种情况发生。

3、协作 ：AI Agent 可以相互发送消息以传达上下文、回复、工件或用户指令。

4、用户体验协商 ：这是一个很有趣的功能。它允许协商数据返回的格式，以符合用户界面的期望（比如：图像、视频、文本等）。

通过 A2A 公开的 AI Agent 的发现是一个重要话题。谷歌建议使用统一的位置来存储组织的“ Agent Card ”。

比如：

```xml
https://<DOMAIN>/<agreed-path>/agent.json
```

这并不意外，因为谷歌将处于最佳位置，能够索引全球所有可用的 AI Agent，可能创建一个类似于当前搜索引擎索引的全球 AI Agent 目录。

我喜欢 A2A 强调无需重新发明轮子，并且建立在现有标准之上：

1、该协议建立在现有、流行的标准之上 ，包括：HTTP、SSE、JSON-RPC，这意味着它更容易与企业日常使用的现有 IT 堆栈集成。

2、默认安全 - A2A 旨在支持企业级身份验证和授权，与 OpenAPI 的身份验证方案相当。

  

****—* 2*** *—*

**MCP 架构设计**

MCP（模型上下文协议）是由 Anthropic 定义的一个开放协议，标准化应用程序如何为大语言模型（LLM）提供上下文。更具体地说，它试图标准化基于 LLM 的应用程序与其他环境集成的协议。

在 AI Agent 系统（Agentic Systems）中，上下文可以通过多种方式提供：

1、外部数据 ：这是长期记忆的一部分。

2、工具 ：系统与环境交互的能力。

3、动态提示词 ：可以作为系统提示词（System Prompt）的一部分注入。

第一、为什么要标准化？

目前，AI Agent 应用的开发流程很混乱：

1、有许多 AI Agent 框架存在细微差异 。虽然看到生态系统蓬勃发展令人鼓舞，但这些细微差异很少能带来足够的价值，但可能会显著改变你的代码编写方式。

2、与外部数据源的集成通常是临时实现的 ，并且使用不同的协议，即使在组织内部也是如此。对于不同公司来说，这显然是如此。

2、工具在代码库中以略微不同的方式定义 。如何将工具附加到增强型 LLM 上也是不同的。

目标是提高我们创新 AI Agent 应用的速度、安全性以及将相关数据带入上下文的便利性。

第二、MCP 架构设计

![图片](https://mmbiz.qpic.cn/mmbiz_png/9TPn66HT9325qUbUw8Vuy5b9t4bY32K29lI4IWTibfHr0VyZMXhib5mOSgBdqJ07Vicx8pPgUULuIKZliaeNmiaLFhA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1、MCP Host ：使用 LLM 为核心并希望通过 MCP 访问数据的程序。

2、MCP Client ：与 MCP Server 保持1:1连接的客户端。

3、MCP Server ：每个 MCP Server 都通过标准化的模型上下文协议公开特定功能的轻量级程序。

4、Local Data Sources ：你计算机上的文件、数据库和服务，MCP Server 可以安全访问。

5、Remote Data Sources ：通过互联网可用的外部系统（比如：通过 API），MCP Server 可以连接到这些系统。

第三、通过 MCP 分离控制责任

MCP Server 公开三个主要元素（Prompts、Resoures、Tools），这些元素是有意设计的，以帮助实现特定的控制分离。

![图片](https://mmbiz.qpic.cn/mmbiz_png/9TPn66HT9325qUbUw8Vuy5b9t4bY32K2WQaVEjFYtFD8iasZPiavhV6JHBWxvibD8KYTF47g9MbH2eNbXv6dZ5WBg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1、Prompts 提示词被设计为用户控制的 。后端的程序员可以公开特定的提示词（适用于与后端服务公开的数据交互），这些提示词可以注入到使用 LLM 的应用程序中，并暴露给给定应用程序的用户。

2、Resoures 资源被设计为应用程序控制的 。Resources 资源是任何可以被利用 LLM 构建的应用程序使用的数据（文本或二进制）。应用程序的程序员（通常是 AI 应用开发工程师）负责将这些信息编码到应用程序中。通常，这里没有自动化，LLM 不参与此选择。

3、Tools 工具被设计为大模型控制的 。如果我们赋予应用程序如何与环境交互的代理权，我们使用 Tools 工具来实现这一点。MCP Server 公开一个端点，可以列出所有可用 Tools 工具及其描述和所需参数，应用程序可以将此列表传递给 LLM，以便它决定哪些 Tools 工具适用于手头的任务以及如何调用它们。

  

****—* 3*** *—*

**A2A + MCP 协同架构设计**

第一、A2A + MCP 协同架构设计

谷歌说得很清楚：AI Agent 应用需要 A2A 和 MCP。我们推荐用 MCP 来处理工具，用 A2A 来处理 AI Agents。

这话啥意思呢？我们来看看一个涉及多个 AI Agent 系统架构。

![图片](https://mmbiz.qpic.cn/mmbiz_png/9TPn66HT9325qUbUw8Vuy5b9t4bY32K2MgvNANiciaWTqiaMQFGPZWaBiaKYCL1HJpfKsMKgpOZic3aH1lrB5IOITqg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

MCP 里的组件：

1、MCP Host：这里有意思了，和 A2A 结合后，MCP Server 就是 AI Agent。

2、MCP Client。

3、MCP Server。

4、Local Data Sources。

5、Remote Data Sources。

A2A 这边：

6、AI Agent（MCP Host）会通过 A2A 协议来实现和通信，这个协议能实现：

- 安全协作：MCP 没有身份验证功能。\[更新：最近 MCP 在身份验证方面有了很多改进。
	- 任务和状态管理。
	- 用户体验协商。
	- 能力发现：和MCP工具类似。

谷歌建议， MCP 主要用于把传统的数据系统（MCP Resources）和 API（MCP Tools）跟基于 LLM 的应用整合起来，而 A2A 则负责 AI Agent 之间的通信 。

我确实觉得，往后发展，大家会越来越倾向于把平台暴露成 AI Agent，而不是 MCP Server ，所以 MCP 在第5点的重要性会逐渐降低。

第二、通过 MCP 进行 AI Agent 发现

谷歌甚至建议通过 MCP Server Resources 来暴露 A2A AI Agent。

![图片](https://mmbiz.qpic.cn/mmbiz_png/9TPn66HT9325qUbUw8Vuy5b9t4bY32K2z2VLJdZggfI8nic2mvvAU4Snu16pClUqRGLYLR1kYxca6zpTOReJBlg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1、网格（Mesh）中的每个 AI Agent 都可以通过 MCP Client 连接到一个专门的 MCP Server，并浏览 Resources 目录来发现其他可用的 AI Agent。建议通过这些 MCP Resources 来暴露 Agent Cards。

2、发现之后，AI Agent 之间会继续利用 A2A 协议进行通信。

话说回来，如果我们朝着通过全球索引进行 AI Agent 发现的方向发展，MCP 在这里的重要性也会降低，甚至可能会消失。

  

****—* 4*** *—*

**长期来看，A2A 会不会取代 MCP？**

第一、MCP 会不会逐渐变得不重要？

其实，一直以来，人们都在寻找一种方法，能让大量的 AI Agent 之间互相连接，还能和传统的系统连接。之前有人提到过无头浏览器（headless browsers），但现在看来，开放的通信协议可能才是未来的方向。我觉得，这也是为什么有人说 MCP 是“新的 HTTP 时刻”（虽然可能有点夸张）。

以下的想法是基于一些假设的：

- 开放的通信协议会把新世界的 AI Agent 整合在一起。
- 成为领先的协议是有好处的。
- 这两种协议都会继续发展，可能会扩大它们的责任范围。

第二、MCP 和 A2A 有一些相似之处

在 AI Agent 协议方面，两者都有明显的相似性，用户可以选择多种方式来构建他们的 AI Agent 应用，并将它们展示给世界。

随着 MCP 的迅速流行，公司把 MCP Server 作为他们产品的一部分变得很常见，这样开发者就可以轻松地把这些平台的内容整合到他们自己的基于 LLM 的应用中。

然而，MCP 在推广过程中遇到了一些问题。

- 这个协议最大的缺点之一就是缺乏安全性和身份验证。如果你想安全地展示一个远程的 MCP Server，你需要在基本实现上做一些调整。
- Tools 工具可以描述任何东西，包括其他 AI Agent。不幸的是，MCP 没有实现任何可以让 AI Agent 通过工具进行适当通信的机制（比如状态/上下文交换、长期任务支持等）。

这可能是谷歌通过 A2A 进入协议竞争的一个切入点，因为它解决了上述问题。

我总觉得 Anthropic 对 MCP 的规划比现在看到的要大，包括把多个 AI Agent 连接在一起。现在，A2A 的出现可能已经关上了向这个方向发展的大门。

从长远来看，AI Agent 的世界会是什么样子呢？  

- 公司会把他们的数据资产暴露给 AI Agent 使用。
	- 公司会暴露可以返回数据或执行操作的 AI Agent。
	- 公司本身就是可以和其他 AI Agent 互动的 AI Agent。

我倾向于最后一种情况。

如果这个假设成立，那么真正有权力的是控制远程 AI Agent 通信协议的那个协议。

即使在短期内，假设新出现的公司默认会选择第二种方式，如果他们选择通过 AI Agent 来暴露数据，那么 A2A 显然是赢家。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/9TPn66HT9325qUbUw8Vuy5b9t4bY32K2f2Nm7U5VBVbUAoBOdvricBTtNSR1ESNvdWUtZDuTyc5vNv0eBlyGy6g/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

说了这么多，MCP 会不会继续作为连接新型应用和传统系统的协议，而一旦 AI Agent 占据主导地位，MCP 就会变得无关紧要呢？谁知道呢，让我们拭目以待。

但如果真有那么一天，猜猜我在行业里会支持谁呢？ ：）

第三、总结一下

我们正处在一个激动人心的时代。新型 AI Agent 应用的大规模连接方式正在我们眼前被定义。

A2A 虽然是新来者，但它很快就在 AI Agent 通信领域崭露头角。虽然 MCP 为 LLM 如何整合上下文带来了结构，但 A2A 正在解决 MCP 所缺乏的东西： 安全性、状态管理和实时协作 。A2A 会不会取代 MCP？谁知道呢。

尽管官方立场是这两种协议解决的是完全不同的问题，但它们之间可能存在潜在的重叠，而且可以预见这些协议的范围也会扩大。

如果未来是 AI Agent 的天下，公司开始暴露 AI Agent 而不仅仅是工具或数据，那么能够实现无缝 AI Agent 互动的协议可能就是赢家。现在看来， A2A 似乎正在做出正确的选择 。

你又怎么看，欢迎留言探讨。

