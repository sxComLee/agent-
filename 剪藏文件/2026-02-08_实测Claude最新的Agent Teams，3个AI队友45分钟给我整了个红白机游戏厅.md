---
标题: "实测Claude最新的Agent Teams，3个AI队友45分钟给我整了个红白机游戏厅"
链接: "https://mp.weixin.qq.com/s/ICUqmkbfQhtVtsQYzyIUQw"
作者: "[[花叔]]"
阅读星级: 3
内容类型: "经验分享"
创建时间: 2026-02-08T12:20:09.737Z
摘要: |
  作者利用Claude Opus 4.6的Agent Teams功能，在45分钟内创建了一个包含133款经典红白机游戏的在线游戏厅网站，展示了AI团队协作在小型项目开发中的高效潜力。
tags:
  - "AI协作"
  - "Claude Opus"
  - "Agent Teams"
  - "红白机游戏"
  - "快速开发"
字数: 6086
状态: "未开始"
总结: |
  本文详细介绍了作者使用Claude Opus 4.6的Agent Teams功能快速开发一个在线红白机游戏厅网站的过程。关键要点包括：
  1. **项目背景**：作者受Anthropic官方案例（如16个AI并行构建C编译器）启发，测试Agent Teams在小型项目中的应用。
  2. **实施过程**：通过一句话指令创建3个AI队友分工协作：
     - emulator-dev：负责模拟器核心引擎（基于jsnes库）。
     - ui-dev：负责前端界面设计（复古风格、CRT效果）。
     - data-dev：负责游戏数据库整理（133款游戏元数据）。
  3. **成果**：45分钟内完成4700多行代码的项目，支持游戏运行、分类搜索、双人模式等功能，已部署到GitHub和在线体验。
  4. **观察与反思**：
     - 3个队友是最佳数量，避免文件冲突和协调开销。
     - 分工需确保任务无依赖，以实现并行高效。
     - 成本较高（Token消耗约7倍），适合从零开始的完整项目。
     - AI选择jsnes库体现了实用性和效率。
  5. **意义**：Agent Teams将AI协作产品化，从“vibe coding”升级到“vibe working”，强调项目管理能力（如任务拆分）是关键。
---

# [[实测Claude最新的Agent Teams，3个AI队友45分钟给我整了个红白机游戏厅]]
### 预读问题
**基于你的目标**：
- Q1:
- Q2:
- Q3:

### 关键图表/代码
![[提取的图表或代码片段]]
### 初步关联
- 已知：[[已掌握的相关热识]]
- 未知：`#\u5f85\u63a2\u7d22`

### 输出目标
- [ ]

# 内容
#flashcards

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/aNEfzwzDSWibtiabNjzMPaO97RNrOXwV3VFtUd7PtGmXJh7EIXibXKKjEb5XyiakRDgejJRHMJMIr2TFIdVGRXicNpMunG4LY9gMsvrtuHiaDRUJ4/640?wx_fmt=png&from=appmsg)

这是一个在线红白机游戏厅。133款经典游戏，直接在浏览器里就能玩。魂斗罗、超级马里奥、俄罗斯方块、塞尔达、双截龙......全都有。有封面、有分类、有搜索，打开就能玩，还带CRT老电视的扫描线效果。

这个网站从零到完成，花了45分钟。

不是我一个人做的——我开了3个AI队友，一起搞的。

昨天Claude发了新的旗舰模型Opus 4.6，OpenAI也几乎同时发了GPT-5.3 Codex，两家只隔了20分钟。模型层面的对比我就不展开了——100万Token上下文、ARC AGI 2翻倍、自适应思考这些，估计你在各家评测号都看过了。

