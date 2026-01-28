---
标题: "The importance of Agent Harness in 2026"
链接: "https://www.philschmid.de/agent-harness-2026"
作者: "[[Philipp Schmid]]"
创建时间: 2026-01-28T23:34:43+08:00
摘要:
tags:
  - "clippings"
字数: 1128
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

## The importance of Agent Harness in 20262026 年智能体驾驭技术的重要性

January 5, 2026 2026 年 1 月 5 日 6 minute read 6 分钟阅读

We are at a turning point in AI. For years, we focused only on the model. We asked how smart/good the model was. We checked leaderboards and benchmarks to see if Model A beats Model B.  
我们正处于人工智能的转折点。多年来，我们只关注模型本身。我们询问模型有多聪明/多优秀。我们查看排行榜和基准测试，看模型 A 是否胜过模型 B。

The difference between top-tier models on static leaderboards is shrinking. But this could be an illusion. The gap between models becomes clear the longer and more complex a task gets. It comes down to durability: How well a model follows instructions while executing hundreds of tool calls over time. A 1% difference on a leaderboard cannot detect the reliability if a model drifts off-track after fifty steps.  
静态排行榜上顶级模型之间的差异正在缩小。但这可能是一种错觉。任务越复杂、持续时间越长，模型之间的差距就越明显。这归根结底是持久性问题：模型在执行数百次工具调用时，能多好地遵循指令。排行榜上 1%的差异无法检测模型在五十步后是否偏离轨道。

We need a new way to show capabilities, performance and improvements. We need systems that proves models can execute multi-day workstreams reliably. One Answer to this are Agent Harnesses.  
我们需要一种新的方式来展示能力、性能和改进。我们需要能够证明模型可以可靠执行多日工作流的系统。解决这一问题的一个答案是智能体约束系统。

## What is an Agent Harness?什么是 Agent Harness？

An Agent Harness is the infrastructure that wraps around an AI model to manage long-running tasks. It is not the agent itself. It is the software system that governs how the agent operates, ensuring it remains reliable, efficient, and steerable.  
Agent Harness 是包裹在 AI 模型外围、用于管理长期运行任务的基础设施。它并非智能体本身，而是管控智能体运行方式的软件系统，确保其保持可靠、高效且可操控的特性。

It operates at a higher level than agent frameworks. While a framework provides the building blocks for tools or implements the agentic loop. The harness provides prompt presets, opinionated handling for tool calls, lifecycle hooks or ready-to-use capabilities like planning, filesystem access or sub-agent management. It is more than a framework, it comes with batteries included.  
其运作层级高于智能体框架。框架提供工具构建模块或实现智能体循环机制，而 Harness 则提供预设提示模板、工具调用的规范化处理、生命周期钩子，以及开箱即用的规划能力、文件系统访问或子智能体管理等功能。它不仅是框架，更是配备完整解决方案的体系。

![[_resources/The importance of Agent Harness in 2026/d0542cffa120b914f17429e8724df849_MD5.jpg]]

We can visualize this by comparing it to a computer:  
我们可以通过计算机类比来直观理解：

- **The Model is the CPU:** It provides the raw processing power.  
	模型是 CPU：它提供原始的处理能力。
- **The Context Window is the RAM:** It is the limited, volatile working memory.  
	上下文窗口是 RAM：它是有限且易失的工作内存。
- **The Agent Harness is the Operating System:** It curates the context, handles the "boot" sequence (prompts, hooks), and provides standard drivers (tool handling).  
	智能体框架是操作系统：它管理上下文，处理“启动”序列（提示词、钩子），并提供标准驱动程序（工具处理）。
- **The Agent is the Application:** It is the specific user logic running on top of the OS.  
	智能体是应用程序：它是在操作系统之上运行的具体用户逻辑。

The Agent harness implements " [Context Engineering](https://www.philschmid.de/context-engineering) " strategies like reducing context via compaction, offloading state to storage, or isolating tasks into sub-agents. For developers, this means you can skip building the operating system and focus solely on the application, defining your agent's unique logic.  
Agent Harness 通过压缩上下文、将状态卸载到存储或将任务隔离到子代理等方式，实现了"上下文工程"策略。对开发者而言，这意味着可以跳过构建操作系统，专注于应用程序本身，只需定义智能体的独特逻辑即可。

