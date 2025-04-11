---
标题: "LLMs.txt：让大模型更懂你的 Web 文档-LLMs.txt：让大模型更懂你的 Web 文档"
链接: "https://mp.weixin.qq.com/s/13ZmGOIozTmEb98A8-kdUA"
作者: "[[追求卓越的]]"
创建时间: "2025-04-11T10:49:10+08:00"
摘要: "本文介绍了LLMs.txt这一新兴Web标准，它通过提供优化的markdown格式文档，帮助AI系统更准确高效地理解和处理网页内容，特别是技术文档和API细节。"
tags:
  - "clippings"
  - "AI"
  - "LLMs.txt"
  - "技术文档"
  - "Web标准"
  - "Jeremy Howard"
字数: "439"
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
原创 追求卓越的 *2025年04月10日 09:28* *湖南*

**编者按：** 当你向 AI 助手询问 API 细节时，它是否经常被文档中的导航栏、样式表等无关内容干扰，给出模棱两可的答案？ AI 助手已成为开发者不可或缺的得力助手。然而，它们在处理网站内容时往往受限于有限的上下文窗口，加上 HTML 页面中大量非核心内容的干扰，导致理解效率低下。

本文深入剖析了新兴的 LLMs.txt 标准如何巧妙解决这一问题。这个由 Answer.AI 联合创始人 Jeremy Howard 提出的解决方案，通过提供优化的 markdown 格式文档，让 AI 系统能够更准确、高效地理解和处理网页内容。

**作者 |** **Derick Ruiz**

**编译 | 岳** **扬**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7FIXGz6P7FncUL1f3RBYKI9ibaMZCs0a1sia6xmwsG479fd5YNicATUibtI1GfntiastFbMu4pABVXqHQ/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1 "undefined")

  

您可能已经留意到，近期不少开发工具都在其文档中新增了对 LLMs.txt 的支持。这个拟议中的 Web 标准正快速获得业界的认可，但它究竟是什么，又为何如此关键？

**不同于专为搜索引擎设计的 robots.txt 和 sitemap.xml，LLMs.txt 专门针对 LLM 推理引擎进行了优化。它以一种易于 LLM 推理引擎理解的方式，提供了网站的详细信息。**

那么，LLMs.txt 是如何在短时间内从一项提案迅速演变为行业趋势的呢？

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7fMRoHIgEopRdArWnTjrQ9bwb52Jy4I0V9PD1KYSWiaKtUBpiaTGSjoeyZ6zxcWynwHhzXvVsXjDPg/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

LLMs.txt Explained (Photo by Jørgen Larsen <sup><span>[1]</span></sup> on Unsplash <sup><span>[2]</span></sup> )

  

01

  

## Mintlify 是如何推动 LLMs.txt 普及的

11 月 14 日，Mintlify 在其文档平台增加了对 LLMs.txt 的支持。这一动作，使得平台上数千个开发工具的文档一夜之间对 LLMs 变得友好，包括 Anthropic 和 Cursor 等。

Anthropic 和其他工具很快就在 X 上宣布了他们对 LLMs.txt 的支持。随后，越来越多的由 Mintlify 托管的文档开始采用这一标准，为 LLMs.txt 的提议创造了一波知名度。

这种趋势激发了社区网站和工具的涌现。@ifox 建立了 directory.llmstxt.cloud <sup><span>[3]</span></sup> ，用于索引对 LLMs 友好的技术文档。@screenfluent 也很快跟进，推出了 llmstxt.directory <sup><span>[4]</span></sup> 。

dotenvx 的开发者 Mot，为其文档网站制作了一个开源生成工具 <sup><span>[5]</span></sup> ，并将其分享出来。而 Firecrawl 的 Eric Ciarla 则开发了一个工具 <sup><span>[6]</span></sup> ，能够抓取网站内容并自动生成 LLMs.txt 文件。

