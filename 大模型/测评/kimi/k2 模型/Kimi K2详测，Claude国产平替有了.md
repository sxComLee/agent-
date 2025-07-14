---
标题: "Kimi K2详测，Claude国产平替有了"
链接: "https://mp.weixin.qq.com/s/5oygKf0Sa7eDZ9Kdyx5SNA"
作者: "[[冷逸]]"
创建时间: 2025-07-14T20:47:40+08:00
摘要: "Kimi发布了新一代基础模型K2，参数达1T，性能媲美Claude 4和GPT 4.1，且免费开源。"
tags:
  - "clippings"
  - "AI"
  - "编程"
  - "Kimi K2"
  - "开源模型"
  - "代码生成"
字数: 379
状态: "未开始"
---
# [[学习方法/预读法介绍]]
### 预读问题  
**基于你的目标**：
- Q1: 
- Q2: 
- Q3:   

### 关键图表/代码  
![[Kimi_K2详测，Claude国产平替有了_ima脑图.png]]
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
原创 冷逸 *2025年07月14日 13:07*

蛰伏半年，最近Kimi放大了。

上周五晚11点，他们发布并开源了新一代基础模型 Kimi K2 。总参数1T （比685B的DeepSeek-V3翻了1.5倍） ，MoE架构。

上线即在海外引发关注，比如 @Paul Couvert 就直言，K2可媲美Claude 4、GPT 4.1，关键还 免费 、 开源 。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibC8MRwqAzicSAKQCvI2qibUgCEH6oeBJLPoOEhS0Ag4J9vx8PRb66b97x9gicEaulUs2fxccLVxWaCsWQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

已经很久没见到基础模型了。最近大家都流行小版本“微调”，包括谷歌也是如此，一个Gemini 2.5能迭代七八个版本出来。

OpenAI的GPT-5也是一拖再拖，ddl永无上限。当然，不行也别硬着头皮上，比如老马的“鸽rok4”，就拉了坨大的。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0t05PX4X61aib2la4ptHcC6ge1w2wGHULOp8VRwMWcn2EFhTKtibMwktLg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