Currently, general-purpose harnesses are rare. **Claude Code** is a prime example of this emerging category, attempting to standardize with the Claude Agent SDK or LangChain DeepAgents. However, one could argue that **all coding CLIs** are, in a way, specialized agent harnesses designed for specific verticals.  
目前通用型智能体框架尚属罕见。Claude Code 是这一新兴领域的典型代表，它正尝试通过 Claude Agent SDK 或 LangChain DeepAgents 建立标准化框架。但也可以说，所有编码命令行工具在某种程度上都是针对特定垂直领域设计的专用智能体框架。

## The Benchmark Problem and the need for Agent Harnesses基准测试难题与智能体框架的必要性

In the past, benchmarks were mostly done on single-turn model outputs. Last year, we started to see a trend to evaluate systems instead of raw models, where the model is one component which could use tools or interacts with the environment, e.g. AIMO, SWE-Bench.  
过去，基准测试主要针对单轮模型输出进行评估。去年开始出现评估系统而非原始模型的趋势，在这种模式下，模型成为可使用工具或与环境交互的组件之一，例如 AIMO、SWE-Bench 等项目就体现了这种转变。

These newer benchmarks struggle to measure [reliability](https://www.philschmid.de/agents-pass-at-k-pass-power-k). They rarely test how a model behaves after its 50th or 100th tool call/turn. This is where the real difficulty lies. A model might be smart enough to solve a hard puzzle in one or two tries, but fail to follow a initial instructions or correctly reasons over intermediate steps after running for an hour. Standard benchmarks struggle to capture the durabilitiy required for long workflows.  
这些新型基准测试难以衡量可靠性。它们很少测试模型在第 50 次或第 100 次工具调用/轮次后的表现。这正是真正的难点所在。一个模型或许足够聪明，能在一两次尝试中解决复杂难题，但在运行一小时后却可能无法遵循初始指令，或无法正确推理中间步骤。标准基准测试难以捕捉长流程工作所需的持久性。

As Benchmarks are going to become more complex we need to bridge the gap between benchmark claims and user experience. A Agent Harness can be essential for three critical reasons:  
随着基准测试日趋复杂，我们需要弥合基准测试宣称效果与用户体验之间的鸿沟。智能体测试框架至关重要，原因有三：

- **Validating Real-World Progress:** Benchmarks are misaligned with user needs. As new models are released frequently, a harness allows users to easily test and compare how the latest models perform against their use cases and constraints.  
	验证实际进展：基准测试与用户需求存在偏差。随着新模型频繁发布，测试框架能让用户轻松测试并比较最新模型在其使用场景和限制条件下的表现。
- **Empowering User Experience:** Without a harness, the user's experience might be behind the model's potential. Releasing a harness allows developers to build agents using proven tools and best practices. This ensures that users are interacting with the same system structure.  
	提升用户体验：缺乏测试框架时，用户体验可能滞后于模型潜力。发布测试框架能让开发者运用已验证的工具和最佳实践构建智能体，确保用户始终与相同的系统架构交互。
- **Hill Climbing via Real-World Feedback:** A shared, stable environment (Harness) creates a feedback loop where researchers can iterate and improve ("hill climb") benchmarks based on actual user adoption.  
	通过真实世界反馈实现渐进优化：一个共享、稳定的环境（Harness）构建了反馈循环，研究人员能够基于实际用户采纳情况，对基准测试进行迭代改进（"渐进优化"）。

The ability to improve a system is proportional to how easily you can verify its output. [\[Ref\]](https://www.jasonwei.net/blog/asymmetry-of-verification-and-verifiers-law) A Harness turns vague, multi-step agent workflows into structured data that we can log and grade, allowing us to hill-climb effectively.  
改进系统的能力与验证其输出的难易程度成正比。\[参考文献\] Harness 将模糊、多步骤的智能体工作流转化为可记录和评分的结构化数据，使我们能够有效实现渐进优化。

## The "Bitter Lesson" of building Agents构建智能体的"苦涩教训"

Rich Sutton wrote an essay called [the Bitter Lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html). He argued that general methods that use computation beat hand-coded human knowledge every time. We see this lesson playing out in agent development right now.  
里奇·萨顿曾撰文论述"苦涩教训"。他指出，利用计算的通用方法每次都能战胜人工编码的知识。我们正目睹这一教训在智能体开发领域重演。

- Manus refactored [their harness five times in six months](https://www.youtube.com/watch?v=6_BcCthVvb8) to remove rigid assumptions.  
	Manus 在六个月内重构了五次其框架，以消除僵化的预设。
- LangChain [re-architected their "Open Deep Research" agent three times](https://www.youtube.com/watch?v=2Muxy3wE-E0) in a single year.  
	LangChain 在一年内对其"开放深度研究"智能体进行了三次架构重构。
- [Vercel removed 80% their agents tool](https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools) leading to fewer steps, fewer tokens, faster responses  
	Vercel 移除了 80%的智能体工具，从而减少了步骤、降低了令牌使用量，并加快了响应速度。

To survive the Bitter Lesson, our infrastructure (Harness) must be lightweight. Every new model release, has a different, optimal way to structure agents. Capabilities that required complex, hand-coded pipelines in 2024 are now handled by a single context-window prompt in 2026.  
为了在"苦涩教训"中生存下来，我们的基础设施（框架）必须保持轻量化。每一次新模型的发布，都带来了构建智能体的不同且最优的方式。2024 年需要复杂、手动编码的流水线才能实现的功能，到 2026 年只需一个上下文窗口提示即可完成。

Developers must build harnesses that allow them to rip out the "smart" logic they wrote yesterday. If you over-engineer the control flow, the next model update will break your system.  
开发者必须构建能够随时替换昨日"智能"逻辑的框架。若过度设计控制流程，下一次模型更新便会摧毁你的系统。

## What Comes Next? 未来何去何从？

We are heading toward a convergence of training and inference environments. We see a new bottleneck being context durability. The Harness will become the primary tool for solving "model drift". Labs will use the harness to detect exactly when a model stops following instructions or reasoning correctly after the 100th step. This data will be fed directly back into training to create models that don't get "tired" during long tasks.  
我们正迈向训练与推理环境融合的时代。上下文持久性将成为新的瓶颈。智能体框架将成为解决"模型漂移"的核心工具。研究机构将运用该框架精准捕捉模型在第 100 步后何时开始偏离指令或推理失常。这些数据将直接反馈至训练过程，从而打造出能在长时任务中保持"精力充沛"的模型。

As builders and developers the focus should shift:  
作为构建者与开发者，我们的重心应当转向：

1. **Start Simple:** Do not build massive control flows. Provide robust atomic tools. Let the model make the plan. Implement guardrails, retries and verifications.  
	从简单开始：不要构建复杂的控制流程。提供强大的原子工具。让模型制定计划。实施防护措施、重试机制和验证流程。
2. **Build to Delete:** Make your architecture modular. New models will replace your logic. You must be ready to rip out code.  
	构建即删除：让你的架构模块化。新模型将取代你的逻辑。你必须准备好随时替换代码。
3. **The Harness is the Dataset:** Competitive advantage is no longer the prompt. It is the trajectories your Harness captures. Every time your agent fails to follow an instruction late in a workflow can be ued for training the next iteration.  
	驾驭即数据集：竞争优势不再是提示本身，而是你的驾驭系统所捕捉的执行轨迹。每当你的智能体在工作流后期未能遵循指令时，这些轨迹都能用于训练下一代迭代。

---

Thanks for reading! If you have any questions or feedback, please let me know on [Twitter](https://twitter.com/_philschmid) or [LinkedIn](https://www.linkedin.com/in/philipp-schmid-a6a2bb196/).  
感谢阅读！如有任何问题或反馈，请通过 Twitter 或 LinkedIn 与我联系。