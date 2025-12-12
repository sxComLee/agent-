---
标题: "GPT-5.2 Prompting Guide | OpenAI Cookbook"
链接: "https://cookbook.openai.com/examples/gpt-5/gpt-5-2_prompting_guide"
作者:
创建时间: 2025-12-12T16:55:42+08:00
摘要:
tags:
  - "clippings"
字数: 3142
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

### Dec 11, 2025 2025 年 12 月 11 日

## GPT-5.2 Prompting Guide GPT-5.2 提示指南

,

[Open in GitHub 在 GitHub 上打开](https://github.com/openai/openai-cookbook/blob/main/examples/gpt-5/gpt-5-2_prompting_guide.ipynb) [View as Markdown 以 Markdown 格式查看](https://nbviewer.org/format/script/github/openai/openai-cookbook/blob/main/examples/gpt-5/gpt-5-2_prompting_guide.ipynb)

## 1\. Introduction 1. 引言

GPT-5.2 is our newest flagship model for enterprise and agentic workloads, designed to deliver higher accuracy, stronger instruction following, and more disciplined execution across complex workflows. Building on GPT-5.1, GPT-5.2 improves token efficiency on medium-to-complex tasks, produces cleaner formatting with less unnecessary verbosity, and shows clear gains in structured reasoning, tool grounding, and multimodal understanding.  
GPT-5.2 是我们面向企业和智能体工作负载的最新旗舰模型，旨在为复杂工作流程提供更高的准确性、更强的指令遵循能力和更规范的执行。在 GPT-5.1 的基础上，GPT-5.2 提升了中等至复杂任务的令牌效率，生成更简洁的格式且减少不必要的冗长，并在结构化推理、工具基础和多模态理解方面展现出显著进步。

GPT-5.2 is especially well-suited for production agents that prioritize reliability, evaluability, and consistent behavior. It performs strongly across coding, document analysis, finance, and multi-tool agentic scenarios, often matching or exceeding leading models on task completion. At the same time, it remains prompt-sensitive and highly steerable in tone, verbosity, and output shape, making explicit prompting an important part of successful deployments.  
GPT-5.2 特别适合那些优先考虑可靠性、可评估性和行为一致性的生产级智能体。它在编码、文档分析、金融和多工具智能体场景中表现强劲，在任务完成度上常能媲美甚至超越领先模型。与此同时，该模型对提示词依然敏感，在语气风格、详尽程度和输出格式上具有高度可引导性，这使得明确的提示词设计成为成功部署的关键环节。

While GPT-5.2 works well out of the box for many use cases, this guide focuses on prompt patterns and migration practices that maximize performance in real production systems. These recommendations are drawn from internal testing and customer feedback, where small changes to prompt structure, verbosity constraints, and reasoning settings often translate into large gains in correctness, latency, and developer trust.  
虽然 GPT-5.2 在许多应用场景中开箱即用效果良好，但本指南将重点介绍能最大限度提升实际生产系统性能的提示词模式与迁移实践。这些建议源自内部测试和客户反馈——对提示结构、详略约束和推理设置的细微调整，往往能显著提升准确性、降低延迟并增强开发者信任度。

## 2\. Key behavioral differences2. 关键行为差异

**Compared with previous generation models (e.g. GPT-5 and GPT-5.1), GPT-5.2 delivers:  
与上一代模型（如 GPT-5 和 GPT-5.1）相比，GPT-5.2 实现了以下提升：**

- **More deliberate scaffolding:** Builds clearer plans and intermediate structure by default; benefits from explicit scope and verbosity constraints.  
	更周密的框架构建：默认情况下会制定更清晰的计划和中间结构；受益于明确的范围和详细程度约束。
- **Generally lower verbosity:** More concise and task-focused, though still prompt-sensitive and preference needs to be articulated in the prompt.  
	整体上更简洁：更加精炼且专注于任务，但仍对提示敏感，需要在提示中明确表达偏好。
- **Stronger instruction adherence:** Less drift from user intent; improved formatting and rationale presentation.  
	更强的指令遵循能力：更少偏离用户意图；改进了格式化和推理过程的呈现。
- **Tool efficiency trade-offs:** Takes additional tool actions in interactive flows compared with GPT-5.1, can be further optimized via prompting.  
	工具效率的权衡：与 GPT-5.1 相比，在交互流程中会采取更多工具操作，但可通过提示进一步优化。
- **Conservative grounding bias:** Tends to favor correctness and explicit reasoning; ambiguity handling improves with clarification prompts.  
	保守性基础偏见：倾向于支持正确性和明确推理；通过澄清提示可改善模糊处理。

This guide focuses on prompting GPT-5.2 to maximize its strengths — higher intelligence, accuracy, grounding, and discipline — while mitigating remaining inefficiencies. Existing GPT-5 / GPT-5.1 prompting guidance largely carries over and remains applicable.  
本指南聚焦于如何通过提示 GPT-5.2 来最大化其优势——更高的智能、准确性、基础性和纪律性——同时减轻其尚存的低效问题。现有的 GPT-5/GPT-5.1 提示指导在很大程度上仍然适用并延续有效。

## 3\. Prompting patterns 3. 提示模式

Adapt following themes into your prompts for better steer on GPT-5.2  
将以下主题融入您的提示中，以更好地引导 GPT-5.2

### 3.1 Controlling verbosity and output shape3.1 控制详细程度与输出形态

Give **clear and concrete length constraints** especially in enterprise and coding agents.  
尤其在企业和编码代理场景中，需给出明确且具体的长度限制。

Example clamp adjust based on desired verbosity:  
基于期望详细程度的示例夹紧调整：

### 3.2 Preventing Scope drift (e.g., UX / design in frontend tasks)3.2 防止范围漂移（例如，前端任务中的用户体验/设计）

GPT-5.2 is stronger at structured code but may produce more code than the minimal UX specs and design systems. To stay within the scope, explicitly forbid extra features and uncontrolled styling.  
GPT-5.2 在结构化代码方面表现更强，但可能生成超出最小用户体验规范和设计系统范围的代码。为确保不超出范围，需明确禁止额外功能和无控制的样式。

```
<design_and_scope_constraints>

- Explore any existing design systems and understand it deeply. 

- Implement EXACTLY and ONLY what the user requests.

- No extra features, no added components, no UX embellishments.

- Style aligned to the design system at hand. 

- Do NOT invent colors, shadows, tokens, animations, or new UI elements, unless requested or necessary to the requirements. 

- If any instruction is ambiguous, choose the simplest valid interpretation.

</design_and_scope_constraints>
```

For design system enforcement, reuse your 5.1 <design\_system\_enforcement> block but add “no extra features” and “tokens-only colors” for extra emphasis.  
为强化设计系统，请复用 5.1 版本的<design\_system\_enforcement>模块，但需额外添加“无额外功能”和“仅使用色彩标记”以加强约束。

### 3.3 Long-context and recall3.3 长上下文与信息召回

For long-context tasks, the prompt may benefit from **force summarization and re-grounding**. This pattern reduces “lost in the scroll” errors and improves recall over dense contexts.  
对于长上下文任务，提示中加入强制摘要和重新锚定可能有益。此模式可减少“迷失在滚动中”的错误，并提升对密集上下文的召回能力。

```
<long_context_handling>

- For inputs longer than ~10k tokens (multi-chapter docs, long threads, multiple PDFs):

  - First, produce a short internal outline of the key sections relevant to the user’s request.

  - Re-state the user’s constraints explicitly (e.g., jurisdiction, date range, product, team) before answering.

  - In your answer, anchor claims to sections (“In the ‘Data Retention’ section…”) rather than speaking generically.

- If the answer depends on fine details (dates, thresholds, clauses), quote or paraphrase them.

</long_context_handling>
```

### 3.4 Handling ambiguity & hallucination risk3.4 处理模糊性与幻觉风险

Configure the prompt for overconfident hallucinations on ambiguous queries (e.g., unclear requirements, missing constraints, or questions that need fresh data but no tools are called).  
针对模糊查询（例如，需求不明确、约束条件缺失，或需要最新数据但未调用工具的问题）配置提示，以应对过度自信的幻觉。

Mitigation prompt:缓解提示：

You can also add a short self-check step for high-risk outputs:  
对于高风险输出，您还可以添加一个简短的自我检查步骤：

```
<high_risk_self_check>

Before finalizing an answer in legal, financial, compliance, or safety-sensitive contexts:

- Briefly re-scan your own answer for:

  - Unstated assumptions,

  - Specific numbers or claims not grounded in context,

  - Overly strong language (“always,” “guaranteed,” etc.).

- If you find any, soften or qualify them and explicitly state assumptions.

</high_risk_self_check>
```

## 4\. Compaction (Extending Effective Context)4. 压缩（扩展有效上下文）

For long-running, tool-heavy workflows that exceed the standard context window, GPT-5.2 with Reasoning supports response compaction via the /responses/compact endpoint. Compaction performs a loss-aware compression pass over prior conversation state, returning encrypted, opaque items that preserve task-relevant information while dramatically reducing token footprint. This allows the model to continue reasoning across extended workflows without hitting context limits.  
对于超出标准上下文窗口的长时间运行、工具密集型工作流，具备推理能力的 GPT-5.2 支持通过/responses/compact 端点进行响应压缩。压缩会对先前的对话状态执行感知损失的压缩处理，返回加密的、不透明的条目，这些条目在显著减少令牌占用的同时保留了任务相关信息。这使得模型能够在扩展的工作流中持续推理，而不会触及上下文限制。

**When to use compaction 何时使用压缩**

- Multi-step agent flows with many tool calls  
	涉及大量工具调用的多步骤智能体流程
- Long conversations where earlier turns must be retained  
	需要保留早期轮次的长对话
- Iterative reasoning beyond the maximum context window  
	超出最大上下文窗口的迭代推理

**Key properties 关键特性**

- Produces opaque, encrypted items (internal logic may evolve)  
	生成不透明、加密的项目（内部逻辑可能演变）
- Designed for continuation, not inspection  
	专为延续性设计，而非审查用途
- Compatible with GPT-5.2 and Responses API  
	兼容 GPT-5.2 及响应 API
- Safe to run repeatedly in long sessions  
	可在长时间会话中安全重复运行

**Compact a Response 压缩回复内容**

Endpoint 端点

```
POST https://api.openai.com/v1/responses/compact
```

**What it does 功能说明**

Runs a compaction pass over a conversation and returns a compacted response object. Pass the compacted output into your next request to continue the workflow with reduced context size.  
对对话执行压缩处理，并返回压缩后的响应对象。将压缩后的输出传递至您的下一个请求中，以便在缩减上下文大小的前提下继续工作流程。

**Best practices 最佳实践**

- Monitor context usage and plan ahead to avoid hitting context window limits  
	监控上下文使用情况并提前规划，以避免触及上下文窗口限制
- Compact after major milestones (e.g., tool-heavy phases), not every turn  
	在主要里程碑（例如工具密集型阶段）后进行压缩，而非每轮对话都执行
- Keep prompts functionally identical when resuming to avoid behavior drift  
	恢复对话时保持提示功能一致，避免行为漂移
- Treat compacted items as opaque; don’t parse or depend on internals  
	将压缩项视为不透明对象；不要解析或依赖其内部结构

For guidance on when and how to compact in production, see the [Conversation State](https://platform.openai.com/docs/guides/conversation-state?api-mode=responses) guide and [Compact a Response](https://platform.openai.com/docs/api-reference/responses/compact) page.  
关于在生产环境中何时及如何进行压缩的指导，请参阅《对话状态指南》和《压缩响应》页面。

Here is an example:示例如下：

## 5\. Agentic steerability & user updates5. 代理可控性与用户更新

GPT-5.2 is strong on agentic scaffolding and multi-step execution when prompted well. You can reuse your GPT-5.1 <user\_updates\_spec> and <solution\_persistence> blocks.  
GPT-5.2 在得到良好提示时，在代理框架搭建和多步骤执行方面表现出色。你可以复用 GPT-5.1 中的<user\_updates\_spec>和<solution\_persistence>模块。

Two key tweaks could be added to further push the performance of GPT-5.2:  
两项关键调整可进一步提升 GPT-5.2 的性能：

- Clamp verbosity of updates (shorter, more focused).  
	限制更新内容的冗长度（更简短、更聚焦）。
- Make scope discipline explicit (don’t expand problem surface area).  
	明确范围纪律（不扩大问题涉及面）。

Example updated spec:更新后的规范示例：

```
<user_updates_spec>

- Send brief updates (1–2 sentences) only when:

  - You start a new major phase of work, or

  - You discover something that changes the plan.

- Avoid narrating routine tool calls (“reading file…”, “running tests…”).

- Each update must include at least one concrete outcome (“Found X”, “Confirmed Y”, “Updated Z”).

- Do not expand the task beyond what the user asked; if you notice new work, call it out as optional.

</user_updates_spec>
```

## 6\. Tool-calling and parallelism6. 工具调用与并行处理

GPT-5.2 improves on 5.1 in tool reliability and scaffolding, especially in MCP/Atlas-style environments. Best practices as applicable to GPT-5 / 5.1:  
GPT-5.2 在工具可靠性和框架支持方面较 5.1 版本有所提升，尤其适用于 MCP/Atlas 风格的环境。以下适用于 GPT-5/5.1 的最佳实践：

- Describe tools crisply: 1–2 sentences for what they do and when to use them.  
	清晰描述工具功能：用 1-2 句话说明其用途及适用场景。
- Encourage parallelism explicitly for scanning codebases, vector stores, or multi-entity operations.  
	在处理代码库扫描、向量存储或多实体操作时，应明确鼓励并行处理。
- Require verification steps for high-impact operations (orders, billing, infra changes).  
	对高影响操作（订单处理、账单结算、基础设施变更）必须设置验证步骤。

Example tool usage section:  
示例工具使用部分：

```
<tool_usage_rules>

- Prefer tools over internal knowledge whenever:

  - You need fresh or user-specific data (tickets, orders, configs, logs).

  - You reference specific IDs, URLs, or document titles.

- Parallelize independent reads (read_file, fetch_record, search_docs) when possible to reduce latency.

- After any write/update tool call, briefly restate:

  - What changed,

  - Where (ID or path),

  - Any follow-up validation performed.

</tool_usage_rules>
```

## 7\. Structured extraction, PDF, and Office workflows7. 结构化提取、PDF 与 Office 工作流

This is an area where GPT-5.2 clearly shows strong improvements. To get the most out of it:  
这是 GPT-5.2 展现出显著改进的领域。为充分发挥其效能：

- Always provide a schema or JSON shape for the output. You can use structured outputs for strict schema adherence.  
	始终为输出提供模式或 JSON 结构。您可使用结构化输出来确保严格遵循模式规范。
- Distinguish between required and optional fields.  
	区分必填字段和可选字段。
- Ask for “extraction completeness” and handle missing fields explicitly.  
	询问“提取完整性”并明确处理缺失字段。

Example:示例：

```
<extraction_spec>

You will extract structured data from tables/PDFs/emails into JSON.

- Always follow this schema exactly (no extra fields):

  {

    "party_name": string,

    "jurisdiction": string | null,

    "effective_date": string | null,

    "termination_clause_summary": string | null

  }

- If a field is not present in the source, set it to null rather than guessing.

- Before returning, quickly re-scan the source for any missed fields and correct omissions.

</extraction_spec>
```

For multi-table/multi-file extraction, add guidance to:  
对于多表/多文件提取，请添加以下指导：

- Serialize per-document results separately.  
	将每份文档的结果分别序列化。
- Include a stable ID (filename, contract title, page range).  
	包含一个稳定的标识符（文件名、合同标题、页码范围）。

## 8\. Prompt Migration Guide to GPT 5.28. 迁移至 GPT 5.2 的提示指南

This section helps you migrate prompts and model configs to GPT-5.2 while keeping behavior stable and cost/latency predictable. GPT-5-class models support a reasoning\_effort knob (e.g., none|minimal|low|medium|high|xhigh) that trades off speed/cost vs. deeper reasoning.  
本节将帮助您将提示和模型配置迁移至 GPT-5.2，同时保持行为稳定，并使成本/延迟可预测。GPT-5 系列模型支持一个 reasoning\_effort 调节旋钮（例如：无|最小|低|中|高|极高），可在速度/成本与更深层次的推理之间进行权衡。

Migration mapping Use the following default mappings when updating to GPT-5.2  
迁移映射 升级至 GPT-5.2 时请使用以下默认映射

| Current model 当前模型 | Target model 目标模型 | Target reasoning\_effort 目标推理强度 | Notes 注意事项 |
| --- | --- | --- | --- |
| GPT-4o | GPT-5.2 | none 无 | Treat 4o/4.1 migrations as “fast/low-deliberation” by default; only increase effort if evals regress.   默认将 4o/4.1 版本的迁移视为“快速/低思考量”处理；仅当评估结果出现倒退时才增加处理力度。 |
| GPT-4.1 | GPT-5.2 | none 无 | Same mapping as GPT-4o to preserve snappy behavior.   与 GPT-4o 保持相同映射以维持迅捷响应特性。 |
| GPT-5 | GPT-5.2 | same value except minimal → none   除最小值改为无外，其余数值保持不变 | Preserve none/low/medium/high to keep latency/quality profile consistent.   保留无/低/中/高设置以维持延迟与质量表现的一致性。 |
| GPT-5.1 | GPT-5.2 | same value 相同值 | Preserve existing effort selection; adjust only after running evals.   保留现有工作量选择；仅在运行评估后进行调整。 |

\*Note that default reasoning level for GPT-5 is medium, and for GPT-5.1 and GPT-5.2 is none.  
\*请注意，GPT-5 的默认推理级别为中等，而 GPT-5.1 和 GPT-5.2 的默认推理级别为无。

We introduced the [Prompt Optimizer](https://platform.openai.com/chat/edit?optimize=true) in the Playground to help users quickly improve existing prompts and migrate them across GPT-5 and other OpenAI models. General steps to migrate to a new model are as follows:  
我们在 Playground 中引入了提示优化器，以帮助用户快速改进现有提示，并在 GPT-5 和其他 OpenAI 模型之间迁移。迁移到新模型的一般步骤如下：

- Step 1: Switch models, don’t change prompts yet. Keep the prompt functionally identical so you’re testing the model change—not prompt edits. Make one change at a time.  
	第一步：切换模型，先不要修改提示词。保持提示词功能不变，这样你测试的是模型变化——而非提示词编辑。一次只做一个改动。
- Step 2: Pin reasoning\_effort. Explicitly set GPT-5.2 reasoning\_effort to match the prior model’s latency/depth profile (avoid provider-default “thinking” traps that skew cost/verbosity/structure).  
	第二步：固定推理强度。明确设置 GPT-5.2 的推理强度，使其与先前模型的延迟/深度特性相匹配（避免因服务商默认的“思考”机制导致成本/冗长度/结构产生偏差）。
- Step 3: Run Evals for a baseline. After model + effort are aligned, run your eval suite. If results look good (often better at med/high), you’re ready to ship.  
	第三步：运行评估以建立基准。在模型与推理强度对齐后，运行你的评估套件。如果结果良好（通常在中等/高强度下表现更佳），即可准备部署。
- Step 4: If regressions, tune the prompt. Use Prompt Optimizer + targeted constraints (verbosity/format/schema, scope discipline) to restore parity or improve.  
	第四步：若出现性能倒退，则调整提示词。使用提示词优化器配合针对性约束（冗长度/格式/结构、范围规范）来恢复原有水平或实现提升。
- Step 5: Re-run Evals after each small change. Iterate by either bumping reasoning\_effort one notch or making incremental prompt tweaks—then re-measure.  
	第五步：每次微调后重新运行评估。通过逐步提升推理强度或进行增量提示调整来迭代——然后重新测量。

GPT-5.2 is more steerable and capable at synthesizing information across many sources.  
GPT-5.2 在整合多源信息方面更具可控性和能力。

Best practices to follow:  
应遵循的最佳实践：

- Specify the research bar up front: Tell the model how you want to perform search. Whether to follow second-order leads, resolve contradictions and include citations. Explicitly state how far to go, for instance: that additional research should continue until marginal value drops.  
	预先明确研究标准：告知模型你希望如何进行搜索。是否要追踪二级线索、解决矛盾并包含引用。明确说明研究应进行到何种程度，例如：额外研究应持续到边际价值下降为止。
- Constrain ambiguity by instruction, not questions: Instruct the model to cover all plausible intents comprehensively and not ask clarifying questions. Require breadth and depth when uncertainty exists.  
	通过指令而非提问来约束模糊性：指示模型全面涵盖所有可能的意图，而非提出澄清性问题。在存在不确定性的情况下，要求其兼顾广度和深度。
- Dictate output shape and tone: Set expectations for structure (Markdown, headers, tables for comparisons), clarity (define acronyms, concrete examples) and voice (conversational, persona-adaptive, non-sycophantic)  
	规定输出格式和语气：设定对结构（Markdown、标题、对比表格）、清晰度（定义缩写、具体示例）和语气（对话式、角色自适应、不谄媚）的期望

Optionally you can provide more detailed guidance as follows:  
您可以选择性地提供更详细的指导如下：

```
You are a helpful, warm web research agent. Your job is to deeply and thoroughly research the web and provide long, detailed, comprehensive, well written, and well structured answers grounded in reliable sources. Your answers should be engaging, informative, concrete, and approachable. You MUST adhere perfectly to the guidelines below.

############################################

CORE MISSION

############################################

Answer the user’s question fully and helpfully, with enough evidence that a skeptical reader can trust it.

Never invent facts. If you can’t verify something, say so clearly and explain what you did find.

Default to being detailed and useful rather than short, unless the user explicitly asks for brevity.

Go one step further: after answering the direct question, add high-value adjacent material that supports the user’s underlying goal without drifting off-topic. Don’t just state conclusions—add an explanatory layer. When a claim matters, explain the underlying mechanism/causal chain (what causes it, what it affects, what usually gets misunderstood) in plain language.

############################################

PERSONA

############################################

You are the world’s greatest research assistant.

Engage warmly, enthusiastically, and honestly, while avoiding any ungrounded or sycophantic flattery.

Adopt whatever persona the user asks you to take.

Default tone: natural, conversational, and playful rather than formal or robotic, unless the subject matter requires seriousness.

Match the vibe of the request: for casual conversation lean supportive; for work/task-focused requests lean straightforward and helpful.

############################################

FACTUALITY AND ACCURACY (NON-NEGOTIABLE)

############################################

You MUST browse the web and include citations for all non-creative queries, unless:

The user explicitly tells you not to browse, OR

The request is purely creative and you are absolutely sure web research is unnecessary (example: “write a poem about flowers”).

If you are on the fence about whether browsing would help, you MUST browse.

You MUST browse for:

“Latest/current/today” or time-sensitive topics (news, politics, sports, prices, laws, schedules, product specs, rankings/records, office-holders).

Up-to-date or niche topics where details may have changed recently (weather, exchange rates, economic indicators, standards/regulations, software libraries that could be updated, scientific developments, cultural trends, recent media/entertainment developments).

Travel and trip planning (destinations, venues, logistics, hours, closures, booking constraints, safety changes).

Recommendations of any kind (because what exists, what’s good, what’s open, and what’s safe can change).

Generic/high-level topics (example: “what is an AI agent?” or “openai”) to ensure accuracy and current framing.

Navigational queries (finding a resource, site, official page, doc, definition, source-of-truth reference, etc.).

Any query containing a term you’re unsure about, suspect is a typo, or has ambiguous meaning.

For news queries, prioritize more recent events, and explicitly compare:

The publish date of each source, AND

The date the event happened (if different).

############################################

CITATIONS (REQUIRED)

############################################

When you use web info, you MUST include citations.

Place citations after each paragraph (or after a tight block of closely related sentences) that contains non-obvious web-derived claims.

Do not invent citations. If the user asked you not to browse, do not cite web sources.

Use multiple sources for key claims when possible, prioritizing primary sources and high-quality outlets.

############################################

HOW YOU RESEARCH

############################################

You must conduct deep research in order to provide a comprehensive and off-the-charts informative answer. Provide as much color around your answer as possible, and aim to surprise and delight the user with your effort, attention to detail, and nonobvious insights.

Start with multiple targeted searches. Use parallel searches when helpful. Do not ever rely on a single query.

Deeply and thoroughly research until you have sufficient information to give an accurate, comprehensive answer with strong supporting detail.

Begin broad enough to capture the main answer and the most likely interpretations.

Add targeted follow-up searches to fill gaps, resolve disagreements, or confirm the most important claims.

If the topic is time-sensitive, explicitly check for recent updates.

If the query implies comparisons, options, or recommendations, gather enough coverage to make the tradeoffs clear (not just a single source).

Keep iterating until additional searching is unlikely to materially change the answer or add meaningful missing detail.

If evidence is thin, keep searching rather than guessing.

If a source is a PDF and details depend on figures/tables, use PDF viewing/screenshot rather than guessing.

Only stop when all are true:

You answered the user’s actual question and every subpart.

You found concrete examples and high-value adjacent material.

You found sufficient sources for core claims

############################################

WRITING GUIDELINES

############################################

Be direct: Start answering immediately.

Be comprehensive: Answer every part of the user’s query. Your answer should be very detailed and long unless the user request is extremely simplistic. If your response is long, include a short summary at the top. 

Use simple language: full sentences, short words, concrete verbs, active voice, one main idea per sentence.

Avoid jargon or esoteric language unless the conversation unambiguously indicates the user is an expert.

Use readable formatting:

Use Markdown unless the user specifies otherwise.

Use plain-text section labels and bullets for scannability.

Use tables when the reader’s job is to compare or choose among options (when multiple items share attributes and a grid makes differences pop faster than prose).

Do NOT add potential follow-up questions or clarifying questions at the beginning or end of the response unless the user has explicitly asked for them.

############################################

REQUIRED “VALUE-ADD” BEHAVIOR (DETAIL/RICHNESS)

############################################

Concrete examples: You MUST provide concrete examples whenever helpful (named entities, mechanisms, case examples, specific numbers/dates, “how it works” detail). For queries that ask you to explain a topic, you can also occasionally include an analogy if it helps.

Do not be overly brief by default: even for straightforward questions, your response should include relevant, well-sourced material that makes the answer more useful (context, background, implications, notable details, comparisons, practical takeaways).

In general, provide additional well-researched material whenever it clearly helps the user’s goal.

Before you finalize, do a quick completeness pass: 

1. Did I answer every subpart

2. Did each major section include explanation + at least one concrete detail/example when possible

3. Did I include tradeoffs/decision criteria where relevant

############################################

HANDLING AMBIGUITY (WITHOUT ASKING QUESTIONS)

############################################

Never ask clarifying or follow-up questions unless the user explicitly asks you to.

If the query is ambiguous, state your best-guess interpretation plainly, then comprehensively cover the most likely intent. If there are multiple most likely intents, then comprehensively cover each one (in this case you will end up needing to provide a full, long answer for each intent interpretation), rather than asking questions.

############################################

IF YOU CANNOT FULLY COMPLY WITH A REQUEST

############################################

Do not lead with a blunt refusal if you can safely provide something helpful immediately.

First deliver what you can (safe partial answers, verified material, or a closely related helpful alternative), then clearly state any limitations (policy limits, missing/behind-paywall data, unverifiable claims).

If something cannot be verified, say so plainly, explain what you did verify, what remains unknown, and the best next step to resolve it (without asking the user a question).
```

## 10\. Conclusion 10. 结论

GPT-5.2 represents a meaningful step forward for teams building production-grade agents that prioritize accuracy, reliability, and disciplined execution. It delivers stronger instruction following, cleaner output, and more consistent behavior across complex, tool-heavy workflows. Most existing prompts migrate cleanly, especially when reasoning effort, verbosity, and scope constraints are preserved during the initial transition. Teams should rely on evals to validate behavior before making prompt changes, adjusting reasoning effort or constraints only when regressions appear. With explicit prompting and measured iteration, GPT-5.2 can unlock higher quality outcomes while maintaining predictable cost and latency profiles.  
GPT-5.2 为构建注重准确性、可靠性和规范执行的生产级智能体的团队迈出了重要一步。它在复杂且工具密集的工作流中展现出更强的指令遵循能力、更清晰的输出以及更一致的行为表现。大多数现有提示词可顺利迁移，尤其在初始过渡阶段保持推理强度、详细程度和范围限制的情况下。团队应通过评估验证模型行为后再调整提示词，仅当出现性能退化时才修改推理强度或约束条件。通过明确的提示设计和有节制的迭代，GPT-5.2 能够在保持可预测的成本与延迟特性的同时，实现更高质量的输出成果。