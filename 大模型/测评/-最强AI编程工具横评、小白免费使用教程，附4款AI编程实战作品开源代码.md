---
标题: -最强AI编程工具横评、小白免费使用教程，附4款AI编程实战作品开源代码
链接: https://mp.weixin.qq.com/s/8_fO1Qi_xrb_B-CBbHtfNw
作者: "[[向阳乔木]]"
创建时间: 2025-04-10T18:17:35+08:00
摘要: 
tags:
  - clippings
  - "#ai编程工具"
  - "#Cursor"
  - "#trae"
  - "#Windsurf"
  - "#测评"
字数: "275"
状态: 已读完
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
原创 向阳乔木 *2025年04月04日 08:20* *天津*

> 字数 1549，阅读大约需 8 分钟

## AI 编程工具有哪些？

印象中最早出现的是 **Cursor** ，前 Scale AI 员工创立。

异军突起的是 **Windsurf** ，原名叫 Codeium。

国内客户端有字节的 **TRAE** ，分国内和海外两个版本。

阿里巴巴的通义灵码是通过 Visual Studio 插件的方式交付。

Visual Studio生态强大，有很多AI辅助编程插件：

- • Cline
- • Roo Code
- • Augmentcode

https://visualstudio.microsoft.com/

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfpOjKwOrp84Bb93YbADdjYeRGv51ko1KrnPsib6RicUaFhT5wze1V9UrA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 专业评测：哪个AI编程工具强？

LiveSWEBench网站做了专业测试。

https://liveswebench.ai/

从三个实际使用场景PK：

- • **Agent模式：** AI自主编程解决能力。
- • **目标编辑：** 按指令修改代码的精准度。
- • **自动补齐：** 代码自动补齐智能度。

公平起见，除Amazon Q，都用Claude 3.7 Sonnet模型做的对比测试，得分如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfyqPXHDrdicibcNMIkNuHKvtia6ftfNA7Zic7mK8GMPMeL9btqIayepJJfw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

| 排名 | 工具名称 | 平均解决率 | Agent模式解决率 | AI编辑解决率 | 自动补齐解决率 |
| --- | --- | --- | --- | --- | --- |
| 1 | SWE-Agent | 47.83% | 43.40% | 52.27% | N/A |
| 2 | OpenHands | 46.89% | 41.51% | 52.27% | N/A |
| 3 | Cursor | 43.67% | 39.62% | 50.00% | 41.38% |
| 4 | GitHub Copilot | 43.04% | 43.40% | 40.91% | 44.83% |
| 5 | Windsurf | 43.02% | 43.40% | 47.73% | 37.93% |
| 6 | Claude Code | 39.32% | 37.74% | 40.91% | N/A |
| 7 | Aider | 33.47% | 28.30% | 38.64% | N/A |
| 8 | Amazon Q | 30.30% | 24.53% | 25.00% | 41.38% |

**简单解读**

- • **SWE-Agent和OpenHands** 在整体和编辑能力上领先，但不提供自动补全功能。
- • **Cursor** 在三个维度都有不错表现，是最全面的工具之一。
- • **GitHub Copilot** 在自动补全方面最强

## 小白用户用哪个？

个人是懂一点HTML和CSS的产品经理，基本算编程小白。

从上个月的密集AI编程实战体感看，个人推荐Windsurf。

支持本地预览，选择页面元素提问修改，非常适合写前端页面。

另外就是字节的TRAE，不花钱免费用顶级AI编程模型Claude 3.7 Sonnet。

而身边的程序员朋友们，感觉多数喜欢Cursor。

还有的会用VS Code + Cline/Roo Code解决方案。

## 字节跳动TRAE

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfvpBkLlibpAWUnLpTric4hiaMnI0z1ia5h0BUZhOTyMkhESw3NNrxLLuCBA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

字节的TRAE编程工具是免费的。

因合规问题，分成国内和海外两个版本，有条件推荐用海外版。

**海外版**

https://www.trae.ai/

内置模型支持顶级编程模型如Claude-3.7-Sonnet。  
就是用的人多，偶尔会排队。

其实用Claude-3.5-Sonnet，质量已经很不错，还有DeepSeek-V3-0324也很强。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpf420dgDYydhrdnicvPA52qr14l09kxD9zOL0mc0uUq53IRgmZK57Nxpg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**国内版**

https://www.trae.com.cn/

支持豆包1.5 Pro和Deepseek R1和V3。

个人推荐DeepSeek-V3-0324模型，速度快，质量好。  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfIdZzaMAamHs18WYeVvqEvfItzyia49Eia9ibEcpqVZGO9quTg5MOF0QBA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 开源免费解决解决方案

下载安装Visual Studio Code

https://visualstudio.microsoft.com/

### 安装Cline插件

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfpkx1q7icaJvk3Vr0x2aaCRQmQibpMAWXYvwgOb407Ka5ZO8sRPib3mjYQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1. 1\. 点击方块形状的插件图标
2. 2\. 搜索“Cline”安装