![Benchmark table comparing Opus 4.6 to other models](https://mmbiz.qpic.cn/mmbiz_jpg/aNEfzwzDSW9roYckMRuRlHZaOctVzpicEXZBlkydyv7javCYkUBhGDWaKfa5Jf5xwRxwhX87fxcCYMLicMfKEN6Jm3waOhsIIO76DNECIwyibg/640?wx_fmt=other&from=appmsg)

但我盯上的是Opus 4.6里一个叫Agent Teams的新功能。简单说就是，AI不再是一个人给你干活了，它可以组队。

所以我特意做了个包含多个模块开发配合的实验。
## Anthropic自己的案例有多夸张

在说我自己的实验之前，得先聊聊Anthropic官方给的案例。因为看完那个，我才动了心思。

他们工程团队发了一篇博客，标题是「Building a C compiler with a team of parallel Claudes」。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aNEfzwzDSWicoEvVB6JUTa5UWn0MBu5vVENPo1yxNag6oicLqO3Uk0zjFAJtFUKIg6zRHTOrq0UZtviagMjJkjP1fAqSPticmvF6eMLnePk4Keo/640?wx_fmt=png&from=appmsg)

用16个Claude实例并行工作，花了大约两周，跑了差不多2000次Claude Code会话，烧了大约2万美元。

产出？一个10万行Rust代码的C编译器。

这个编译器能干什么？能编译Linux 6.9内核（x86、ARM、RISC-V三个架构都支持）。能编译QEMU、FFmpeg、SQLite、PostgreSQL、Redis。GCC的torture test通过率99%。

甚至能编译并运行Doom。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/aNEfzwzDSW8obCSPQ8fmicaAnibLkKCXRDeRVMsTkvQP4wxkEtGPiaLiaokLhTP2LgvYEaqA0ibFnqzicLtcPias6ic5nicGiawsmyYnfj3QdWmhhkSgk/640?wx_fmt=png&from=appmsg)

说实话，看到这个案例的时候我愣了一下。

让我愣住的不是结果——10万行代码的编译器，厉害，但也就是「厉害」。让我愣住的是方法。16个AI各管一摊，通过文件锁同步代码，通过git协调版本，各自认领任务、完成、提交。

你品一下。

其实开多个Claude Code窗口去搞多个项目，或者同时设计一个项目的多个模块没啥奇怪的，我之前也整天这么干了。但在Agent Teams这个概念里，多个Agent之间会相互协调配合，分别去处理不同的任务，然后再组合和测试，这点让我觉得很有趣。

相当于人类不需要再成为AI写代码速度的瓶颈了，AI已经能自己踩着自己往上飞了...
## 我想试试：45分钟能做什么

16个Agent、2万美元、两周，这是大工程的玩法，我是没法为了测试去搞这么久，我没这耐心，两周后天知道又有什么模型出来了。

但我想知道的是，普通人拿这功能做个小东西，到底行不行？速度是不是真的能更快。

选什么项目呢？

我想到一个事。之前做小猫补光灯App的时候，为了藏一个开发者模式入口，我用了红白机游戏里经典的作弊码方式——在设置页面用特定顺序点开关来激活。当时还在即刻发了一条：「玩过红白机游戏的都不陌生，就是通过左左右右BABA之类的特殊按钮方式调出开发者模式。」

那不如就做个红白机游戏的网站吧。一个在线的FC游戏厅，能直接在浏览器里玩那些经典游戏。

要求也简单：至少100个能直接运行的游戏，有封面，有分类，界面要好看。
## 一句话分工

打开Claude Code，先开启Agent Teams功能（目前是实验性功能，需要在settings.json里手动打开），然后我就说了一句话：

> 创建一个团队，3个teammate并行完成以下任务，建一个红白机游戏的导航站，上面有丰富完整的红白机游戏功能，至少包含100个可直接运行的游戏。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aNEfzwzDSWicACFKYzM1HRfic5t7OiaDLVytalM9oNb9pfzceznqd5z7FPhS9jfxWvH7eKqycGdltcTLzRBibWXon94AicmyicCFsKmW9ZYoCarbw/640?wx_fmt=png&from=appmsg)

Claude想了一下，给我解释了为什么不建议用太多队友：

