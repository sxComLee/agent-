---
标题: "一文复现Anthropic刚刚发布的ReSearch，原来底层是MCP协议驱动的"
链接: "https://mp.weixin.qq.com/s/Jenytho4E-6XnQr3ff7mMw?scene=1"
作者: "[[绛烨]]"
创建时间: "2025-04-22T12:14:35+08:00"
摘要: "文章介绍了如何技术复现Anthropic最新发布的ReSearch功能，并揭示其底层由MCP协议驱动。"
tags:
  - "clippings"
  - "AI"
  - "MCP协议"
  - "Anthropic"
  - "ReSearch"
  - "技术复现"
字数: "266"
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
原创 绛烨

2025-04-16 03:10:57

精确发文时间由壹伴提供

手机阅读

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUQp93Wbo57aZyQem2f3VgDC651vQyq3Qb88kcXz1lYISVcFGbROBDlQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**点击蓝字**

**关注我们**

Claude于今日凌晨推出新的功能，将 ReSearch和 Google Workspace 集成、以及把 电子邮件、日历和文档与 Claude 相关联，claude可以在工作环境和联网环境下借助 Research快速作出决策和行动。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUo89c00GI4dB341oQ0DZUHWp2XDUaUmaNdJNP9qyqoLdRrZ4s4U44uw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

首先来介绍一下 Research。

Research改变了 Claude 查找和推理信息的方式。

Claude 以Agent方式运作，进行多次相互依赖的搜索，同时确定下一步要调查的确切内容。它会自动探索您问题的不同角度，并系统地解决开放性问题。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUgeibHBCeT1qXOhwLP8MX6DukYRsCmGOVOWcfECODvGB3nmZoQPE4lRg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这种方法提供了详尽的答案，并附有易于检查的引文，因此您可以信任 Claude 的发现。

Research 可在几分钟内提供高质量、全面的答案，适用于整个工作日中处理的多项研究任务，这种速度和质量的平衡使它与众不同。

ReSearch和 Google Workspace 集成

Claude 现在集成了 Gmail 、 Google 日历、 Documents 等，通过 关联到 Google Workspace，Claude 可以搜索电子邮件、查看文档并查看日程安排，省去了上传文件和提供日程信息的动作。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUILsoIVYoMCGIHWGYJgRGh98GUTwdqI4mwOwVMVIbz88lcd7BLibicibYg/640?wx_fmt=webp&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

通过 Google Workspace 使用信息检功能，可以检索电子邮件里面的来信和文件，搜索相关信息作为真实信息来源，由claude借助 Research 进行信息收集，相较于传统的AI搜索，Claude+ Research解决了信息壁垒的问题。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvU8mNj4y9lx4Ykqf4edhsby25Ngy2dUxPhBYVfbMFY9MAmkVp1KjmibYA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

除了这些，企业内部不同职能团队，可以借助 Research高效完成各项任务。

营销团队 可以使用Claude 从网络上收集竞争情报，提取相关产品规格、定位和战略文件来制定全面的发布计划，加速规划产品发布。

销售团队 可以通过让 Claude 搜索通信历史记录、带有会议记录的日历邀请以及有关潜在客户公司的最新更新来创建详细的简报文件，从而更有效地为客户会议做准备。

工程师 通过 Claude 分析设计文档和系统规范以及外部 API 文档、实施模式和安全最佳实践， 创建与现有系统集成的技术解决方案。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUDWzpibiaNB91jC9mmiaqicTVZDAwYiarFpwuBE7PvVoU5pLrldgzquRE6GQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

对于个人用户来说，是一个完美的信息收集助手。

大学生 通过与 Claude 一起分析学习材料和过去课程的笔记来学习新主题，同时搜索最新的学术研究、互动学习资源和专家讲解来制定个性化的学习计划。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvU4RslJvicKjZ5liatsZ8jMh3aKLfc74WLLLAEEia7oeia45yg3ia5rhqj4rA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

父母 让 Claude 扫描电子邮件和日历事件来突出显示重要事项，在网上搜索可能影响家庭计划的更新的学校日历、当地社区活动和天气预报，从而简化个人组织工作。

Google 文档编目

Claude Enterprise 管理员还可以启用编目功能，以提高 Claude 的检索质量和准确性。启用编目功能后，Claude 会利用组织文档的专用索引来查找所需信息，即使这些信息隐藏在冗长的文档中或分散在多个文件中。

这项技术利用检索增强生成技术，使 Claude 能够搜索文档生态系统，而无需指定具体文件。凭借企业级安全性，Claude 可确保数据始终在掌控之中，在提供精准答案的同时，维护组织知识的机密性。

使用门槛

早期 Beta 版 Research 功能 ：

- 地区：美国、日本、巴西。
- 套餐：Max、Team、Enterprise。
- 操作：用户可在聊天中切换“ Research”设置开启。

网页搜索 功能：

- 上线时间与地区：3月在美国推出，现已扩展至巴西和日本。
- 套餐：付费套餐自动启用。
- 启用要求：Claude for Work 管理员需在设置中为组织启用。

Google Workspace 集成的 Beta 版 功能：

- 适用对象：所有付费用户。
- 操作：用户可在个人资料设置中体验。
- 启用要求：团队版和企业版计划管理员需先在全公司范围内启用。

Google 文档编目 功能：

- 适用对象：Claude 企业版计划。
- 操作：企业版管理员可为整个组织启用。

  