### 配置Cline

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfbx9W1Adtyicc3tnGkycmiaoy2PaD471WUPEAgGwDvxuCHsLKUBgw6SvA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1. 1\. 配置给Cline什么权限，比如是否能自己读写代码，能否用命令行，能否调用MCP等
2. 2\. 这里是对话框，跟AI对话提需求。
3. 3\. 配置AI编程模型
4. 4\. 设置MCP服务器

MCP相关可暂时忽略，重点说说配模型。

支持几乎所有大模型API或API服务商，甚至支持Deepseek、阿里Qwen，本地Ollama模型。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfV9NV2JX0SOw4jg58PicM3bE9z60v3mD60wBKA2ZPxsJpKTgiaXbInXTg/640?wx_fmt=png&from=appmsg)

最值得用的，个人觉得有四个。

**1\. OpenRouter**  
https://openrouter.ai/

可理解为国外的硅基流动，聚合所有大模型API，注册它，就能获得所有模型API。  
缺点是不支持国内支付，顶级模型用起来贵。

**2\. Google Gemini**  
谷歌大模型，免费申请Key，可惜并发不好。  
https://aistudio.google.com/app/apikey

**3\. OpenAI兼容模式API**

什么意思呢？  
就是任何兼容OpenAI API结构的服务都能用。

以火山方舟Deepseek V3为例，讲讲配置方法。

**打开火山方舟网站**  
https://console.volcengine.com/ark/region:ark+cn-beijing/

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfazjo2I7m6zXCexiaqvxkK45pPTfhByFxl7MHkRpKogWVtMNjMfyHaPw/640?wx_fmt=png&from=appmsg)

1. 1\. 点击在线推理
2. 2\. 创建推理接入点，填写接入点名称，添加模型（找到Deepseek V3 三月版本）
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpf1I4Zco4iaDVqnA92iaae8eeSPX0p0ia8xCZtIYCWdDfib55OqaHPH7ooYA/640?wx_fmt=png&from=appmsg)

1. 3\. 创建好以后会有模型ID
2. 4\. 查看获取API
**拿到以上信息，在Cline中配置**  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfN0C80zFrOm1ewpHykD61fvUqLHYY8MbQV3mYIvXMFa8aicfpNMiajMcg/640?wx_fmt=png&from=appmsg)

**Base URL填写**

https://ark.cn-beijing.volces.com/api/v3/

**API Key填写**  
火山方舟的API Key

**Model ID填写**  
刚创建模型的ID

**4\. Deepseek API**

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfMXv1B2attialbpPBib1pNjExgH38iacbR5VXZQZxhBRP7xx0icicIgP6Uzg/640?wx_fmt=png&from=appmsg)

打开Deepseek开放平台  
https://platform.deepseek.com/usage

充值10块钱，应该就能用很久。

获取API Key后填写到Cline中就行。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfYqbh9NHVCJvJCfp0ibtAeqquAbjDibBC5OqPHzWZk4C5H27I6ial15yBA/640?wx_fmt=png&from=appmsg)

上面是AI编程工具的个人探索。

**但更重要的把这些工具用起来，去创造，去解决实际遇到的问题。**

昨天在X上写了一段编程实战小结，作为结尾。

## 3月AI编程实战小结

近几周密集用AI辅助编程，做出不少小工具，也趟了不少坑。

个人编程基础，不能说是零，至少懂一些HTML和CSS。

可能这些年一直做产品工作，没吃过猪肉，也见过猪跑。

比完全没编程经验的人来说，要好上一些，但不多。

朋友问我，写出这些网站和工具，是否有看什么AI编程课。

实话说，几乎没看过，都是硬着头皮上。

AI真的是强大，只要足够有耐心，能精准描述需求，总是能做出一点点产品雏形。

当然，沮丧时刻也非常多，甚至有时候想摔电脑。

明明只是让AI加个小Feature，它竟然会把之前正确的界面样式、功能全搞乱。

甚至会进入鬼打墙死循环，改十多遍都改不对。

这时，可能需要来回换不同AI编程工具，从Cursor、WIndsurf、Trae，到网页版的Gemini 2.5 、Grok都会试，总是希望有新的不一样的解法思路。

还有大量实在搞不定，只能放弃的时刻。  
一点点删减保留稳定功能，拿简版发出去。

我觉得没有必要过分吹捧AI编程，但它真的提供了一种可能性，让普通人也能做出自己趁手的软件或工具。

**这在3年前是很难想象的一件事，感谢AI的进步发展，感恩生活在这个时代。**

以下上个月AI开发的所有产品：

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCXGWGmfVkNqZvX3L9o67gpfiadP3DI97KQIqia1NGsQltIlMnQddXmFed18y6JUfWEPglD9PB468LSw/640?wx_fmt=png&from=appmsg)

**全部免费开源：**

https://github.com/joeseesun

**如果觉得以上内容对你有帮助，欢迎一键三连！**

  

向阳乔木

