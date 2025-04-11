---
标题: -Claude think ≠ extended thinking，傻傻分不清？官方教程来了！
链接: https://mp.weixin.qq.com/s/fIWmuNH7XQ0eEqhrjcuifg
作者: "[[JJJohn]]"
创建时间: 2025-04-10T18:03:59+08:00
摘要: 
tags:
  - clippings
  - "#claude_think"
字数: "469"
状态: 结束
---
# [[预读法介绍]]
### 预读问题  
**基于你的目标**：
- Q1: 
- Q2: 
- Q3:   

### 关键图表/代码  
- 如果Claude一开始就有足够信息回答问题，用「extended thinking」就够了
- 如果Claude需要处理外部信息（如工具调用结果），「think」工具就派上用场了
### 初步关联  
- 已知：[[已掌握的相关知识]]  
- 未知：`#待探索`  

### 输出目标
- [ ] 

### 总结
- 是什么
- 为什么
- 怎么用
#review
# 内容
原创 JJJohn *2025年03月22日 10:52* *北京*

**如何让Claude 进行正确的思考？**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF75Giak3sEgmHxNianUZYjRQr9mQlw0Mm9DYTbvN8nZfVFzEbgtxKa5JIibP0ACVvwIe79NW8pia12ibA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Anthropic 发布了一个全新官方博客：Engineering at Anthropic，专门为开发者提供实用建议和最新发现。

文中详细讲解了Claude的「think」工具，让AI能够在复杂任务中 **暂停并思考** ！

