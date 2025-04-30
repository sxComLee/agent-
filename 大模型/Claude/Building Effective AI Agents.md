---
标题: "Building Effective AI Agents"
链接: "https://www.anthropic.com/engineering/building-effective-agents"
作者: "[[@AnthropicAI]]"
创建时间: "2025-04-29T15:37:10+08:00"
摘要: "Anthropic分享了构建有效AI代理的经验，包括简单可组合的模式、工作流程与代理的区别、何时使用代理以及工具开发的最佳实践。"
tags:
  - "clippings"
  - "AI"
  - "编程"
  - "大型语言模型"
  - "Anthropic"
  - "智能体系统"
字数: "2883"
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
[Engineering at Anthropic  
Anthropic 的工程](https://www.anthropic.com/engineering)

Over the past year, we've worked with dozens of teams building large language model (LLM) agents across industries. Consistently, the most successful implementations weren't using complex frameworks or specialized libraries. Instead, they were building with simple, composable patterns.  
过去一年中，我们与数十个团队合作，在各个行业构建大型语言模型（LLM）智能体。始终如一，最成功的实施并没有使用复杂的框架或专门的库。相反，他们使用的是简单、可组合的模式。

In this post, we share what we’ve learned from working with our customers and building agents ourselves, and give practical advice for developers on building effective agents.  
在这篇文章中，我们分享了我们与客户合作以及我们自己构建智能体的经验，并为开发者提供了构建有效智能体的实用建议。

## What are agents? 智能体是什么？

"Agent" can be defined in several ways. Some customers define agents as fully autonomous systems that operate independently over extended periods, using various tools to accomplish complex tasks. Others use the term to describe more prescriptive implementations that follow predefined workflows. At Anthropic, we categorize all these variations as **agentic systems**, but draw an important architectural distinction between **workflows** and **agents**:  
"智能体"可以有多种定义方式。一些客户将智能体定义为在长时间内独立运行的完全自主系统，使用各种工具来完成复杂任务。其他人则用这个词来描述遵循预定义工作流程的更具体实现。在 Anthropic，我们将所有这些变体都归类为智能体系统，但在架构上对工作流程和智能体进行了重要的区分：

- **Workflows** are systems where LLMs and tools are orchestrated through predefined code paths.  
	工作流程是那些通过预定义代码路径编排 LLMs 和工具的系统。
- **Agents**, on the other hand, are systems where LLMs dynamically direct their own processes and tool usage, maintaining control over how they accomplish tasks.  
	相反，智能体是 LLMs 动态指导自己的流程和工具使用的系统，保持对完成任务方式的控制。

Below, we will explore both types of agentic systems in detail. In Appendix 1 (“Agents in Practice”), we describe two domains where customers have found particular value in using these kinds of systems.  
下面，我们将详细介绍这两种智能体系统。在附录 1（《实践中的智能体》）中，我们描述了两个客户发现使用这些系统特别有价值的领域。

## When (and when not) to use agents何时（以及何时不）使用代理

When building applications with LLMs, we recommend finding the simplest solution possible, and only increasing complexity when needed. This might mean not building agentic systems at all. Agentic systems often trade latency and cost for better task performance, and you should consider when this tradeoff makes sense.  
在使用 LLMs 构建应用程序时，我们建议寻找最简单的解决方案，并在需要时才增加复杂性。这可能意味着根本不构建 Agentic 系统。Agentic 系统通常以**牺牲延迟和成本为代价**来换取更好的任务性能，你应该考虑这种权衡何时是合理的。

When more complexity is warranted, workflows offer predictability and consistency for well-defined tasks, whereas agents are the better option when flexibility and model-driven decision-making are needed at scale. For many applications, however, optimizing single LLM calls with retrieval and in-context examples is usually enough.  
当需要更多的复杂性时，**workflows** 为定义**明确的任务提供可预测性和一致性**，而 **agents** 在需要大规模的**灵活性和模型驱动决策**时是更好的选择。然而，对于许多应用程序来说，优化单个 LLM 调用，使用检索和上下文示例通常就足够了。

## When and how to use frameworks何时以及如何使用框架

There are many frameworks that make agentic systems easier to implement, including:  
有许多框架使实现智能体系统变得更加容易，包括：

- [LangGraph](https://langchain-ai.github.io/langgraph/) from LangChain;  
	LangChain 的 LangGraph；
- Amazon Bedrock's [AI Agent framework](https://aws.amazon.com/bedrock/agents/);  
	亚马逊 Bedrock 的 AI 代理框架；
- [Rivet](https://rivet.ironcladapp.com/), a drag and drop GUI LLM workflow builder; and  
	Rivet，一个拖放式 GUI LLM 工作流程构建器；以及
- [Vellum](https://www.vellum.ai/), another GUI tool for building and testing complex workflows.  
	Vellum，另一个用于构建和测试复杂工作流程的 GUI 工具。

These frameworks make it easy to get started by simplifying standard low-level tasks like calling LLMs, defining and parsing tools, and chaining calls together. However, they often create extra layers of abstraction that can obscure the underlying prompts and responses, making them harder to debug. They can also make it tempting to add complexity when a simpler setup would suffice.  
这些框架通过简化标准低级任务（如调用 LLMs、定义和解析工具以及链式调用）来简化入门过程。然而，它们通常会增加额外的抽象层，这可能会掩盖底层提示和响应，使得调试变得更加困难。它们还可能诱使人们在不必要的情况下增加复杂性。

We suggest that developers start by using LLM APIs directly: many patterns can be implemented in a few lines of code. If you do use a framework, ensure you understand the underlying code. Incorrect assumptions about what's under the hood are a common source of customer error.  
我们建议开发者直接使用 LLM API：许多模式可以用几行代码实现。如果你确实使用了框架，请确保你理解底层代码。对底层代码的错误假设是客户错误的一个常见来源。

See our [cookbook](https://github.com/anthropics/anthropic-cookbook/tree/main/patterns/agents) for some sample implementations.  
请参阅我们的食谱，了解一些示例实现。

## Building blocks, workflows, and agents构建模块、工作流程和智能体

In this section, we’ll explore the common patterns for agentic systems we’ve seen in production. We'll start with our foundational building block—the augmented LLM—and progressively increase complexity, from simple compositional workflows to autonomous agents.  
在本节中，我们将探讨我们在生产中看到的常见代理系统模式。我们将从我们的基础构建块——增强型 LLM（大型语言模型）开始，逐步增加复杂性，从简单的组合工作流程到自主代理。

### Building block: The augmented LLM构建块：增强型 LLM

The basic building block of agentic systems is an LLM enhanced with augmentations such as retrieval, tools, and memory. Our current models can actively use these capabilities—generating their own search queries, selecting appropriate tools, and determining what information to retain.  
代理系统的基础构建块是一个经过增强的 LLM，例如检索、工具和记忆。我们的当前模型可以积极使用这些功能——生成自己的搜索查询，选择合适的工具，并确定要保留的信息。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2Fd3083d3f40bb2b6f477901cc9a240738d3dd1371-2401x1000.png&w=3840&q=75)

The augmented LLM 增强型 LLM

We recommend focusing on two key aspects of the implementation: tailoring these capabilities to your specific use case and ensuring they provide an easy, well-documented interface for your LLM. While there are many ways to implement these augmentations, one approach is through our recently released [Model Context Protocol](https://www.anthropic.com/news/model-context-protocol), which allows developers to integrate with a growing ecosystem of third-party tools with a simple [client implementation](https://modelcontextprotocol.io/tutorials/building-a-client#building-mcp-clients).  
我们建议关注实施的两个关键方面：将这些功能定制到您的特定用例中，并确保它们为您的 LLM 提供简单、文档齐全的接口。虽然实现这些增强有多种方法，但一种方法是通过我们最近发布的模型上下文协议，它允许开发人员通过简单的客户端实现与不断增长的第三方工具生态系统集成。

For the remainder of this post, we'll assume each LLM call has access to these augmented capabilities.  
在本文的剩余部分，我们将假设每个 LLM 调用都具备这些增强功能。

### Workflow: Prompt chaining工作流程：提示链

Prompt chaining decomposes a task into a sequence of steps, where each LLM call processes the output of the previous one. You can add programmatic checks (see "gate” in the diagram below) on any intermediate steps to ensure that the process is still on track.  
提示链将任务分解为一系列步骤，其中每个 LLM 调用处理上一个步骤的输出。您可以在任何中间步骤添加程序性检查（见下图中“门”），以确保流程仍在正轨上。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F7418719e3dab222dccb379b8879e1dc08ad34c78-2401x1000.png&w=3840&q=75)

The prompt chaining workflow 提示链工作流程

**When to use this workflow:** This workflow is ideal for situations where the task can be easily and cleanly decomposed into fixed subtasks. The main goal is to trade off latency for higher accuracy, by making each LLM call an easier task.  
使用此工作流程的时机：此工作流程适用于任务可以轻松且干净地分解为固定子任务的情况。主要目标是权衡延迟以换取更高的准确性，通过使每个 LLM 调用成为一个更简单的任务。

**Examples where prompt chaining is useful:  
提示链式调用的应用示例：**

- Generating Marketing copy, then translating it into a different language.  
	生成营销文案，然后将其翻译成另一种语言。
- Writing an outline of a document, checking that the outline meets certain criteria, then writing the document based on the outline.  
	撰写文档大纲，检查大纲是否符合某些标准，然后根据大纲撰写文档。

### Workflow: Routing 工作流程：路由

Routing classifies an input and directs it to a specialized followup task. This workflow allows for separation of concerns, and building more specialized prompts. Without this workflow, optimizing for one kind of input can hurt performance on other inputs.  
路由将输入进行分类并引导它到专门的后续任务。此工作流程允许分离关注点，并构建更专业的提示。如果没有此工作流程，针对一种类型的输入进行优化可能会损害其他输入的性能。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F5c0c0e9fe4def0b584c04d37849941da55e5e71c-2401x1000.png&w=3840&q=75)

The routing workflow 路由工作流程

**When to use this workflow:** Routing works well for complex tasks where there are distinct categories that are better handled separately, and where classification can be handled accurately, either by an LLM or a more traditional classification model/algorithm.  
何时使用此工作流程：路由适用于具有明显类别且更适合单独处理的复杂任务，以及分类可以准确处理的情况，无论是通过 LLM 还是更传统的分类模型/算法。

**Examples where routing is useful:  
路由应用示例：**

- Directing different types of customer service queries (general questions, refund requests, technical support) into different downstream processes, prompts, and tools.  
	将不同类型的客户服务查询（一般问题、退款请求、技术支持）引导到不同的下游流程、提示和工具中。
- Routing easy/common questions to smaller models like Claude 3.5 Haiku and hard/unusual questions to more capable models like Claude 3.5 Sonnet to optimize cost and speed.  
	将简单/常见问题路由到较小的模型如 Claude 3.5 Haiku，将复杂/不寻常问题路由到更强大的模型如 Claude 3.5 Sonnet，以优化成本和速度。

### Workflow: Parallelization工作流程：并行化

LLMs can sometimes work simultaneously on a task and have their outputs aggregated programmatically. This workflow, parallelization, manifests in two key variations:  
LLMs 有时可以同时处理一个任务并将输出程序化地汇总。这种工作流程，即并行化，有两种关键变体：

- **Sectioning**: Breaking a task into independent subtasks run in parallel.  
	分区：将任务分解成独立子任务并行运行。
- **Voting:** Running the same task multiple times to get diverse outputs.  
	投票：多次运行相同的任务以获得多样化的输出。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F406bb032ca007fd1624f261af717d70e6ca86286-2401x1000.png&w=3840&q=75)

The parallelization workflow 并行化工作流程

**When to use this workflow:** Parallelization is effective when the divided subtasks can be parallelized for speed, or when multiple perspectives or attempts are needed for higher confidence results. For complex tasks with multiple considerations, LLMs generally perform better when each consideration is handled by a separate LLM call, allowing focused attention on each specific aspect.  
何时使用此工作流程：当子任务可以并行化以提高速度或需要多个视角或尝试以提高置信度结果时，并行化是有效的。对于需要考虑多个方面的复杂任务，当每个考虑因素由单独的 LLM 调用处理时，LLMs 通常表现更好，允许对每个特定方面进行专注的注意。

**Examples where parallelization is useful:  
示例中并行化有用的场景：**

- **Sectioning**:分节：
	- Implementing guardrails where one model instance processes user queries while another screens them for inappropriate content or requests. This tends to perform better than having the same LLM call handle both guardrails and the core response.  
		实施防护措施，其中一个模型实例处理用户查询，另一个实例筛选不适当的内容或请求。这通常比让同一个 LLM 调用同时处理防护措施和核心响应表现得更好。
	- Automating evals for evaluating LLM performance, where each LLM call evaluates a different aspect of the model’s performance on a given prompt.  
		自动评估以评估 LLM 性能，其中每个 LLM 调用评估给定提示下模型性能的不同方面。
- **Voting**:投票：
	- Reviewing a piece of code for vulnerabilities, where several different prompts review and flag the code if they find a problem.  
		检查代码是否存在漏洞，通过多个不同的提示来审查代码，如果发现问题则标记。
	- Evaluating whether a given piece of content is inappropriate, with multiple prompts evaluating different aspects or requiring different vote thresholds to balance false positives and negatives.  
		评估给定内容是否不适当，多个提示评估不同方面或需要不同的投票阈值，以平衡误报和漏报。

### Workflow: Orchestrator-workers工作流程：协调器-工作者

In the orchestrator-workers workflow, a central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results.  
在协调器-工作者工作流程中，一个中央 LLM 动态分解任务，将它们委托给工作者 LLM，并综合他们的结果。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F8985fc683fae4780fb34eab1365ab78c7e51bc8e-2401x1000.png&w=3840&q=75)

The orchestrator-workers workflow 协调器-工作者工作流程

**When to use this workflow:** This workflow is well-suited for complex tasks where you can’t predict the subtasks needed (in coding, for example, the number of files that need to be changed and the nature of the change in each file likely depend on the task). Whereas it’s topographically similar, the key difference from parallelization is its flexibility—subtasks aren't pre-defined, but determined by the orchestrator based on the specific input.  
何时使用此工作流程：此工作流程非常适合复杂任务，在这些任务中，您无法预测所需的子任务（例如，在编码中，需要更改的文件数量以及每个文件更改的性质可能取决于任务）。虽然它与并行化在拓扑上相似，但其关键区别在于其灵活性——子任务不是预先定义的，而是由协调器根据特定输入确定。

**Example where orchestrator-workers is useful:  
协调器-工作者有用的示例：**

- Coding products that make complex changes to multiple files each time.  
	编码每次都需要对多个文件进行复杂更改的产品。
- Search tasks that involve gathering and analyzing information from multiple sources for possible relevant information.  
	搜索涉及从多个来源收集和分析信息以获取可能相关信息的任务。

### Workflow: Evaluator-optimizer工作流程：评估-优化器

In the evaluator-optimizer workflow, one LLM call generates a response while another provides evaluation and feedback in a loop.  
在评估-优化器工作流程中，一次 LLM 调用生成响应，而另一次在循环中提供评估和反馈。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F14f51e6406ccb29e695da48b17017e899a6119c7-2401x1000.png&w=3840&q=75)

The evaluator-optimizer workflow 评估-优化工作流程

**When to use this workflow:** This workflow is particularly effective when we have clear evaluation criteria, and when iterative refinement provides measurable value. The two signs of good fit are, first, that LLM responses can be demonstrably improved when a human articulates their feedback; and second, that the LLM can provide such feedback. This is analogous to the iterative writing process a human writer might go through when producing a polished document.  
使用此工作流程的时机：当拥有明确的评估标准，且迭代优化能够带来可衡量的价值时，此工作流程特别有效。良好的匹配的两个标志是，首先，当人类明确表达反馈时，LLM 的响应可以明显改进；其次，LLM 可以提供此类反馈。这类似于人类作家在创作精炼文档时可能经历的迭代写作过程。

**Examples where evaluator-optimizer is useful:  
评估优化器有用的例子：**

- Literary translation where there are nuances that the translator LLM might not capture initially, but where an evaluator LLM can provide useful critiques.  
	文学翻译中，翻译 LLM 可能最初无法捕捉到的细微差别，但评估 LLM 可以提供有用的批评。
- Complex search tasks that require multiple rounds of searching and analysis to gather comprehensive information, where the evaluator decides whether further searches are warranted.  
	需要进行多轮搜索和分析以收集全面信息的复杂搜索任务，其中评估者决定是否需要进行进一步的搜索。

### Agents 代理

Agents are emerging in production as LLMs mature in key capabilities—understanding complex inputs, engaging in reasoning and planning, using tools reliably, and recovering from errors. Agents begin their work with either a command from, or interactive discussion with, the human user. Once the task is clear, agents plan and operate independently, potentially returning to the human for further information or judgement. During execution, it's crucial for the agents to gain “ground truth” from the environment at each step (such as tool call results or code execution) to assess its progress. Agents can then pause for human feedback at checkpoints or when encountering blockers. The task often terminates upon completion, but it’s also common to include stopping conditions (such as a maximum number of iterations) to maintain control.  
随着大型语言模型（LLMs）在理解复杂输入、进行推理和规划、可靠地使用工具以及从错误中恢复等关键能力上的成熟，代理正在生产中兴起。代理的工作开始于来自人类用户的命令或与人类用户的交互式讨论。一旦任务明确，代理将独立地进行计划和操作，可能需要返回人类用户获取更多信息或判断。在执行过程中，代理在每个步骤（如工具调用结果或代码执行）从环境中获取“真实情况”以评估其进度至关重要。代理可以在检查点或遇到阻碍时暂停以获取人类反馈。任务通常在完成时终止，但也可以包括停止条件（如最大迭代次数）以保持控制。

Agents can handle sophisticated tasks, but their implementation is often straightforward. They are typically just LLMs using tools based on environmental feedback in a loop. It is therefore crucial to design toolsets and their documentation clearly and thoughtfully. We expand on best practices for tool development in Appendix 2 ("Prompt Engineering your Tools").  
代理可以处理复杂的任务，但它们的实现通常很简单。它们通常是使用基于环境反馈的循环工具的 LLMs。因此，设计工具集及其文档清晰、周到至关重要。我们在附录 2（提示工程你的工具）中扩展了工具开发的最佳实践。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F58d9f10c985c4eb5d53798dea315f7bb5ab6249e-2401x1000.png&w=3840&q=75)