彩蛋：使用Dify+zapier复现

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUgeibHBCeT1qXOhwLP8MX6DukYRsCmGOVOWcfECODvGB3nmZoQPE4lRg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在zapier里面添加Gmail、calendar、Drive的相关Action（需要一个一个手动添加）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUciciavbqqlITVCYR9kD3E41jnVV4ibcWlXe46uEIpSSIrbWEVgWAK9zicA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后，在dify里面，构建工作流，选用MCP Agent策略

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUw3x8RCyvYBE48SqpDKEiawQxZRhquyX1OGT28uhrd2bLn32AQtzC0Hg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

放在一个非常简单的工作流里面，

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUic2nmJZicWhRYwB9iaxVvOYUdkiatEZe2EibicdqvbibnR7xDhTcM4jtRiaOlw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Agent主要设置一下Agent策略、模型以及工具（一个海外搜索，需要自己注册找到API），然后填入自己的MCP服务地址。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUPxgHicT2jnfZjtOwqLX9iajdDretJcR2N9Y5aK4h44cAuqAKnspcJbAg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

提示词：

```perl
我是绛烨，帮我向ycw2309280700@126.com邮箱里面发一个主题为claude+research的邮件，介绍https://www.anthropic.com/news/research的信息
```

如下为dify充当的MCP 客户端。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUNvJVaFHmTUXDfVJia1C39nVCuW7ic4VNRRo4qcIv26OoP2FVkUNL8ofg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

如下为126邮箱。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUvZWEZgIE6WntVZ52YOBwUfdDiaicNqzM6JWZFgI3tursp4ptaicQMfz9g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

使用claude官方的promt：

```apache
Hey, I'm planning to take a 3-month sabbatical to hike the Appalachian Trail on May 1. Draft an out of office plan using info from my email, calendar, and docs. Can you please also search for spots where I'll have good service to check in with my colleagues?
```

在dify工作流输入提示指令之后，开始运行

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUjc5zSpKSjJbm9FEDMSSL3zHNf6kSlJOSkb0LsstISQbrsq9Uic6hVcw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在Agent策略里面可以看到三轮的执行逻辑

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUYZLNorkAndvZsOicib6ibAPcLaia8PbmM4bzkfkicjqItxWe82HpI1QZpNw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

round1是关于查询当前时间的，调用时间插件。

round2是在Gmail里面查询信息、检索Google日历以及云盘里面的信息。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUwxpgQcmBJfC5RyyXz7OTN3kY7ibLYwjVBFMibpnUfqIvybicvvhCPvRrg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

第一个节点输入很有意思，此部分确定了选用的工具，包括工具名称啥的，以及每个工具的入参，是由大模型来确定的。

```json
{  "output": "",  "tool_input": {    "gmail_find_email": {      "query": "out of office"    },    "google_calendar_find_multiple_": {      "calendarid": "primary"    },    "google_drive_find_a_file": {      "title": "out of office"    }  },  "tool_name": "gmail_find_email;google_calendar_find_multiple_;google_drive_find_a_file"}
```

其中的一个调用逻辑如下

```swift
{  "output": {    "tool_call_id": "call_0_e7378500-091b-4e93-b548-4bc9408b99b2",    "tool_call_input": {      "query": "out of office"    },    "tool_call_name": "gmail_find_email",    "tool_response": "[{'type': 'text', 'text': '[{\"_zap_search_was_found_status\": false}]'}]"  }}
```

其实跟上面的对比一下，然后你会发现，这就是MCP协议去实现的！

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUgeibHBCeT1qXOhwLP8MX6DukYRsCmGOVOWcfECODvGB3nmZoQPE4lRg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Searched messages：

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUMzDHI1xOykSeWpJtia0eebnNV0FBiaTUefxWBwXey2DZVFP8xuNYKU2A/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Searched Calendar events：

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUdx6B8nfULk6ApcfoIcbsFibmBCjicIxhib0iaFPiaCWeBMlzMaUc0UjrrsA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Searched Google Drive：

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUEx3e3XYykGmySqibHDAFFA3HuqSevLfQfTGZQLormhrkOWomZ04IDKg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

round3其实就是最终综合如上信息进行回复的对话思维链。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUa8GYsEqsFwBBOevibqedvIiaVdNf07Nv0DLDDkLa8Ql6scnKqVRia3IXA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

因为我的谷歌云盘、日程安排里面是空白的，他没有找到相关信息，所以，你懂的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUh2Ak6zeyaQNPjwqfSByVpLctNZLwaDYOtYzwaWMaFmxSicKTKEkLPRg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/mmbiz_png/Zvdfc01tMziboV3gprAicicG1aYianXGHSvUL3cNARgwgXE8xWh1ZPzqicZeWbFBfmWrAnCp3g8wSxfnwHNGDp6JfMg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

通过如上的技术复现，就可以发现，MCP协议已经开始融入claude的产品里面，接下来的几个月来，将会有更多惊才绝艳的产品出来。

非常期待。

如果你对MCP协议感兴趣&有合作机会，可以加我vx:xinzhiaigc，来聊聊。

关注我，带你了解更多行业信息！

可以加我v：xinzhiaigc，感兴趣可以拉你加入AI交流群，一起学习交流。

如果觉得不错，欢迎点赞、在看、转发，您的转发和支持是我不懈创作的动力~

如果想第一时间收到推送，可以给我个星标⭐～

谢谢你挤出时间看我的文章推送，一眼万年，不胜感激。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/Zvdfc01tMzibtqdj8AWogUWVicMW31xviaCgfTpykIvBLf9f9ISOMpLoXGdlCPkv2M8gVYxSToMyg20BpGyWwHKiaQ/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

个人观点，仅供参考

继续滑动看下一个

AIGC新知

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功