---
标题: "-【推荐】微信公众号排版神器 + AI Prompt 技巧，应群友要求创作，耗时3小时。"
链接: "https://mp.weixin.qq.com/s/kYOQT2GvCcITZcgKKDd5zw"
作者: "[[向阳乔木]]"
创建时间: "2025-04-10T18:49:35+08:00"
摘要:
tags:
  - "clippings"
字数: "260"
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
原创 向阳乔木 *2025年02月26日 11:33* *天津*

> 字数 1556，阅读大约需 8 分钟

## 排版难影响公众号更新

很多人不愿写微信公众号，最大原因： **排版太麻烦** 。

每当想到，不仅要写完，写完还要配图，再加上排版美化，写作热情立马熄灭一半。

我年初打算好好写点 AI 工具教程，也因为上面原因，更新不多。

尝试用过一些排版工具，但都不够好用！

## NB 工具解救了我

直到上周，终于在 X 上发现 **一款叫做 Doocs 的微信公众号排版神器** 。

> 源代码： https://github.com/doocs/md <sup><span>[1]</span></sup>

不仅完全开源免费，今天仔细看了使用协议， **太TMD酷了！**

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCUosQXRolffJjkb2MibIaQgz64g8Nqh55dYEN9KvPuBt8SeSZ9VXtyc5drMIKHk7lfT2VtyNTBdAyw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

意思是，你不仅能安装到自己的电脑或服务器上。

你能任意修改，甚至去掉作者名字和Logo，二次包装卖钱都行。

我在自己服务也部署了一套，方便自用。

> https://md.qiaomu.ai/ <sup><span>[2]</span></sup>

近几天更新公众号，不少朋友觉得排版好，问怎么做的？

**原因就是上面的工具。**

如果你追求实用，看到这里就可以结束了。

直接用官网或上面网址即可，文章、配置、样式选择都在本地，别人看不到。

可以理解为，一个免费在线App，千人千面。

---

## 安装 Markdown 排版神器 Doocs

如果你想折腾，在自己电脑或服务器安装，也不难。

安装 Github 代码，以前想想都觉得头疼，现在只需要一句简单Prompt，AI 就能耐心能指导你完成。

**Prompt如下：**

```
我是电脑小白，一步步指导我如何安装
https://github.com/doocs/md
```

我帮你测试了Deepseek、豆包、腾讯混元、Grok3等国内外模型，都能给出很详尽操作步骤。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCUosQXRolffJjkb2MibIaQgz4bFl4hTBAKQHI41ws840iandbiaKaadOz616ab6iaxAIciavxlPrHPAxew/640?wx_fmt=png&from=appmsg)

尤其是 Grok3，真的很细致。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCUosQXRolffJjkb2MibIaQgzEs7G8XDqUGxz8qajaibyqDvfmibhZxxXT8krrJL2IoUsWVxf8haicMFzA/640?wx_fmt=png&from=appmsg)

工具界面如下图所示：

![产品界面标注](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCUosQXRolffJjkb2MibIaQgzBh3Xkz3BkYPLdXbNDNrqGjjjUlXmOBicv0eY4fJGXQ5EHUqu68icBW3g/640?wx_fmt=png&from=appmsg)

产品界面标注

1. 1\. 点击左侧抽屉，查看已有文章
2. 2\. 点击“新增内容”，可以创建新文章
3. 3\. 写完后点击复制，到微信公众号粘贴

## Markdown 扩展支持GFM

Doocs 编辑器有很多Markdown工具不支持的细节 Feature，比如 GFM

> GFM（GitHub Flavored Markdown) ，是 GitHub 对标准 Markdown 的扩展版本，提供了额外的格式化功能。

比如警告块、提示块等

**警告块显示效果：**

> Warning
> 
> 这是一个警告块。

**提示块显示效果：**

> Tip
> 
> 这是一个提示块

语法都是引用块加上特殊标记：

```
> [!CAUTION]
> Negative potential consequences of an action.
```

更多标记如下：  
`[!NOTE] ，[!MPORTANT] 、 [!CAUTION]`

## 简约主题模版 & 自定义

Doocs编辑器可以通过菜单，或点击右上角的齿轮设置图标，自选搭配喜欢的主题。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCUosQXRolffJjkb2MibIaQgzMUB7IVMepBNiaJpkNkuwMHEibd8sPjx7Feaic0FHibXmjmicXvfBFKfe9vg/640?wx_fmt=png&from=appmsg)

后续研究下，怎么自己定制主题风格。

