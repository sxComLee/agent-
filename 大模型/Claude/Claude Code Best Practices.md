---
标题: "Claude Code Best Practices"
链接: "https://www.anthropic.com/engineering/claude-code-best-practices"
作者: "[[@AnthropicAI]]"
创建时间: "2025-04-29T15:34:39+08:00"
摘要: "本文介绍了Claude Code的最佳实践，包括自定义设置、工具使用、常见工作流程和优化技巧，旨在帮助用户更高效地利用这一代理编程工具。"
tags:
  - "clippings"
  - "AI"
  - "编程"
  - "效率"
  - "Claude Code"
  - "Anthropic"
字数: "5084"
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

We recently [released Claude Code](https://www.anthropic.com/news/claude-3-7-sonnet), a command line tool for agentic coding. Developed as a research project, Claude Code gives Anthropic engineers and researchers a more native way to integrate Claude into their coding workflows.  
我们最近发布了 Claude Code，这是一个用于 agentic 编码的命令行工具。作为一项研究项目开发，Claude Code 为 Anthropic 的工程师和研究人员提供了一种更原生的方式将 Claude 集成到他们的编码工作流程中。

Claude Code is intentionally low-level and unopinionated, providing close to raw model access without forcing specific workflows. This design philosophy creates a flexible, customizable, scriptable, and safe power tool. While powerful, this flexibility presents a learning curve for engineers new to agentic coding tools—at least until they develop their own best practices.  
Claude Code 故意采用低级和客观的设计，提供接近原始模型访问，而不强制特定的工作流程。这种设计理念创造了一个灵活、可定制、可脚本化和安全的强大工具。虽然功能强大，但这种灵活性对于新接触 agentic 编码工具的工程师来说存在一定的学习曲线——至少在他们形成自己的最佳实践之前是这样的。

This post outlines general patterns that have proven effective, both for Anthropic's internal teams and for external engineers using Claude Code across various codebases, languages, and environments. Nothing in this list is set in stone nor universally applicable; consider these suggestions as starting points. We encourage you to experiment and find what works best for you!  
本文概述了一些已被证明有效的通用模式，这些模式不仅适用于 Anthropic 的内部团队，也适用于使用 Claude Code 在各种代码库、语言和环境中的外部工程师。此列表中的内容并非一成不变，也不是普遍适用的；请将这些建议视为起点。我们鼓励您进行实验，找到最适合您的方法！

*Looking for more detailed information? Our comprehensive documentation at [claude.ai/code](https://claude.ai/code)* *covers all the features mentioned in this post and provides additional examples, implementation details, and advanced techniques.*  
想要获取更详细的信息吗？我们全面的文档在 claude.ai/codecovers 中涵盖了本帖中提到的所有功能，并提供额外的示例、实现细节和高级技巧。

## 1\. Customize your setup 1. 自定义您的设置

Claude Code is an agentic coding assistant that automatically pulls context into prompts. This context gathering consumes time and tokens, but you can optimize it through environment tuning.  
Claude Code 是一个智能编码助手，它自动将上下文拉入提示。这种上下文收集会消耗时间和令牌，但您可以通过环境调整来优化它。

### a. Create CLAUDE.md files a. 创建 CLAUDE.md 文件

`CLAUDE.md` is a special file that Claude automatically pulls into context when starting a conversation. This makes it an ideal place for documenting:  
`CLAUDE.md` 是 Claude 在开始对话时自动拉入上下文的特殊文件。这使得它成为记录文档的理想之地：

- Common bash commands 常用 bash 命令
- Core files and utility functions  
	核心文件和实用函数
- Code style guidelines 代码风格指南
- Testing instructions 测试说明
- Repository etiquette (e.g., branch naming, merge vs. rebase, etc.)  
	仓库礼仪（例如，分支命名、合并与变基等）
- Developer environment setup (e.g., pyenv use, which compilers work)  
	开发环境搭建（例如，使用 pyenv，哪些编译器可用）
- Any unexpected behaviors or warnings particular to the project  
	项目特有的任何意外行为或警告
- Other information you want Claude to remember  
	你希望 Claude 记住的其他信息

There’s no required format for `CLAUDE.md` files. We recommend keeping them concise and human-readable. For example:  
`CLAUDE.md` 文件没有要求特定的格式。我们建议保持它们简洁且易于阅读。例如：

```
# Bash commands
- npm run build: Build the project
- npm run typecheck: Run the typechecker

# Code style
- Use ES modules (import/export) syntax, not CommonJS (require)
- Destructure imports when possible (eg. import { foo } from 'bar')

# Workflow
- Be sure to typecheck when you’re done making a series of code changes
- Prefer running single tests, and not the whole test suite, for performance
```

You can place `CLAUDE.md` files in several locations:  
你可以将 `CLAUDE.md` 文件放置在几个位置：

- **The root of your repo**, or wherever you run `claude` from (the most common usage). Name it `CLAUDE.md` and check it into git so that you can share it across sessions and with your team (recommended), or name it `CLAUDE.local.md` and `.gitignore` it  
	你的仓库根目录，或者你运行 `claude` 的位置（最常见的使用方式）。将其命名为 `CLAUDE.md` 并将其提交到 git 中，以便可以在会话之间以及与团队共享（推荐），或者将其命名为 `CLAUDE.local.md` 和 `.gitignore`
- **Any parent of the directory** where you run `claude`. This is most useful for monorepos, where you might run `claude` from `root/foo`, and have `CLAUDE.md` files in both `root/CLAUDE.md` and `root/foo/CLAUDE.md`. Both of these will be pulled into context automatically  
	运行目录的任何父目录。这在单一代码库中非常有用，您可能从父目录中运行 `claude` ，并且 `root/foo` 和 `CLAUDE.md` 文件同时存在于 `root/CLAUDE.md` 和 `root/foo/CLAUDE.md` 中。这两个都将自动纳入上下文。
- **Any child of the directory** where you run `claude`. This is the inverse of the above, and in this case, Claude will pull in `CLAUDE.md` files on demand when you work with files in child directories  
	运行目录的任何子目录。这是上述内容的逆操作，在这种情况下，当您在子目录中处理文件时，Claude 将按需拉取 `CLAUDE.md` 文件。
- **Your home folder** (`~/.claude/CLAUDE.md`), which applies it to all your *claude* sessions  
	您的主目录（ `~/.claude/CLAUDE.md` ），这适用于您所有的 Claude 会话。

When you run the `/init` command, Claude will automatically generate a `CLAUDE.md` for you.  
当您运行 `/init` 命令时，Claude 将自动为您生成 `CLAUDE.md` 。

### b. Tune your CLAUDE.md filesb. 调整您的 CLAUDE.md 文件

Your `CLAUDE.md` files become part of Claude’s prompts, so they should be refined like any frequently used prompt. A common mistake is adding extensive content without iterating on its effectiveness. Take time to experiment and determine what produces the best instruction following from the model.  
您的 `CLAUDE.md` 文件将成为 Claude 的提示的一部分，因此它们应该像任何频繁使用的提示一样进行优化。一个常见的错误是在没有迭代其有效性之前添加大量内容。请花时间进行实验，以确定什么会产生最佳的模型指令。

You can add content to your `CLAUDE.md` manually or press the `#` key to give Claude an instruction that it will automatically incorporate into the relevant `CLAUDE.md`. Many engineers use `#` frequently to document commands, files, and style guidelines while coding, then include `CLAUDE.md` changes in commits so team members benefit as well.  
您可以手动添加内容到您的 `CLAUDE.md` ，或者按 `#` 键给 Claude 一个指令，它会自动将其纳入相关的 `CLAUDE.md` 。许多工程师在编码时经常使用 `#` 来记录命令、文件和风格指南，然后在提交中包含 `CLAUDE.md` 变更，以便团队成员也能从中受益。

At Anthropic, we occasionally run `CLAUDE.md` files through the [prompt improver](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompt-improver) and often tune instructions (e.g. adding emphasis with "IMPORTANT" or "YOU MUST") to improve adherence.  
在 Anthropic，我们偶尔会通过提示改进器运行 `CLAUDE.md` 文件，并经常调整指令（例如，使用 "重要" 或 "你必须" 等强调词），以提高遵守度。

![Claude Code tool allowlist](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F6961243cc6409e41ba93895faded4f4bc1772366-1600x1231.png&w=3840&q=75)

Claude Code tool allowlist

### c. Curate Claude's list of allowed toolsc. 精选 Claude 的允许工具列表

By default, Claude Code requests permission for any action that might modify your system: file writes, many bash commands, MCP tools, etc. We designed Claude Code with this deliberately conservative approach to prioritize safety. You can customize the allowlist to permit additional tools that you know are safe, or to allow potentially unsafe tools that are easy to undo (e.g., file editing, `git commit`).  
默认情况下，Claude Code 会请求权限以执行可能修改您系统的任何操作：文件写入、许多 bash 命令、MCP 工具等。我们故意采用这种保守的方法来优先考虑安全性。您可以自定义允许列表，以允许您知道是安全的工具，或者允许可以轻松撤销的潜在不安全工具（例如，文件编辑， `git commit` ）。

There are four ways to manage allowed tools:  
有四种方式来管理允许的工具：

- **Select "Always allow"** when prompted during a session.  
	在会话期间被提示时选择“始终允许”。
- **Use the `/allowed-tools` command** after starting Claude Code to add or remove tools from the allowlist. For example, you can add `Edit` to always allow file edits, `Bash(git commit:*)` to allow git commits, or `mcp__puppeteer__puppeteer_navigate` to allow navigating with the Puppeteer MCP server.  
	在启动 Claude Code 后使用 `/allowed-tools` 命令添加或从允许列表中删除工具。例如，您可以添加 `Edit` 以始终允许文件编辑， `Bash(git commit:*)` 以允许 git 提交，或 `mcp__puppeteer__puppeteer_navigate` 以允许使用 Puppeteer MCP 服务器进行导航。
- **Manually edit** your `.claude/settings.json` or `~/.claude.json` (we recommend checking the former into source control to share with your team)*.*  
	手动编辑你的 `.claude/settings.json` 或 `~/.claude.json` （我们建议将前者提交到源代码管理以与团队共享）。
- **Use the ` --allowedTools` CLI flag** for session-specific permissions.  
	使用 ` --allowedTools` CLI 标志以设置会话特定权限。

### d. If using GitHub, install the gh CLId. 如果使用 GitHub，请安装 gh CLI

Claude knows how to use the `gh` CLI to interact with GitHub for creating issues, opening pull requests, reading comments, and more. Without `gh` installed, Claude can still use the GitHub API or MCP server (if you have it installed).  
Claude 会使用 `gh` CLI 与 GitHub 交互，用于创建问题、打开拉取请求、阅读评论等。如果没有安装 `gh` ，Claude 仍然可以使用 GitHub API 或 MCP 服务器（如果你已安装）。

Claude has access to your shell environment, where you can build up sets of convenience scripts and functions for it just like you would for yourself. It can also leverage more complex tools through MCP and REST APIs.  
Claude 可以访问您的 shell 环境，您可以在其中为它构建一系列方便的脚本和函数，就像为自己做的那样。它还可以通过 MCP 和 REST API 利用更复杂的工具。

### a. Use Claude with bash toolsa. 使用 bash 工具与 Claude 配合

Claude Code inherits your bash environment, giving it access to all your tools. While Claude knows common utilities like unix tools and `gh`, it won't know about your custom bash tools without instructions:  
Claude Code 继承了您的 bash 环境，使其能够访问所有工具。虽然 Claude 知道常见的工具，如 Unix 工具和 `gh` ，但如果没有说明，它将不知道您的自定义 bash 工具：

1. Tell Claude the tool name with usage examples  
	告诉 Claude 工具名称，并附上使用示例
2. Tell Claude to run `--help` to see tool documentation  
	告诉 Claude 运行 `--help` 查看工具文档
3. Document frequently used tools in `CLAUDE.md`  
	在 `CLAUDE.md` 中记录常用工具

### b. Use Claude with MCPb. 使用 Claude 与 MCP

Claude Code functions as both an MCP server and client. As a client, it can connect to any number of MCP servers to access their tools in three ways:  
Claude Code 既是 MCP 服务器又是客户端。作为客户端，它可以连接到任意数量的 MCP 服务器，以三种方式访问它们的工具：

- **In project config** (available when running Claude Code in that directory)  
	在项目配置中（在当前目录下运行 Claude Code 时可用）
- **In global config** (available in all projects)  
	在全局配置中（在所有项目中可用）
- **In a checked-in `.mcp.json` file** (available to anyone working in your codebase). For example, you can add Puppeteer and Sentry servers to your `.mcp.json`, so that every engineer working on your repo can use these out of the box.  
	在签入的 `.mcp.json` 文件（任何在您的代码库中工作的人都可以访问）。例如，您可以将 Puppeteer 和 Sentry 服务器添加到您的 `.mcp.json` 中，这样每个在您的仓库中工作的工程师都可以直接使用它们。

When working with MCP, it can also be helpful to launch Claude with the `--mcp-debug` flag to help identify configuration issues.  
当使用 MCP 时，使用 `--mcp-debug` 标志启动 Claude 也有助于识别配置问题。

### c. Use custom slash commandsc. 使用自定义斜杠命令

For repeated workflows—debugging loops, log analysis, etc.—store prompt templates in Markdown files within the `.claude/commands` folder. These become available through the slash commands menu when you type `/`. You can check these commands into git to make them available for the rest of your team.  
对于重复的工作流程——调试循环、日志分析等——在 `.claude/commands` 文件夹中存储提示模板到 Markdown 文件中。当您输入 `/` 时，这些命令将通过斜杠命令菜单可用。您可以将这些命令提交到 git 中，以便整个团队都可以使用。

Custom slash commands can include the special keyword `$ARGUMENTS` to pass parameters from command invocation.  
自定义斜杠命令可以包含特殊关键词 `$ARGUMENTS` ，用于从命令调用中传递参数。

For example, here’s a slash command that you could use to automatically pull and fix a Github issue:  
例如，这里有一个可以自动拉取和修复 Github 问题的斜杠命令：

Putting the above content into `.claude/commands/fix-github-issue.md` makes it available as the `/project:fix-github-issue` command in Claude Code. You could then for example use `/project:fix-github-issue 1234` to have Claude fix issue #1234. Similarly, you can add your own personal commands to the `~/.claude/commands` folder for commands you want available in all of your sessions.  
将上述内容放入 `.claude/commands/fix-github-issue.md` 中，使其成为 Claude Code 中的 `/project:fix-github-issue` 命令。例如，您可以使用 `/project:fix-github-issue 1234` 来让 Claude 修复 #1234# 的问题。同样，您可以将自己的个人命令添加到 `~/.claude/commands` 文件夹中，以便在所有会话中可用。

## 3\. Try common workflows 3. 尝试常见的工作流程

Claude Code doesn’t impose a specific workflow, giving you the flexibility to use it how you want. Within the space this flexibility affords, several successful patterns for effectively using Claude Code have emerged across our community of users:  
Claude Code 不强制特定的工作流程，让您可以根据自己的需求灵活使用。在这个灵活性所提供的空间内，我们用户社区中已经出现了几种有效使用 Claude Code 的成功模式：

### a. Explore, plan, code, commit探索、规划、编码、提交

This versatile workflow suits many problems:  
这种灵活的工作流程适用于许多问题：

1. **Ask Claude to read relevant files, images, or URLs**, providing either general pointers ("read the file that handles logging") or specific filenames ("read logging.py"), but explicitly tell it not to write any code just yet.  
	让 Claude 阅读相关的文件、图片或 URL，提供一般性的提示（“阅读处理日志的文件”）或具体的文件名（“阅读 logging.py”），但明确告诉它现在不要编写任何代码。
	1. This is the part of the workflow where you should consider strong use of subagents, especially for complex problems. Telling Claude to use subagents to verify details or investigate particular questions it might have, especially early on in a conversation or task, tends to preserve context availability without much downside in terms of lost efficiency.  
		这是工作流程中应该考虑使用子代理的强有力部分，尤其是对于复杂问题。告诉 Claude 使用子代理来验证细节或调查它可能有的特定问题，尤其是在对话或任务的早期，往往可以保持上下文可用性，而不会在效率方面造成太大的损失。
2. **Ask Claude to make a plan for how to approach a specific problem**. We recommend using the word "think" to trigger extended thinking mode, which gives Claude additional computation time to evaluate alternatives more thoroughly. These specific phrases are mapped directly to increasing levels of thinking budget in the system: "think" < "think hard" < "think harder" < "ultrathink." Each level allocates progressively more thinking budget for Claude to use.  
	请让 Claude 制定一个解决问题的方案。我们建议使用“思考”这个词来触发扩展思考模式，这会给 Claude 更多的计算时间来更彻底地评估替代方案。这些特定的短语直接映射到系统中不断增加的思考预算级别：“思考” < “深思” < “更深入地思考” < “超思考”。每个级别都为 Claude 分配更多用于思考的预算。
	1. If the results of this step seem reasonable, you can have Claude create a document or a GitHub issue with its plan so that you can reset to this spot if the implementation (step 3) isn’t what you want.  
		如果这一步骤的结果看起来合理，你可以让 Claude 创建一个文档或 GitHub 问题，以便在实现（步骤 3）不是你想要的结果时重置到这个位置。
3. **Ask Claude to implement its solution in code**. This is also a good place to ask it to explicitly verify the reasonableness of its solution as it implements pieces of the solution.  
	请让 Claude 用代码实现其解决方案。这也是让 Claude 在实现解决方案的各个部分时明确验证其解决方案合理性的好时机。
4. **Ask Claude to commit the result and create a pull request**. If relevant, this is also a good time to have Claude update any READMEs or changelogs with an explanation of what it just did.  
	请让 Claude 提交结果并创建一个拉取请求。如果相关，这也是让 Claude 更新任何 README 或变更日志，解释它刚刚做了什么的好时机。

Steps #1-#2 are crucial—without them, Claude tends to jump straight to coding a solution. While sometimes that's what you want, asking Claude to research and plan first significantly improves performance for problems requiring deeper thinking upfront.  
步骤 #1-#2 至关重要——没有它们，Claude 往往会直接跳到编写解决方案。虽然有时这正是你想要的，但要求 Claude 先进行研究和规划，对于需要前期深入思考的问题，可以显著提高性能。

### b. Write tests, commit; code, iterate, commitb. 编写测试，提交；编码，迭代，提交

This is an Anthropic-favorite workflow for changes that are easily verifiable with unit, integration, or end-to-end tests. Test-driven development (TDD) becomes even more powerful with agentic coding:  
这是 Anthropic 喜爱的一个工作流程，对于可以通过单元测试、集成测试或端到端测试轻松验证的更改。具有代理编码的测试驱动开发（TDD）变得更加强大：

1. **Ask Claude to write tests based on expected input/output pairs**. Be explicit about the fact that you’re doing test-driven development so that it avoids creating mock implementations, even for functionality that doesn’t exist yet in the codebase.  
	要求 Claude 根据预期的输入/输出对编写测试。明确指出你正在进行测试驱动开发，以避免为代码库中尚未存在的功能创建模拟实现。
2. **Tell Claude to run the tests and confirm they fail**. Explicitly telling it not to write any implementation code at this stage is often helpful.  
	告诉 Claude 运行测试并确认它们失败。明确地告诉它在这个阶段不要编写任何实现代码通常很有帮助。
3. **Ask Claude to commit the tests** when you’re satisfied with them.  
	当你对测试满意时，请让 Claude 提交测试。
4. **Ask Claude to write code that passes the tests**, instructing it not to modify the tests. Tell Claude to keep going until all tests pass. It will usually take a few iterations for Claude to write code, run the tests, adjust the code, and run the tests again.  
	请让 Claude 编写通过测试的代码，并指示它不要修改测试。告诉 Claude 继续编写，直到所有测试都通过。通常，Claude 编写代码、运行测试、调整代码并再次运行测试需要几个迭代。
	1. At this stage, it can help to ask it to verify with independent subagents that the implementation isn’t overfitting to the tests  
		在这个阶段，可以请它通过独立的子代理验证实现是否过度拟合测试可能会有所帮助。
5. **Ask Claude to commit the code** once you’re satisfied with the changes.  
	当你对更改满意时，请让 Claude 提交代码。

Claude performs best when it has a clear target to iterate against—a visual mock, a test case, or another kind of output. By providing expected outputs like tests, Claude can make changes, evaluate results, and incrementally improve until it succeeds.  
Claude 在有一个明确的迭代目标时表现最佳——一个视觉原型、一个测试案例或任何其他类型的输出。通过提供预期的输出，如测试，Claude 可以做出改变，评估结果，并逐步改进，直到成功。

### c. Write code, screenshot result, iteratec. 编写代码，截图结果，迭代

Similar to the testing workflow, you can provide Claude with visual targets:  
与测试工作流程类似，您可以向 Claude 提供视觉目标：

1. **Give Claude a way to take browser screenshots** (e.g., with the [Puppeteer MCP server](https://github.com/modelcontextprotocol/servers/tree/c19925b8f0f2815ad72b08d2368f0007c86eb8e6/src/puppeteer), an [iOS simulator MCP server](https://github.com/joshuayoes/ios-simulator-mcp), or manually copy / paste screenshots into Claude).  
	为 Claude 提供一种获取浏览器截图的方法（例如，使用 Puppeteer MCP 服务器、iOS 模拟器 MCP 服务器或手动复制/粘贴截图到 Claude）。
2. **Give Claude a visual mock** by copying / pasting or drag-dropping an image, or giving Claude the image file path.  
	通过复制/粘贴或拖放图片，或者提供图片文件路径，给 Claude 一个视觉原型。
3. **Ask Claude to implement the design** in code, take screenshots of the result, and iterate until its result matches the mock.  
	让 Claude 根据设计实现代码，并截图结果，直到与原型匹配为止。
4. **Ask Claude to commit** when you're satisfied.  
	当你满意时，让 Claude 提交。

Like humans, Claude's outputs tend to improve significantly with iteration. While the first version might be good, after 2-3 iterations it will typically look much better. Give Claude the tools to see its outputs for best results.  
与人类一样，Claude 的输出通常在迭代中显著改进。虽然第一个版本可能不错，但经过 2-3 次迭代后，通常看起来会好得多。给 Claude 提供查看其输出的工具以获得最佳效果。

![Safe yolo mode](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F6ea59a36fe82c2b300bceaf3b880a4b4852c552d-1600x1143.png&w=3840&q=75)

Safe yolo mode

### d. Safe YOLO mode d. 安全 YOLO 模式

Instead of supervising Claude, you can use `claude --dangerously-skip-permissions` to bypass all permission checks and let Claude work uninterrupted until completion. This works well for workflows like fixing lint errors or generating boilerplate code.  
不再监督 Claude，您可以使用 `claude --dangerously-skip-permissions` 绕过所有权限检查，让 Claude 不间断地工作直到完成。这对于修复 lint 错误或生成样板代码等工作流程非常有效。

Letting Claude run arbitrary commands is risky and can result in data loss, system corruption, or even data exfiltration (e.g., via prompt injection attacks). To minimize these risks, use `--dangerously-skip-permissions` in a container without internet access. You can follow this [reference implementation](https://github.com/anthropics/claude-code/tree/main/.devcontainer) using Docker Dev Containers.  
允许 Claude 运行任意命令存在风险，可能导致数据丢失、系统损坏，甚至数据泄露（例如，通过提示注入攻击）。为了最小化这些风险，请在没有互联网访问的容器中使用 `--dangerously-skip-permissions` 。您可以参考以下 Docker Dev Containers 的实现。

### e. Codebase Q&A e. 代码库问答

When onboarding to a new codebase, use Claude Code for learning and exploration. You can ask Claude the same sorts of questions you would ask another engineer on the project when pair programming. Claude can agentically search the codebase to answer general questions like:  
当加入新的代码库时，请使用 Claude Code 进行学习和探索。您可以向 Claude 提出与您在结对编程时向项目中的其他工程师提出的问题相同的问题。Claude 可以主动搜索代码库以回答一般性问题，例如：

- How does logging work?日志是如何工作的？
- How do I make a new API endpoint?  
	我该如何创建一个新的 API 端点？
- What does `async move { ... }` do on line 134 of `foo.rs`?  
	`foo.rs` 中的第 134 行 `async move { ... }` 做了什么？
- What edge cases does `CustomerOnboardingFlowImpl` handle?  
	`CustomerOnboardingFlowImpl` 处理了哪些边缘情况？
- Why are we calling `foo()` instead of `bar()` on line 333?  
	为什么我们在第 333 行调用 `foo()` 而不是 `bar()` ？
- What’s the equivalent of line 334 of `baz.py` in Java?  
	`baz.py` 中第 334 行的 Java 等价代码是什么？

At Anthropic, using Claude Code in this way has become our core onboarding workflow, significantly improving ramp-up time and reducing load on other engineers. No special prompting is required! Simply ask questions, and Claude will explore the code to find answers.  
在 Anthropic，以这种方式使用 Claude Code 已成为我们的核心入职流程，显著提高了上手速度并减轻了其他工程师的负担。无需特殊提示！只需提问，Claude 就会探索代码以找到答案。

![Use Claude to interact with git](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2Fa08ea13c2359aac0eceacebf2e15f81e8e8ec8d2-1600x1278.png&w=3840&q=75)

Use Claude to interact with git

### f. Use Claude to interact with gitf. 使用 Claude 与 git 交互

Claude can effectively handle many git operations. Many Anthropic engineers use Claude for 90%+ of our *git* interactions:  
Claude 可以有效地处理许多 git 操作。许多 Anthropic 工程师使用 Claude 来完成 90%以上的 git 交互：

- **Searching *git* history** to answer questions like "What changes made it into v1.2.3?", "Who owns this particular feature?", or "Why was this API designed this way?" It helps to explicitly prompt Claude to look through git history to answer queries like these.  
	搜索 git 历史记录以回答诸如“哪些更改被包含在 v1.2.3 版本中？”、“谁拥有这个特定的功能？”或“为什么这个 API 被设计成这样？”等问题。明确提示 Claude 查看 git 历史记录以回答此类查询很有帮助。
- **Writing commit messages**.Claude will look at your changes and recent history automatically to compose a message taking all the relevant context into account  
	编写提交信息。Claude 会自动查看您的更改和最近的历史记录，以考虑所有相关上下文来编写信息。
- **Handling complex git operations** like reverting files, resolving rebase conflicts, and comparing and grafting patches  
	处理复杂的 Git 操作，如撤销文件、解决变基冲突以及比较和接合补丁

### g. Use Claude to interact with GitHub使用 Claude 与 GitHub 交互

Claude Code can manage many GitHub interactions:  
Claude Code 可以管理许多 GitHub 交互：

- **Creating pull requests**: Claude understands the shorthand "pr" and will generate appropriate commit messages based on the diff and surrounding context.  
	创建拉取请求：Claude 理解 "pr" 简写，并将根据差异和上下文生成适当的提交信息。
- **Implementing one-shot resolutions** for simple code review comments: just tell it to fix comments on your PR (optionally, give it more specific instructions) and push back to the PR branch when it's done.  
	实现单次解决简单代码审查评论：只需告诉它修复你的 PR 中的评论（可选地提供更具体的指令），完成后推送到 PR 分支。
- **Fixing failing builds** or linter warnings  
	修复失败的构建或代码检查警告
- **Categorizing and triaging open issues** by asking Claude to loop over open GitHub issues  
	通过让 Claude 遍历开放的 GitHub 问题来分类和优先排序开放的问题

This eliminates the need to remember `gh` command line syntax while automating routine tasks.  
这样就消除了在自动化常规任务时记住 `gh` 命令行语法的需求。

### h. Use Claude to work with Jupyter notebooks使用 Claude 与 Jupyter 笔记本协同工作

Researchers and data scientists at Anthropic use Claude Code to read and write Jupyter notebooks. Claude can interpret outputs, including images, providing a fast way to explore and interact with data. There are no required prompts or workflows, but a workflow we recommend is to have Claude Code and a `.ipynb` file open side-by-side in VS Code.  
Anthropic 的研究人员和数据科学家使用 Claude Code 来读取和编写 Jupyter 笔记本。Claude 可以解释输出，包括图像，提供快速探索和交互数据的方式。无需任何提示或工作流程，但我们推荐的工作流程是在 VS Code 中同时打开 Claude Code 和 `.ipynb` 文件。

You can also ask Claude to clean up or make aesthetic improvements to your Jupyter notebook before you show it to colleagues. Specifically telling it to make the notebook or its data visualizations “aesthetically pleasing” tends to help remind it that it’s optimizing for a human viewing experience.  
您还可以要求 Claude 在您向同事展示之前清理或美化您的 Jupyter 笔记本。具体告诉它使笔记本或其数据可视化“美观”通常有助于提醒它正在优化人类观看体验。

## 4\. Optimize your workflow4. 优化您的流程

The suggestions below apply across all workflows:  
以下建议适用于所有工作流程：

### a. Be specific in your instructionsa. 在您的指示中要具体明确

Claude Code’s success rate improves significantly with more specific instructions, especially on first attempts. Giving clear directions upfront reduces the need for course corrections later.  
Claude Code 的成功率随着指示的更加具体而显著提高，尤其是在初次尝试时。提前给出明确的指示可以减少后续的纠正需求。

For example:例如：

| Poor 贫穷 | Good 良好 |
| --- | --- |
| add tests for foo.py 为 foo.py 添加测试 | write a new test case for foo.py, covering the edge case where the user is logged out. avoid mocks   为 foo.py 编写一个新的测试用例，覆盖用户登出时的边缘情况。避免使用模拟 |
| why does ExecutionFactory have such a weird api?   为什么 ExecutionFactory 的 API 如此奇怪？ | look through ExecutionFactory's git history and summarize how its api came to be   查看 ExecutionFactory 的 Git 历史，总结其 API 是如何形成的 |
| add a calendar widget 添加一个日历小部件 | look at how existing widgets are implemented on the home page to understand the patterns and specifically how code and interfaces are separated out. HotDogWidget.php is a good example to start with. then, follow the pattern to implement a new calendar widget that lets the user select a month and paginate forwards/backwards to pick a year. Build from scratch without libraries other than the ones already used in the rest of the codebase.   查看主页上现有小部件的实现方式，以了解模式和代码以及接口是如何分离的。以 HotDogWidget.php 为例开始，然后按照这种模式实现一个新的日历小部件，允许用户选择月份并向前/向后翻页选择年份。从头开始构建，除了代码库中已经使用的库之外，不使用任何其他库。 |

Claude can infer intent, but it can't read minds. Specificity leads to better alignment with expectations.  
Claude 可以推断意图，但它不能读心。具体性有助于更好地符合预期。

![Give Claude images](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F75e1b57a0b696e7aafeca1ed5fa6ba7c601a5953-1360x1126.png&w=3840&q=75)

Give Claude images

### b. Give Claude images b. 提供 Claude 图像

Claude excels with images and diagrams through several methods:  
Claude 在处理图像和图表方面表现出色，通过以下几种方法：

- **Paste screenshots** (pro tip: hit *cmd+ctrl+shift+4* in macOS to screenshot to clipboard and *ctrl+v* to paste. Note that this is not cmd+v like you would usually use to paste on mac and does not work remotely.)  
	粘贴截图（提示：在 macOS 上，按住 cmd+ctrl+shift+4 进行截图并复制到剪贴板，然后按 ctrl+v 粘贴。注意，这不同于通常在 mac 上粘贴的 cmd+v，且在远程操作中不可用。）
- **Drag and drop** images directly into the prompt input  
	直接将图像拖放到提示输入框中
- **Provide file paths** for images  
	提供图像的文件路径

This is particularly useful when working with design mocks as reference points for UI development, and visual charts for analysis and debugging. If you are not adding visuals to context, it can still be helpful to be clear with Claude about how important it is for the result to be visually appealing.  
这在处理设计原型作为 UI 开发的参考点以及用于分析和调试的视觉图表时尤其有用。如果您没有在上下文中添加视觉元素，仍然需要向 Claude 明确指出结果需要具有视觉吸引力。

![Mention files you want Claude to look at or work on](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F7372868757dd17b6f2d3fef98d499d7991d89800-1450x1164.png&w=3840&q=75)

Mention files you want Claude to look at or work on

### c. Mention files you want Claude to look at or work onc. 提及您希望 Claude 查看或处理的文件

Use tab-completion to quickly reference files or folders anywhere in your repository, helping Claude find or update the right resources.  
使用 Tab 补全功能快速参考存储库中的文件或文件夹，帮助 Claude 找到或更新正确的资源。

![Give Claude URLs](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2Fe071de707f209bbaa7f16b593cc7ed0739875dae-1306x1088.png&w=3840&q=75)

Give Claude URLs

### d. Give Claude URLs d. 给 Claude 提供 URL

Paste specific URLs alongside your prompts for Claude to fetch and read. To avoid permission prompts for the same domains (e.g., docs.foo.com), use `/allowed-tools` to add domains to your allowlist.  
将特定 URL 粘贴到您的提示旁边，以便 Claude 抓取和阅读。为了避免对同一域名（例如，docs.foo.com）的权限提示，使用 `/allowed-tools` 将域名添加到允许列表中。

### e. Course correct early and often早期且频繁地进行课程纠正

While auto-accept mode (shift+tab to toggle) lets Claude work autonomously, you'll typically get better results by being an active collaborator and guiding Claude's approach. You can get the best results by thoroughly explaining the task to Claude at the beginning, but you can also course correct Claude at any time.  
虽然自动接受模式（按 shift+tab 切换）可以让 Claude 自主工作，但通常通过成为积极的合作者和指导 Claude 的方法，你会得到更好的结果。你可以在一开始就彻底地向 Claude 解释任务，但也可以在任何时候纠正 Claude。

These four tools help with course correction:  
这四个工具有助于进行课程纠正：

- **Ask Claude to make a plan** before coding. Explicitly tell it not to code until you’ve confirmed its plan looks good.  
	让 Claude 在编码前制定计划。明确告诉它在你确认其计划看起来不错之前不要编码。
- **Press Escape to interrupt** Claude during any phase (thinking, tool calls, file edits), preserving context so you can redirect or expand instructions.  
	按下 Esc 键以在任何阶段（思考、工具调用、文件编辑）中断 Claude，以保留上下文，以便您可以重新定向或扩展指令。
- **Double-tap Escape to jump back in history**, edit a previous prompt, and explore a different direction. You can edit the prompt and repeat until you get the result you're looking for.  
	双击 Esc 键返回历史记录，编辑之前的提示，并探索不同的方向。您可以编辑提示并重复，直到得到您想要的结果。
- **Ask Claude to undo changes**, often in conjunction with option #2 to take a different approach.  
	要求 Claude 撤销更改，通常与选项#2 结合使用，以采取不同的方法。

Though Claude Code occasionally solves problems perfectly on the first attempt, using these correction tools generally produces better solutions faster.  
虽然 Claude Code 有时可以完美地在一开始就解决问题，但使用这些纠正工具通常可以更快地产生更好的解决方案。

### f. Use /clear to keep context focused使用 /clear 保持上下文集中

During long sessions, Claude's context window can fill with irrelevant conversation, file contents, and commands. This can reduce performance and sometimes distract Claude. Use the `/clear` command frequently between tasks to reset the context window.  
在长时间会话中，Claude 的上下文窗口可能会充满无关的对话、文件内容和命令。这可能会降低性能，有时还会分散 Claude 的注意力。在任务之间频繁使用 `/clear` 命令以重置上下文窗口。

### g. Use checklists and scratchpads for complex workflowsg. 使用清单和便签纸进行复杂的工作流程

For large tasks with multiple steps or requiring exhaustive solutions—like code migrations, fixing numerous lint errors, or running complex build scripts—improve performance by having Claude use a Markdown file (or even a GitHub issue!) as a checklist and working scratchpad:  
对于需要多个步骤或需要详尽解决方案的大任务——如代码迁移、修复多个 lint 错误或运行复杂的构建脚本——通过让 Claude 使用 Markdown 文件（甚至 GitHub 问题！）作为清单和工作便签纸来提高性能：

For example, to fix a large number of lint issues, you can do the following:  
例如，要修复大量代码风格问题，你可以这样做：

1. **Tell Claude to run the lint command** and write all resulting errors (with filenames and line numbers) to a Markdown checklist  
	指示 Claude 运行 lint 命令，并将所有结果错误（包括文件名和行号）写入 Markdown 清单
2. **Instruct Claude to address each issue one by one**, fixing and verifying before checking it off and moving to the next  
	指导 Claude 逐个处理每个问题，修复并验证后再勾选并移动到下一个

### h. Pass data into Claudeh. 将数据传递给 Claude

Several methods exist for providing data to Claude:  
Claude 存在多种提供数据的方法：

- **Copy and paste** directly into your prompt (most common approach)  
	直接复制粘贴到你的提示中（最常见的方法）
- **Pipe into Claude Code** (e.g., `cat foo.txt | claude`), particularly useful for logs, CSVs, and large data  
	通过 Claude Code 管道输入（例如， `cat foo.txt | claude` ），特别适用于日志、CSV 和大量数据
- **Tell Claude to pull data** via bash commands, MCP tools, or custom slash commands  
	让 Claude 通过 bash 命令、MCP 工具或自定义斜杠命令拉取数据
- **Ask Claude to read files** or fetch URLs (works for images too)  
	请让 Claude 读取文件或获取 URL（也适用于图片）

Most sessions involve a combination of these approaches. For example, you can pipe in a log file, then tell Claude to use a tool to pull in additional context to debug the logs.  
大多数会话都涉及这些方法的组合。例如，您可以输入日志文件，然后告诉 Claude 使用工具来获取额外的上下文以调试日志。

## 5\. Use headless mode to automate your infra5. 使用无头模式来自动化您的基础设施

Claude Code includes [headless mode](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview#automate-ci-and-infra-workflows) for non-interactive contexts like CI, pre-commit hooks, build scripts, and automation. Use the `-p` flag with a prompt to enable headless mode, and `--output-format stream-json` for streaming JSON output.  
Claude Code 包含无头模式，适用于 CI、预提交钩子、构建脚本和自动化等非交互式环境。使用提示中的 `-p` 标志来启用无头模式，并使用 `--output-format stream-json` 来流式传输 JSON 输出。

Note that headless mode does not persist between sessions. You have to trigger it each session.  
注意，无头模式不会在会话之间持久化。您需要在每个会话中触发它。

### a. Use Claude for issue triagea. 使用 Claude 进行问题分类

Headless mode can power automations triggered by GitHub events, such as when a new issue is created in your repository. For example, the public [Claude Code repository](https://github.com/anthropics/claude-code/blob/main/.github/actions/claude-issue-triage-action/action.yml) uses Claude to inspect new issues as they come in and assign appropriate labels.  
无头模式可以为 GitHub 事件触发的自动化提供动力，例如，当您在存储库中创建新问题时。例如，公共 Claude Code 存储库使用 Claude 检查新问题并分配适当的标签。

### b. Use Claude as a linterb. 将 Claude 用作代码检查器

Claude Code can provide [subjective code reviews](https://github.com/anthropics/claude-code/blob/main/.github/actions/claude-code-action/action.yml) beyond what traditional linting tools detect, identifying issues like typos, stale comments, misleading function or variable names, and more.  
Claude 代码可以提供超越传统代码检查工具的主观代码审查，识别诸如错别字、过时的注释、误导性的函数或变量名等问题。

## 6\. Uplevel with multi-Claude workflows6. 使用多 Claude 工作流程提升

Beyond standalone usage, some of the most powerful applications involve running multiple Claude instances in parallel:  
除了独立使用之外，一些最强大的应用涉及并行运行多个 Claude 实例：

### a. Have one Claude write code; use another Claude to verifya. 让一个 Claude 编写代码；使用另一个 Claude 进行验证

A simple but effective approach is to have one Claude write code while another reviews or tests it. Similar to working with multiple engineers, sometimes having separate context is beneficial:  
一种简单但有效的方法是让一个 Claude 编写代码，另一个进行审查或测试。类似于与多个工程师合作，有时拥有单独的上下文是有益的：

1. Use Claude to write code  
	使用 Claude 编写代码
2. Run `/clear` or start a second Claude in another terminal  
	运行 `/clear` 或在另一个终端启动第二个 Claude
3. Have the second Claude review the first Claude's work  
	让第二个 Claude 审查第一个 Claude 的工作
4. Start another Claude (or `/clear` again) to read both the code and review feedback  
	再次启动另一个 Claude（或 `/clear` ），以阅读代码和审阅反馈
5. Have this Claude edit the code based on the feedback  
	让这个 Claude 根据反馈编辑代码

You can do something similar with tests: have one Claude write tests, then have another Claude write code to make the tests pass. You can even have your Claude instances communicate with each other by giving them separate working scratchpads and telling them which one to write to and which one to read from.  
你还可以用类似的方法处理测试：让一个 Claude 编写测试，然后让另一个 Claude 编写代码以通过这些测试。你甚至可以让你的 Claude 实例通过给它们不同的工作草稿并告诉它们写入哪个、读取哪个来相互通信。

This separation often yields better results than having a single Claude handle everything.  
这种分离通常比让单个 Claude 处理所有事情产生更好的结果。

### b. Have multiple checkouts of your repob. 对你的仓库进行多次检出

Rather than waiting for Claude to complete each step, something many engineers at Anthropic do is:  
与等待 Claude 完成每个步骤相比，Anthropic 的许多工程师会这样做：

1. **Create 3-4 git checkouts** in separate folders  
	在不同的文件夹中创建 3-4 个 git 检出
2. **Open each folder** in separate terminal tabs  
	在不同的终端标签页中打开每个文件夹
3. **Start Claude in each folder** with different tasks  
	在每个文件夹中启动 Claude 执行不同的任务
4. **Cycle through** to check progress and approve/deny permission requests  
	循环检查进度并批准/拒绝权限请求

### c. Use git worktrees c. 使用 git worktree

This approach shines for multiple independent tasks, offering a lighter-weight alternative to multiple checkouts. Git worktrees allow you to check out multiple branches from the same repository into separate directories. Each worktree has its own working directory with isolated files, while sharing the same Git history and reflog.  
此方法适用于多个独立任务，提供了一种比多个检出更轻量级的替代方案。Git worktree 允许您从同一存储库检出多个分支到不同的目录。每个 worktree 都有自己的工作目录和独立的文件，同时共享相同的 Git 历史和 reflog。

Using git worktrees enables you to run multiple Claude sessions simultaneously on different parts of your project, each focused on its own independent task. For instance, you might have one Claude refactoring your authentication system while another builds a completely unrelated data visualization component. Since the tasks don't overlap, each Claude can work at full speed without waiting for the other's changes or dealing with merge conflicts:  
使用 git 工作树，您可以在项目的不同部分同时运行多个 Claude 会话，每个会话都专注于自己的独立任务。例如，您可能有一个 Claude 正在重构您的认证系统，而另一个则构建一个完全无关的数据可视化组件。由于任务不重叠，每个 Claude 都可以以全速工作，无需等待另一个的更改或处理合并冲突：

1. **Create worktrees**: `git worktree add ../project-feature-a feature-a` 创建工作树： `git worktree add ../project-feature-a feature-a`
2. **Launch Claude in each worktree**: `cd ../project-feature-a && claude`  
	在每个工作树中启动 Claude： `cd ../project-feature-a && claude`
3. **Create additional worktrees** as needed (repeat steps 1-2 in new terminal tabs)  
	根据需要创建更多工作树（在新终端标签中重复步骤 1-2）

Some tips:一些技巧：

- Use consistent naming conventions  
	使用一致的命名约定
- Maintain one terminal tab per worktree  
	每个工作树维护一个终端标签页
- If you’re using iTerm2 on Mac, [set up notifications](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview#notification-setup) for when Claude needs attention  
	如果你在 Mac 上使用 iTerm2，为 Claude 需要关注时设置通知
- Use separate IDE windows for different worktrees  
	为不同的工作树使用独立的 IDE 窗口
- Clean up when finished: `git worktree remove ../project-feature-a`  
	完成后清理： `git worktree remove ../project-feature-a`

### d. Use headless mode with a custom harnessd. 使用带有自定义脚手的无头模式

`claude -p` (headless mode) integrates Claude Code programmatically into larger workflows while leveraging its built-in tools and system prompt. There are two primary patterns for using headless mode:  
`claude -p` （无头模式）将 Claude Code 程序化集成到更大的工作流程中，同时利用其内置工具和系统提示。使用无头模式主要有两种模式：

1\. **Fanning out** handles large migrations or analyses (e.g., analyzing sentiment in hundreds of logs or analyzing thousands of CSVs):  
1\. 扩展处理大量迁移或分析任务（例如，分析数百个日志中的情感或分析数千个 CSV 文件）：

1. Have Claude write a script to generate a task list. For example, generate a list of 2k files that need to be migrated from framework A to framework B.  
	让 Claude 编写一个生成任务列表的脚本。例如，生成需要从框架 A 迁移到框架 B 的 2k 个文件列表。
2. Loop through tasks, calling Claude programmatically for each and giving it a task and a set of tools it can use. For example: `claude -p “migrate foo.py from React to Vue. When you are done, you MUST return the string OK if you succeeded, or FAIL if the task failed.” --allowedTools Edit Bash(git commit:*)`  
	遍历任务，针对每个任务调用 Claude，并给它分配一个任务以及可以使用的工具集。例如： `claude -p “migrate foo.py from React to Vue. When you are done, you MUST return the string OK if you succeeded, or FAIL if the task failed.” --allowedTools Edit Bash(git commit:*)`
3. Run the script several times and refine your prompt to get the desired outcome.  
	运行脚本多次，并不断优化你的提示以获得期望的结果。

2\. **Pipelining** integrates Claude into existing data/processing pipelines:  
2\. 管道集成将 Claude 集成到现有的数据处理/处理管道中：

1. Call `claude -p “<your prompt>” --json | your_command`, where `your_command` is the next step of your processing pipeline  
	调用 `claude -p “<your prompt>” --json | your_command` ，其中 `your_command` 是你的处理管道的下一步
2. That’s it! JSON output (optional) can help provide structure for easier automated processing.  
	就这样！可选的 JSON 输出可以帮助提供结构，以便于更轻松的自动化处理。

For both of these use cases, it can be helpful to use the `--verbose` flag for debugging the Claude invocation. We generally recommend turning verbose mode off in production for cleaner output.  
对于这两个用例，使用 `--verbose` 标志进行 Claude 调用的调试可能会有所帮助。我们通常建议在生产环境中关闭详细模式以获得更清晰的输出。

What are your tips and best practices for working with Claude Code? Tag @AnthropicAI so we can see what you're building!  
您在使用 Claude Code 时有哪些技巧和最佳实践？请标记@AnthropicAI，以便我们可以看到您正在构建的内容！

## Acknowledgements 致谢

Written by Boris Cherny. This work draws upon best practices from across the broader Claude Code user community, whose creative approaches and workflows continue to inspire us. Special thanks also to Daisy Hollman, Ashwin Bhat, Cat Wu, Sid Bidasaria, Cal Rueb, Nodir Turakulov, Barry Zhang, Drew Hodun and many other Anthropic engineers whose valuable insights and practical experience with Claude Code helped shape these recommendations.  
本文由 Boris Cherny 撰写。这项工作借鉴了更广泛的 Claude Code 用户社区的实践经验，他们的创新方法和工作流程一直激励着我们。特别感谢 Daisy Hollman、Ashwin Bhat、Cat Wu、Sid Bidasaria、Cal Rueb、Nodir Turakulov、Barry Zhang、Drew Hodun 以及许多其他 Anthropic 工程师，他们的宝贵见解和 Claude Code 的实际经验帮助形成了这些建议。