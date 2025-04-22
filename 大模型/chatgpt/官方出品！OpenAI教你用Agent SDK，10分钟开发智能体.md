---
标题: "官方出品！OpenAI教你用Agent SDK，10分钟开发智能体"
链接: "https://mp.weixin.qq.com/s/w93ZS2FtJukK8NGRnY3vWA"
作者: "[[微信公众平台]]"
创建时间: "2025-04-22T12:25:54+08:00"
摘要: "{{\"One-sentence summary of the article content,translated to Chinese\"}}"
tags:
  - "clippings"
  - "{{\"Analyze the article and create up to 5 tags in comma-separated format. Tags should be in Chinese unless necessary for company names"
  - "person names or abbreviations. One tag must be selected from: \"UI 设计"
  - "AI"
  - "编程"
  - "经济"
  - "效率"
  - "产品\". Other tags should be based on the article's topic"
  - "mentioned people"
  - "companies or products.\"}}"
字数: "11"
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
2025-04-21 06:49:32

精确发文时间由壹伴提供

手机阅读

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMkvxLZ6qyzuEIa1sKPtqR9XSPSMAqdckRpK7QtLAsUagMhcc06NOTN8YUUgugV8Ip3aUqmjDTOHPg/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247519924&idx=1&sn=1d9ab5f154bab99bf87b8ba6539385a2&scene=21#wechat_redirect)

OpenAI 发布了首个 Agent官方 开发指南，帮助开发者如何通过其 SDK 快速开发智能体。

在这份指南中， OpenAI 详细介绍了从智能体的大模型选择，工具定义，复杂智能体，安全护栏等所有开发流程，并附加了大量实际开发案例。

即便你不使用 OpenAI 开源的 AgentSDK 来开发智能体，也可以作为开发参考样本，它提供了清晰的开发框架和思路，无论是开发老鸟还是刚入门的新人都能获得很好的启发。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cqFS2ib9iaiaHx3icdJvicD0s5yfoouNibFu1Cq3tePT0GELlSbmbCTgEpLjA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

文件地址： https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf?

开源 SDK ： https://github.com/openai/openai-agents-python

下面「 AIGC 开放社区」就为大家简单解读一下这份指南。

根据 Gartner2024 年报告显示,全球企业在业务流程自动化的年投入已超 470 亿美元,但 73% 的企业表示传统规则引擎（如 RPA ）在处理复杂决策时效率很低。例如,金融行业的支付欺诈分析中,传统规则引擎仅能基于预设阈值标记交易,而无法识别规则外的隐性风险模式。

而 OpenAI 的调研显示,在客服、供应链管理、代码审查等场景中,超过 60% 的流程因涉及非结构化数据处理或模糊决策,难以通过传统自动化技术实现。这种困境在保险理赔处理中尤为明显。

某头部保险公司数据显示,其人工处理一份家庭保险索赔平均耗时 4.2 小时,其中 70% 的时间用于解读用户文本描述和文档内容。传统 OCR 技术虽能提取结构化字段,但面对用户手写备注或模糊表述时,准确率仅为 58%,而基于大模型的智能体则能将处理效率提升至 1.5 小时,准确率达 92% 。

多智能体复杂架构

OpenAI 认为，在开发多智能体时并非简单的智能体叠加，而是通过系统化的任务拆解、控制权转移与上下文共享，使不同智能体在统一目标下形成高效协作，其设计核心在于平衡分工效率与协同成本。

多智能体架构的应用场景主要集中在三类复杂场景：流程需跨领域知识整合，例如，医疗诊断需结合影像分析、病史记录与药理学等；

工具数量超过单智能体管理阈值，通常建议超过 20 个工具时考虑拆分；决策逻辑包含多层条件分支，例如，金融风控中的申请初审 → 信用评分 → 人工复核链式判断。

以某跨国企业的供应链智能体为例，其单智能体在集成仓储、运输、海关、供应商管理等 30+ 工具后，出现工具调用冲突率上升 18% 、响应延迟增加等问题。通过拆分为 “ 需求预测智能体 ”“ 物流调度智能体 ”“ 合规审查智能体 ” 后，冲突率降至 3% ，整体处理时效提升 40% 。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cuRwkdoU2ia6wppPtlE5Rw9rcD29iaRVDkbXv4qFhwhT6h1biaP7TbWXPw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在多智能体协作模式方面主要有管理者和去中心化两种模式：在管理者模式中，中央智能体作为唯一入口，通过工具调用接口协调多个专用智能体。例如，翻译智能体接收到 “ 将合同译为英法西三语 ” 请求时，管理者智能体分别调用英语、法语、西班牙语子智能体，收集结果后合并输出，全程由管理者维护上下文一致性。

