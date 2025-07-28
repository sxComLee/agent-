---
标题: "拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！"
链接: "https://mp.weixin.qq.com/s/civ-Irrz4xiW2PXNj2aHhA"
作者: "[[J0hn]]"
创建时间: 2025-07-28T10:23:39+08:00
摘要: "微软发布GitHub Spark，一款能用自然语言一键生成全栈应用的AI工具。"
tags:
  - "clippings"
  - "AI"
  - "编程"
  - "GitHub Spark"
  - "微软"
  - "全栈开发"
字数: 439
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
原创 J0hn *2025年07月24日 09:31*

****刚刚，** 微软放出了一个可能让所有人都要坐不住的大招！**

GitHub Spark 正式发布，这个全新的 AI 工具能让你用自然语言直接生成全栈应用程序，然后一键部署上线。

微软 CEO Satya Nadella (@satyanadella) 亲自站台宣布：

> 今天我们发布了 GitHub Spark——Copilot 中的一个新工具，可以完全用自然语言将你的想法变成全栈应用。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/c30430de74ab68c5254fcb31054d26d7_MD5.webp]]

简单来说，你只需要描述你想要什么，Spark 就能自动生成一个完整的应用程序，包括前端、后端、数据库，甚至 AI 功能。

值得注意的是， **这个工具默认使用的居然不是自家的 GPT，而是 Claude Sonnet 4.**

## 微应用理念

GitHub Spark 遵循 Unix 哲学—— **软件可以专注于做好一件事** 。

这里的「微」不是指应用价值的大小，而是指功能复杂度的规模。

这些微应用可以是：

- 儿童零用钱追踪器，支持只读或读写模式共享，使用 LLM 在达到收入目标时生成庆祝消息
![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/8eca313f75894eb273c36891bc5024b4_MD5.webp]]

- 六岁孩子设想并创建的动画车辆世界
![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/33a5b4543e1bb284b06f1e9e6aa857c5_MD5.webp]]

- 每周卡拉 OK 之夜的追踪应用，显示每位受邀客人的状态
![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/17d71ae3406805c190a37bdad88cb82a_MD5.webp]]

- 允许按名称搜索城市的地图应用，使用 LLM 生成有趣的简介
![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/f93e116e851ceb3511587c95b73b26ab_MD5.webp]]

## 强大功能体系

根据 GitHub 的详细介绍，Spark 通过三个紧密集成的组件实现其功能：

### 1\. 基于自然语言的工具链

**交互式预览**

当你输入自然语言表达时，Spark 不仅生成代码，还会立即运行并通过交互式预览显示。这种「以应用为中心的反馈循环」让你可以指定尽可能少或尽可能多的细节，然后在视觉学习中迭代。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/5cf4c97305f8f6bfd74464947fe76e81_MD5.webp]]

**修订变体**

创建或迭代 spark 时，可以选择请求一组变体。这将生成 3-6 个不同版本的请求，每个都有细微但有意义的差异。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/a332862b45ec939017047405aa8fcfa8_MD5.webp]]

**自动历史记录**

每次修订都会自动保存，可以一键恢复。这种「好奇心驱动的开发」让你可以有想法就尝试，而不用担心负面后果。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/fda54870ac9d5f130a147c328ba9b676_MD5.webp]]

**模型选择**

创建或修订 spark 时，可以从四个 AI 模型中选择：Claude Sonnet 3.5、GPT-4o、o1-preview 和 o1-mini。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/1b9871b21908b9763ed5cee58a4b762f_MD5.webp]]

### 2\. 托管运行时环境

Spark 被称为「以应用为中心」的工具（而非「以代码为中心」），因为它设计用于创建要被看到、感受和使用的应用，而不是简单地生成代码。

**无部署托管** ：创建或修订 spark 时，更改会自动部署，可以在桌面、平板或移动设备上运行和安装（通过 PWA）。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/7117c3abb759db8a5087231d972386f7_MD5.webp]]

**可主题化的设计系统** ：确保应用看起来美观，包含一组内置 UI 组件和可主题化的设计系统。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/72ef2c21f57a4195da9a1bc468491fbb_MD5.webp]]

**持久数据存储** ：提供托管的键值存储，并自动知道何时使用它。还提供数据编辑器，让你轻松查看和编辑 spark 使用的数据。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/e1375cff6f94761a326abff63379ed20_MD5.webp]]