![Abstract shapes illustrating Anthropic's Engineering Blog](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnF75Giak3sEgmHxNianUZYjRQu0rDLQKFYGIyLHrHz9S89smZpK2DFTrj84YbbLODYf4718Ga9TaBNg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

而Claude 3.7 Sonnet Thinking 在 LMArena 排行榜上的排名也已公布。该模型在多个类别中表现出色，包括：

- 在风格控制过滤后的总体排名中，Claude 3.7 Sonnet Thinking（thinking-32k）并列第三。
- 在硬提示、数学、指令遵循和长查询等类别中，Claude 3.7 Sonnet Thinking 均位列前五。

可以通过访问 lmarena.ai/leaderboard 查看 Claude 3.7 Sonnet Thinking 在你最关心的类别中的表现。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnF75Giak3sEgmHxNianUZYjRQfL77QNPjJNYgKhgnhCIesw4BLW4d88WE9GoFTPLV2O5rJ2jSOwTZXw/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![Image](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnF75Giak3sEgmHxNianUZYjRQGibKP14ExZUdvBjnpVmicmmm9DdCPp96BGewCK4YP4MRjFLtRPOl3y0Q/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**有开发者看到这个消息，兴奋得睡不着觉：**

> 「这绝对是开发者的宝库！等不及看你们分享的实用知识了。」—— Karen Elysia

> 「太棒了！现在开发者有了获取Claude使用技巧和最新突破的专门场所。喜欢这个想法。」—— Eddie Ho

## 「think」工具是什么？

简单来说，「think」工具就是给Claude创造一个 **专门的思考空间** ，让它能在复杂问题解决过程中进行结构化思考。

这听起来很简单，但效果却出奇地好！

根据Anthropic的测试，这个小工具在Claude的 **代理工具使用能力** 上带来了显著提升，包括：

- 更好地遵循政策
- 做出更一致的决策
- 更有效地处理多步骤问题

最厉害的是，实现这一功能几乎没有什么额外开销！

## 「think」≠「extended thinking」

等等，看到这里，你可能会问： **「think」工具和Claude的「extended thinking」（延伸思考）功能有什么区别？**

别着急，Anthropic已经给出了明确解释：

**「extended thinking」是Claude在开始生成回应前的深度思考** ，就像你在回答问题前先在脑中制定计划。

而 「think」工具是Claude在开始回应后，发现需要更多信息时使用的额外思考步骤 。这特别适用于长链工具调用或多步骤对话场景。

也就是说：

- 如果Claude一开始就有足够信息回答问题，用「extended thinking」就够了
- 如果Claude需要处理外部信息（如工具调用结果），「think」工具就派上用场了

## 性能表现惊人

Anthropic用τ-bench（tau-bench）基准测试了「think」工具的效果，这是一个专门测试模型在真实客服场景中使用工具能力的全面基准。

测试结果：

在 **航空领域** 的测试中，使用优化提示的「think」工具达到了0.570的pass^1分数，比基准线的0.370提高了 **54%** ！

在 **零售领域** 的测试中，即使没有额外提示，仅仅使用「think」工具也达到了0.812的分数，超过了基准线的0.783。

最有趣的是，当「think」工具与优化提示结合时，效果远超单独使用「extended thinking」模式或「think」工具。

## 何时使用「think」工具？

根据测试结果，Anthropic确定了「think」工具最有用的三种场景：

1. **工具输出分析** ：当Claude需要在采取行动前仔细处理之前工具调用的输出，并可能需要回溯其方法
2. **政策密集环境** ：当Claude需要遵循详细指南并验证合规性时
3. **顺序决策制定** ：当每个行动都建立在之前的行动基础上，而且错误代价高昂时

## 最佳实施实践

如何从「think」工具中获得最大提升呢？

Anthropic提供了这些建议：

1. **使用领域特定示例进行战略提示** ：提供清晰指导，说明何时以及如何使用「think」工具
2. **在系统提示中放置复杂指导** ：当指导又长又复杂时，将其放在系统提示中比放在工具描述中更有效

而使用起来只需几个简单步骤：

1. 在代理工具使用场景中测试
2. 添加定制化的工具定义
3. 监控和改进使用效果

最棒的是，添加这个工具几乎没有性能损失。除非Claude决定使用它，否则不会改变外部行为，也不会干扰现有工具或工作流程。

这一更新立即引发了开发者社区的热烈反响：

> 「重大举措。实用见解+Claude=必读。已关注👀」—— Rafael

> 「我只想让下一代Claude在评论中看到我，嗨Claude🥰」—— payraw

**原文译文**

## "think"工具：让Claude停下来思考

Engineering at Anthropic

随着我们持续增强Claude在复杂问题解决方面的能力，我们发现了一种特别有效的方法："think"工具，它在复杂任务中为结构化思考创造了专门的空间。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF75Giak3sEgmHxNianUZYjRQhR0zibS5HyfRDkteUWXejmoTEbv33A4icKRW3bjadChXOUMXraDjmuPg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

这个简单却强大的技术——正如我们将在下文解释的，它与Claude的新extended thinking (https://www.anthropic.com/research/visible-extended-thinking)（延伸思考）功能不同——在Claude的代理工具使用能力方面带来了显著改进。这包括遵循政策、做出一致决策和处理多步骤问题，所有这些都只需最小的实施开销。

在这篇文章中，我们将探讨如何在不同应用程序上实施"think"工具，基于已验证的基准测试结果为开发者提供实用指导。

## 什么是"think"工具？

通过"think"工具，我们给予Claude添加额外思考步骤的能力——包括其自己的专属空间——作为获得最终答案过程的一部分。

虽然听起来与延伸思考类似，但它是一个不同的概念。延伸思考是关于Claude在开始生成回应前所做的一切。通过延伸思考，Claude在采取行动前深入考虑并迭代其计划。"think"工具是为了让Claude在开始生成回应后，添加一个步骤来停下来思考它是否拥有所有需要的信息来继续前进。这在执行长链工具调用或与用户进行长时多步骤对话时特别有用。

这使得"think"工具更适合那些Claude不仅凭用户查询就能获得所有需要信息的情况，以及它需要处理外部信息（例如工具调用结果中的信息）的情况。Claude使用"think"工具所进行的推理不如通过延伸思考所能获得的推理全面，而且更专注于模型发现的"新"信息。

我们建议在更简单的工具使用场景下使用延伸思考，如非顺序工具调用或直接指令遵循。延伸思考对于不需要Claude调用工具的用例也很有用，如编码、数学和物理。"think"工具更适合当Claude需要调用复杂工具、在长链工具调用中仔细分析工具输出、在具有详细指南的政策密集环境中导航，或做出顺序决策，其中每一步都建立在前面的基础上且错误代价高昂。

以下是使用来自τ-Bench(https://arxiv.org/abs/2406.12045)的标准工具规范格式的示例实现：

```json
{  "name": "think",  "description": "使用该工具思考某事。它不会获取新信息或更改数据库，只会将思考添加到日志中。在需要复杂推理或某种缓存记忆时使用它。",  "input_schema": {    "type": "object",    "properties": {      "thought": {        "type": "string",        "description": "要思考的想法。"      }    },    "required": ["thought"]  }}
```

## 在τ-Bench上的表现

我们使用τ-bench（tau-bench）评估了"think"工具，这是一个全面的基准测试，设计用于测试模型在真实客服场景中使用工具的能力，其中"think"工具是评估标准环境的一部分。

τ-bench评估Claude的能力包括：

- 与模拟用户进行真实对话导航
- 一致地遵循复杂的客服代理政策指南
- 使用各种工具访问和操作环境数据库

τ-bench中使用的主要评估指标是pass^ k ，它衡量给定任务的所有 k 个独立任务试验都成功的概率，并在所有任务中取平均值。与其他LLM评估中常见的pass@ k 指标（衡量 k 个试验中至少有一个成功）不同，pass^ k 评估一致性和可靠性——这对客服应用至关重要，因为在这些应用中一致遵守政策是必不可少的。

### 性能分析

我们的评估比较了几种不同的配置：

1. 基准线（无"think"工具，无延伸思考模式）
2. 仅延伸思考模式
3. 仅"think"工具
4. 带优化提示的"think"工具（针对航空领域）

结果显示，当Claude 3.7在基准测试的"航空"和"零售"客服领域有效使用"think"工具时，性能显著提升：

- **航空领域** ：带优化提示的"think"工具在pass^1指标上达到0.570，相比基准线的0.370——相对提升54%；
- **零售领域** ：仅"think"工具达到0.812，相比基准线的0.783。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF75Giak3sEgmHxNianUZYjRQXFwniaia6zIYpc3XqqwLSkXC8KAcVnB7Iib2OiaceiaYVQ7G8cKdj0YG7PA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图1：显示Claude 3.7 Sonnet在Tau-Bench评估的"航空"领域的性能折线图

Claude 3.7 Sonnet在Tau-Bench评估的"航空"领域的性能

| 配置 | *k*  \=1 | *k*  \=2 | *k*  \=3 | *k*  \=4 | *k*  \=5 |
| --- | --- | --- | --- | --- | --- |
| "Think" + 提示 | 0.584 | 0.444 | 0.384 | 0.356 | 0.340 |
| "Think" | 0.404 | 0.254 | 0.186 | 0.140 | 0.100 |
| 延伸思考 | 0.412 | 0.290 | 0.232 | 0.192 | 0.160 |
| 基准线 | 0.332 | 0.206 | 0.148 | 0.116 | 0.100 |

四种不同配置的评估结果。分数为比例。

在航空领域获得最佳性能是通过将"think"工具与优化提示结合实现的，该提示提供了在分析客户请求时使用的推理方法类型的示例。以下是优化提示的示例：

```markdown
## 使用think工具

在收到工具结果后采取任何行动或回应用户之前，使用think工具作为草稿来：

- 列出适用于当前请求的特定规则

- 检查是否收集了所有必需信息

- 验证计划的行动是否符合所有政策

- 迭代工具结果以确保正确性

  

以下是在think工具内迭代的一些示例：

<think_tool_example_1>

用户想要取消航班ABC123

- 需要验证：用户ID、预订ID、原因

- 检查取消规则：

* 是否在预订后24小时内？

* 如果不是，检查机票等级和保险

- 验证没有已飞行或过去的航段

- 计划：收集缺失信息，验证规则，获取确认

</think_tool_example_1>

  

<think_tool_example_2>

用户想要预订3张去纽约的机票，每人2个托运行李

- 需要用户ID来检查：

* 会员等级以确定行李限额

* 个人资料中存在哪些支付方式

- 行李计算：

* 经济舱×3名乘客

* 如果是普通会员：每人1个免费行李→3个额外行李=$150

* 如果是银卡会员：每人2个免费行李→0个额外行李=$0

* 如果是金卡会员：每人3个免费行李→0个额外行李=$0

- 需要验证的支付规则：

* 最多1张旅行证书，1张信用卡，3张礼品卡

* 所有支付方式必须在个人资料中

* 旅行证书余额将被浪费

- 计划：

1. 获取用户ID

2. 验证会员等级以确定行李费用

3. 检查个人资料中的支付方式及其组合是否允许

4. 计算总额：机票价格+任何行李费用

5. 获取预订的明确确认

</think_tool_example_2>
```

特别有趣的是不同方法的比较。使用带优化提示的"think"工具相比延伸思考模式（其表现与未提示的"think"工具相似）取得了显著更好的结果。仅使用"think"工具（不带提示）相比基准线改进了性能，但仍低于优化方法。

"think"工具与优化提示的组合以显著优势提供了最强的性能，这可能是由于基准测试中 航空政策 部分的高复杂性，模型从被给予如何"思考"的示例中获益最多。

在零售领域，我们也测试了各种配置以了解每种方法的具体影响。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnF75Giak3sEgmHxNianUZYjRQPwygFTetvDV54Bnc8vc1KicIEqSYkMu84Y9UbrvJvAbiasKTOtTmpmLQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图2：显示Claude 3.7 Sonnet在Tau-Bench评估的"零售"领域在三种不同配置下的性能折线图

Claude 3.7 Sonnet在Tau-Bench评估的"零售"领域的性能

| 配置 | *k*  \=1 | *k*  \=2 | *k*  \=3 | *k*  \=4 | *k*  \=5 |
| --- | --- | --- | --- | --- | --- |
| "Think" + 无提示 | 0.812 | 0.735 | 0.685 | 0.650 | 0.626 |
| 延伸思考 | 0.770 | 0.681 | 0.623 | 0.581 | 0.548 |
| 基准线 | 0.783 | 0.695 | 0.643 | 0.607 | 0.583 |

三种不同配置的评估结果。分数为比例。

"think"工具即使没有额外提示也达到了最高的pass^1分数0.812。与航空领域相比， 零售政策 明显更容易导航，Claude能够仅仅通过拥有思考空间而无需进一步指导就获得改进。

### τ-Bench分析的关键见解

我们的详细分析揭示了几种可以帮助您有效实施"think"工具的模式：

1. **在困难领域中提示非常重要** 。 仅仅提供"think"工具可能会在某种程度上改善性能，但将其与优化提示配对在困难领域产生了显著更好的结果。然而，更简单的领域可能仅仅通过访问"think"就能获益。
2. **试验中的一致性提高** 。 使用"think"带来的改进在pass^k直到k=5时都得以保持，表明该工具帮助Claude更有效地处理边缘情况和不寻常场景。

## 在SWE-Bench上的表现

当评估Claude 3.7 Sonnet时，一个类似的"think"工具被添加到我们的SWE-bench设置中，为达到0.623的最先进分数做出了贡献。经过调整的"think"工具定义如下：

```json
{  "name": "think",  "description": "使用工具思考某事。它不会获取新信息或对存储库进行任何更改，只是记录思考。在需要复杂推理或头脑风暴时使用它。例如，如果您探索存储库并发现bug的源头，调用此工具来头脑风暴几种独特的修复bug的方法，并评估哪些更改可能最简单和最有效。或者，如果您收到一些测试结果，调用此工具来头脑风暴修复失败测试的方法。",  "input_schema": {    "type": "object",    "properties": {      "thought": {        "type": "string",        "description": "您的想法。"      }    },    "required": ["thought"]  }}
```

我们的实验（n=30个带"think"工具的样本，n=144个不带"think"工具的样本）显示，包含此工具的隔离效果平均提高了1.6%的性能（Welch's t-test：t(38.89) = 6.71，p <.001，d = 1.47）。

## 何时使用"think"工具

根据这些评估结果，我们确定了Claude最能从"think"工具中受益的特定场景：

1. **工具输出分析** 。当Claude需要在采取行动前仔细处理之前工具调用的输出，并可能需要在其方法中回溯时；
2. **政策密集环境** 。当Claude需要遵循详细指南并验证合规性时；以及
3. **顺序决策制定** 。当每个行动都建立在前面的基础上，而且错误代价高昂时（通常在多步骤领域中发现）。

## 实施最佳实践

根据我们的τ-bench实验，我们推荐以下实施实践，以便从Claude的"think"工具中获得最大收益。

### 1\. 带有领域特定示例的战略提示

最有效的方法是提供清晰指导，说明何时以及如何使用"think"工具，如用于τ-bench航空领域的指导。提供针对特定用例量身定制的示例显著提高了模型有效使用"think"工具的方式：

- 推理过程中预期的详细程度；
- 如何将复杂指令分解为可操作步骤；
- 处理常见场景的决策树；
- 如何检查是否收集了所有必要信息。

### 2\. 将复杂指导放在系统提示中

我们发现，当指导又长又复杂时，将关于"think"工具的指导放在系统提示中比放在工具描述本身中更有效。这种方法提供了更广泛的上下文，帮助模型更好地将思考过程整合到其整体行为中。

## 何时不使用"think"工具

虽然"think"工具可以提供实质性改进，但它并不适用于所有工具使用的用例，并且会增加提示长度和输出词元。具体来说，我们发现在以下用例中"think"工具不会提供任何改进：

1. **非顺序工具调用** 。如果Claude只需要进行单个工具调用或多个并行调用来完成任务，则不太可能从添加"think"中获得任何改进。
2. **简单指令遵循** 。当Claude不需要遵守很多约束，且其默认行为已足够好时，额外的"think"不太可能带来收益。

## 入门

"think"工具是对Claude实现的一个简单添加，只需几个步骤即可带来有意义的改进：

1. **使用代理工具用例进行测试** 。从具有挑战性的用例开始——那些Claude目前在政策合规性或长工具调用链中的复杂推理方面存在困难的用例。
2. **添加工具定义** 。实现针对您领域定制的"think"工具。它需要最少的代码，但能够进行更结构化的推理。还要考虑在系统提示中包含有关何时以及如何使用该工具的指导，并提供与您领域相关的示例。
3. **监控和改进** 。观察Claude在实践中如何使用该工具，并调整您的提示以鼓励更有效的思考模式。

最好的部分是添加这个工具在性能结果方面几乎没有负面影响。除非Claude决定使用它，否则它不会改变外部行为，也不会干扰您现有的工具或工作流程。

## 结论

我们的研究表明，"think"工具可以显著提高Claude 3.7 Sonnet在需要政策遵守和长链工具调用中推理的复杂任务上的性能¹。"think"不是一个万能的解决方案，但它为正确的用例提供了实质性的益处，所有这些都只需最小的实现复杂性。

我们期待看到您如何使用"think"工具构建更强大、更可靠和更透明的Claude AI系统。

¹虽然我们的τ-Bench结果关注的是Claude 3.7 Sonnet使用"think"工具的改进，但我们的实验表明，Claude 3.5 Sonnet（新版）也能够使用与3.7 Sonnet相同的配置获得性能提升，表明这一改进也适用于其他Claude模型。