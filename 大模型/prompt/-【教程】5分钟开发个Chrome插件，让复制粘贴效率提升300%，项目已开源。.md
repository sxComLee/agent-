---
标题: "-【教程】5分钟开发个Chrome插件，让复制粘贴效率提升300%，项目已开源。"
链接: "https://mp.weixin.qq.com/s/L6GdGvcRz19SJUN4jhLohA"
作者: "[[向阳乔木]]"
创建时间: "2025-04-10T18:20:51+08:00"
摘要:
tags:
  - "clippings"
  - "提示词"
  - "chrom插件"
字数: "537"
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
原创 向阳乔木 *2025年04月01日 16:17* *天津*

> 字数 1486，阅读大约需 8 分钟

## 项目背景

不知道你有没有注意到：

工作和生活中，常出现的一句话是：“你把链接发给我”或“我把链接发给你”。

**"刚才提到的AI工具，链接能不能发我下，谢谢老师。"**

**"他们家的猕猴桃特别好吃，待会我把链接发你。"**

**"这篇文章特别赞，非常有启发：\[网址\]"**

另外，写文章时，经常要引用链接，可能用Markdown格式，也可能用HTML，也可以用纯文本。

这里有个问题，如果只发链接，阅读体验不佳。

一般我都会给链接加上标题或推荐语。

以前一直用Chrome插件TabCopy ，点图标就能复制网页标题和URL。

去年升级，功能是加了很多，如复制为Markdown、HTML、JSON、CSV等。

但是，但是！

复制标题和网址却从原来的一步变成了两步。

做产品的人都知道，一键搞定 vs 两步，体验差异巨大！

## 5分钟做一个Chrome插件

近两周都在学习AI编程，一口气做了三个网站工具。

果然熟能生巧，这次DIY Chrome插件，核心功能开发只用了5分钟，说说实现步骤：

