---
标题: "DeepSeek+开源n8n：24小时推特(X)热点监控工作流太绝了！【附赠：完整工作流】-DeepSeek+开源n8n：24h推特(X)热点监控Workflow太绝了！【附赠：完整工作流】"
链接: "https://mp.weixin.qq.com/s/jC_bPFcha-SZmBO_EMGJMg"
作者: "[[袋鼠帝]]"
创建时间: "2025-04-11T10:57:30+08:00"
摘要: "文章介绍了如何使用DeepSeek和开源工具n8n搭建一个24小时监控推特热点的自动化工作流，并提供了完整的工作流文件。"
tags:
  - "clippings"
  - "AI"
  - "效率"
  - "自动化"
  - "推特监控"
  - "开源工具"
字数: "269"
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
原创 袋鼠帝 *2025年04月11日 07:55* *云南*

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/Gp1VfqvVj8uiaut9y599AZ4F9k1uFXO0bfxLbZpIbIHFjwZ86KTlpicBt3Tvo1kNMvuDDroGkzEMmXYtg5PibkaMQ/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/UibKpBUbFicLKReXkDljWvKH0WAMsgUk0oecSnMCEJzLZrWI6n8Bpr7KGrIO99M8WzicZRpW65h8KCFDpMhreAsibw/640?tp=webp&wxfrom=5&wx_lazy=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/OwJzuwfJwufpGiaEmgibCvvibib8MZrT9NJCYtLlp6zcic77Ecz64tqgrk5urlWM4mDzZ1Xjibr0DqPGic8VSU1tD3XKg/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

点击上方 蓝字 关注我们