文件冲突——人太多容易互相覆盖代码。协调开销——队友越多，沟通成本越高。Token消耗——每个队友都是独立的Claude实例，10个就是10倍成本。

它建议3个。我觉得合理。

然后它自动创建了3个队友：

- emulator-dev：负责模拟器核心引擎——封装jsnes库，处理60fps画面渲染、Web Audio音频输出、键盘输入映射
- ui-dev：负责整个前端界面——HTML骨架、CSS样式、游戏卡片网格、搜索、分类筛选、播放器弹窗
- data-dev：负责游戏数据库——整理100+款游戏的元数据，包括中英文名、年份、分类、评分、ROM文件名

![图片](https://mmbiz.qpic.cn/mmbiz_png/aNEfzwzDSWibo6XFcFskL2FuFnb6Kqm3EfCPhRTicC89IqZgL15D75CibRiaUTT71ODZPR8luq44ZgHJkNydEesg1diaGIVoS8Dkzphco64Ricdso/640?wx_fmt=png&from=appmsg)

这三块互相不挨着。模拟器不用管有多少游戏，游戏数据不用管模拟器咋工作的，界面只管调接口就行。

然后三个队友就各干各的了。我在旁边看着。
## 三个队友各自干了什么### emulator-dev：模拟器工程师

这个队友把jsnes这个JavaScript NES模拟器库包了一层TypeScript。

核心做了几件事：

一个NesEmulator类，管游戏的生命周期——loadRom、start、pause、reset、stop。画面渲染用requestAnimationFrame跑60fps，把NES原生的256x240像素逐帧写到Canvas上。

音频用Web Audio API实现。采样率44100Hz，用ScriptProcessorNode处理音频缓冲。虽然ScriptProcessorNode已经被标记为deprecated了，但它兼容性最好，这个选择挺务实的。

键盘输入做了防冲突处理。玩过网页游戏的都知道，方向键会让页面滚动，Enter会触发按钮点击，Tab会切焦点。它把这些按键全拦截了，还做了双人游戏的按键映射——玩家1用方向键+ZX，玩家2用WASD+GH。
### ui-dev：前端设计师

这个队友做的界面我确实没想到会这么好看。

整体是暗黑主题加NES经典红色（#e60012），有一种复古街机的感觉。

几个让我印象深刻的细节：

CRT电视开机动画——打开游戏的时候，画面会模拟老式电视机的开机过程，先是一条水平亮线，然后逐渐展开成完整画面。

扫描线效果，用CSS实现的，1px宽的半透明黑色条纹反复叠加，看起来真的就像老电视。画面四周还有边缘晕映，微微变暗，模拟CRT显示器的那种感觉。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/aNEfzwzDSWicqKyfib585MibfEicvmXeObo1TXBgc5k3mqWMIMicnDL14yG7hsgiciaLTLbxIWFTDlSV2ibweJgnaLzysHZssIC1STobCR1JT5tFibA0/640?wx_fmt=png&from=appmsg)

[图片：游戏卡片细节截图，展示悬停发光效果]

游戏卡片做成了仿NES卡带的样式。顶部有一条红色边纹，悬停的时候会发光。封面是4:3的比例，没有封面的游戏会显示一个大字母缩写加分类标签作为占位。

搜索支持中英文模糊匹配。分类有12种——动作、冒险、RPG、益智、体育、射击、平台、格斗、赛车、策略、模拟、经典。

全屏模式也做了。ESC退出。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/aNEfzwzDSW8nHruhlUlqqRT4iaFV9hebL1gHZwWw3icUlRBCQP9WER3yTb9KSbafkbsBGNQBccQxLJ7pib6B5OEgs84kqSjEIAMiaJL33sfSJ9w/640?wx_fmt=png&from=appmsg)
### data-dev：数据库管理员

这个队友整理了133款游戏的完整数据。每款游戏都有英文名、中文名、发行年份、分类、描述、玩家人数、ROM文件名、评分。