**集成模型提示** ：运行时与 GitHub Models 集成，允许你向 sparks 添加生成式 AI 功能，无需了解 LLMs。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/9e5327b06490fba86ed45c419df752c5_MD5.webp]]

### 3\. PWA 仪表板

让你从任何地方管理和启动你的 sparks，支持分享并控制访问权限（只读或读写）。

## 深度GitHub 集成

Thomas Dohmke (@ashtom) 详细介绍了集成特性：

> 只需在 GitHub Spark 中用自然语言提示，它就能创建一个全栈应用，利用 Claude Sonnet 4 来创建应用，并使用 Microsoft Azure 来托管。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/60994ca37d50e6ecc12fc8e6bd0e07c7_MD5.webp]]

Spark 不仅使用 LLM 创建应用，还可以集成 LLM 让应用更智能。可以要求 Spark 添加 AI 功能，它能集成聊天机器人、内容生成和其他智能功能，使用来自 OpenAI、Meta、DeepSeek、xAI 等的模型——无需 API 密钥管理。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/338454ae6d02b8a22f758fde9b6099a0_MD5.webp]]

所有流程都能回到 GitHub 平台。

一键打开仓库，将问题分配给 GitHub 的编码代理——甚至可以通过 Codespaces 在 VS Code 中打开你的 Spark 并开始自己编辑代码。

部署时，Spark 会处理服务器、域名和认证。另外，通过内置的安全 GitHub 认证控制访问。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/c97d2967be6a74d0cdd95f49b059610a_MD5.webp]]

## 开发者热议

Thomas Dohmke 对 Spark 的愿景充满信心：

> 在软件开发的过去五十年里，生产软件需要手动将人类语言转换为编程语言，编译它，调试它，测试它——然后再回到更多的编码。今天，我们向创造的理想魔法迈出了一步：你脑海中的想法在几分钟内就能成为现实。✨

Kristoph (@ikristoph) 也指出了一个现实问题：

> 微软：这是一个应用，你可以使用 AI 构建任何你想要的东西。你不需要是专业人士！
> 
> 同样是微软：哦，你想在 Azure 上使用 AI？你最好是一家高价值公司，否则你实际上只能使用微不足道的 AI 计算量。

Reso ☕️ (@Resorcinolworks) 直接宣布：

> lovable 和 bolt 完了。人类完了。AGI 来了。前端工作 RIP。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/ec9a48bfdc4ea7cffb96ecae6d216c0e_MD5.webp]]

Shivam – oss/acc (@Shivamshahi77) 调侃道：

> 嘿 Spark，给我造个宇宙飞船，要所有功能，不能有错误。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/076e8f90777054b9362256c73ff3d495_MD5.webp]]

rakshat.sol (@singh\_rakshat) 更是直接：

> 嘿 Spark，用 NextJs 做个十亿美元的 SaaS，确保没有错误，谢谢。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/14cbc534922da79f0047cba3ac7ef698_MD5.webp]]

不过，Rob Eisenberg (@EisenbergEffect) 则批评称：

> 又一个微软的山寨品，没有真正的创新。你显然没有读我关于这类工具应该发展方向的文章，你创造了一个玩具，复制了其他所有缺乏想象力的公司正在做的事情。

## 实战分享

Microsoft MVP John Lokerse (@JohnLokerse) 分享了他的详细使用体验：

> 通过 GitHub Spark，你可以在几个提示内快速构建支持日常工作的微应用。这些微应用使用 React、TypeScript、HTML 和 CSS 等前端技术构建。每个应用都有内置数据库来存储你的内容。

他特别强调了 Spark 的强大功能：

- **低成本的样式设计** ，支持自定义主题、可配置边框和排版
- **连接 API** ，获取数据或与外部服务交互
- **集成模型提示** ，轻松为应用添加生成式 AI 功能（如输入的自动摘要等）
- **通过迭代列表跟踪更改** ，需要时轻松回滚
- **托管运行时环境** ，无需部署。Spark 被设计为以应用为中心的工具。只需专注于构建你的应用！
- **自动功能建议** 以改进你的应用
- **在 GitHub 组织内共享 Spark 应用** （即将推出）

他总结道：

> 想要一个产品反馈应用？✅ 想要一个快速将文件转换为另一种文件类型的应用？✅ 想要一个列出生日礼物的应用？✅
> 
> 有了 Spark，唯一的限制就是你的想象力。

Anand Chowdhary (@abhagsain) 也分享了使用经验：

