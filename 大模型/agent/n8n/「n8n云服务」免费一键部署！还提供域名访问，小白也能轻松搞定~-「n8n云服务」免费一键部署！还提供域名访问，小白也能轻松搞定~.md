---
标题: "「n8n云服务」免费一键部署！还提供域名访问，小白也能轻松搞定~-「n8n云服务」免费一键部署！还提供域名访问，小白也能轻松搞定~"
链接: "https://mp.weixin.qq.com/s/O0AJL3avOtmfr_EqJh28ew"
作者: "[[袋鼠帝]]"
创建时间: "2025-04-11T10:47:51+08:00"
摘要: "文章介绍了如何通过huggingface和supabase免费一键部署n8n云服务，并支持外网https+域名访问，适合新手快速搭建AI工作流平台。"
tags:
  - "clippings"
  - "n8n"
  - "云部署"
  - "AI"
  - "开源工具"
  - "效率"
字数: "190"
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
原创 袋鼠帝 *2025年04月09日 23:42* *云南*

![图片](https://mmbiz.qpic.cn/sz_mmbiz_gif/Gp1VfqvVj8uiaut9y599AZ4F9k1uFXO0bfxLbZpIbIHFjwZ86KTlpicBt3Tvo1kNMvuDDroGkzEMmXYtg5PibkaMQ/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/UibKpBUbFicLKReXkDljWvKH0WAMsgUk0oecSnMCEJzLZrWI6n8Bpr7KGrIO99M8WzicZRpW65h8KCFDpMhreAsibw/640?tp=webp&wxfrom=5&wx_lazy=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/OwJzuwfJwufpGiaEmgibCvvibib8MZrT9NJCYtLlp6zcic77Ecz64tqgrk5urlWM4mDzZ1Xjibr0DqPGic8VSU1tD3XKg/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

点击上方 蓝字 关注我们

![图片](https://mmbiz.qpic.cn/mmbiz_png/0ZZqtBBibibI78uRxI2WdaJmxiaCDrP41TFNe01fJ8lNlxU6dZHrRTkHYE2DXElx3ibvFhTVHQNYuHde8vic8ZIqHOg/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

大家好，我是袋鼠帝，上期给大家介绍了目前我认为 最强的开源AI Workflow平台：n8n

> 最强开源AI Workflow平台
> 
> 袋鼠帝，公众号：袋鼠帝AI客栈 [狂揽75K Star！最强开源AI Workflow平台【内置1500+工具和模板】效率起飞～](https://mp.weixin.qq.com/s/ctAqu27OZFL0Fp46d4R6Eg)

经过一段时间的使用之后发现，很多App节点都需要配置： 授权重定向URL，就要求我们的n8n能通过外网访问。

甚至有些App节点 还需配置公共顶级域名和要求https访问，，，

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyvzWhnr1t5HgnW8ZibibfksIjHfe9HmHJ6komticFMicUIgko6mUDiaibiaN4w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

正常要满足上述条件，我们需要 租一台云服务器 ，然后 购买一个域名 ，还有需要 配置SSL的证书 等等...，一套流程下来 非常繁琐。

*如果只是本地部署，不能支持外网https+域名访问的话，很多App节点的功能我们是用不了的，只能算阉割版的n8n，真的很难受...*

为了 用上n8n完全体 ，我找到了一个 免费 、且 快速搞定 上面这套流程的方案， 10分钟内 就能部署 一套免费、且支持https+域名的n8n云服务。

*X的节点，Google的表格等节点配置，都需要云部署*

好了，话不多说，我们直接 开始喂饭~

*友情提示：今天的教程需要科学上网*

  

![图片](https://mmbiz.qpic.cn/mmbiz_png/fRp5p4jMuDQjdXQXUMBDtPtLS0iaiaxVKblUBecgRUn30Lv2liaIUfnwcVib2D28Om4F0LpOd4oiah0psOJlRBHqewA/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

免费一键部署n8n云服务

![图片](https://mmbiz.qpic.cn/mmbiz_png/jLdw7EZFJmIjAic1276gZeyjcsS9UMqa3VkvD2WgU11EyJAoVCSagkO3Kmia89jgusIXDficZIgTTb6ia32cibxVKgQ/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

我们采用 huggingface + supabase 的方式进行一键部署。

*咱们先操作，最后说明为什么用这套组合*

supabase是一个 云数据库平台

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tycb2VTsBTwoCtEbR1LIiaoqkuBEdG8l49ic9ohMfMiamTr5gZXO2m0HVibg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

它虽然是收费的，但是它的 免费版 所提供的资源（如下图）已经够咱们配合n8n使用了

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyClHlFHgXYdticIr99V78sP9QF3JJNfufNvygMu7q6IJx1BHRiaC34O5A/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

supabase地址：

https://supabase.com/

进入官网之后，点击左上角的 sign in 先注册一下

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyNRhzLJZlGvIsFx8RMHbk7dfJPXlwo6CWF3FAMTKsJ9v5rgKn1PWSWQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

注册成功之后会 自动跳转到创建组织页面 ，这里plan默认就是免费（free），不用动，直接点击 create organization （创建组织）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyd4efZkpMW8GIWmOEVZpXptaqe28YWxZibEpYiaLIuB99aowEPGZWgkeg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着会跳转到创建项目的页面，这里需要 设置一个数据库密码 （自行设置，最好不要有特殊符号）

region （地区）我们 选择美国 ，点击 create new project （新建项目）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyPLtnVU89glFXUgg1VmUDbAhQs6ic1hwfo60QibXnwicM7QnoUyGNzHxvQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后会跳转到下面这个页面，点击顶部的 connect （连接）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyNpHR3GT14pEryicATVHwdqR7e1PE7ibcZat6csBCdBLjwJaKqiazYqMiaw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

type这里下拉选择 SQLAlchemy

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6ty3M32Rj9ngFEfBLicMgO6Fuq1ArPIPTYg4vHgwicEoAg7DbBbfLAXJZEQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

拉到最下面（找到下图红框位置的 数据库配置 ，待会儿要用到）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyGDhqOl0A8h1RUn9gvSoxF7txOp7WIlcPRLVPadO6UzFGmBajriaY0Ew/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

紧接着我们 打开 huggingface （别名：抱抱脸）的一个 n8n地址空间：

https://huggingface.co/spaces/fuliai/ain8n

点击 右上角三个点 -> duplicate this space （复制此空间）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyOl3IpiaevmbCOxcNxRwV02dreRSf0IHibTGbOErib5pNTgyF8XxCNE0tA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

把刚刚 supabase红框里面的 数据库相关配置 复制过来（如下图）

选择 public （公开访问）：到时候会设置密码，不怕

*注意：WEBHOOK\_URL的前半段要和owner-space name一致*

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6ty06AZxBrzN9CC8uHtyzt79R1rjwk4wWTqtdFa2anZqk34aUtLCPPs2Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

配置好之后点击左下角的 duplicate space （复制空间）

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tySXicZjW0fk0TOwOsiauxJGT4PaWHdbxyWocqH8y6ZDZsJ8Thk3SpKDcQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接下来它就开始 全自动 吭哧吭哧 部署 了

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6ty4WSr4IhYkzLicF2SgiaDaRmUWRrXRCqllJ1IkhTob6zPSXB3UesWUarA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

当 container 下出现下图红框中的日志时，就代表部署成功（5分钟内）

可以看到版本也是目前 n8n最新版本：1.86.1

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyibbXdxkOtzbibN2FNwicWHtuB5d7GiaCJm0R1C4Qwo0jLiaNVqnXMqz9ibicw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

复制日志中的地址（上图最底部那个地址），在浏览器直接访问咱们刚刚云部署好的n8n~

我的n8n地址：

https://kangarookingluohm-ain8n.hf.space/

第一次访问需要 注册 一下 管理员账号

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyvrV7OBgKRN6EibGbn30KMXoFSiaHTF7MJq1dNgia4Wib0W70Bkf8OBh30w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

跟着步骤，到下图，点击send me a free license key

![图片](https://mmbiz.qpic.cn/mmbiz_png/3QzcPBL9P1DZJk2ZXx26INgme01kN6tyL3Y4QOrNOG2IOzlTTlmnlITma9nPbOic7iaLluEL4vJmdia538zAMPFGw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

到这里就全部搞定啦！

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

想回到n8n地址空间的话，也可以点击 右上角头像->用户名 ，就能看到了

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

用这套方案的原因是： huggingface的云服务资源虽然免费，但是长时间不用会停止，停止或者重启之后由于docker容器不会保存数据，就会造成数据丢失。但是搭配上 supabase的免费数据库就不一样了，数据会保存到 supabase的数据库中，即便服务停止或者重启之后也能从数据库中读取到之前保存的数据，解决了数据丢失的问题。

*即便有这层保障，但还是建议大家搭建好一个工作流后，尽量都导出一份，备份到本地（有备无患）*

好了，今天先分享到这里， 下期开始教大家怎么使用n8n。

说实话， n8n还是有一些上手难度的 ，但它的 功能非常强大 ，熟练了的话，可以 快速搭建一些复杂但实用的AI工作流 ，它还支持把生成的内容 一键导出word、Excel等格式的文件到本地 ，非常方便。

********能看到这里的都是凤毛麟角的存在！********

********如果觉得不错，随手点个赞、在看、转发三连吧~********  

********如果想第一时间收到推送，也可以给我个星标 ⭐********

********谢谢你耐心看完我的文章~********

********KG中转站新增了国产新模型：qwq-32b、hunyuan-t1、deepseek-v3-0324********

********https://kg-api.cloud/********

********星球有DeepSeek接入微信的详细教程（全新方案，更稳定）********

********![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)********

********![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)********

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过