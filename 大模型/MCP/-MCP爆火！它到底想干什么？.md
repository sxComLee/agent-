---
标题: "-MCP爆火！它到底想干什么？"
链接: "https://mp.weixin.qq.com/s/5Bph-10vb--Rx9XHPsu_5Q"
作者: "[[JJJohn]]"
创建时间: "2025-04-10T17:58:39+08:00"
摘要:
tags:
  - "clippings"
字数: "427"
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
原创 JJJohn *2025年03月08日 10:25* *北京*
#flashcards

转译自rohanpaul\_ai 的《📡 Model Context Protocol (MCP) 101》

## 模型上下文协议(MCP)入门

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF8czH7T9LRia141Uym8ZgJnicbJAPwCLeeU9etldZKh9Q5gTKwHdsMD1yaNO78z5ic5EdhgyIPYuZsQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

MCP（模型上下文协议）标准化了 :: 基于LLM的应用程序如何与外部系统连接 。

相比于手动编码每个链接（聊天机器人连接Gmail、聊天机器人连接GoogleDrive等），MCP为所有AI工具和数据源提供了单一协议。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF8czH7T9LRia141Uym8ZgJnEdTK0YeaicQARWx8uBHQ7yq6ice0kGXNDGIe8iaUZ06ib4ZuWaWOxopjYg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**这将N x N集成减少为每个AI工具一个实现和每个外部系统一个实现。**

更多模型上下文协议(MCP)的更多信息，可参阅文档 ：

https://modelcontextprotocol.io/introduction

## 🔧 MCP的架构

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF8czH7T9LRia141Uym8ZgJnbrAN2MXQHK8XicLpvhHPUNjib354ia2FOr9f9eT50sRnMpLq7QYHXFqtA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

MCP使用客户端-主机-服务器细节方案如下：

### MCP使用客户端(Client)-服务器(Server)模型。

在 **客户端** 侧，我们有熟悉的Cursor, Windsurf 的AI IDE，或是类似Claude Desktop、IDE插件或任何需要获取信息或执行操作的AI驱动工具。

在 **服务器** 侧，我们有小型程序(MCP服务器)，每个都专门提供特定功能集—例如，访问计算机上的文件、查询数据库或调用第三方API。

#### 每个服务器都以标准化方式“讲”MCP协议

它们都共享请求和响应的通用格式(通常基于JSON)，这使任何兼容MCP的客户端能够自动发现并使用服务器的功能。

#### 标准化保障通信

这种标准化确保每个服务器使用可预测的模式进行通信。

例如，无论服务器是获取文件还是访问数据库，请求和响应都遵循预先约定的JSON格式，具有特定的键和数据类型。

#### 自动发现

由于通信格式统一，兼容MCP的客户端可以查询任何服务器以了解其功能。

通常，服务器提供 **清单** 或一组元数据端点，列出它们支持的功能或操作(如读取文件、查询数据库或调用Web API)。

客户端不需要为每个服务器定制代码——它可以自动检测可用的操作及如何调用它们。

#### 互操作性和即插即用

由于每个服务器遵循相同的协议，客户端可以在不同服务器之间切换或添加新服务器，而无需重新设计通信方式。

这种“即插即用”特性类似于前面说的USB的方式，可以让我们使用同一个端口连接各种设备到计算机。

### MCP主机

比如Claude Desktop、我们熟知的各种AI IDE，能够运行主要AI应用程序。

### MCP客户端

连接主机和服务器——每个连接使用专用客户端管理安全和请求。

### MCP服务器

容纳工具集、API或本地/远程资源。LLM通过标准化MCP调用调用这些资源。

### MCP协议传输内容

在MCP下，服务器可以公开：

- **资源** ：LLM可以浏览或检索的"只读"或"参考"数据(如文档、表格或文件)。
- **工具** ：LLM可以执行的操作(如创建新文件、运行代码或向API发送数据)。
- **提示** ：可重用的"提示模板"，让我们以标准化指导LLM的方式(如代码生成或数据分析的一致格式)。

### 采样机制

MCP还包括一种称为 **采样** 的机制，服务器可以请求LLM生成补全(例如，用于AI驱动的代码建议、文本摘要等)。这确保服务器在需要高级语言或推理能力时可以将“思考”卸载给LLM。

主机向LLM展示服务器可用的工具。

LLM将决定使用哪些工具，客户端促进调用，输出返回给LLM，LLM响应用户。

## 为什么MCP 有用

### 统一接口

使用MCP，我们将获得单一的“通用端口”，而非funtion call 时五花八门的API（OpenAPI）。

