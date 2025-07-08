---
标题: "苹果开发者自曝用Claude完成95%开发，开发应用已上架"
链接: "https://mp.weixin.qq.com/s/XOuCUgyABpkFuQWzRYWM3A"
作者: "[[关注前沿科技]]"
创建时间: "2025-07-08T14:36:39+08:00"
摘要:
tags:
  - "clippings"
字数: "163"
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

![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mUnfPQ3O3DYvJCeAFSX0V8g7h2TNQL812D5IBFmvo2HxV7FzialrN0yw/0?wx_fmt=jpeg)

关注前沿科技 [量子位](https://mp.weixin.qq.com/s/) *2025年07月07日 17:35*

##### 闻乐 发自 凹非寺量子位 | 公众号 QbitAI

苹果开发者自曝用AI开发应用程序， Claude含量95% ！

事情是这样的，一位苹果开发者最新发布了一款用于调试MCP服务器的原生macOS应用 **Context** ——

一款几乎完全由 Claude Code 构建的应用程序。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mzfsnDI8bnNlYh878OnMroaUEYibZB31xYUORzdicTpXeD6fjVfsS6YMQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

作者 **indragiek** 从2008年就开始为Mac开发软件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mL0BcNpl0eoVc219J1UOsu6OOJ1hNQcW5HsBYJsUFicxp5K1kg383goQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

这次，他的目标是使用Apple的SwiftUI框架，打造一款在macOS平台上使用起来很顺手且实用的开发者工具。

与以往不同的是，Claude Code承担了Context项目95%的工作量，indragiek声称：

> 在这个 **20000行** 代码的项目中，我亲手编写的代码估计 **不到1000行** 。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtACnoeCszYZw4C41YqtjK2miam94TjMsToXAQfSib61TbaZiaKpEIjZ0okDUT7g4fINtRiaCUbJ0riaRkg/640?wx_fmt=jpeg&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

“工程师”Claude也是好起来了，能给苹果打工（doge）。

调侃归调侃，下面让我们来“学习”一下这位开发者是怎么用Claude的。

## 苹果开发者教你“驯服”Claude

作为一名经验丰富的工程师，Indragie像许多同行一样，拥有一个“烂尾项目”list。

尽管能够构建项目原型，但最后20%的交付工作往往耗费巨大时间和精力，导致项目搁置。

所以，他已经6年未能成功发布任何一个副项目。

在今年2月，他开始尝试用 **Claude Code** 辅助完成项目，不过最后Claude几乎帮他完成了所有工作。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mzbpEbunnypXibYQxrsMHwTUcTmmiaq19b0aqYLNibMHHVFfqypTVcibWkw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

Claude以 **“Agent循环”** 为开发核心，仅通过一个简单的文本框来输入提示词，这直接 “取代”了作为VS Code分支的传统IDE。

在实际开发过程中，Claude能够定位并阅读项目中的现有源代码、理解代码风格和设计模式、阅读提供的额外文档、生成测试验证、编译程序并运行测试，并根据编译和测试失败进行迭代修复等。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mWf5jwBOZHZ4daAFRibptY4GdtrJgz2r57L3fXqorlricU6eUn6wrbbLQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

经Indragie反馈称，在Swift和SwiftUI的使用上，Claude在Swift 5.5之前的版本上表现更出色，尤其在是在SwiftUI方面。

它能够生成准确但可能不够美观的UI代码，但美观的问题可以通过迭代改善。

就像Indragie提到的那样，直接在文本框输入：让它更美观。

于是就得到了这样的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2m00k8ZBmXMJicIZ6Lo6wgKt7hCzCaiaKJVwEs07kAZTbKzVZnaZCtHXwQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

重点来了！

对于Swift Concurrency等重大变化和新旧API的选择上，Claude有时会“拿捏不准”。

于是Indragie创建一个包含使用现代API基本说明的 **CLAUDE.md文件** ，可以让Claude避免常见的“陷阱”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mNiaQ1Xb05bHDQl2VT12EEYpEZh2LkwhBowKEIk6sc13RtCxeSqO12MQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

Indragie强调 **“上下文工程”** 很重要，他采用了“预设Agent”的方法实现Claude的效能最大化。

他发现，虽然模型拥有200k tokens的上下文窗口，但模型的性能会随着上下文窗口的使用增加而下降，且“压缩”机制可能导致重要的细节被丢失。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2m1BaWMh3qib4tfGzrS8anunGia621HItoTNO1f3D9CSVIjcErICaD3PGw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

为此，他采用了“预设Agent”的方法，让Agent预先阅读额外的上下文（如 CLAUDE.md文件、特定文档或源代码）来提高输出质量。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mhoAS5w5tv7g4ff46TnhthByBQtXK87IHSsLdFFxjUjTNpw1YXuwU8g/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

Claude还需要 **详细的需求规格说明** 。

语音、打字等任何输入方式都可以，不过Indragie称自己更喜欢打字～

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mEqLMcytXzNphv2YY0BIAcOoJBqtO3gs4buhn1Fibacz6cfl0qliaTbrg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

先打开 **扩展思考** 模式是关键！

为了避免Claude盲目地直接进入实现阶段而导致结果质量不佳，Indragie会要求Claude先使用其它的扩展思考 模式并 “制定计划”。

通过使用 **“think”<“think hard”<“think harder”<“ultrathink”** 等关键词，可以激活Claude的不同级别扩展思考，其中 “ultrathink” 消耗的token最多但能产生最佳结果。

Claude能够独立驱动反馈循环，使其能够进行更改、测试并收集失败原因的上下文。

所以，Indragie建议 **设置有效的反馈循环** ——构建、测试、修复错误、修复用户体验。

他使用了XcodeBuildMCP来简化构建和运行应用的问题，不过，对于需要用户交互才会触发的Bug或UX问题，仍然需要手动提供日志或截图。

除了编写代码，Indragie还发现Claude Code作为一个通用模型，能完成的不止编码任务。还包括编辑文案、规划功能等。

他认为最有用的一个是 **生成逼真的模拟数据** ，这大大加速了UI原型的开发和功能验证，尤其在没有真实数据的情况下。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2mwdibv7wdoicwH92SibcnAGD2HlrHBWN2CnrBhDQZ5IhSJ57CgGTfDg8Dw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

Indragie还发现 **构建高质量的自动化** 几乎是 **免费** 的

他让Claude编写了一个2000行的Python发布脚本，该脚本能检查环境、生成更新日志、生成Sparkle appcast *（描述macOS应用程序的更新信息的XML文件）* 、发布到GitHub并上传调试等。

在脚本完成后，他使用了一个简单的单行提示词来美化CLI输出，最终得到了这个效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2micicoJvSyJE5ecwFxgEUmaYqVibuLKzl2n5chiavHMtapHJEwmtTGkJgsg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

一番教学之后，Indragie意识到自己使用的主要工具只有两个：Claude Code和GitHub Desktop。

于是，他认为未来的IDE将会非常不同，源代码编辑器可能不再是IDE的核心，它们将专注于帮助开发者 **预设Agent的上下文** 并设置对Agent至关重要的 **反馈循环** 。

成功发布Context应用后，Indragie兴奋地表示：

> 对我而言，这个过程中最令人兴奋的事情不是我所构建的应用，而是我现在能够再次满足我的编程欲望并发布精良的副项目。这就像我每天多出了5个小时，而我付出的代价只是每月200美元。

## One More Thing

据Claude Code公布的数据，自今年2月份上线以来，它已经被 11.5 万 开发者使用，并且在单周内处理了 1.95亿 行代码。

假设Claude code是一个初级工程师，这些数据意味着它的年收入可达 1.3亿 美元。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACnoeCszYZw4C41YqtjK2m4ZCevAotelicpeWTKZ5jAQPJwYAk5npXicNZ0xEKU7AWzdyALy52wMFg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

1亿美元年薪的风也算是吹到了Claude～

*项目地址：https://github.com/indragiek/Context*

*参考链接：  
\[1\]https://www.indragie.com/blog/i-shipped-a-macos-app-built-entirely-by-claude-code  
\[2\]https://news.ycombinator.com/item?id=44481286  
\[3\]https://x.com/deedydas/status/1941683553361854710*

  

**一键三连** **「点赞」「转发」「小心心」**

**欢迎在评论区留下你的想法！**

— **完** —

  

专属AI产品从业者的 **实名社群** ，只聊AI产品 **最落地的真问题** 扫码添加小助手，发送 **「姓名+公司+职位」** 申请入群～

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtACXBaAPKiaAiavjgaxpA5e6VSqNT3LDEKTjblKVdC8bRlDFW4AuHtyibCs12QibQ86hD59XE8VadvouQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

进群后，你将直接获得：

👉 最新最专业的AI产品信息及分析 🔍

👉 不定期发放的热门产品内测码 🔥

👉 内部专属内容与专业讨论 👂

  

**🌟 点亮星标 🌟**

**科技前沿进展每日见**

  

继续滑动看下一个

量子位

向上滑动看下一个

量子位