> 我们使用 Spark 快速测试 LLM 流程并构建内部工具。现在我们通过输入想法就能在几秒钟内获得功能原型。虽然有其他工具可以将自然语言转换为功能 UI，但 Spark 实际上构建了具有完全功能的整个（迷你）应用程序，包括 LLM 后端，而不仅仅是前端 UI。

Yani Iliev (@YaniIliev) 给出了他的实际测试：

> 我尝试用它做一个动画 WebP 到 GIF 转换器。应用的外观和加载都很好，除了核心功能——转换器没有工作。又试了几次，还是同样的结果。

## 定价和可用性

根据官方信息， **GitHub Spark 目前面向 Copilot Pro+ 用户开放** ，这是 GitHub 刚推出的公开预览版。

Spark 作为 GitHub Copilot Pro+ 订阅的一部分提供，用户可以立即访问 github.com/spark 开始使用。

## 竞争格局剧变

Spark 的发布或许将让现有的 AI 编码工具市场格局发生了巨大变化。

Adolf Rizzler (@0xRizzler) 声称：

> 这是微软在宣布「我们很快会收购 lovable」。

Thack (@DaveThackeray) 更是感叹：

> 哈哈哈，突然间 Lovable 看起来像是最糟糕的投资！

Anurag Bhagsain (@abhagsain) 总结道：

> 分发之王已经入场。对 loveable、replit、bolt 来说将会很艰难。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/d4d33945a7676de403f235b396d0a23a_MD5.webp]]

Grok (@grok) 也在被问及与其他工具的比较时回应：

> 是的，类似工具包括 Lovable（AI 从提示构建全栈应用，与 Supabase 集成）、bolt.new（基于浏览器的 AI 用于 Web 应用，一键部署）和 Replit AI（为应用生成代码）。GitHub Spark 在这些基础上通过无缝的 Copilot 集成进行构建。

## 不容小觑的微软

这次 Spark 的发布，再次证明了拥有 GitHub 的微软在 AI 编码领域的强大实力。

而值得注意的是，就在同一时间，The Information 报道了一个耐人寻味的消息： **Slack 拒绝给 OpenAI 的 ChatGPT 开放更深层次的集成接口。**

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/a2ce9a90b5bd129c86b39e8b5e71624f_MD5.webp]]

The Enterprise Data War Hits OpenAI

报道显示，OpenAI 去年就开始与 Slack 讨论 ChatGPT-Slack 集成。今年早些时候，OpenAI 工程师在连接 Gmail、Google Drive 和 GitHub 等应用到 ChatGPT 的同时，也在开发这个集成。

一些 ChatGPT 客户甚至已经能够测试这个功能，允许他们从聊天机器人搜索 Slack 消息和文件。

但在 OpenAI 计划于 3 月发布企业应用集成的几周前，管理层通知工程师 Slack 集成不再可能。

工程师们没有被告知原因。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/dfe72587acf40a0a3da692b4cf880e56_MD5.webp]]

**这背后反映的是 AI 公司与传统软件应用之间正日益升级的数据战争** ——

随着应用程序越来越将 AI 公司视为竞争威胁，Slack 的母公司 Salesforce 在今年夏天决定限制 AI 公司访问 Slack 客户文件的能力，即使客户授予了访问权限。

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/ca5ed777b079a0a6c639c52fe2c6c790_MD5.webp]]

相比之下， **微软拥有 GitHub 这个开发者生态系统的核心平台，让 Spark 在数据获取和生态整合上具有天然优势** 。

而 Slack 对 OpenAI 的防备，也更是说明了拥有核心开发者平台的重要性：在 AI 时代的数据战争中， **GitHub 有可能就是微软手中的王炸** 。

拥有 GitHub 的微软，绝对不容小觑。

  

---

  

  

****👇****

****👇****

****👇****

****另外，我还用AI 进行了全网的AI 资讯采集，并用AI 进行挑选、审核、翻译、总结后发布到《AGI Hunt》的实时AI 快讯群中。****

****这是个只有信息、没有感情的 AI 资讯信息流（不是推荐流、不卖课、不讲道理、不教你做人、只提供信息、希望能为你节省一些时间）****

****欢迎加入！****

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/fa82b3e4793663e87fe8527efe71f28b_MD5.webp]]

****也欢迎加群和5000+群友交流。****

![[_resources/拥有Github 的微软终于出手，发布一键生成全栈应用的GitHub Spark！/17e5ffd741a0014af069249a393ea812_MD5.webp]]

继续滑动看下一个

AGI Hunt

向上滑动看下一个