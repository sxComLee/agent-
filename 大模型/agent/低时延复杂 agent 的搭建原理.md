---
标题: "‌​‬⁣‬​‍⁢﻿​﻿⁢‌​​‌‬⁤‬﻿‬⁢⁡﻿⁢⁡⁣​‌‌⁤﻿⁤⁣​﻿⁡​⁡‍⁢​⁣⁢​‌﻿‌⁡⁡[对外] 低时延复杂 agent 的搭建原理 - 飞书云文档"
链接: "https://bytedance.larkoffice.com/docx/OzcXd9B9fo5KPcxpZX4cL4Qonpd"
作者:
创建时间: "2025-05-28T15:04:23+08:00"
摘要: "本文探讨了低时延复杂agent的搭建原理，包括搭建方式、时延优化方法及关键流程要点。"
tags:
  - "clippings"
  - "AI"
  - "低时延"
  - "复杂agent"
  - "意图识别"
  - "效率"
字数: "83"
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

# 背景
    

我们提供了搭建复杂 agent 的最佳实践 [[对外] Agent 联网搜索+设备控制+闲聊+长期记忆搭建](https://bytedance.larkoffice.com/docx/CEJedaaf8oxJMox7g6DcOBnAnbh)，那为什么要这样搭建呢，与其他方案的优势在哪里 ？

[[_resources/低时延复杂 agent 的搭建原理/48fc618c2e3d9a49ba0415d891192733_MD5.jpeg|Open: Pasted image 20250528151052.png]]
![[_resources/低时延复杂 agent 的搭建原理/48fc618c2e3d9a49ba0415d891192733_MD5.jpeg]]

  
# 搭建 agent 的几种方式
    
## 单 agent （LLM 模式）
    

这是一种最常规的搭建方式，适合处理简单的任务。如果要处理复杂任务，必须编写非常详细和冗长的提示词。而且需要添加各种插件和工作流等，这增加了调试智能体的复杂性。调试时任何一处细节改动，都有可能影响到智能体的整体功能，实际处理用户任务时，处理结果可能与预期效果有较大出入。

所以它的场景是：

1. 适用于简单的闲聊，对时延要求不高
    
2. 不适用于复杂的逻辑场景
    
3. 添加插件/工作流会让速度大幅变慢（下文解释原理）
    
## 多 agents

为了解决单 Agent 的上述问题，扣子提供了多 Agent 模式，该模式下您可以为智能体添加多个 Agent，并连接、配置各个 Agent 节点，通过多节点之间的分工协作来高效解决复杂的用户任务。

多 Agent 模式通过以下方式来简化复杂的任务场景。
> 
> - 您可以为不同的 Agent 配置独立的提示词，将复杂任务分解为一组简单任务，而不是在一个智能体的提示词中设置处理任务所需的所有判断条件和使用限制。
>     
> - 多 Agent 模式允许您为每个 Agent 节点配置独立的插件和工作流。这不仅降低了单个 Agent 的复杂性，还提高了测试智能体时 bug 修复的效率和准确性，您只需要修改发生错误的 Agent 配置即可。
>     

所以它的场景是：

1. 适用于复杂的逻辑场景
    
2. 对时延要求不高
    
3. 添加插件/工作流会让速度大幅变慢（下文解释原理）
## 2.3 单 agent （对话流模式）

这种模式系统只定义了开始和结束节点，中间的逻辑完全由用户设计，所以足够灵活也足够高效，但用户往往无从下手。所以我们提供了 [[对外] Agent 联网搜索+设备控制+闲聊+长期记忆搭建](https://bytedance.larkoffice.com/docx/CEJedaaf8oxJMox7g6DcOBnAnbh)，但架构为什么这样设计，时延问题是怎么解决的，我们继续分解。

# 时延的优化

## 模型部署
模型都采用火山引擎[自建推理节点](https://console.volcengine.com/ark/region:ark+cn-beijing/endpoint/create?customModelId=)。避免使用公共节点不可控，版本可能比较旧。

## 模型处理

模型的耗时分为输入和输出，都跟相应的长度有关，很直观的输入越长处理越久。但输出长度很容易忽略，每个输出的 token 耗时**约 20-50ms**，应减少输出 token，采用流式输出等方式优化。
- 每个输出的 token 耗时**约 20-50ms**

## 工具调用模型（ fc/function_call ）的本质

场景：一个单 agent（LLM 模式），使用了 搜索、新闻、天气 三个插件，用户来查询天气。这种场景需要用工具调用模型，我们看看发生了什么？

![[_resources/低时延复杂 agent 的搭建原理/81915a7de200c1460010964b5bee769c_MD5.jpg]]

1. 调用模型做决策，用户的 query 应该触发哪个插件，插件的参数应该是什么，会将插件的所有参数传给模型，所以**输入会很长**，我们只是简单的问了一句天气，就触发了大量的 token 输入，输出是标黄的部分（还记得每个输出 token 耗时～20ms 吗），所以第一次模型调用消耗了大量时间，用最新的 Doubao-pro-32k/functioncall-preview，耗时 2100 ms。
2. 调用插件
3. 根据用户的 query 和插件返回的结果做总结，并把结果流式输出，这一步很快，用户只关注首 token，一般 300ms

输入：
{"messages":[{"content":"It is 2025/02/08 10:56:24 Saturday now.\n生活小助手\n\n","role":"system"},{"content":"今天深圳的天气","role":"user"}],"model":"Doubao-pro-32k/functioncall-240515","model_meta":{"frequency_penalty":0,"max_tokens":1024,"stream":true,"temperature":0.7,"top_p":0.7},"tools":[{"function":{"description":"必应搜索引擎。当你需要搜索你不知道的信息，比如天气、汇率、时事等，这个工具非常有用。但是绝对不要在用户想要翻译的时候使用它。","name":"biyingsousuo-bingWebSearch","parameters":{"description":"","properties":{"count":{"description":"响应中返回的搜索结果数量。默认为10，最大值为50。实际返回结果的数量可能会少于请求的数量。","properties":{},"type":"integer"},"freshness":{"description":"查询时间范，例如：2020-03-20..2023-09-09","properties":{},"type":"string"},"offset":{"description":"从返回结果前要跳过的基于零的偏移量。默认为0。","properties":{},"type":"integer"},"query":{"description":"用户的搜索查询词。查询词不能为空。","properties":{},"type":"string"}},"type":"object"}},"type":"function"},{"function":{"description":"搜索新闻讯息","name":"toutiaoxinwen-getToutiaoNews","parameters":{"description":"","properties":{"q":{"description":"搜索新闻的关键词，必须用中文","properties":{},"type":"string"}},"required":["q"],"type":"object"}},"type":"function"},{"function":{"description":"获取指定日期的天气","name":"mojitianqi-DayWeather","parameters":{"description":"","properties":{"city":{"description":"市名，包括直辖市，比如：北京市、天津市、上海市、重庆市","properties":{},"type":"string"},"end_time":{"description":"待查询结束日期","properties":{},"type":"string"},"province":{"description":"省份名，不要包括直辖市(比如：北京、北京市、北京省、天津市、上海市、重庆市)","properties":{},"type":"string"},"start_time":{"description":"待查询开始日期","properties":{},"type":"string"},"towns":{"description":"区/县/镇","properties":{},"type":"string"},"villages":{"description":"乡/村","properties":{},"type":"string"}},"type":"object"}},"type":"function"}]}

输出：

{"choices":[{"index":0,"message":{"content":"当前提供了3个工具，分别是[\"biyingsousuo-bingWebSearch\",\"toutiaoxinwen-getToutiaoNews\",\"mojitianqi-DayWeather\"]，需求为获取今天（2025年2月8日）深圳的天气，需要调用mojitianqi-DayWeather工具进行查询","role":"assistant","tool_calls":[{"function":{"arguments":"{\"city\": \"深圳\", \"end_time\": \"2025-02-08\", \"province\": \"广东\", \"start_time\": \"2025-02-08\"}","name":"mojitianqi-DayWeather"}}]},"stop_reason":"tool_calls"}],"model":"Doubao-pro-32k/functioncall-240515","usage":{"completion_tokens":125,"prompt_tokens":489,"total_tokens":614}}


所以**对时延有高要求的，就避免使用 工具调用模型，而应该自建流程**。

## 意图识别

自建流程的第一步，就是意图识别，应当在入口就对用户的意图做区分，对不同的意图定制化处理提高性能。当前对话流中自带的 意图识别 节点较慢，需要自己设计。慢的原因是节点的 LLM 输出内容太多，输出了很长的 reason（还记得每个输出 token 20ms 吗）

![[_resources/低时延复杂 agent 的搭建原理/55e05571fdb91136f1f627ca9d2e0f72_MD5.jpg]]![[_resources/低时延复杂 agent 的搭建原理/078f651ef76c5732607853f84ccb31ca_MD5.jpg]]

因此我们自建意图识别节点，节点的输出就一个字符，一个 token，从 1000ms 降低到 250ms。具体的模型选型，因为模型在不断迭代更新，可以根据测评方案选 [[对外] 意图识别模型对比](https://bytedance.larkoffice.com/docx/VQCtdpYeFoPOMDx8hFVcT7FUnEd)，在当前（2025 年初）可选的有 pro 1.5， pro 1.5 lite ，这里要注意的是避免让意图识别节点直接回答问题，直接回答就会有大量输出 token，时间就很长了。在意图识别节点的提示词中，使用 markdown 格式，豆包对于 markdown 格式的理解力较强。也提供一些示例，few shot 的示例可以很好的引导模型回答。

## 参数抽取与结果总结

1. 在调用插件之前往往需要 LLM 节点把参数抽取出来，比如对于查询天气等等场景，抽取出城市、时间等等，这种简单的抽取 pro 1.5， pro 1.5 lite 都可以胜任，抽取出的参数如果有多个，可以用特殊符号拼接在一起（尽量减少输出的token数量），再使用代码节点，解析成多个具体的参数。提供工具根据插件信息生成意图识别和提取参数的提示词：[[对外] prompt generator 使用手册](https://bytedance.larkoffice.com/docx/IPaVdDwc2omcBrxFOO1cWZQfnSg)。


比如抽取场景是：抽取出查询天气的城市和日期
	参数提取节点的结果是：深圳|20250101|20250102
	代码节点将字符串处理成json
	{
	    "city":"深圳","start_date":"20250101","end_date":"20250102"
	}
	墨迹天气插件，引用代码节点解析出的字段


2. 结果总结可以重点关注 browsing 系列模型，是专门为此训练的，速度比 pro 快不少。
![[_resources/低时延复杂 agent 的搭建原理/bd8264dc5b59c674718f7f48eab40ef1_MD5.jpg]]

## 安抚
在意图识别之后，往往并行的进行逻辑处理和安抚，逻辑处理一般需要 2s 左右，安抚可以第一时间让用户感知到系统在处理中，特别是在语音链路，安抚语播报大概 1.5 秒，播报完逻辑处理正好完成，用户的感知就非常流畅。如果接入的是 coze 提供的语音链路，记得将安抚语以句号感叹号结尾。 原因是 coze 的语音链路文本转语音是采用大模型语义识别，当它识别到断句才会进行语音合成。
## 用户画像和长期记忆
当前 coze 提供了 “长期记忆” 开关，不过内部实现是黑盒，记录的内容不可控，不方便定制。并且在开启后，每次 query 都会触发长期记忆查询速度较慢，我们采用变量的方式来自定义实现。关闭系统自带的长期记忆。

![[_resources/低时延复杂 agent 的搭建原理/cd86faf5999e7bd8b595c1ee7e48d989_MD5.jpg]]

![[_resources/低时延复杂 agent 的搭建原理/a480b8dcc47ff5e63c6f2f3d647ee4b6_MD5.jpg]]

这些流程是异步的，不影响主流程的时延，每个变量存储 1000 字符没有明显的性能损耗。在读取变量时，也与意图识别并行进行，所以并不会增加整个链路的时延。抽取用户画像和记忆的规则，在相应的 LLM 节点，可以按需定制。在 “拼接用户记忆点” 的模块，可以自定义存储多少个记忆点，默认 50 条，可以自定义。

![[_resources/低时延复杂 agent 的搭建原理/cd84590a29b489463348f654e18e6bd5_MD5.jpg]]

## 知识库

当前尽量用文本知识库，只涉及向量查询。表格知识库目前有性能问题，在意图识别和用大模型将自然语言转SQL耗时长，导致整体查询慢。

## 输出结果与结束节点

在每个分支处理完后，记得用输出节点输出。记得开启流式输出，否则会等待大模型完全处理完才一次性输出。而结束节点，只需要输出空变量即可。如果在结束节点输出最终的变量，就会等待所有分支执行完才会输出结果，比如闲聊就会等更新完用户记忆点才输出，当然就很慢了。


![[_resources/低时延复杂 agent 的搭建原理/d23c74778a120362b5add88815d83058_MD5.jpg]]![[_resources/低时延复杂 agent 的搭建原理/3bb2cae71c094f04aec0d282e09d033d_MD5.jpg]]

  

  

# 对话流支持自定义参数
    

对话流如果跟 bot 绑定，目前是不支持自定义参数的。解决办法是不要将对话流与 bot 绑定，将对话流从 bot 中移除。通过 OpenAPI 直接调用对话流，这种方式可以传入自定义参数。接口是：https://www.coze.cn/open/docs/developer_guides/workflow_chat

  
# 参考资料

[一些减少 output token 手段](https://bytedance.larkoffice.com/docx/GMHqdEmKOo3CEtx2kG7ctWyvnie)