一家法律科技公司采用此模式开发合同审查系统，主智能体负责解析用户需求，子智能体分别处理 “ 合规性检查 ”“ 条款风险评估 ”“ 行业惯例匹配 ” 任务，使复杂合同审查效率从 20 小时缩短至 3 小时，错误率下降 55% 。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cq4tq2ACrsEOj8vzKsEplic4kzVwpshCg71oQVhEMoM91ic7iadMOnB0jw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

去中心化模式则摒弃中央协调者，智能体间通过 Handoff 机制直接转移控制权。例如，客户服务系统中的 “ 分诊智能体 ” 识别到技术故障请求后，直接将对话状态传递给 “ 技术支持智能体 ” ，后者处理完毕后可自主决定是否交接回主智能体或结束流程。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cQgslUiaTTQhZGqHiclQ0839YsDqXRp9TrNeyKM4qOrhenpicAFibSmHgcw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

一个电商售后智能体采用此模式，将 “ 退货申请 → 商品检测 → 退款处理 ” 流程分配给三个智能体，通过交接机制实现全自动化，人工介入率从 32% 降至 8% ，且每个环节的处理时效可独立优化，例如，检测智能体引入计算机视觉模型后，质检时间从 24 小时缩短至 4 小时。

但是这两种模式在实施的时候有着明显的差异：管理者模式依赖统一的工具例如， OpenAIAgentsSDK 中的 as\_tool() 接口，确保子智能体可被中央智能体识别为标准化工具，其优势在于集中控制风险，但可能形成单点瓶颈；

去中心化模式则需定义跨智能体的上下文传递协议，如 JSON 格式的对话历史，优势在于并行处理能力强，如多个子智能体可同时处理不同任务分支，但对智能体间的语义一致性要求更高。

所以，在实际应用中经常会使用混合的智能体架构。例如，一个制造智能体在 “ 订单接收 → 工艺设计 → 生产调度 → 质量检测 ” 主流程中采用管理者模式，由中央智能体统筹；

而在 “ 工艺设计 ” 环节内部，启用去中心化模式，让 “ 模具设计智能体 ”“ 材料选型智能体 ”“ 成本核算智能体 ” 并行协作，最终使订单交付周期缩短 25% ，工艺设计成本降低 18% 。这种 “ 分层协同 ” 策略既避免单一模式的局限性，又能根据任务阶段动态调整协同粒度。

智能体工具定义

工具定义是智能体与实际业务交互的核心，主要围绕标准化、可复用性与安全性展开，确保智能体能够通过 API 、 MCP 等接口，高效调用外部系统自动完成复杂任务。

工具定义主要可划分为三大类：第一类是数据获取工具，用于收集任务所需信息，例如， Web 搜索工具、文档解析工具（可提取 PDF 中的关键数据），一个法律智能体通过集成 Westlaw 法律数据库 API ，将案例检索效率提升 4 倍；

第二类是操作执行工具，直接对外部系统执行操作，例如，支付接口、代码合并工具（ GitHubActions ），一个 DevOps 智能体通过调用代码执行工具，将自动化测试部署时间从 2 小时压缩至 15 分钟；

第三类是智能体间协作工具，允许将其他智能体封装为工具，实现复杂任务的分解，例如，翻译智能体可调用法语、西班牙语等子智能体完成多语言处理，响应延迟控制在 2 秒以内。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cwcXa5ZiaBXtjsJrn0eKT5GcXq7RnOhrl1ECEmKtUia6dgibaEy9ygic9Vg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

开发者在使用各种工具时，从功能、安全角度来考虑， OpenAI 给出了 4 大建议。

风险分级管理机制：根据工具操作的影响程度，例如，只读、写入、可逆性、财务风险，将工具划分为低、中、高风险等级。

低风险工具（如天气查询）可直接自动调用，中风险工具（如用户数据修改）需附加参数校验，高风险工具（如资金转账、系统删除）则必须触发人工审核或二次确认流程。

一个银行智能体对大额转账工具设置双重生物识别验证，使操作失误率从 0.3% 降至 0.05% ，同时通过实时监控工具调用日志，实现风险事件的秒级响应。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cGWTB9eexV3pjHkuyHKD4LVc8evd4ESuju8VOvLcnEQnCUhGktiaKsFw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

对于那些无法使用 API 的遗留系统， OpenAI 建议使用 UI 自动化库模拟人类操作，这类工具通过图像识别定位界面元素并执行点击、输入等动作。虽执行效率低于 API 调用，但可兼容老旧系统。例如，一个制造业企业的智能体通过计算机视觉工具接入未升级的 ERP 系统，成功将设备报修流程自动化，人工介入率从 80% 降至 20% 。