理论上只需懂点CSS就可以，主要是H标题、p、ul、ol等Markdown常用标签的CSS 样式修改。

## AI 生成图表

个人觉得最酷的功能，Doocs 竟然支持 Mermaid 渲染！

> Mermaid 是一种用简单文本描述就能画出漂亮图表的神奇工具，用文本画出流程图、时序图等专业图表，堪称开发者和文档创作者的"画图神器"。

**为什么重要？**

让 AI 基于文本生成 Mermaid 代码，渲染后就是专业图。

**一图胜千言。**

例如，我的Prompt

> 生成原始Mermaid代码，含标记。  
> 解释：用户体验5要素

**Mermaid 代码如下**

```
\`\`\`mermaid
graph TB
    A[表现层<br>Surface] --> B[框架层<br>Skeleton]
    B --> C[结构层<br>Structure]
    C --> D[范围层<br>Scope]
    D --> E[战略层<br>Strategy]
    
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#bbf,stroke:#333,stroke-width:2px
    style C fill:#dfd,stroke:#333,stroke-width:2px
    style D fill:#ffd,stroke:#333,stroke-width:2px
    style E fill:#fdb,stroke:#333,stroke-width:2px
    
    %% 添加说明
    A1[感知设计：视觉、听觉等] --> A
    B1[界面设计：导航、按钮布局] --> B
    C1[交互设计：信息架构] --> C
    D1[功能规格：特性和功能] --> D
    E1[用户需求和商业目标] --> E
```

**渲染效果**

## 如何插入GIF图

有朋友问，如何录屏生成GIF动图，插入微信公众号。

**用什么工具？**

飞书按快捷键 `Shift + Option + R` ，就会出现截屏、录屏，选录屏->GIF ，还能控制是否显示鼠标。

![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCUosQXRolffJjkb2MibIaQgzjYFRSCUialJavNEgyIrRAiaCvPQ3fDFOicayqicWdAXmF53ibPSNuJALrqA/640?wx_fmt=png&from=appmsg)

**效果演示如下：**

![图片](https://mmbiz.qpic.cn/mmbiz_gif/jibL99tg2bCUosQXRolffJjkb2MibIaQgzShia1YATTnlQtQmRW8WeeOHK5kVDic1fJNIQPsl8CtLdJcPibVLYeFFVA/640?wx_fmt=gif&from=appmsg)

## 配置图床

Doocs 提供了国内外各种图床配置。  
![图片](https://mmbiz.qpic.cn/mmbiz_png/jibL99tg2bCUosQXRolffJjkb2MibIaQgzwpXr1fgg8ZyIzywMxNLTlmgs7RVkc4b9EGHkyCE9adQOLEo6mCM90g/640?wx_fmt=png&from=appmsg)

有付费（七牛、阿里云等），也有免费服务（Github、 Cloudflare R2），根据自己需要选择就行。

**好处：** 粘贴图片，自动上传，转成Markdown图片引用，你只需要专心写作，其他事不用操心。

当复制到微信时，又会把这些图片同步，非常方便。

Cloudflare R2配置，推荐下面教程：

> 基于Cloudflare R2搭建零成本图床，配合免费CDN  
> https://post.smzdm.com/p/al8xzkke/ <sup><span>[3]</span></sup>

配置有点复杂，小白不推荐。

## 总结

不知不觉写了 3 个小时，坐着有点累。

但是，觉得这篇文章很值的写。

一方面，希望通过这篇文章让更多朋友降低对公众号写作的顾虑和障碍。

另一方面，正如知名投资人纳瓦尔所说： **媒体杠杆和代码杠杆，不需要任何人许可就能用，是21世纪新财富密码。**

而我还想补充最后一点：

工业革命后，物质极大丰富，人不怎么运动，最后锻炼成了少数人的爱好或不得不做的事情。

AI 时代，仿佛智力平权了。

实际上， **预测未来多数人会把思考决策权，轻易让渡给 AI，不再思考，包括你，包括我。**

未来阶层分化会更严重。

**写作，是对抗这种趋势的一种“脑力锻炼”。**

虽然痛苦，但不得不做。

好了，不说教了。

如果感觉有帮助，欢迎打赏，或转发到朋友圈，提前拜谢了。

公众号关注地址：

#### 引用链接

`[1]` https://github.com/doocs/md:  
`[2]` https://md.qiaomu.ai/:  
`[3]` https://post.smzdm.com/p/al8xzkke/:  

向阳乔木

干货满满，一杯咖啡的鼓励！

 **微信扫一扫赞赏作者**

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过