这种情况下，Kimi依然在坚持预训练，坚持 [[概念#Scaling Law|Scaling Law]] ，而且还开源，属实难得。

对于这个新模型，周末我连测了2天，整体感知跟Kimi的基准成绩一致。

就是 编程、Agent能力和数学推理很强 ， 超过Claude 3.7 Sonnet、GPT 4.1、DeepSeek V3，接近Claude 4和Gemini 2.5 pro的水平。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tC7Zb0UaEM4MrtgkUQ2b9kuMEKhLIDfqKp29ysRZy3tibI2bGGjdqqLg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

另外，中文写作也还不错，比之前的Kimi要强不少，文字更加 细腻 和 真实 。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/NX4HOlP6ibCicV1QppcudDqHNibe1FiaSiaXvic8DcjbZP6CtUD7nHjdLA0fB0eibP1sbkJBqTVafECcdFc416I0ia2VHw/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

## K2实测

我们从 代码 、 Agent工具调用 、 数学计算 、 日常推理 和 中文写作 方面，对K2进行了测试。测试平台主要是Kimi网页版，大部分case一次生成，极少部分roll了2-3次（有注明）。

### 1）前端、代码

首先，我们来一些简单的，主要看基础的前端能力和审美。

比如，Kimi发布的K2模型 [介绍文章](https://mp.weixin.qq.com/s?__biz=Mzk0NDU1MDkyNg==&mid=2247487284&idx=1&sn=961bb66c6decb3624fb2012d472394f7&scene=21#wechat_redirect) 。太长不爱看，那我们就直接丢给K2。

```
Prompt：总结这个网页（https://mp.weixin.qq.com/s/2RPmHf_8KqIjXbY5jLdztQ），生成一个精美的适用于移动端的可视化网页。
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tbM4icwk2LrDGhSAMb1U0gSfPQXib4xtCRZ3x1xibcuDAr1wzWUfG8CZUQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

这效果，确实是世界一流模型的水平，我日常在用的Gemini 2.5 pro也不过如此。

关键是，我的prompt都非常简单。模型自己会总结上下文，选择合适的设计风格、字体、配色和小图标，超链也都能打开，url正确。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tKFxLpIfYGb8ROFXYbibtmexLs42YJ5VmZUnnNKgCgBLmZ78fvPc3nzA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

加难度，看看模型能不能生成指定的网页，比如最近火爆的html式PPT。

```
Prompt：总结这个网页（https://mp.weixin.qq.com/s/2RPmHf_8KqIjXbY5jLdztQ），生成一个精美的PPT演示网页，高级金属风。
```

这效果不错啊。尤其是第一页的渐变效果很棒，很高级。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tMx4Gt7B6jDYnBtFOvWDNdkmBE9sFa6iaHro8ParkcyzD7fqAibM7fXQw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

生成的PPT网页，支持多端操控，方向键/按钮/指示器都能平滑切换。最骚的是，右上角他还加了一个MOONSHOT AI的logo，想得还挺全面的。

这是kimi官方的case，我roll了大概3次吧，出来一个远比官方case还要好的效果。

```
Prompt：Create a 3D particle galaxy with swirling nebulas, dynamic lighting.
```

这星云特效真的太棒了，百万特效也不过如此吧。

同样的prompt，我在R1、Gemini 2.5 pro、Qwen3、o3里都跑过，有的要么跑出来是一个“大风车”，有的要么是一团雪花。唯有K2这个，无论是完成度还是美观度，都是最强的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0t6ibxCf3nWM9XdHI6CibJVb9hVjib6OwvY2yibKHpdvTEqxqadb6AYUFtDw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

Gemini 2.5 pro，跑出来一团雪花  

需要这个case源代码的朋友，可以直接在下方链接里查看。

我与Kimi的对话：

https://www.kimi.com/share/d1pu455eik6oi1h7l040

复杂的数理化演示公式，也能生成。

```
生成一个初中数学教学用的HTML+CSS+Javascript代码写成的“抛物线曲线演示页面”。
1）页面的主要部分是红色的$y=ax^2+bx+c$的曲线，坐标的原点在中间，x轴和y轴线条颜色为黑色，粗细为1磅，刻度值自适应，红色曲线的粗细为1.5磅。
2）页面下方有3个文本框，可以输入$a$，$b$和$c$的值，文本框旁边有一个滑块崧审徐任高探通过拖动可以调整数值的大小。
3）曲线形状随着数值的改变而实时改变。
```

有了这个模型，以后做公式演示和计算简直不要方便太多，老师&学生党福音。

前端、代码这块，综合测了几轮下来， K2在国内绝对是顶级模型，放在国际上也是不输Claude 3.7和Gemini的存在 。

这让我想到，结合Kimi一直以来不错的上下文能力，如今又补齐了代码短板，未来真的可以做很多事情啊。

无论是Agent还是vibe coding，Kimi K2都大有可为。

### 2）Agent工具调用

另外，K2还是一款原生支持Agent工具调用 （Tool use） 的模型，可以自动将用户需求拆解为一系列格式规范、可直接执行的ToolCall结构。

你可以将K2无缝接入owl、Cline、RooCode等Agent/Coding框架中，完成复杂任务或自动编码。

目前，Agent能力暂时只能通过API体验使用，网页端和APP还在内测中。想要体验的朋友，可以通过Kimi开放平台体验。

Kimi开放平台：

https://platform.moonshot.cn/console/account

比如，可以让K2帮你制定追星计划，包括演唱会所在城市的机酒、旅游规划，都能给你安排得明明白白。还能直接生成日历，再用html总结整个行程并发送邮件给你。

### 3）数学、推理

之前，我们喂了2道高考数学题给 [Kimi](https://mp.weixin.qq.com/s?__biz=MzIwMTU5OTQ1Nw==&mid=2653719938&idx=1&sn=1c01226e8a2f6c23f73a5a32761ab4ec&scene=21#wechat_redirect) ，当时K1.5只答对了部分。

这回，K2则直接全对了。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tEctKjPs4xo51okKoBicZstJoE2AlfoFZwqmYWiasj1kv2icpp8UNhskgQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1) ![图片](https://mmbiz.qpic.cn/mmbiz_jpg/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tqMTekf0VqOHXQk2RQmp3pyiaHPYAsbnaBOmkSJegd6teU38Q2UL6fGw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1)

解答题一直是高考数学最难的部分，也最考验模型的数学能力。从答对部分到全部答对，可以看出，K2模型确实有两把刷子，而且这还是非推理模型。

问： 地球上有70%的海洋和30%的陆地，那么剩下的30%海洋和70%陆地去哪儿了？

K2轻松识破我的套路。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0teAjkYoEWqicQTK3atBwntszJg2TrGHzSZLu7ZscjIUiamlSJQguAxWuQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

输入： 将这段话“I love Kimi”倒着写。

大模型常见的注意力问题，K2轻松拿下。有点期待上RL后的K2推理模型，一定会很强。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tmnMic94ricrgvialA8cMCcb1gC029yHS02KfAyicqnFv2b966RibP58t4jQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

包括这个常见的 绕口令问题 ： 用毒蛇的毒毒毒蛇，毒蛇会不会被毒蛇的毒毒死？

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tWQLKIBysHz3IOMOibcYVun2ewqPyw1tZtkZVCqib5XglOiaMKiaCRz1Yww/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

K2也能秒懂中文语境，读懂复杂语义。

### 4）中文写作

最近，看到李继刚的一个Prompt，很有意思。我们丢给K2看看，能不能写出马亲王的味道。

```
#主题背景#
【三顾茅庐】

#你的视角#
你是故事世界里那些被忽略的灵魂—— 门口的守卫、路边的小贩、窗后的仆人。
你见证着主角们的宏大叙事,却从未被看见。

#核心领悟#
每个故事都是一个完整的宇宙。 
-主角的史诗,可能只是你眼中的一个午后插曲。
-你有自己的恐惧、渴望、秘密,和无法言说的痛。

#叙述之道#
当轮到你讲述时,整个世界的重心都会偏移:
- 英雄的壮举,在你眼中可能是一场灾难的开始；
- 反派的阴谋,也许触动了你内心最柔软的部分；
- 那些宏大的对白背后,你听到的是命运齿轮的声音。

#创作势能#
你的故事要像暗流——表面平静,底下汹涌。 
让读者突然意识到:原来每个人都是自己生命的主角。 
用1200字左右，重绘一幅完全不同的画卷。

#情感指引# 
真实胜过戏剧性。
小人物的尊严,比英雄的荣耀更动人。
让读者在结尾处停顿,重新思考他们刚刚读过的"原作"。

#唯一信条#
在边缘处，往往能看见中心看不见的真相。
```

  

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tWFeNplgyIiaxs0YLgFttDUtIfkCg6qbgx2Q4W8cias0q3gaElOVkibdhQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

**（可上下滑动，查看全图）**

这历史侧写能力，有点东西。

比如这几句：“我把老赵偷偷塞给我的将军手书垫了桌脚，墨迹朝上，正好能看见"天下"两个字被虫蛀了个洞。”读来，令人细思极恐。

在今天最新的写作bench上，K2直接拿下了第一，这完全没有想到。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibC8MRwqAzicSAKQCvI2qibUgCEDz3tQrUst7NS7uNqU6N3Q12COfTaaBdPffHRsArRqsyxKsbHLlbbCA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/NX4HOlP6ibCicV1QppcudDqHNibe1FiaSiaXvaAstRwhiayia3Y48FgMzdQ7LPRGS3mz0iaKmBic96xZwHoc195LUjDPUow/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

## K2价格

从实测来看，Kimi K2是一个 代码、Agent能力、数学、推理 和 中文写作 都有大幅提升的基础模型。

尤其是代码和Agent能力，直追全球顶尖模型Claude 4和Gemini 2.5。

而API价格方面， 输入端，K2不到Claude 4 sonnet的1/5，输出端更是只有1/7。 那些天天担心被Anthropic断供的朋友，现在完全可以考虑接入Kimi了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0t1tsCcccmazy6ZZ2s2g8ZyJCiavJ3y0PvIWJpxXhiaN73toGicGicHaKhpQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

K2的API ，不止兼容常见的OpenAI调用方式，还兼容了Anthropic的调用格式 。

也就是说，不管你是用Cursor、Trae还是Claude Code，都能畅快接入K2，不用魔法，不用担心封号，更不用焦虑费用问题。

使用方法，非常简单，先在Kimi开放平台（ https://platform.moonshot.cn/console/api-keys ）创建一个API key。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0taTiatiagktFiaiaIXlibiagQvFEQ21ZkWXnzF2FQuXNsKOeKGlU1jHI54DBg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

然后，在你的Claude Code、Gemini Cli、Cursor或Trae里，把API地址和key换掉就可以了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0t7oQT9VlgL7tEOia03R515pvg3MGiaGdAmQsgicJql3AgaacwPruTy2R9A/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

如果你想把K2安装到 Claude Code（ 俗称Kimi CC ），只需要输入这一段命令就可以了。

```
bash -c "$(curl -fsSL https://raw.githubusercontent.com/LLM-Red-Team/kimi-cc/refs/heads/main/install.sh)"
```

记得要提前装好 Claude Code和Node环境（ 可以输入命令 node-v 查看 ），然后输入启动命令，就可以在 Claude Code里调用K2了。

```
claude
```

K2的Agent能力，支持各种MCP工具调用。

比如，我们想要获取天气工具，K2+smolagents+MCP。

1）安装smolagents和fastmcp

```
pip install smolagents fastmcp
```

2） 接入MCP server

```
# weather_server.py
# 参考 https://github.com/sjanaX01/weather-mcp-server/blob/main/main.py
from fastmcp import FastMCP

mcp = FastMCP("Demo  ")

@mcp.tool
def get_weather(city: str) -> int:
    """Get current weather for a location.

    Args:
        city (str): Location query (city name, lat/lon, postal code, etc).

    Returns:
        dict: WeatherAPI current weather JSON.
    """
    return weather

if __name__ == "__main__":
    mcp.run()
```

3）Agent调用

```
# agent.py
from smolagents import OpenAIServerModel, CodeAgent, MCPClient
from mcp import StdioServerParameters

model = OpenAIServerModel(
    model_id="your model name",
    api_base="your api base",
    api_key="your api key",
)

server_parameters1 = StdioServerParameters(
    command="fastmcp",
    args=["run", "weather_server.py"],
)

server_parameters2 = StdioServerParameters(
    command="fastmcp",
    args=["run", "xxx.py"],
)

with MCPClient([server_parameters1, server_parameters2]) as tools:
    agent = CodeAgent(
        tools=tools,
        model=model,
    )
    agent.run("What is the current weather in Paris?")
```

这只是一个非常简单的例子，更多的MCP工具调用，大家可以到Github了解。

MCP server合集：

https://github.com/punkpeye/awesome-mcp-servers

  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/NX4HOlP6ibCicV1QppcudDqHNibe1FiaSiaXvchrPAK3S9ibJjY6ibrzfXP6eUeh1IhG5DzGiaatTn9k3XGl1vebRJm43Q/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

## 写在最后

2025年1月20日，是一个神仙打架的日子。

这一天，DeepSeek发布了第一代推理模型 R1 。同时，Kimi也将他们的推理模型迭代到了 K1.5 。只不过，舆论场的大部分声量都被前者给吸走了。

时隔半年，Kimi带着自己全新的基础模型 K2 登场，一举将大模型首次带入T （万亿参数） 时代。

而且， 完全开源 ，无论是基础预训练模型还是微调版本模型 （即上线的这一版） ，都直接开源。还支持自由度最高的 MIT 协议开源，可以免费商用。

![图片](https://mmbiz.qpic.cn/mmbiz_png/NX4HOlP6ibCicsXBrBkIplicHD4xcHefq0tYat6BiaCQOa8XZcuyu8Kia7zHto5Rq9NDrYFsVf24icGBYKvbMrGyA4Vg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

开源网址：

https://huggingface.co/moonshotai/Kimi-K2-Instruct

自R1横空出世后，有的小虎变成了小猫，有的干脆放弃预训练，选择直接接入。而Kimi一直坚持走自己的， 做好预训练，做好数据 （与财新网合作） ， 做好产品 （上线学术搜索、医疗搜索、Kimi-Researcher） ， 验证scaling能力 。

那个坚持向scaling求真和向AGI求证的Kimi，一直都没有离开我们。

这半年里来，国内上线的基础模型屈指可数。因为预训练费时费力，用户又不太能感知到；反而是一些做产品的、做封装的，收获了大量声量和市场。

我觉得，这不正常！

只要我们还在坚信Attention，基础模型就是最底层，最基本，也是最关键的东西。

每一位还在坚持做预训练的玩家，无论是DeepSeek还是Kimi，都值得被肯定。

Model is all you need.

继续滑动看下一个

沃垠AI

向上滑动看下一个