建议可复用的工具库，企业可建立共享工具仓库，沉淀通用工具（如地址校验、验证码生成），避免重复开发。某跨国企业通过工具库管理 200+ 标准化工具，在开发新智能体时， 70% 的工具可直接复用，研发周期缩短 50% 。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2ck02MpicMSAnTV8gKOYUibMHW1MQ6eeDR7ibZjFJaXtSzNJrmtfZ9a0tnQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

此外，工具需配备版本管理机制，通过语义化版本号（如 v1.2.3 ）标识功能变更，某金融科技公司通过强制工具版本兼容性检查，将因工具升级导致的智能体故障减少 90% 。

在工具与智能体的交互层面， OpenAI 推荐使用函数调用格式，如 JSON-RPC 传递参数，确保数据结构的一致性。例如，智能体调用 “ 订单查询工具 ” 时，需传入包含订单号、用户 ID 的结构化参数，工具返回包含物流状态、预计到达时间的 JSON 对象，这种标准化交互使智能体逻辑与工具实现解耦，便于独立升级。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cKibqeooBlYwsHyTZeB04OqHicLNgTtdxVTuyaJP2qrn3CV6w0Tw9wREA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

一个电商智能体在切换物流供应商 API 时，仅修改工具实现层代码，智能体核心逻辑无需调整，系统停机时间从 4 小时降至 30 分钟。

如何选择适合智能体的大模型

智能体与传统的 RPA 最大区别在于使用了大模型充当其“大脑”，这比 OCR 、 NLP 、 ASR 等传统 AI 在数据识别、理解方面更强。

不过在应用智能体时不仅要从能力方面选择大模型，还要从经济角度来考虑。例如， GPT-4o 具备更强的复杂推理能力，但其 token 成本是 GPT-3.5-turbo 的 16 倍，且单次调用延迟约为后者的 3-5 倍。

这种差异直接影响智能体在实际场景中的可行性 —— 某电商客服智能体若采用 GPT-4o 处理所有对话，月算力成本超 12,000 美元，而切换至 GPT-3.5-turbo 后成本可降至 4,500 美元以下，而意图识别准确率仅下降 3% （从 95% 至 92% ），这一性价比优势使其成为更优选择。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/bVibMfbuuqMkZsFwKsJmys2iaicHicFGAK2cGOJcr4TzwkQ6Wo2PAiaEyUoEtDibeHciadiaKicTaR3LC9KDibKkOKwnsQGw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

所以， OpenAI 建议开发者在选择大模型时，可以根据场景来进行适配，执行简单自动化任务时，可以选择延迟、成本低的模型；执行跨平台复杂任务时可以选择性能更强的大模型，尤其是在金融、医疗这样对数据识别率要求极高的行业。

OpenAI 还建议使用模型蒸馏和提示词优化，进一步降低智能体大模型的成本。例如，将 GPT-4o 的决策逻辑蒸馏至 GPT-3.5-turbo ，可使模型体积缩小 80% ，同时通过提示词优化，例如，增加请分步骤思考等引导语，在代码生成任务中使小模型的准确率仅比原模型低 5% 。

一家教育科技公司通过此方法，将编程教学智能体的模型成本降低 70% ，而学生代码通过率维持在 85% 以上。

此外，在选择合适的大模型时还需要建立闭环反馈机制。智能体在生产环境中持续收集模型调用数据，例如，响应时间、错误类型、用户满意度，通过 A/B 测试对比不同模型组合的表现。

一家物流公司的智能体在路径规划任务中，初始采用 GPT-3.5-turbo ，但发现复杂路况下路线优化效率不足，经数据反馈后引入专门训练的轻量级强化学习模型与 GPT-3.5-turbo 协同工作，使运输成本降低 12% ，配送时效提升 9%。

本文素材来源OpenAI，如有侵权请联系删除

END

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMmBbbpQsIn8UfHicQ8BmicGjUuv1RSwibIceJUCVuL1kOPIMso1FVwgVRwZuQ5YwyOcVS6R7xPBW6R3g/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247520041&idx=1&sn=ce2593f449fcb0dc96d470e0a08d032d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/bVibMfbuuqMmBbbpQsIn8UfHicQ8BmicGjUCibxydoE4wIiaicyjQoSgonImMLUU1VpdOqYuYI9V6icJDllia0wHAuE8IA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=Mzg3Mzg5MjY3Nw==&mid=2247519850&idx=1&sn=ca9eba73ef827f579159aaf52577f2de&scene=21#wechat_redirect)

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E) ![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

素材来源官方媒体/网络新闻

继续滑动看下一个

AIGC开放社区

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功