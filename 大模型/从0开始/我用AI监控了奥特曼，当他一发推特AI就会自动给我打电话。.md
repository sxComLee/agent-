---
标题: "我用AI监控了奥特曼，当他一发推特AI就会自动给我打电话。"
链接: "https://mp.weixin.qq.com/s/jJ2DG-aLTVfZRJs8YSdr9w"
作者: "[[数字生命卡兹克]]"
创建时间: "2025-04-22T13:18:29+08:00"
摘要:
tags:
  - "clippings"
字数: "116"
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

![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/OjgKEXmLURpIicXtndhAKofJf05WYmO1ssq0GuJ0PvxgicgdGzDFGaG8If8vOicV0XBeicWf7wZcRvq3zkKOIw5OAA/0?wx_fmt=jpeg)

原创 数字生命卡兹克 [数字生命卡兹克](https://mp.weixin.qq.com/s/)

2025-04-22 09:03:06

精确发文时间由壹伴提供

手机阅读

上周我真的扛不住了。

奥特曼这个孙贼，发了个X说，“要发一个礼拜的好东西”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sMaaxXEdCUc2xJMhEGj6p7OzBD45nzNDrboheeia5pEIhwicenMEOIUxw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我信了他的邪，明明出差1周，每天早上9点不到就要起来参加活动，但是晚上根本不敢睡觉，天天蹲到凌晨3点半，蹲到他们那边时间中午12点多，我才敢去睡觉。

真的，那一整周，我每天就睡3、4个小时，你们不知道那种感觉，从凌晨12点开始，每过几分钟我都要刷下X，真的，快特么刷出幻觉了。

然后，奥特曼这个口嗨，疯狂放鸽子。

一周5天，也就发了GPT4.1和O3这两能看的，其他的，你管他们叫好东西？他是不是对好东西有啥误解？

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1s41YTGVBgobXicoUrNfPHr8GPTqmDeek4LQX9k7JJwFCGZvm2zTtmkVg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

真的，这一周之后，周末我回到家，我觉得这样不行，再这么被搞下去，我觉得我会猝死，会英年早噶。

于是我就想，能不能做一个监控，在奥特曼发X的时候，直接打电话叫醒我，这样，我就就不用干等了。

该12点睡觉就12点睡觉，如果真的有啥新东西，啪一个电话直接把我喊起来，而不是每天在那傻傻的刷新。

这个思路在我看来，还挺简单，基本就是分为2步。

1\. 监控奥特曼的X，每几分钟爬取1次，检查有没有新的帖子。

2\. 抓到了新的帖子，就直接给我打电话，实现深夜叫醒服务。

第一步超级简单，我直接用Trae给我写了一个Python，可以实现每五分钟爬取一次，提示词是这样的：

"我想做一个推特监控，用来实时监控一些账号的内容，如果有新内容，发到我的邮箱里，邮件标题要用大模型翻译成中文，用python"

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sZ5OTP5oCSz1jCiadju9ichLcY9q7PicDc4w1lglshM38AohiaRSCoe7Bow/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

没一会，Trae就帮我写好了完整的代码，写的非常细致，还给出了README.md。

直接就可以参考里面的步骤，复制粘贴上在X开发平台的密钥信息，就可以用了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sqSIk5D0ctsTtDKKmKcvEZJqG950ukpaAHIsibLzicJpYWNVcuwJAliapg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

X官方API每个月只给了100次的免费读取次数，但用来应对奥特曼这种临时的足够了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sc0rf229rF4jicqNnfOgGuT5ibQOpBTfvONvCaP5gicsCHR6lqyIsC6Mzg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

当然，还可以进一步优化，比如告诉Trae，降低爬取的频率，不要在太平洋时间的半夜爬取信息，重点关注太平洋时间的早上7点到11点等等。

第一步完成的超级顺利，导致我自信心非常爆棚，甚至我本来以为，这个小东西，应该很快就完事了。

为此我还特别松弛的在厕所蹲坑的时候，开了一句lol手游。。。

当重新坐在电脑前，开始搜索怎么实现打电话的时候，面色越来越凝重。

这玩意，怎么这么复杂。。。

打电话，学名叫，电话呼叫服务，很多云平台其实都提供了，我第一反应也就是去阿里云腾讯云百度云火山引擎上去找。

但是才发现，几乎所有提供接口的呼叫服务都得申请，而且都需要等好几个工作日。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sAKNysQGXM8icakRc6zt3WKy02wLYzjps6j5FBGydxT7IsCLYkqLx6yA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

中所周知，我是一个急急国王，你让我等2小时行，你让我等7个工作日？

当然平台的本意估计是防止骚扰电话，但对我这种 急急国王来说，真的太不友好了。

而且需要填的资料，一大堆，还需要资质。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sKopShdSlKd11cGGAuTdNzs62MI6KiazRTfT2LQNgMrzM3tgw8nRlYzg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我这种需要自动电话叫醒服务的，估计平台都懵了。

所有平台翻了一圈，都大差不差。

就在我快要放弃的时候，刚好我们公司要开会了，我没进，他们在飞书上，给我打了个电话加急，大概就是这样的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1s5MG2wdA2WDtH6P0Do3eqvxQjeZapq55ZAicUapGE4icGl6xNXmnQkibmw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

那一刹那，我灵光一现。

打电话，也不一定非说要打系统电话吗，微信也行，飞书也行，只要能把我喊起来，管他是个什么电话，你说对吧。

微信没有API，但是飞书有开放平台。

于是我去开放平台上搜了一下，还真有。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1shaW5ibEpQuD7M4Iyny3InQ3SjQfOHfFfTp1FkwAAaiab1w3EWTHARVew/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

名字就叫，"发送电话加急"，可以通过飞书的客户端和电话进行通知，简直就是为我量身定做的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1ssmXYqjDYbp0XR3cficeUibd0pk1jCwbdV9pUM7voRDaUthRZwdiaicEAdQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

而且，这玩意儿超级良心，只要认证一下每个月就能用50次，如果开了商业版或企业版，那次数绝对够用了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sxP8qiabQgh2nB5eePTlWPSySm9UYJAwokRv4dwicunKBv8PN5V9PED8g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

用来监控奥特曼发推特，绰绰有余。

这块的构建，其实也不难，别看看这复杂，但是我保证你肯定会。

整个方案其实就三大步： 创建应用、配置权限、实现调用。

一、创建飞书自建应用

在开始之前，我们需要有一个企业自建应用，如果之前还没有创建过，可以通过下面这个页面创建一个。

操作也很简单，只用填写一下名称，描述和图标就能做一个。随便写，不用太认真，反正就自己用。

https://open.feishu.cn/app

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sR0ApbEW2jgEZicibWoZvC5Rl4LgTaYAuic0KAeUnwzH0R7jeORM4Afy3g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

进入应用后，在首页的应用凭证很重要，一会调用API的时候会用到。这个就相当于你的钥匙，没有它，飞书不认识你是谁。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1saCT86nBMM7sreMUU6p8mKroZybmI83MaTLarZlekLCiawHdAoUCWMqw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

二、配置必要权限

然后要给它加上"机器人"的应用能力，这个能力就能让它实现发送消息。没有机器人能力，这个应用就干不了相关的工作。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sELYyZ282SN9wCYIbZeDxRWW38HH4fbQRwFN3SU0MzFuqCIl3ZIvscQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着在权限管理页面，还要给它开通以下的权限，它才能给我们发送消息，拨打电话等。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sMgWYjwXopr51L8t8IiaG4vkuyj8tAgibWeUGB8ZiaO4dNyMrd7xJLTlJw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

最后点击顶部的创建版本，在可用范围设置需要接收消息的人员，我这边设置的是所有员工（虽然就给我一个人打电话）。

最后点一下保存，应用这边的设置就完成啦。就这么简单，是不是没想到？

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sxIEUWkJMWnaRMYaf8k4GLU1oLCNPk7pVduQDVr6DKkcibehwibMqfZxQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

三、 实现电话通知功能

接着打开发送电话加急的界面，界面很清爽，左边是接口的文档，右边是可以测试API的控制台，对于像我这样的代码小白来说简直不要太友好。

https://open.feishu.cn/document/server-docs/im-v1/buzz-messages/urgent\_phone?appId=cli\_a775236edef8500d

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sHdhmKxniaCx1KQfQGL2o2BFI2Ab3TQ392wNuSWTsCqEBunyVF8H2w2g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

但现在还不能给我打电话，因为我还没有message\_id的信息，要先从左边文档的路径参数里，切换到发送消息，发完信息后就能获取到对应信息的id。

比如我发了一条"奥特曼发推特了"，飞书立刻弹出了对应的消息，这时我们在测试结果里就能看到这条消息的id，复制备用。

记得保存好，丢了就得重来。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1s67Xm1nZPg4FttjRLbPNwwO9glpDepYvSVbicaGLHsCQH5emph5kFKkA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1) ![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sXib68s7g6VwwNY106u4Tht0HicFzbGWqQbaBTMYhIz5bz1HOiaz94jGnQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后回到刚刚的呼叫页面，填写刚刚的信息id。把用户id的类型改成user\_id，通过飞书提供的快速复制功能，就能复制出自己的id。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1s2z5vu0HDbjNOj6Uv9y88M8XaGKEmeE8f3ZuA9OmR02LEGEt5Kgn79w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

最后点击开始调试，就可以收到来自飞书的电话了，记得给飞书的号码加个白名单，因为很容易被标记为 骚扰电话。。。

我试了下，这只能打一次电话，不能做到一直打，直到我醒来。

我有的时候睡觉比较死，一个电话打不醒。。。

所以我又翻了半天，没在这个加急电话的页面找到返回接听电话的地方。于是我再次求助飞书文档搜索。

然后，看到了一个有趣的东西，消息已读。

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sibSTV1q7MRDt4ODVib6jF1icb5BrAjRzeIWoYCDLETg6d88go0PPvtFTQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这就是现成的解决方案嘛。

刚刚就是发了一条消息，然后可以通过消息是否已读，来实现检测我是否醒了，只要消息还是未读，就一直给我打电话，直到我被烦醒为止。

完美的方案。

通过把这些接口还有之前的推文检测功能整合在一起，经过一番调试，大功告成！

![图片](https://mmbiz.qpic.cn/mmbiz_png/OjgKEXmLURpIicXtndhAKofJf05WYmO1sQuJwX2wUsVZJKS4tHibuOzic9THnUEP9efGRpIQzag9heehLH5JHB1ibg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这样我就拥有了能在半夜叫我起床看奥特曼推文的智能闹钟。

而且这还不是普通闹钟，我还加上了AI翻译和判断内容是否和AI有关的功能。

毕竟总不能半夜被叫醒，结果就是看奥特曼在那晒娃吧，那我绝对会把它挂在电风扇上转着圈打。

这两天也不断有身边的朋友问我，有没有什么方法能及时看到一些的最新动态。

过往，我做过Discord监控，做过AI总结，做过RSS订阅等等。

但是却一直没有解决，提醒太弱的问题。

那现在，终于可以让我睡个好觉了。

人类的需求，总是从想睡好觉，想偷个懒开始。

需求即产品。

实现需求的路径，会越来越多元化。

相信未来，类似的自动化工具会越来越多，让我们不再需要靠干熬来等第一手信息。

好啦，教程也说完了。

剩下的。

就交给你自己去折腾了。

******以上，既然看到这里了，如果觉得不错，随手点个赞、在看、转发三连吧，如果想第一时间收到推送，也可以给我个星标⭐～谢谢你看我的文章，我们，下次再见。******

\>/ 作者：卡兹克、dongyi

\>/ 投稿或爆料，请联系邮箱： wzglyay@virxact.com

![](https://mmbiz.qlogo.cn/mmbiz_jpg/FpebDiaL1hZ6VyrXAqGwZibiaianZXowOzv3zDn2SP6DufLvxHkIjiaX8udYWqCml7QpA3TItQs0yo765TzTY383VZw/0?wx_fmt=jpeg)

谢谢你看我的文章

 [喜欢作者](https://mp.weixin.qq.com/s/)

有手就行 16

继续滑动看下一个

数字生命卡兹克

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功