---
标题: "The \"think\" tool: Enabling Claude to stop and think"
链接: "https://www.anthropic.com/engineering/claude-think-tool"
作者: "[[@AnthropicAI]]"
创建时间: "2025-04-29T15:32:52+08:00"
摘要: "Anthropic 开发了一种名为“思考”工具的新方法，显著提升了 Claude 在复杂工具使用场景中的问题解决能力。"
tags:
  - "clippings"
  - "AI"
  - "工具使用"
  - "复杂问题解决"
  - "性能优化"
  - "编程"
字数: "2375"
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

As we continue to enhance Claude's complex problem-solving abilities, we've discovered a particularly effective approach: a "think" tool that creates dedicated space for structured thinking during complex tasks.  
随着我们继续提升 Claude 解决复杂问题的能力，我们发现了一种特别有效的方法：一个在复杂任务中创建专用结构化思考空间的“思考”工具。

This simple yet powerful technique—which, as we’ll explain below, is different from Claude’s new “ [extended thinking](https://www.anthropic.com/research/visible-extended-thinking) ” capability—has resulted in remarkable improvements in Claude's agentic tool use ability. This includes following policies, making consistent decisions, and handling multi-step problems, all with minimal implementation overhead.  
这种简单而强大的技术——正如我们下面将要解释的，它与 Claude 的新“扩展思考”功能不同——在 Claude 的代理工具使用能力方面带来了显著改进。这包括遵循策略、做出一致的决定以及处理多步问题，所有这些都可以以最小的实施开销实现。

In this post, we'll explore how to implement the “think” tool on different applications, sharing practical guidance for developers based on verified benchmark results.  
在本文中，我们将探讨如何在不同应用中实现“思考”工具，分享基于验证的基准测试结果的开发者实用指南。

### What is the "think" tool?什么是“思考”工具？

With the "think" tool, we're giving Claude the ability to include an additional thinking step—complete with its own designated space—as part of getting to its final answer.  
使用“思考”工具，我们赋予 Claude 在得出最终答案的过程中包含一个额外的思考步骤——并为其分配一个专门的空间。

While it sounds similar to extended thinking, it's a different concept. Extended thinking is all about what Claude does before it starts generating a response. With extended thinking, Claude deeply considers and iterates on its plan before taking action. The "think" tool is for Claude, once it starts generating a response, to add a step to stop and think about whether it has all the information it needs to move forward. This is particularly helpful when performing long chains of tool calls or in long multi-step conversations with the user.  
虽然听起来与扩展思考类似，但这是一个不同的概念。扩展思考主要关注 Claude 在开始生成回复之前所做的一切。使用扩展思考，Claude 会深入考虑并迭代其计划，然后再采取行动。而“思考”工具则是为了在 Claude 开始生成回复后，增加一个步骤来思考是否拥有继续前进所需的所有信息。这在执行长链工具调用或与用户进行长多步对话时尤其有用。

This makes the “think” tool more suitable for cases where Claude does not have all the information needed to formulate its response from the user query alone, and where it needs to process external information (e.g. information in tool call results). The reasoning Claude performs with the “think” tool is less comprehensive than what can be obtained with extended thinking, and is more focused on *new* information that the model discovers.  
这使得“思考”工具更适合于 Claude 无法仅从用户查询中获取所需信息来制定其响应的情况，以及需要处理外部信息（例如工具调用结果中的信息）的情况。Claude 使用“思考”工具进行的推理不如扩展思维全面，更侧重于模型发现的新信息。

We recommend using extended thinking for simpler tool use scenarios like non-sequential tool calls or straightforward instruction following. Extended thinking is also useful for use cases, like coding, math, and physics, when you don’t need Claude to call tools. The “think” tool is better suited for when Claude needs to call complex tools, analyze tool outputs carefully in long chains of tool calls, navigate policy-heavy environments with detailed guidelines, or make sequential decisions where each step builds on previous ones and mistakes are costly.  
我们建议在非顺序工具调用或直接指令遵循等简单的工具使用场景中使用扩展思维。扩展思维在编码、数学和物理学等不需要 Claude 调用工具的使用案例中也很有用。当 Claude 需要调用复杂工具、仔细分析工具调用长链中的输出、在具有详细指南的政策密集型环境中导航或进行需要每个步骤都建立在之前步骤之上且错误代价高昂的顺序决策时，“思考”工具更为合适。

Here's a sample implementation using the standard tool specification format that comes from [τ-Bench](https://arxiv.org/abs/2406.12045):  
下面是一个使用来自τ-Bench 的标准工具规范格式的示例实现：

```
{
  "name": "think",
  "description": "Use the tool to think about something. It will not obtain new information or change the database, but just append the thought to the log. Use it when complex reasoning or some cache memory is needed.",
  "input_schema": {
    "type": "object",
    "properties": {
      "thought": {
        "type": "string",
        "description": "A thought to think about."
      }
    },
    "required": ["thought"]
  }
}
```

### Performance on τ-Bench τ-Bench 性能

We evaluated the "think" tool using τ-bench (tau-bench), a comprehensive benchmark designed to test a model’s ability to use tools in realistic customer service scenarios, where the "think" tool is part of the evaluation’s standard environment.  
我们使用τ-bench（tau-bench）评估了“思考”工具，τ-bench 是一个综合基准，旨在测试模型在现实客户服务场景中使用工具的能力，其中“思考”工具是评估标准环境的一部分。

τ-bench evaluates Claude's ability to:  
τ-bench 评估 Claude 的能力：

- Navigate realistic conversations with simulated users  
	与模拟用户进行现实对话的导航
- Follow complex customer service agent policy guidelines consistently  
	一致地遵循复杂的客户服务代理政策指南
- Use a variety of tools to access and manipulate the environment database  
	使用各种工具访问和操作环境数据库

The primary evaluation metric used in τ-bench is pass^ *k*, which measures the probability that all *k* independent task trials are successful for a given task, averaged across all tasks. Unlike the pass@ *k* metric that is common for other LLM evaluations (which measures if at least one of *k* trials succeeds), pass^ *k* evaluates consistency and reliability—critical qualities for customer service applications where consistent adherence to policies is essential.  
τ-bench 中使用的首要评估指标是 pass^k，它衡量的是对于给定任务，所有 k 个独立任务试验成功的概率，平均分布在所有任务上。与常见于其他 LLM 评估的 pass@k 指标（衡量至少有一个 k 个试验成功）不同，pass^k 评估的是一致性和可靠性——这对于客户服务应用中政策一致遵守至关重要的品质。

#### Performance Analysis 性能分析

Our evaluation compared several different configurations:  
我们的评估比较了几个不同的配置：

1. Baseline (no "think" tool, no extended thinking mode)  
	基准（无“思考”工具，无扩展思考模式）
2. Extended thinking mode alone  
	仅扩展思考模式
3. "Think" tool alone "思考"工具单独使用
4. "Think" tool with optimized prompt (for airline domain)  
	"思考"工具与优化后的提示（针对航空领域）

The results showed dramatic improvements when Claude 3.7 effectively used the "think" tool in both the “airline” and “retail” customer service domains of the benchmark:  
结果显示，当 Claude 3.7 在基准测试的“航空”和“零售”客户服务领域有效使用"思考"工具时，效果显著提升：

- **Airline domain**: The "think" tool with an optimized prompt achieved 0.570 on the pass^1 metric, compared to just 0.370 for the baseline—a 54% relative improvement;  
	"Airline"领域：使用优化提示的"think"工具在 pass^1 指标上达到了 0.570，而基线仅为 0.370，相对提高了 54%；
- **Retail domain**: The "think" tool alone achieves 0.812, compared to 0.783 for the baseline.  
	零售领域：仅“思考”工具就达到了 0.812，而基线为 0.783。

![A line graph showing the performance of Claude 3.7 Sonnet on the "airline" domain of the Tau-Bench eval](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2Fff91e5c84be59ae71306bcc60adba9affed86484-2200x1300.jpg&w=3840&q=75)

Claude 3.7 Sonnet's performance on the "airline" domain of the Tau-Bench eval under four different configurations. Claude 3.7 Sonnet 在 Tau-Bench 评估的"airline"领域，在四种不同配置下的性能

Claude 3.7 Sonnet's performance on the "Airline" domain of the Tau-Bench eval  
Claude 3.7 Sonnet 在 Tau-Bench 评估的"Airline"领域的性能

| Configuration 配置 | *k* =1 | *k* =2 | *k* =3 | *k* =4 | *k* =5 |
| --- | --- | --- | --- | --- | --- |
| "Think" + Prompt "Think" + 提示 | 0.584 | 0.444 | 0.384 | 0.356 | 0.340 |
| "Think" 思考 | 0.404 | 0.254 | 0.186 | 0.140 | 0.100 |
| Extended thinking 扩展思考 | 0.412 | 0.290 | 0.232 | 0.192 | 0.160 |
| Baseline 基准 | 0.332 | 0.206 | 0.148 | 0.116 | 0.100 |

Evaluation results across four different configurations. Scores are proportions.  
四种不同配置下的评估结果。分数为比例。

The best performance in the airline domain was achieved by pairing the “think” tool with an optimized prompt that gives examples of the type of reasoning approaches to use when analyzing customer requests. Below is an example of the optimized prompt:  
在航空领域，通过将“思考”工具与一个优化后的提示相结合，该提示提供了在分析客户请求时使用推理方法的示例，实现了最佳性能。以下是一个优化后的提示示例：

```
## Using the think tool

Before taking any action or responding to the user after receiving tool results, use the think tool as a scratchpad to:
- List the specific rules that apply to the current request
- Check if all required information is collected
- Verify that the planned action complies with all policies
- Iterate over tool results for correctness 

Here are some examples of what to iterate over inside the think tool:
<think_tool_example_1>
User wants to cancel flight ABC123
- Need to verify: user ID, reservation ID, reason
- Check cancellation rules:
  * Is it within 24h of booking?
  * If not, check ticket class and insurance
- Verify no segments flown or are in the past
- Plan: collect missing info, verify rules, get confirmation
</think_tool_example_1>

<think_tool_example_2>
User wants to book 3 tickets to NYC with 2 checked bags each
- Need user ID to check:
  * Membership tier for baggage allowance
  * Which payments methods exist in profile
- Baggage calculation:
  * Economy class × 3 passengers
  * If regular member: 1 free bag each → 3 extra bags = $150
  * If silver member: 2 free bags each → 0 extra bags = $0
  * If gold member: 3 free bags each → 0 extra bags = $0
- Payment rules to verify:
  * Max 1 travel certificate, 1 credit card, 3 gift cards
  * All payment methods must be in profile
  * Travel certificate remainder goes to waste
- Plan:
1. Get user ID
2. Verify membership level for bag fees
3. Check which payment methods in profile and if their combination is allowed
4. Calculate total: ticket price + any bag fees
5. Get explicit confirmation for booking
</think_tool_example_2>
```

What's particularly interesting is how the different approaches compared. Using the “think” tool with the optimized prompt achieved significantly better results over extended thinking mode (which showed similar performance to the unprompted “think” tool). Using the "think" tool alone (without prompting) improved performance over baseline, but still fell short of the optimized approach.  
尤其有趣的是比较不同的方法。使用“思考”工具与优化后的提示词相比，在扩展思考模式下取得了显著更好的结果（扩展思考模式的表现与未提示的“思考”工具相似）。仅使用“思考”工具（不进行提示）比基线性能有所提高，但仍然低于优化方法。

The combination of the "think" tool with optimized prompting delivered the strongest performance by a significant margin, likely due to the high complexity of the [airline policy](https://github.com/sierra-research/tau-bench/blob/main/tau_bench/envs/airline/wiki.md) part of the benchmark, where the model benefitted the most from being given examples of how to “think.”  
将“思考”工具与优化后的提示词结合使用，以显著的优势提供了最强的性能，这可能是由于基准测试中航空公司政策部分的复杂性较高，模型从被给出如何“思考”的示例中受益最大。

In the retail domain, we also tested various configurations to understand the specific impact of each approach  
在零售领域，我们也测试了各种配置，以了解每种方法的具体影响。

![Line graph showing the performance of Claude 3.7 Sonnet on the "retail" domain of the Tau-Bench eval](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F5819616b4cc109d30f1a7d47ec8a32a6b839637b-7638x4513.jpg&w=3840&q=75)

Performance of Claude 3.7 Sonnet on the "retail" domain of the Tau-Bench eval under three different configurations. 在 Tau-Bench 评估的“零售”领域，Claude 3.7 Sonnet 在三种不同配置下的性能表现。

Claude 3.7 Sonnet's performance on the "Retail" domain of the Tau-Bench eval  
Claude 3.7 Sonnet 在 Tau-Bench 评估“零售”领域的表现

| Configuration 配置 | *k* =1 | *k* =2 | *k* =3 | *k* =4 | *k* =5 |
| --- | --- | --- | --- | --- | --- |
| "Think" + no prompt "思考" + 无提示 | 0.812 | 0.735 | 0.685 | 0.650 | 0.626 |
| Extended thinking 扩展思考 | 0.770 | 0.681 | 0.623 | 0.581 | 0.548 |
| Baseline 基准 | 0.783 | 0.695 | 0.643 | 0.607 | 0.583 |

Evaluation results across three different configurations. Scores are proportions.  
在三种不同配置下的评估结果。分数为比例。

The "think" tool achieved the highest pass^1 score of 0.812 even without additional prompting. The [retail policy](https://github.com/sierra-research/tau-bench/blob/main/tau_bench/envs/retail/wiki.md) is noticeably easier to navigate compared to the airline domain, and Claude was able to improve just by having a space to think without further guidance.  
即使没有额外的提示，“思考”工具也实现了最高的通过率^1，达到了 0.812。与航空领域相比，零售政策明显更容易导航，Claude 仅仅通过有一个思考的空间就能在没有进一步指导的情况下进行改进。

#### Key Insights from τ-Bench Analysisτ-Bench 分析的关键见解

Our detailed analysis revealed several patterns that can help you implement the "think" tool effectively:  
我们详细的分析揭示了几个有助于您有效实施“思考”工具的模式：

1. **Prompting matters significantly on difficult domains**. Simply making the "think" tool available might improve performance somewhat, but pairing it with optimized prompting yielded dramatically better results for difficult domains. However, easier domains may benefit from simply having access to “think.”  
	在困难领域，提示至关重要。仅仅使“思考”工具可用可能会在一定程度上提高性能，但与优化的提示相结合，在困难领域取得了显著更好的结果。然而，对于容易的领域，仅仅能够访问“思考”可能就足够了。
2. **Improved consistency across trials**. The improvements from using “think” were maintained for pass^k up to k=5, indicating that the tool helped Claude handle edge cases and unusual scenarios more effectively.  
	提高了试验的一致性。使用“思考”带来的改进在 pass^k 至 k=5 时仍然保持，这表明该工具有助于 Claude 更有效地处理边缘情况和异常情况。

### Performance on SWE-Bench SWE-Bench 上的性能

A similar “think” tool was added to our SWE-bench setup when evaluating Claude 3.7 Sonnet, contributing to the achieved state-of-the-art score of 0.623. The adapted “think” tool definition is given below:  
在评估 Claude 3.7 Sonnet 时，我们向 SWE-bench 设置中添加了一个类似的“思考”工具，这有助于实现 0.623 的当前最佳成绩。下面给出了修改后的“思考”工具定义：

```
{
  "name": "think",
  "description": "Use the tool to think about something. It will not obtain new information or make any changes to the repository, but just log the thought. Use it when complex reasoning or brainstorming is needed. For example, if you explore the repo and discover the source of a bug, call this tool to brainstorm several unique ways of fixing the bug, and assess which change(s) are likely to be simplest and most effective. Alternatively, if you receive some test results, call this tool to brainstorm ways to fix the failing tests.",
  "input_schema": {
    "type": "object",
    "properties": {
      "thought": {
        "type": "string",
        "description": "Your thoughts."
      }
    },
    "required": ["thought"]
  }
}
```

Our experiments (*n* =30 samples with "think" tool, *n* =144 samples without) showed the isolated effects of including this tool improved performance by 1.6% on average (Welch's *t* -test: *t* (38.89) = 6.71, *p* <.001, *d* = 1.47).  
我们的实验（包含“思考”工具的样本 n=30，不包含的样本 n=144）显示，包含此工具的孤立效应平均提高了 1.6%的性能（Welch 的 t 检验：t(38.89) = 6.71，p <.001，d = 1.47）。

### When to use the "think" tool何时使用“思考”工具

Based on these evaluation results, we've identified specific scenarios where Claude benefits most from the "think" tool:  
基于这些评估结果，我们已确定 Claude 在以下特定场景中从“思考”工具中获益最大：

1. **Tool output analysis.** When Claude needs to carefully process the output of previous tool calls before acting and might need to backtrack in its approach;  
	工具输出分析。当 Claude 需要仔细处理之前工具调用的输出并在行动前可能需要回溯其方法时；
2. **Policy-heavy environments**. When Claude needs to follow detailed guidelines and verify compliance; and  
	政策导向的环境。当 Claude 需要遵循详细指南并验证合规性时；
3. **Sequential decision making**. When each action builds on previous ones and mistakes are costly (often found in multi-step domains).  
	顺序决策。当每个行动都建立在之前的基础上，且错误代价高昂（通常出现在多步骤领域）。

## Implementation best practices

To get the most out of the "think" tool with Claude, we recommend the following implementation practices based on our τ-bench experiments.

#### 1\. Strategic prompting with domain-specific examples

The most effective approach is to provide clear instructions on when and how to use the "think" tool, such as the one used for the τ-bench airline domain. Providing examples tailored to your specific use case significantly improves how effectively the model uses the "think" tool:

- The level of detail expected in the reasoning process;
- How to break down complex instructions into actionable steps;
- Decision trees for handling common scenarios; and
- How to check if all necessary information has been collected.

#### 2\. Place complex guidance in the system prompt

We found that, when they were long and/or complex, including instructions about the "think" tool in the system prompt was more effective than placing them in the tool description itself. This approach provides broader context and helps the model better integrate the thinking process into its overall behavior.

### When not to use the "think" tool

Whereas the “think” tool can offer substantial improvements, it is not applicable to all tool use use cases, and does come at the cost of increased prompt length and output tokens. Specifically, we have found the “think” tool does not offer any improvements in the following use cases:

1. **Non-sequential tool calls**. If Claude only needs to make a single tool call or multiple parallel calls to complete a task, there is unlikely to be any improvements from adding in “think.”
2. **Simple instruction following**. When there are not many constraints to which Claude needs to adhere, and its default behaviour is good enough, there are unlikely to be gains from additional “think”-ing.

### Getting started

The "think" tool is a straightforward addition to your Claude implementation that can yield meaningful improvements in just a few steps:

1. **Test with agentic tool use scenarios.** Start with challenging use cases—ones where Claude currently struggles with policy compliance or complex reasoning in long tool call chains.
2. **Add the tool definition**. Implement a "think" tool customized to your domain. It requires minimal code but enables more structured reasoning. Also consider including instructions on when and how to use the tool, with examples relevant to your domain to the system prompt.
3. **Monitor and refine**. Watch how Claude uses the tool in practice, and adjust your prompts to encourage more effective thinking patterns.

The best part is that adding this tool has minimal downside in terms of performance outcomes. It doesn't change external behavior unless Claude decides to use it, and doesn't interfere with your existing tools or workflows.

### Conclusion

Our research has demonstrated that the "think" tool can significantly enhance Claude 3.7 Sonnet's performance <sup>1</sup> on complex tasks requiring policy adherence and reasoning in long chains of tool calls. “Think” is not a one-size-fits-all solution, but it offers substantial benefits for the correct use cases, all with minimal implementation complexity.

We look forward to seeing how you'll use the "think" tool to build more capable, reliable, and transparent AI systems with Claude.

1\. While our τ-Bench results focused on the improvement of Claude 3.7 Sonnet with the “think” tool, our experiments show Claude 3.5 Sonnet (New) is also able to achieve performance gains with the same configuration as 3.7 Sonnet, indicating that this improvement generalizes to other Claude models as well.