因此LLM不必了解数据库驱动程序或Web API的具体细节——它只需要知道如何使用MCP，MCP服务器处理其余部分。

### 可插拔架构

想要新的功能或想切换到不同的LLM 供应商？

无需重写所有内容，只需替换或添加相关的MCP服务器/客户端，即可。

### 工作流自动化

由于每个操作都标准化，我们可以将多个服务器和工具链接成复杂的自动化流程。

例如：从数据库读取数据→用LLM总结→将总结发布到飞书文档。

## 不用MCP行吗？

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

当然行！

——只要你体力够好，完全行！

我们可以通过自定义API的方式，手动将每个AI工具连接到每个外部系统。

只是这样，我们会发现 **每个AI工具都需要通过自定义代码连接到每个外部系统。**

**假设有10,000个AI工具和10,000个外部系统。这就是10,000 x 10,000 = 1亿个不同的集成。**

一个小目标就这样达成了——

想要跑路不干了，对吧？

而有了MCP，每个AI工具构建一个MCP实现，每个外部系统也构建一个MCP实现，总共10,000 + 10,000 = 20,000个。

**o(n^2) -> o(n) 的飞跃啊！**

而且这样改造完成后，支持MCP的所有内容都可以与支持MCP的所有其他内容通信。

**这将1亿个单独集成减少到20,000个** ，大大减少了开发工作和维护开销。

## 以下是演示MCP简单使用的两个Python脚本：

- `banking_server.py` (服务器)
- `banking_client.py` (客户端)

## 1\. MCP服务器示例

**文件：** `banking_server.py` ——银行服务端

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

## 服务器中干了些什么？

1. `FastMCP("banking")`
- 我们创建一个标签为 **banking** 的MCP服务器。
	- 可以将其视为启动一个小型Web服务器，但这个 **服务器** 使用MCP通信。
3. `@mcp.tool()`
- 每个带有此装饰器的函数都会自动被识别为MCP工具。
	- 这意味着外部客户端可以通过名称(例如 `"check_loan_eligibility"` )以及特定参数调用它。
5. **业务逻辑**
- 在每个函数内部，我们定义一些基本逻辑(例如，计算“评分因子”——比比支付宝的借呗在计算用户信用分之后决定要不要给用户放贷)。
	- 我们将返回一个字典，最终 **转换为客户端的结构化响应** 。
7. `mcp.run()`
- 启动MCP服务器，以便它通过标准输入/输出(或其他支持的传输方式)监听传入请求。
	- 这类似于说：“好了，我们准备好处理来自AI客户端的任何调用。”

## 服务端如何实现的MCP？

- 通过使用 `FastMCP` 和 `@mcp.tool()` 装饰器，我们告诉MCP库 **确切地** 要公开哪些函数。
- 在后台，MCP库以标准格式打包这些函数。它还知道如何读取客户端发送的 **请求** 并将它们转换为函数调用。

**好处：** 我们（或其他任何人）可以以最小的工作来添加新功能，我们的AI应用可以使用相同的统一协议发现并调用它们——无需每次都修改新的自定义端点或JSON模式。

## 2\. MCP客户端示例

文件： `banking_client.py` ——银行客户端

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

## 客户端里干了些什么？

1. `StdioServerParameters(...)`
- 这告诉我们的MCP客户端 **如何** 启动或连接到服务器(在本例中，通过使用Python运行 `banking_server.py` )。
	- 服务器和客户端通过 **标准输入和输出** (stdio)进行通信。
3. `stdio_client(server_params)`
- 这个命令实际上启动服务器进程(如果尚未运行)并创建两个流：一个用于读取，一个用于写入。
5. `ClientSession(...)`
- 发送初始化消息，让服务器知道我们已准备就绪。
	- 发送对特定工具的请求。
	- 接收服务器的响应。
- 我们将读/写流包装在"会话"中。这个会话负责：
8. `await session.call_tool("tool_name", arguments={...})`
- 这是核心MCP调用。我们指定 **要调用的工具** (例如， `"check_loan_eligibility"` )并传入参数字典。
	- 库自动 **按照MCP标准打包这些参数** ，将它们发送到服务器，等待服务器的响应，并为我们解包响应。
10. **解析响应**
- 服务器通常以JSON格式返回文本内容，因此我们使用 `json.loads(...)` 将其转换回Python字典。

## 客户端如何实现的MCP？

- 客户端使用相同的协议(MCP)从服务器请求工具名称和参数。
- 因为服务器和客户端 **确切地** 了解如何交换请求和响应(幸好有MCP库)，所以不会有混淆或不匹配。