Autonomous agent 自主代理

**When to use agents:** Agents can be used for open-ended problems where it’s difficult or impossible to predict the required number of steps, and where you can’t hardcode a fixed path. The LLM will potentially operate for many turns, and you must have some level of trust in its decision-making. Agents' autonomy makes them ideal for scaling tasks in trusted environments.  
何时使用代理：代理可用于难以预测或无法预测所需步骤数量的开放性问题，以及无法硬编码固定路径的情况。LLM 可能会进行多次操作，你必须对其决策有一定程度的信任。代理的自主性使它们在可信赖的环境中扩展任务时成为理想选择。

The autonomous nature of agents means higher costs, and the potential for compounding errors. We recommend extensive testing in sandboxed environments, along with the appropriate guardrails.  
代理的自主性意味着更高的成本和累积错误的潜在风险。我们建议在沙盒环境中进行广泛的测试，并采取适当的防护措施。

**Examples where agents are useful:  
以下是一些代理有用的例子：**

The following examples are from our own implementations:  
以下例子来自我们自己的实现：

- A coding Agent to resolve [SWE-bench tasks](https://www.anthropic.com/research/swe-bench-sonnet), which involve edits to many files based on a task description;  
	一个用于解决 SWE-bench 任务的编码代理，这些任务涉及根据任务描述对多个文件进行编辑；
- Our [“computer use” reference implementation](https://github.com/anthropics/anthropic-quickstarts/tree/main/computer-use-demo), where Claude uses a computer to accomplish tasks.  
	我们“计算机使用”的参考实现，其中 Claude 使用计算机来完成任务。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F4b9a1f4eb63d5962a6e1746ac26bbc857cf3474f-2400x1666.png&w=3840&q=75)

High-level flow of a coding agent 编码代理的高级流程

## Combining and customizing these patterns组合和定制这些模式

These building blocks aren't prescriptive. They're common patterns that developers can shape and combine to fit different use cases. The key to success, as with any LLM features, is measuring performance and iterating on implementations. To repeat: you should consider adding complexity *only* when it demonstrably improves outcomes.  
这些构建块并非强制性规定。它们是开发者可以塑造和组合以适应不同用例的通用模式。与任何 LLM 功能一样，成功的关键在于衡量性能并在实现上进行迭代。重复一遍：只有在明显改善结果的情况下，才应考虑增加复杂性。

## Summary 摘要

Success in the LLM space isn't about building the most sophisticated system. It's about building the *right* system for your needs. Start with simple prompts, optimize them with comprehensive evaluation, and add multi-step agentic systems only when simpler solutions fall short.  
在 LLM 领域取得成功，并非在于构建最复杂的系统。关键在于构建满足您需求的系统。从简单的提示开始，通过全面的评估进行优化，只有当简单解决方案不足时，才添加多步骤的智能体系统。

When implementing agents, we try to follow three core principles:  
在实施智能体时，我们试图遵循三个核心原则：

1. Maintain **simplicity** in your agent's design.  
	保持您的智能体设计简洁。
2. Prioritize **transparency** by explicitly showing the agent’s planning steps.  
	明确展示智能体的规划步骤，以增强透明度。
3. Carefully craft your agent-computer interface (ACI) through thorough tool **documentation and testing**.  
	通过详尽的工具文档和测试，精心设计智能体-计算机界面（ACI）。

Frameworks can help you get started quickly, but don't hesitate to reduce abstraction layers and build with basic components as you move to production. By following these principles, you can create agents that are not only powerful but also reliable, maintainable, and trusted by their users.  
框架可以帮助您快速入门，但在向生产阶段过渡时，不要犹豫减少抽象层，使用基本组件进行构建。遵循这些原则，您可以创建既强大又可靠、易于维护且用户信任的智能体。

### Acknowledgements 致谢

Written by Erik Schluntz and Barry Zhang. This work draws upon our experiences building agents at Anthropic and the valuable insights shared by our customers, for which we're deeply grateful.  
本作品由 Erik Schluntz 和 Barry Zhang 撰写。本作品借鉴了我们构建 Anthropic 代理的经验以及客户分享的宝贵见解，对此我们深表感激。

Our work with customers has revealed two particularly promising applications for AI agents that demonstrate the practical value of the patterns discussed above. Both applications illustrate how agents add the most value for tasks that require both conversation and action, have clear success criteria, enable feedback loops, and integrate meaningful human oversight.  
我们与客户的合作揭示了 AI 代理的两个特别有前景的应用，这些应用展示了上述讨论的模式的实际价值。这两个应用都说明了代理如何为既需要对话又需要行动的任务增加最大价值，这些任务有明确的成功标准，能够实现反馈循环，并整合有意义的人类监督。

### A. Customer support A. 客户支持

Customer support combines familiar chatbot interfaces with enhanced capabilities through tool integration. This is a natural fit for more open-ended agents because:  
客户支持将熟悉的聊天机器人界面与通过工具集成增强的功能相结合。这对于更开放式的智能体来说是一种自然的选择，因为：

- Support interactions naturally follow a conversation flow while requiring access to external information and actions;  
	支持交互自然遵循对话流程，同时需要访问外部信息和执行操作；
- Tools can be integrated to pull customer data, order history, and knowledge base articles;  
	可以集成工具以提取客户数据、订单历史和知识库文章；
- Actions such as issuing refunds or updating tickets can be handled programmatically; and  
	可以通过编程方式处理退款或更新工单等操作；并且
- Success can be clearly measured through user-defined resolutions.  
	成功可以通过用户定义的决议来明确衡量。

Several companies have demonstrated the viability of this approach through usage-based pricing models that charge only for successful resolutions, showing confidence in their agents' effectiveness.  
多家公司通过基于使用量的定价模型证明了这种方法的可行性，这些模型只对成功的解决方案收费，显示了他们对代理有效性的信心。

### B. Coding agents B. 编码代理

The software development space has shown remarkable potential for LLM features, with capabilities evolving from code completion to autonomous problem-solving. Agents are particularly effective because:  
软件开发领域已经展示了 LLM 功能的巨大潜力，其能力从代码补全发展到自主解决问题。代理之所以特别有效，因为：

- Code solutions are verifiable through automated tests;  
	代码解决方案可以通过自动化测试进行验证；
- Agents can iterate on solutions using test results as feedback;  
	代理可以使用测试结果作为反馈来迭代解决方案；
- The problem space is well-defined and structured; and  
	问题空间定义明确且结构化；并且
- Output quality can be measured objectively.  
	输出质量可以客观测量。

In our own implementation, agents can now solve real GitHub issues in the [SWE-bench Verified](https://www.anthropic.com/research/swe-bench-sonnet) benchmark based on the pull request description alone. However, whereas automated testing helps verify functionality, human review remains crucial for ensuring solutions align with broader system requirements.  
在我们的实现中，代理现在可以仅根据拉取请求描述解决 SWE-bench 验证基准中的真实 GitHub 问题。然而，虽然自动化测试有助于验证功能，但人工审查对于确保解决方案符合更广泛系统要求仍然至关重要。

No matter which agentic system you're building, tools will likely be an important part of your agent. [Tools](https://www.anthropic.com/news/tool-use-ga) enable Claude to interact with external services and APIs by specifying their exact structure and definition in our API. When Claude responds, it will include a [tool use block](https://docs.anthropic.com/en/docs/build-with-claude/tool-use#example-api-response-with-a-tool-use-content-block) in the API response if it plans to invoke a tool. Tool definitions and specifications should be given just as much prompt engineering attention as your overall prompts. In this brief appendix, we describe how to prompt engineer your tools.  
无论你正在构建哪种智能体系统，工具都可能成为你智能体的重要组成部分。工具使 Claude 能够通过指定外部服务和 API 的确切结构和定义来与它们交互。当 Claude 响应时，如果它计划调用工具，它将在 API 响应中包含一个工具使用块。工具的定义和规范应该像你的整体提示一样，得到足够的提示工程关注。在本附录中，我们描述了如何提示工程你的工具。

There are often several ways to specify the same action. For instance, you can specify a file edit by writing a diff, or by rewriting the entire file. For structured output, you can return code inside markdown or inside JSON. In software engineering, differences like these are cosmetic and can be converted losslessly from one to the other. However, some formats are much more difficult for an LLM to write than others. Writing a diff requires knowing how many lines are changing in the chunk header before the new code is written. Writing code inside JSON (compared to markdown) requires extra escaping of newlines and quotes.  
通常有几种方式可以指定相同的行为。例如，你可以通过编写 diff 或重写整个文件来指定文件编辑。对于结构化输出，你可以在 markdown 或 JSON 中返回代码。在软件工程中，这些差异只是外观上的，可以从一种格式无损地转换为另一种格式。然而，某些格式对于 LLM 来说比其他格式更难编写。编写 diff 需要知道在写入新代码之前，块标题中有多少行正在更改。在 JSON 中编写代码（与 markdown 相比）需要额外的换行符和引号转义。

Our suggestions for deciding on tool formats are the following:  
我们关于决定工具格式的建议如下：

- Give the model enough tokens to "think" before it writes itself into a corner.  
	给模型足够的 token 进行“思考”，以免它将自己写进死胡同。
- Keep the format close to what the model has seen naturally occurring in text on the internet.  
	保持格式接近模型在互联网文本中自然出现的格式。
- Make sure there's no formatting "overhead" such as having to keep an accurate count of thousands of lines of code, or string-escaping any code it writes.  
	确保没有格式“冗余”，例如需要准确计数数千行代码，或者对它所写的代码进行字符串转义。

One rule of thumb is to think about how much effort goes into human-computer interfaces (HCI), and plan to invest just as much effort in creating good *agent* -computer interfaces (ACI). Here are some thoughts on how to do so:  
一条经验法则是思考投入人机界面（HCI）的多少努力，并计划投入同样多的努力来创建良好的智能体-计算机界面（ACI）。以下是一些关于如何做到这一点的想法：

- Put yourself in the model's shoes. Is it obvious how to use this tool, based on the description and parameters, or would you need to think carefully about it? If so, then it’s probably also true for the model. A good tool definition often includes example usage, edge cases, input format requirements, and clear boundaries from other tools.  
	把自己放在模型的立场上。根据描述和参数，使用这个工具是否显而易见，还是需要仔细思考？如果是后者，那么对模型来说可能也是如此。一个好的工具定义通常包括示例用法、边缘情况、输入格式要求以及与其他工具的明确界限。
- How can you change parameter names or descriptions to make things more obvious? Think of this as writing a great docstring for a junior developer on your team. This is especially important when using many similar tools.  
	你如何更改参数名称或描述，使其更直观？把这想象成为你的团队中的初级开发者编写一个优秀的文档字符串。这在使用许多类似工具时尤为重要。
- Test how the model uses your tools: Run many example inputs in our [workbench](https://console.anthropic.com/workbench) to see what mistakes the model makes, and iterate.  
	测试模型如何使用您的工具：在我们的工作台中运行许多示例输入，以查看模型犯下的错误，并进行迭代。
- [Poka-yoke](https://en.wikipedia.org/wiki/Poka-yoke) your tools. Change the arguments so that it is harder to make mistakes.  
	确保你的工具没有缺陷。改变参数，使出错更难。

While building our agent for [SWE-bench](https://www.anthropic.com/research/swe-bench-sonnet), we actually spent more time optimizing our tools than the overall prompt. For example, we found that the model would make mistakes with tools using relative filepaths after the agent had moved out of the root directory. To fix this, we changed the tool to always require absolute filepaths—and we found that the model used this method flawlessly.  
在构建我们的 SWE-bench 代理时，我们实际上花在优化工具上的时间比整体提示词还要多。例如，我们发现代理离开根目录后，使用相对文件路径的工具会导致模型出错。为了解决这个问题，我们将工具改为始终要求绝对文件路径——我们发现模型完美地使用了这种方法。