![图片](https://mmbiz.qpic.cn/mmbiz_png/0ZZqtBBibibI78uRxI2WdaJmxiaCDrP41TFNe01fJ8lNlxU6dZHrRTkHYE2DXElx3ibvFhTVHQNYuHde8vic8ZIqHOg/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

大家好，我是袋鼠帝

做自媒体一年多了，终于有了一点点成绩，最近 「 袋鼠帝AI客栈」 也是排到了 个人AI公众号排行榜第3名 （托大家的福）。

*持续输出AI相关技术、干货、效率工具、喂饭级教程~*

![图片](https://mmbiz.qpic.cn/mmbiz_png/ibFTiaLQPCIsVjNEiavW6HEsLhu6QUShyy6Rm1CmFBerfN3xuq97aVMCKo8vAjv7HdwHpBepNpOGhpnNuKKUIk2LA/640?wx_fmt=png&from=appmsg&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)

众所周知，做自媒体想要流量大， 追热点 肯定是最简单快捷的方式。

而我，基本上没有抢到过最实时的热点，，，

每次都是 慢半拍 。

前两天给大家分享了一个我认为 最强的开源AI Workflow平台：n8n

> n8n
> 
> 袋鼠帝，公众号：袋鼠帝AI客栈 [狂揽75K Star！最强开源AI Workflow平台【内置1500+工具和模板】效率起飞～](https://mp.weixin.qq.com/s/ctAqu27OZFL0Fp46d4R6Eg)

当时就有朋友在评论区问： 热点监控如何实现？

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1A3g3tQKkaghxT9Iwool64gJXSN0lczmpgicNibOCCuX18l64wKWYoHp7oVVt3MtAWRNMjibgg7IZqPw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

经过这几天的研究

我用 n8n 实现了 一套超实用 的 X（原Twitter）热点监控workflow （工作流）

*为什么要监控X的推文信息呢？因为X上面真的有太多优质博主、和优质内容了，比如马斯克、山姆\*奥特曼等等...以及有很多官媒：OpenAI，DeepSeek，，，所以更容易拿到优质内容，和一手信息。*

它由 两个workflow(工作流)组成

第一个workflow 如下图，会定时从X（原Twitter）抓取设定好的一批博主、或者官媒 最新的推文信息 （包含推文 内容、点赞数、评论数、阅读量、发布时间 等等...）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1A3g3tQKkaghxT9Iwool64gDo5TbO95bPujEbhLPIyLYppzicBYWgAEYC4TwgdJYgKJiajDhsYduHiaA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

第二个workflow 是针对抓取到的增量推文，用AI Agent筛选过滤，提取出有价值的推文，然后让DeepSeek针对每条筛选出来的推文资讯，进行写文选题方向、标题建议，接着存储到Google表格中。

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1A3g3tQKkaghxT9Iwool64gxl8J2gfMjhPpANDzNiaTicYAm40ojMtWPvUwcsuv4AExT4icoZCMDP08Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

最后会把整理好的热点信息整合， 邮件通知我 （还支持电话、App推送等其他通知方式）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1A3g3tQKkaghxT9Iwool64gNgCbCHx4fq6au5JQjOJHh4xibKQYfNgODhCpBdYFDzC4nicMrmTsMh3w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

本文我将给大家 讲解这套X热点推文监控workflow是如何搭建、使用的。

并且会在 文末将它们免费赠送给大家。

*PS：是两个json文件，直接在n8n里面导入就能用啦*

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1A3g3tQKkaghxT9Iwool64gHeykC12kRV2iap02lf4Ug4PyEJ0h3Zq4Ghq5OBcLs1RbzFcNrrv5DIA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

好了，话不多说，我们开始喂饭~

  

![图片](https://mmbiz.qpic.cn/mmbiz_png/fRp5p4jMuDQjdXQXUMBDtPtLS0iaiaxVKblUBecgRUn30Lv2liaIUfnwcVib2D28Om4F0LpOd4oiah0psOJlRBHqewA/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Workflow流程解读

![图片](https://mmbiz.qpic.cn/mmbiz_png/jLdw7EZFJmIjAic1276gZeyjcsS9UMqa3VkvD2WgU11EyJAoVCSagkO3Kmia89jgusIXDficZIgTTb6ia32cibxVKgQ/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这两个workflow的主要功能是：准实时监控一些X的博主、官媒的最新推文，并通过AI自动筛选出对我有价值的信息（邮件通知我），最后生成一些写文、标题建议，存储到表格中。这样极大的节省了我收集、筛选、处理信息的时间。

两个workflow需要配合起来一起使用。

我们先来讲解一下 第一个workflow：定时抓取X博主最新推文

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1A3g3tQKkaghxT9Iwool64gwvmbCI0Pj5JzZZK8kicKxxNUrUicFtc4Eic1d2ib73tWtI10Ww11hSEBIA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

该workflow是 定时触发 （可设置触发时间间隔，分钟、小时、天等等）

在第二个节点处可以配置想监控的博主id，比如我这里就设置了小户、OpenAI、DeepSeek

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

不是多个博主并行抓取，会挨个抓取，获取每个博主最新的top n条推文，最后经过字段筛选，把每条推文中有用的信息存储到一个Google表格里面，一行代表一条推文（姑且就叫 「 X最新推文表格」 吧）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

流程里面会循环请求，分页获取博主的推文，但每页推文条数不是固定的...

可以通过下图中的 if节点控制请求次数 （如果是2：每个博主都获取2页推文数据，以此类推）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

接下来是 第二个workflow： 监听X博主最新推文

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这个workflow是通过监听上一个工作流的「 X最新推文表格」新增行（row added）动作触发的，也就是说只有当「 X最新推文表格」有新推文插入时才会触发这个workflow（监听增量数据）。

这样咱们就不会拿到旧数据（已经处理过的数据），而是每次都能拿到最新的推文（因为workflow1可能会拿到重复的数据，但是重复的数据在插入Google表格的时候，只会覆盖不会新增）。

接着就是通过DeepSeek加持的AI Agent过滤掉一些对我没有价值的推文，并提取推文摘要。在第二个AI agent节点处提供一些写文方向、标题建议，最后存储到一个新的Google表格中「价值推文表格」，最后将筛选过后的热点信息通过gmail通知到我。

温馨提示：这两个工作流需要按照上篇的方式，云部署n8n才能正常使用哦

> 免费一键云部署n8n
> 
> 袋鼠帝，公众号：袋鼠帝AI客栈 [「n8n云服务」免费一键部署！还提供域名访问，小白也能轻松搞定~](https://mp.weixin.qq.com/s/O0AJL3avOtmfr_EqJh28ew)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Workflow相关App节点配置

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这两个workflow中，有三类节点是我们需要通过API外部调用的

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

1.获取X推文的节点；

2.Google表格、邮箱节点；

3.大模型调用节点；

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

*朋友们拿到工作流，导入n8n之后需要自行配置这三个节点才能正常使用*

既然要监控X热点推文，那么肯定是要自动通过API获取X的数据。

X官方 其实是提供了这块API功能的，但是他们价格 太贵了 ， 至少100$一个月 。虽然有免费版，但是限流太严重（pass）

然后为了经济实惠，我又找了一些可以抓取X数据的开源项目，稳妥起见，我还专门新注册了一个X小号来测试，结果，t喵的刚刚接入，号就没了...

找来找去，最后发现这个叫 TwitterAPI.io 的平台最适合（应该是全网最良心的X数据抓取平台了）

*数据实时，每抓取1000条推文才0.15$，非常实惠，关键会免费送5$体验（都够用很久了）*

地址： https://twitterapi.io/

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

他们的接口，我最近调用567次，才花了不到0.6$（花的还是免费额度）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

注册成功之后点击 右上角头像->Dashboard

复制 twitterapi.io的apikey备用

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

1.配置X的请求节点凭证

进入workflow1的编辑页面，双击下图中的request节点

*这个节点会通过API调用twitterapi.io获取相关X博主的最新推文*

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

创建新的凭证（ create new credential ）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

name填写： X-API-Key ，value粘贴刚刚 复制的 twitterapi.io的apikey

点击 保存

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

到这里 twitterapi.io的request节点就配置好了（后续新增节点，直接选择刚刚创建好的凭证即可，不用重复填写）

  

2.配置Google Sheet、邮箱凭证

接下来需要配置Google sheet（Google表格）、邮箱的 凭证

先访问Google Cloud控制台：  

https://console.cloud.google.com/auth/clients

会自动打开如下页面（前提是已经登录了）

点击一个 oauth 2.0 client （没有就先创建）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

点击之后会进入详情页，如下

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

接着咱们回到workflow1的编辑页面

双击打开Google Sheet节点

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

同样需要新建凭证（ create new credential ）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

按照下图的指示配置

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

配置完之后点击 sign in with Google （会弹出一个小框，需要登录一下自己的谷歌邮箱账号，授权一下）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

授权完成之后，顶部这里 出现 Account connected （已连接账户）

就代表授权成功啦~

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

咱们还需要在Google Cloud控制台把 Gmail API 和 Google Sheet API启用。

先在搜索栏 通过关键词搜索，然后点进去

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

如果都是API Enabled，那么就代表已经是开启状态了，如果没有开启，点击Enable的蓝色按钮开启即可（没有开启才显示这个按钮）。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

另外workflow2中的Gmail节点凭证跟Google Sheet的凭证配置方式一模一样，就不重复赘述了。

  

3.配置大模型节点

最后咱们再把大模型节点配置一下

进入workflow2的编辑页面

有两个模型节点，双击打开

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

同样是添加凭证

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

可以直接粘贴DeepSeek官方apikey，点击保存

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

*第二个模型节点我使用的是openrouter*

*地址：https://openrouter.ai/*

*大家可以换成别的*

也支持别的模型节点（可以随意切换使用）

让AI Agent和DeepSeek模型节点断开链接，点击加号，左边就会出现一堆其他的大模型节点（大部分中转站，还有别的一些平台都可以用OpenAI节点实现连接）

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

最后我们可以根据需要调整一下两个workflow的定时触发频率。

workflow1的定时触发频率我建议是10分钟-1个小时一次

*那么获取信息最多滞后10分钟-1小时，因为每次获取X推文都会消耗额度，所以我觉得当配置的博主太多时，也没必要执行的很频繁，可以接受一定程度的滞后（当然，土豪随意，设置1秒一次都行，那就完全实时获取了）*

workflow2的定时触发频率我建议可以设置在1分钟到5分钟一次

假设我配置 workflow1每隔30分钟执行一次，workflow2每隔1分钟执行一次。  

当workflow1执行，并且有新的数据插入 「 X最新推文表格」，workflow2每隔1分钟会执行一次，单还需要判断 「 X最新推文表格」有新增数据才会触发工作流，否则也不会触发。

注意：调试的时候workflow2每次都会获取 「 X最新推文表格」的全量数据

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

只有变成 激活（active）状态 ，才会按照配置的时间定时触发工作流。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

激活之后，workflow2才会只获取 「 X最新推文表格」的增量数据。

在 「 袋鼠帝AI客栈」 公众号后台 私信："n8n工作流" 即可 免费领取 这两个 workflow

说实话，这次分享的内容还挺有难度的，我也花了大量的时间去研究，但是我觉得非常实用。

希望大家都能通过我分享的工作流，了解n8n的配置和使用，最后能自己搭建合适的workflow，让效率飞升~

有个n8n的中文学习文档：

https://n8n.akashio.com/

过程中有问题的朋友可以进群沟通、交流。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

大家还有什么想用n8n实现的需求，欢迎评论区聊聊~

********能看到这里的都是凤毛麟角的存在！********

********如果觉得不错，随手点个赞、在看、转发三连吧~********  

********如果想第一时间收到推送，也可以给我个星标 ⭐********

********谢谢你耐心看完我的文章~********

********KG中转站新增了国产新模型：qwq-32b、hunyuan-t1、deepseek-v3-0324********

********https://kg-api.cloud/********

********星球有DeepSeek接入微信的详细教程（全新方案，更稳定）********

********![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)********

********![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)********

袋鼠帝

 **微信扫一扫赞赏作者**

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过