**好处：**

- 我们可以轻松地从一个MCP服务器切换到另一个，而无需重写客户端逻辑。唯一的区别是我们调用的 **工具名称** 或 **参数** 。
- 如果我们在服务器端构建了新工具，我们的客户端可以使用相同的模式发现并调用它。

## 这么设计的好处

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF8czH7T9LRia141Uym8ZgJnK4ic0Q91RHl0HfE38rs7dejz6cSSJ7UvbKXngbdavIYna5pdVTgXF1w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 一致的接口使用MCP，服务器上的每个功能都以相同的方式被发现和调用——无需单独的REST端点，无需额外的Web框架。模块化和可扩展性随着添加更多工具(例如，calculate\_mortgage、check\_account\_balance等)，无需为每个工具创建全新的自定义集成。只需用@mcp.tool()装饰它们，它们就会自动可用。更易于AI集成如果我们的AI系统或聊天机器人有MCP客户端组件，它可以直接以结构化方式调用这些工具。实际上，我们可以教AI系统了解服务器的功能。减少重复工作不再为每个项目重写逻辑或手动设置新端点。如果我们有标准的MCP方法，可以在多个应用或团队中重用这种模式。面向未来因为MCP是开放标准，社区可能会创建各种服务器、工具和功能。我们的AI或应用程序可以连接到新服务器，而无需重新设计整个集成。

## 全流程整合

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

当 **运行服务器** 时：

```nginx
python banking_server.py
```

它开始监听MCP请求(公开 `check_loan_eligibility` 和 `calculate_loan_interest` 工具)。

当我们在另一个终端 **运行客户端** 时：

```nginx
python banking_client.py
```

它执行以下所有操作：

1. 生成或连接到服务器。
2. 初始化MCP会话。
3. 使用特定参数调用两个工具( `check_loan_eligibility` 和 `calculate_loan_interest` )。
4. 接收每个调用的结构化JSON响应。
5. 打印结果。

这个 **两脚本** 示例简单演示了"用 `@mcp.tool()` 包装的 **任何** 代码或函数如何使用标准消息传递对AI客户端可访问"。

## 集成到Windsurf 中

而如何将上述的 **银行** MCP服务器代码集成到 **Windsurf IDE** 中呢？

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

以Windsurf 为例，我们可以在 **Windsurf IDE** 工作区或设置文件夹中，找到（或创建）名为 `mcp_config.json` 的文件。

在其中，定义 **banking** 服务器及所需的路径详细信息，例如：

```json
{  "mcpServers": {    "banking": {      "command": "python3",      "args": ["/Users/john/workspaces/mcp-bank/banking_server.py"],      "cwd": "/Users/john/workspaces/mcp-bank"    }  }}
```

保存 `mcp_config.json` 后：

1. **重新加载** Windsurf IDE（如有不行就上重启大法），以便它识别新的服务器配置。
2. 我们就应该能在Windsurf环境中看到 `banking` 服务器作为可用的MCP服务器了。
3. 当我们的AI工具或IDE内置MCP客户端需要调用 `check_loan_eligibility` 或 `calculate_loan_interest` 时（比如我们输入某个prompt 后，LLM 在工作流规划中认为需要调用），它们现在可以通过Windsurf的MCP集成来执行，自动启动并与 `banking_server.py` 脚本交互。

大功告成。

👇

👇

👇

👇

另，我用AI 建了个同名星球《AGI Hunt》，AI 会实时采集和监控X 等各平台的热点 AI 内容，并基于数个资讯处理的 AI agent 挑选、审核、翻译、总结到星球中。

——这是个只有干货、没有感情的前沿一线AI 资讯信息流（不是推荐流、不卖课、不讲道理、不教你做人、只提供信息，懂的懂）

- 每天约监控6000 条消息，可节省约800+ 小时的阅读成本；
- 每天挖掘出10+ 热门的/新的 github 开源 AI 项目；
- 每天转译、点评 10+ 热门 arxiv AI 前沿论文。

**星球非免费。** 定价99元/年，0.27元/天。(每+100人，+20元。元老福利~）

- 一是运行有成本，我希望它能自我闭环，这样才能长期稳定运转；
- 二是对人的挑选，鱼龙混杂不是我想要的，希望找到关注和热爱 AI 的人。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

**欢迎你的加入！也欢迎加群和2000+群友交流 ![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)** 

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

除了冰冷的实时资讯，还会有冰冷的AI 早晚报，欢迎你来！

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

JJJohn

 **微信扫一扫赞赏作者**

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过