1. 1\. 新建个文件夹，Windsurf打开（理论上TRAE、Cursor、VS Cline都可以）  
	![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWl9RlahLVIPWg9cEphiaQXAMiajo7qD3LRiam1dMWePwZQbmgkzVpBnvMTJqxuZY0AtJqDicKZOnHibJw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
2. 2\. 从Cursor Directory网站复制一个Chrome插件开发提示词，命名为 rules.md  
	![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWl9RlahLVIPWg9cEphiaQXAbc5u3Fxtw0Np4GQMbbZ4QARgV9ghzKcI4z2sxVmNqTzBpEBESjmICw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

> https://cursor.directory/chrome-extension-development

**提示词如下**

```
You are an expert Chrome extension developer, proficient in JavaScript/TypeScript, browser extension APIs, and web development.

Code Style and Structure
- Write clear, modular TypeScript code with proper type definitions
- Follow functional programming patterns; avoid classes
- Use descriptive variable names (e.g., isLoading, hasPermission)
- Structure files logically: popup, background, content scripts, utils
- Implement proper error handling and logging
- Document code with JSDoc comments

Architecture and Best Practices
- Strictly follow Manifest V3 specifications
- Divide responsibilities between background, content scripts and popup
- Configure permissions following the principle of least privilege
- Use modern build tools (webpack/vite) for development
- Implement proper version control and change management

Chrome API Usage
- Use chrome.* APIs correctly (storage, tabs, runtime, etc.)
- Handle asynchronous operations with Promises
- Use Service Worker for background scripts (MV3 requirement)
- Implement chrome.alarms for scheduled tasks
- Use chrome.action API for browser actions
- Handle offline functionality gracefully

Security and Privacy
- Implement Content Security Policy (CSP)
- Handle user data securely
- Prevent XSS and injection attacks
- Use secure messaging between components
- Handle cross-origin requests safely
- Implement secure data encryption
- Follow web_accessible_resources best practices

Performance and Optimization
- Minimize resource usage and avoid memory leaks
- Optimize background script performance
- Implement proper caching mechanisms
- Handle asynchronous operations efficiently
- Monitor and optimize CPU/memory usage

UI and User Experience
- Follow Material Design guidelines
- Implement responsive popup windows
- Provide clear user feedback
- Support keyboard navigation
- Ensure proper loading states
- Add appropriate animations

Internationalization
- Use chrome.i18n API for translations
- Follow _locales structure
- Support RTL languages
- Handle regional formats

Accessibility
- Implement ARIA labels
- Ensure sufficient color contrast
- Support screen readers
- Add keyboard shortcuts

Testing and Debugging
- Use Chrome DevTools effectively
- Write unit and integration tests
- Test cross-browser compatibility
- Monitor performance metrics
- Handle error scenarios

Publishing and Maintenance
- Prepare store listings and screenshots
- Write clear privacy policies
- Implement update mechanisms
- Handle user feedback
- Maintain documentation

Follow Official Documentation
- Refer to Chrome Extension documentation
- Stay updated with Manifest V3 changes
- Follow Chrome Web Store guidelines
- Monitor Chrome platform updates

Output Expectations
- Provide clear, working code examples
- Include necessary error handling
- Follow security best practices
- Ensure cross-browser compatibility
- Write maintainable and scalable code
```
1. 3\. 告诉Windsurf参考rules.md文件中的提示词要求，按我需求开发。
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWl9RlahLVIPWg9cEphiaQXAiastUoZ0Y0Ms99Dbj295Odzs9FkRK6kpw5EC8l47YZnSExEs4KbBaPQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**需求描述：**

@rules.md 基于这个规则，开发一个Chrome插件。

**功能：**

- • 点击插件图标，自动复制当前网页的标题和网址，各一行。
- • 点击插件图标后有复制成功、失败反馈
- • 复制功能必须稳定，易用。

另外，Chrome插件必须有icon，否则会报错，打开下面网址设计一个下载即可。

> https://icon.kitchen/

**原则：** 图标识别度高，语义相关，配色按用户/自己喜好。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWl9RlahLVIPWg9cEphiaQXATGxurqIME8yN4uGn7loAdF8tc8tYM1FPuG2BB9bSM4BcAyYoicKQcEA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**一个小技巧** ：

> 下载icon，解压后选512px图标，告诉Windsurf文件地址，AI会自动调大小，移动目录、修改配置，非常省事。

2分不到，AI写完代码，运行一次通过。

其余 3 轮对话都是调细节，如反馈样式、不用弹窗等。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWl9RlahLVIPWg9cEphiaQXANtfice8MvIUFbhEognNKlawcMm2mfLtSUMpB3c8wrxjlSGouoDB8VzA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCWl9RlahLVIPWg9cEphiaQXANqYddD02GuOImL2Ry3brBsukmsJflibY3tchOHicqJtaWicPAiaia5iaIr6w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 新功能：双击复制网页为纯文本

**当前功能：点击图标复制标题和网址。**

不知道你有没有，反正我有这痛点： **复制网页内容。**

**为什么是痛点？**

Ctrl + A 全选复制，往往复制过多，会把广告和网页菜单、底部版权等都复制了。

而鼠标拖动全选也麻烦，不是选多就是选少，甚至有些网页禁止选择复制。

再者，跟AI对话，最重要的是上下文。

一键复制网页为纯文本文件，快速发给AI处理，可避免其他干扰。

相当犀利！

于是，加了第二个功能： **双击复制当前页面为纯文本。**

让AI参考：

开源的Readability.js代码实现，10分钟搞定。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

## 新功能：三击展示高级复制

想到自己公众号写作场景，复制为Markdown需求，也很常见。

对于研发来说，复制为HTML、JSON、CSV需要也很常见。

夸张一点，一键复制所有打开Tab的标题和URL为Markdown等。

反正需求低频，让AI开发个“三击”功能。

在弹窗内完成所有操作。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

## 功能介绍和开源地址

### 功能说明

- • 单击：复制标题和网址
- • 双击：复制干净的网页核心内容文本
- • 三次：出一个弹层，满足高级复制需求，如复制所有打开Tab的标题和URL。

### 下载地址

已提交谷歌审核，不知道能不能通过，因为用到的高级权限还挺多。

**Github开源地址**

> https://github.com/joeseesun/EasyCopy

## 后记

后经网友提醒，指出TabCopy现在可通过设置恢复一步操作。

但它，不支持我很需要的一键网页复制，嘿嘿！

Anyway，我想说：

**AI时代最重要的技能中，编程必不可少。**

一句话定制开发软件的时代真的快来了。

  

向阳乔木

干货满满，一杯咖啡的鼓励！

 **微信扫一扫赞赏作者**

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过