![image.png](https://mmbiz.qpic.cn/sz_mmbiz_png/3FmD9EKJYf7fMRoHIgEopRdArWnTjrQ9cHVPCcQQ45QeJcq4JrAXPkjMSDAMicp9ibwajmrPIkNtM7rfwSc9aaUQ/640?from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Anthropic 公司 Claude Relations 部门的负责人 Alex Albert，在 X 上宣布了对 LLMs.txt 的支持

  

02

  

## LLMs.txt 由谁提出，其目的是什么？

Answer.AI 的联合创始人 Jeremy Howard 提出 LLMs.txt 是为了解决一个具体的技术难题。

人工智能系统在处理信息时，只能依靠有限的上下文窗口，这导致它们在理解庞大的文档库时会遇到困难。传统的 SEO 优化技术主要是针对搜索引擎的爬虫设计的，而不是针对 LLM 推理引擎，因此它们无法解决这一限制。

当人工智能系统直接处理 HTML 页面时，常常会被页面中的导航栏、JavaScript 脚本、CSS 样式表等非内容性信息所干扰，这些元素占用了原本可以展示有用内容的空间。

LLMs.txt 的出现，恰好解决了这一问题，它以一种 AI 能够轻松解读的格式，提供了 AI 所需的准确信息。

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Jeremy Howard 在 X 的个人资料，他是 LLMs.txt Web 标准提案的发起者

  

03

  

## LLMs.txt文件到底是什么？

LLMs.txt 是一种格式严谨的 markdown 文档。其规范明确了两种不同的文件类型：

- **/llms.txt** ：这是一个简化版的文档导航视图，旨在帮助 AI 系统迅速把握网站的框架结构。
- **/llms-full.txt** ：这是一个集成了所有文档的完整文件，方便集中查阅。

## 3.1 /llms.txt

在这个文件中，开头需使用 H1 格式标注项目名称，并紧接着一个 blockquote 格式的摘要。文件的后续部分通过 H2 标题来整理文档链接。还有一个“Optional”部分，专门用来标注那些相对不那么重要的资源。

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

有关的简单示例，可以参考 llmtxt.org 自家的 LLM.txt 文件 <sup><span>[7]</span></sup> 。而如果想看一个详细且包含多种语言的例子，可以查阅 Anthropic 提供的文件 <sup><span>[8]</span></sup> 。

## 3.2 /llms-full.txt

与 /llms.txt 仅提供导航视图和文档结构不同，/llms-full.txt 包含了全部的文档内容，这些内容都是用 markdown 编写的。

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

上图的内容摘录是来自于 Cursor 的 /llms-full.txt 文件。如需查看完整文件，请访问 Cursor 的官方文档页面。

  

04

  

## LLMs.txt vs sitemap.xml vs robots.txt

**LLMs.txt 文件的功能与 sitemap.xml 和 robots.txt 等现行 Web 标准有着本质的区别。**

/sitemap.xml 虽然列出了所有可供索引的页面，但对于内容处理并无助益。AI 系统在处理时，仍需解析复杂的 HTML，并处理冗余信息，从而使上下文窗口变得杂乱无章。

/robots.txt 文件则用于指导搜索引擎爬虫的访问，但它同样不提供内容理解上的帮助。

**而 /llms.txt 则专为解决 AI 系统面临的挑战而设计。它有助于克服上下文窗口的限制，删除不必要的 tokens 和脚本，并以优化后的结构来展示内容，便于人工智能处理。**

  

05

  

## 如何将 LLMs.txt 应用于AI系统

与那些主动在网络中进行搜寻的搜索引擎不同，现有的 LLMs 并不会自动识别并收录 LLMs.txt 文件。

您需要手动将文件内容输入到 AI 系统中。操作方法包括粘贴链接、直接将文件内容贴入输入框，或者利用 AI 工具的文件上传功能。

## 5.1 ChatGPT

首先，您需要前往相关文档或 /llms-full.txt 的网页地址。接着，将内容或网址复制到聊天界面，提出具体问题，说明你想完成什么。

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

在 ChatGPT 中使用 llms-full.txt 文件的截图（图片由作者提供）

## 5.2 Claude

Claude 目前还不能浏览网页，所以请将文档的 /llms-full.txt 文件内容复制到剪贴板。或者，也可以将其保存为.txt 文件并上传。现在，你就可以自信地提出任何问题，确信 Claude 拥有完整且最新的上下文信息。

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

在 Claude 中使用 llms-full.txt 文件的截图（图片由作者提供）

## 5.3 Cursor

Cursor 可以让我们添加并索引外部文档，这样就能在对话中引用这些内容。操作方法很简单，只需输入 @Docs > Add new doc。随后会出现一个弹窗，我们可以在那里粘贴 /llms-full.txt 文件的链接。之后，就能像使用其他文档一样，将其作为对话的上下文。

想深入了解这项功能，可以查阅 Cursor 的 @Docs 功能介绍 <sup><span>[9]</span></sup> 。

![image.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

将 llms-full.txt 文件作为上下文导入 Cursor 的操作截图（图片由作者提供）

  

06

  

## 如何生成 LLMs.txt 文件

我们可以选用以下几种工具来生成自己的 LLMs.txt 文件：

- Mintlify <sup><span>[10]</span></sup> ：能够自动为在线文档生成 /llms.txt 和 /llms-full.txt。
- llmstxt by dotenv <sup><span>[5]</span></sup> ：由 dotenvx 的开发者 Mot 提供的工具，它可以通过网站的 sitemap.xml 来生成 llms.txt。
- llmstxt by Firecrawl <sup><span>[6]</span></sup> ：由 Firecrawl 的创始人 Eric Ciarla 开发的工具，它利用 Firecrawl 抓取网站信息来制作 llms.txt 文件。

  

07

  

## LLMs.txt 的发展方向是什么？

LLMs.txt 标志着向以 AI 为先的文档方向转变。

正如 SEO 对于网站在搜索结果中的可见性至关重要一样，拥有可供 AI 读取的内容对于开发工具和文档来说也将变得不可或缺。

随着越来越多的网站开始使用这个文件，我们可以预见将出现新的工具和最佳实践，以实现人类和 AI 助手对网站内容的共同可访问性。

目前，LLMs.txt 提供了一个切实有效的解决方案，帮助 AI 系统更深入地理解和运用网络资源，特别是在技术文档和 API 领域。

*Thanks for reading!*

*Hope you have enjoyed and learned new things from this blog!*

  

***About the authors***

## Derick Ruiz

I help developer tool companies reach more devs with technical content at Abundant.dev

**END**

**本期互动内容 🍻**

  

**❓** **已经尝试过 LLMs.txt 的同学，能分享一下实施前后的效果对比吗？**

**🔗文中链接🔗**

\[1\]https://unsplash.com/@px7digital?utm\_content=creditCopyText&utm\_medium=referral&utm\_source=unsplash

\[2\]https://unsplash.com/photos/a-close-up-of-a-piece-of-paper-with-numbers-on-it-00PCjphxzpo?utm\_content=creditCopyText&utm\_medium=referral&utm\_source=unsplash

\[3\]https://directory.llmstxt.cloud/

\[4\]https://llmstxt.directory/

\[5\]https://github.com/dotenvx/llmstxt

\[6\]https://llmstxt.firecrawl.dev/

\[7\]https://llmstxt.org/llms.txt

\[8\]https://docs.anthropic.com/llms.txt

\[9\]https://docs.cursor.com/context/@-symbols/@-docs

\[10\]https://mintlify.com/

**原文链接：**  

https://towardsdatascience.com/llms-txt-414d5121bcb3

![微信图片_20240716175748.png](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E "undefined")

**AI及大模型技术分享交流群**

**干货分享，联系小助手入群**

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

如果觉得有帮助，就点点 **『在看』** 哦！

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过