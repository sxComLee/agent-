---
标题: "开发者遭ChatGPT“赶鸭子上架”！AI编造假功能，结果吸引大量用户，不得不开发出来了"
链接: "https://mp.weixin.qq.com/s/hozcZrrp8APYvmXjzXnXlQ"
作者: "[[关注前沿科技]]"
创建时间: "2025-07-08T14:25:52+08:00"
摘要: "ChatGPT编造了一个乐谱扫描网站不支持的功能，导致大量用户涌入，迫使开发者不得不实现该功能。"
tags:
  - "clippings"
  - "AI"
  - "编程"
  - "ChatGPT"
  - "乐谱扫描"
  - "Soundslice"
字数: "141"
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
![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCqqyibV0ZZJ8h6eAZrFjH5iaWRG5edVM39pUY1IdicQIH2paHAZAo0tHicw/0?wx_fmt=jpeg)

关注前沿科技 [量子位](https://mp.weixin.qq.com/s/) *2025年07月08日 11:31*

##### 西风 发自 凹非寺量子位 | 公众号 QbitAI

笑不活了，ChatGPT闯大祸！

AI幻觉随意编造一个产品的新功能，误导用户大量涌入，最后 **开发者不得不把这 个虚构的功能真 的做了出来** 。

受害者是一个 乐谱扫描网站 ，最近莫名收到大量用户上传的ASCII吉他谱截图，这些截图还都是来自ChatGPT的。

网站开发者懵了：

> WTF？我们 **压根不支持扫描ASCII吉他谱** 啊？？？

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvC0lUNPlDrDoD0m0Nwy1iabE1vvyPmXMg48lRKJ3ZWrU1SJsrEsVLHicRA/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

直到这位开发者自己亲自用ChatGPT倒腾了一番才发现，好你小汁，原来如此～

ChatGPT生成ASCII吉他谱之后，会自动推荐大伙儿到他们的网站收听或是进一步创作。

然鹅，该网站平时扫描的都是传统标准五线谱，根本不支持ASCII吉他谱这种小众格式……

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCKtpzoATdEKesiaVrykkVCrlS0jUpricbt0ZvMOR7pCTvRxPDgfaCj6tw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

更更笑不活的是，大量用户尝试该功能，把开发者架在那儿了，不支持该功能难免会让满怀期待赶来用户感到失望，显得网站很差劲。

于是乎，这位开发者被迫，加急赶工把这个功能给造了出来。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCJ5AqERE1rYP9LvxUFxJO0v9boEuVMj1ydWDRM7scswJjiaj8M88gIug/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

## 被ChatGPT“赶鸭子上架”造新功能

这个能扫描乐谱的网站名叫 **S oundsli ce** ，其中的乐谱扫描仪功能能将图片照片中的 音乐数字化 ，这样你就能收听、编辑和练习。

这位网站开发者表示，他们一直在持续改进这个系统，而他的工作内容之一就是负责留意错误日志，看看哪些图片的处理结果不尽如人意。

过去几个月里，他逐渐开始在错误日志中发现一种奇怪的上传内容。

不是像这种传统乐谱的图片：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCs2SDe8zblJ1NGaCuHRKUICupcYYib436gv38L3gIDjOgBvoyeiaWWFibw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

而是酱婶儿的ChatGPT对话屏幕截图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvC6p7wia1T93fX2ML7SEHtrRZWLrAGzfdkHOoVZUibFonSj31ibnTNmgc6w/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

一看截图内容，小哥愣住了，“搞什么呀？这显然这不是标准的音乐记谱法。这是ASCII吉他谱，还是一种相当简陋的吉他记谱形式”。

他们的 扫描系统本来就没有，也没打算支持这种记谱形式 。那为啥会收到这么多来自ChatGPT的ASCII吉他谱截图呢？

小哥为此困惑了好几个星期，直到自己试着用了用ChatGPT，才发现原来是 ChatGPT告诉大家去Soundslice注册账号，导入ASCII吉他谱，就能听到音频播放 。

一切就说得通了。

小哥非常气愤，ChatGPT完全是在误导大家，而且在这个过程中，它还无形中让网站形象受损，让用户对他们服务的预期设下了错误的引导。

小哥也很无奈，该怎么办？源源不断的新用户都被告知关于该网站的错误信息。难道他们要在网站各处贴上免责声明，写着“别信ChatGPT说的我们支持ASCII吉他谱”吗？

最终他们决定：管它呢，不如顺应市场需求吧。

于是他们专门开发了一个ASCII吉他谱导入器，小哥还强调这在他的“2025年预计要写的软件”几乎排在最末尾。换句话说，在此之前就没想着要开发这玩意儿。

而且他们还修改了扫描系统的界面文字，向大家介绍这个新功能。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCstcXVVmzU9CZ0odVyXlkxpH2Tn27kbUmys9y4wbP8JIBetg9SWaMPg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

当ASCII吉他谱导入到Soundslice后，大家伙儿就能播放这段谱子并进行编辑了。该网站还会自动生成对应的标准乐谱，效果be like：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCZSVttMoRoYBc5fcW7iaUiaibicBxO8WJtzg1cB8WGWsXnqnqLcPiaOF3bZw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

网站特别声明，ASCII吉他谱是一种局限性很强的格式。它既不标注音符时值和节奏，有时甚至连小节线都没有。因此，他们仅将其视为把音乐导入Soundslice的第一步，用户还可能需要使用他们的编辑器对其进行整理。

随后附上了他们对音乐记谱特定方面支持的详细说明：

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCkwicCiaWUGjlZZJtptOTibCnJYQIVxbywISHC4Eibqk5wPwWHBkeUOlz4g/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

看得出来小哥有多无奈，据他所知，这是首例因为ChatGPT错误地告诉人们某项功能存在，而促使一家公司去开发该功能的案例。

他本人对此表示心情很复杂：

> 能增加一个帮助人们的工具，我很高兴。但我感觉我们是在一种奇怪的情况下被迫这么做的。我们真的应该为了应对错误信息而去开发功能吗？

有意思的是，这位开发者一眼就能看出ChatGPT截图是ASCII吉他谱，还和团队火速造出了ASCII吉他谱扫描功能，其实他本人也是位吉他手。

## 吉他手&Web开发者

Soundslice网站的创始人，也是分享上面这起离谱事件的人，名叫 Adrian Holovaty ，是一名来自芝加哥的Web开发者，也是一名音乐人。

音乐方面，他发布的专辑作品包括《Layer Cake》（2025 年）、《Melodic Guitar Music》（2023 年）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCKXUeJ01bUibJHniadnicH7s60jZ162h6kVpnorbuQktJRDUS8JvqOpiccg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

他还是W3C音乐记谱社区组 *（W 3C Musi c Notation Community Group）* 的三位联合主席之一，该组织负责制定和维护音乐记谱的相关规范。

其工作重点是MNX格式，他们希望它能成为下一代数字化音乐记谱的编码格式。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvC6UoGK3ekfxhgzBhe6dwJsicACh9BT56aILOuHUAmo3tcSAdOSoGgxxw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

而Soundslice网站创建初衷是想让喜欢音乐的人能够用这个工具 把乐谱变成 交互式学习环境 ，然后进行练习、教学、分享、转录。

该网站能自动适配设备的音乐渲染功能，还有功能完备的基于网页的乐谱编辑器，以及能从照片或PDF中识别音符的“光学音乐识别”系统。

除此之外，早在2005年，他还开发了最早嵌入谷歌地图网站之一的chicagocrime.org （网站 已不存在 ） ，《纽约时报》将其评为年度最佳创意之一；2004年，他开发了一个浏览器扩展组件，启发了Greasemonkey和“用户脚本”的诞生；2007年，他还曾创办了社区新闻与讨论网站EveryBlock，后来该网站被出售。

更早之前，Adrian Holovaty还是一名新闻从业者，曾工作于《华盛顿邮报》等。

他把这场由ChatGPT说谎而造成的开发新功能事件发出来后，引起众多网友讨论。

有意思的是，网友的思路也是很清奇，认为恰恰可以利用ChatGPT的幻觉来搞开发：

> 我发现这是借助GPT-4进行编程的超实用方法之一。
> 
> 我不会直接跟它讲API怎么运作，而是让它去“猜”，比如拿一段需要新增功能的示例代码当起点。有时候，它能想出比我原本思路更妙的方案。接着我就调整API，让它写的代码能跑起来。
> 
> 反过来，我也会把现成的代码扔给它，问它这段代码是干啥的。要是它理解错了，那就说明我的API设计得让人犯迷糊，而且能看出到底是哪些地方容易让人困惑。
> 
> 这其实是利用了神经网络最擅长的事儿：不是输出精准信息，而是一本正经 “胡编” 出超像那么回事的内容，也就是所谓的“幻觉”。靠的是创造力，而非逻辑。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCu2ztPZzlyfeg74D8LIAHDL4Ewxb7GxTIPRuVmFqQAJgwKLSwf7kXaQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

> 这和人机交互设计领域一种古老的“绿野仙踪法（Wizard of Oz）”很像。具体来说，就是让人工操作者假装成一个还没开发出来的应用程序，这种方法在发掘新功能方面非常有用。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCsIIlXonIzMNibrcA0P6IfSvOhEru6PPqP2DtSaysfiaKzPCAuGficlhZQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

还有网友觉得这事儿有意思的点在于：

> 推出一个新功能都比让OpenAI给ChatGPT打个补丁、别再假装这个功能存在要容易（我都不确定他们该怎么弄，总不能直接全面屏蔽所有提到SoundSlice的内容吧）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCicumgDiaQBaZrAbZ7qygRzRfL0oenjTU9GUicMHicHp0GstRKnBGsbYSww/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1) ![图片](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtD3Br1ICKUOqnG8MkWeJibvCxMPWCKoib4HfCictYic7iaXuXWxYFY6VmQp26SSn1OaiaBicEpsZoRAvRPmw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1)

*参考链接：*  
*\[1\]https://www.holovaty.com/writing/chatgpt-fake-feature/*  
*\[2\]https://news.ycombinator.com/item?id=44491071*

  

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