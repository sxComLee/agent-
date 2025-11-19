---
标题: "技能如何运作？, 技能类型, 主要优势, 技能与其他 Claude 功能的比较, 了解更多关于技能的信息-What are Skills? | Claude Help Center"
链接: "https://support.claude.com/en/articles/12512176-what-are-skills"
作者:
创建时间: 2025-11-19T09:04:11+08:00
摘要: "技能是 Claude 动态加载的指令、脚本和资源文件夹，用于提升特定任务的执行效果，通过渐进式披露机制智能调用相关技能来完成任务。"
tags:
  - "clippings"
  - "AI"
  - "效率"
  - "产品"
  - "Claude技能"
  - "工作流程自动化"
字数: 508
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
## What are Skills? 什么是技能？

Skills are folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. Skills teach Claude how to complete specific tasks in a repeatable way, whether that's creating documents with your company's brand guidelines, analyzing data using your organization's specific workflows, or automating personal tasks.  
技能是指令、脚本和资源的文件夹集合，Claude 通过动态加载这些内容来提升特定任务的执行效果。技能教会 Claude 以可重复的方式完成具体任务——无论是按照公司品牌规范创建文档，运用组织特定工作流程分析数据，还是实现个人任务自动化。

Skills are available as a feature preview for users on Pro, Max, Team, and Enterprise plans. This feature preview requires [code execution to be enabled](https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude#h_1c99382190). Skills are also available in beta for Claude Code users and for all API users using the code execution tool.  
技能功能目前面向 Pro、Max、Team 及 Enterprise 方案用户作为预览版开放。该预览功能需启用代码执行权限。同时技能功能也面向 Claude Code 用户处于测试阶段，所有使用代码执行工具的 API 用户均可使用。

Skills improve Claude’s consistency, speed, and performance on many tasks. Skills work through progressive disclosure—Claude determines which Skills are relevant and loads the information it needs to complete that task, helping to prevent context window overload.  
技能能显著提升 Claude 在处理各类任务时的一致性、速度和性能。其运作基于渐进式披露机制——Claude 会智能判断相关技能并动态加载所需信息来完成任务，有效避免上下文窗口过载问题。

When you ask Claude to complete a task, it reviews available Skills, loads relevant ones, and applies their instructions.  
当你要求克劳德完成任务时，它会检查可用技能，加载相关技能，并应用这些技能的指令。

These are Skills created and maintained by Anthropic, such as enhanced document creation for Excel, Word, PowerPoint, and PDF files. Anthropic Skills are available to all users and Claude invokes them automatically when relevant.  
这些是由 Anthropic 创建和维护的技能，例如针对 Excel、Word、PowerPoint 和 PDF 文件的增强文档创建功能。所有用户均可使用 Anthropic 官方技能，克劳德会在相关场景下自动调用这些技能。

These are Skills you or your organization create for specialized workflows and domain-specific tasks. Here are some potential workflows you could enable using custom Skills:  
这些是您或您的组织为专业工作流程和特定领域任务创建的技能。以下是您可以通过自定义技能实现的一些潜在工作流程：

- Apply brand style guidelines to documents and presentations.  
	将品牌风格指南应用于文档和演示文稿。
- Generate communications following company email templates.  
	按照公司电子邮件模板生成通讯内容。
- Structure meeting notes with company-specific formats.  
	按照公司特定格式整理会议记录。
- Create tasks in company tools (JIRA, Asana, Linear) following team conventions.  
	遵循团队规范，在公司工具（JIRA、Asana、Linear）中创建任务。
- Execute company-specific data analysis workflows.  
	执行公司特定的数据分析工作流程。
- Automate personal workflows and customize Claude to match your work style.  
	自动化个人工作流程，并自定义 Claude 以匹配您的工作风格。

**Improvement in Claude’s performance of specific tasks**: Skills provide specialized capabilities for tasks like document creation, data analysis, and domain-specific work that requires supplementing Claude's general knowledge.  
提升克劳德在特定任务中的表现：技能为文档创建、数据分析和需要补充克劳德通用知识的领域特定工作等任务提供专业化能力。

**Organizational knowledge capture**: Package your company's workflows, best practices, and institutional knowledge for Claude to use consistently across your team.  
组织知识沉淀：将公司的工作流程、最佳实践和制度知识打包封装，供克劳德在团队中保持统一使用。

**Easy customization**: Anyone can create Skills by writing instructions in Markdown—no coding required for simple Skills, though you can attach executable scripts to custom Skills for more advanced functionality.  
轻松定制：任何人都可以通过编写 Markdown 格式的指令来创建技能——简单技能无需编码，但您可以为自定义技能附加可执行脚本以实现更高级的功能。

[Projects](https://support.claude.com/en/articles/9517075-what-are-projects) provide static background knowledge that's always loaded when you start chats within them. Skills provide specialized procedures that activate dynamically when needed and work everywhere across Claude.  
项目提供静态背景知识，在项目内开始对话时始终加载。技能则提供专门流程，在需要时动态激活，并在 Claude 全域通用。

MCP connects Claude to external services and data sources. Skills provide procedural knowledge—instructions for how to complete specific tasks or workflows. You can use both together: MCP connections give Claude access to tools, while Skills teach Claude how to use those tools effectively.  
MCP 将 Claude 连接到外部服务和数据源。技能提供程序性知识——即如何完成特定任务或工作流程的指导说明。您可以同时使用两者：MCP 连接让 Claude 能够使用工具，而技能则教会 Claude 如何高效运用这些工具。

[Custom instructions](https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features) apply broadly to all your conversations. Skills are task-specific and only load when relevant, making them better for specialized workflows.  
自定义指令广泛适用于所有对话。技能则针对特定任务，仅在相关时加载，因此更适用于专业化工作流程。

For more detailed information about how Skills work, see [Agent Skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) in our Claude Docs.  
有关技能工作原理的更多详细信息，请参阅 Claude 文档中的代理技能。

Did this answer your question?  
这回答了您的问题吗？