游戏列表挺全的。超级马里奥三代、魂斗罗、俄罗斯方块、塞尔达传说、银河战士、勇者斗恶龙系列、洛克人系列、忍者龙剑传、双截龙、热血系列、三国志系列......

133款，覆盖12个分类，每个分类至少5款。

同时还给127款游戏配了真实的盒装封面图，从libretro的CDN上拉的。只有6款没找到封面。
## 最后的效果

45分钟。

Vite + TypeScript + jsnes，133款可直接运行的NES游戏，127张官方游戏封面，CRT电视模拟效果，12种分类筛选，中英文搜索，双人游戏支持，全屏模式，响应式布局。

总共4700多行代码，188MB项目文件（主要是ROM和封面图片）。

已经推到了GitHub：github.com/alchaincyf/nes-arcade

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/aNEfzwzDSWicoib2xNKgUyWuibvtwV8ZKmYrKPWAfkmuweian4QO00AnGPPjvyhl6ug98G06YMZ6CFVUGJEq34gtRSW9YRbTeVo1ibEyH3qWpGps/640?wx_fmt=png&from=appmsg)

如果让我一个人从零做这个，不用AI，天知道要多久了，我真写不了。

用单个Claude Code会话做，可能也要2-3小时——因为任务之间有先后，模拟器做完才能做界面集成，数据整理好才能测试。

Agent Teams的好处就在这——三个队友同时干，谁也不用等谁。最后代码合到一起也没出什么问题，除了要求了几次在用户体验上再优化优化，实际部署的bug是一次没出现过。
## 一些观察

用完这一次，有几个感受。

第一，3个队友确实是这种规模项目的最佳数量。

Claude自己也解释了为什么不用更多——文件冲突、协调开销、Token消耗都会随人数线性增长。3个队友各管一摊，互不干扰，是最高效的配置。Anthropic那个16人写编译器的项目，是因为编译器本身就是一个巨大的工程，需要那么多并行的工作面。

第二，分工的关键是「无依赖」。

模拟器引擎、前端界面、游戏数据——这三个方向天然就不挨着。如果我让一个做前端、一个做后端、一个做测试，后两个就得干等着。所以拆任务的时候得想清楚，让它们能同时跑起来。

第三，成本确实高。

Agent Teams的Token消耗大约是普通会话的7倍。这个项目跑下来，Token用量不少。对于日常的小修小补，还是单会话更划算。Agent Teams适合的是「从零开始做一个完整项目」这种场景。

第四，AI选择jsnes作为模拟器是个挺聪明的决定。

我没指定用什么技术栈，只说了「红白机游戏导航站」。emulator-dev自己选了jsnes——一个纯JavaScript的NES模拟器，API简洁，社区成熟，TypeScript类型声明可以自己补。如果换成更复杂的模拟器方案，45分钟大概率搞不定。实际体感非常丝滑，我还特意上网查了查相似的模拟器游戏网站，真没见过比我这加载速度快的。
## 从一个人写代码到带队写代码

其实这个玩法并不新。去年就有人手动开好几个Claude Code窗口，一个窗口一个任务，人肉版Agent Teams。

Agent Teams把这件事产品化了。你不用手动开窗口、手动分任务、手动合代码。一句「建一个团队，做这件事」就够了。

Anthropic的一个产品负责人Scott White在发布会上说了句挺有意思的话：「We are now transitioning almost into vibe working.」

Vibe coding大家都知道了——你对AI说「帮我写这个功能」。Vibe working更进一步，你对一个AI团队说「帮我把这个项目做了」。

今天这45分钟，我确实感受到了这个区别。

不过有一点，能不能用好这个功能，关键其实不在编程能力，在于你能不能把一个大活拆成几个互不干扰的小活。说白了是项目管理的能力。

话说回来，上上下下左右左右BA，调出的不是30条命，是一个AI团队。

如果你想看看我这个网站究竟咋样的话，欢迎通过下面的链接体验👇

https://nes.bookai.top/
