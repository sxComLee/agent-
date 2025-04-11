---
标题: "Apache Doris × AI 的5个应用场景（附完整案例）"
链接: "https://mp.weixin.qq.com/s/ZHBLaRnzED00KsY-rJOMQw"
作者: "[[ADC张彬华]]"
创建时间: "2025-04-11T11:38:09+08:00"
摘要: "文章介绍了Apache Doris与AI技术结合的五个应用场景，包括数据智能助手、RAG知识库、ChatBI系统等，并附有完整案例。"
tags:
  - "clippings"
  - "AI"
  - "数据分析"
  - "Apache Doris"
  - "大数据"
  - "效率"
字数: "651"
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
原创 ADC张彬华 *2025年04月08日 07:38* *广东*

点击上方 蓝字 关注一臻数据👆

免费领取 DeepSeek➕数据AI知识库 🔗 一起共建共进  

> ❝
> 
> 你是否也有过这样的经历：一边是堆积如山的企业数据，一边是炙手可热的AI大模型，两者之间却像是隔了一条鸿沟，难以搭建起高效的桥梁。
> 
> 数据分析师忙得焦头烂额，业务人员对数据 x AI洞察的渴望却始终难以满足...不过，随着 `Apache Doris与AI技术的深度融合` ，这一困境正在被彻底打破。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCkqoGhDWGrRzI2zOqabxc1ILlMYn3vibicLyE7JLhWheJ1npaMPkH2LtQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## Doris遇上AI，火花四溅

"嘿，听说了吗？Apache Doris现在能和AI `谈恋爱` 了！"

办公室里，数据架构师小张兴奋地对产品经理小李说道。

"啥？数据库也能谈恋爱？"小李一脸困惑。

"不是字面意思啦！是 `Apache Doris与AI的深度融合` 。

好比用自然语言就能直接查询Doris数据，并结合 AI 自动进行决策分析， RAG 技术让企业知识库变得超级智能， ChatBI 让 人人都能成为数据分析师..."

## Doris x AI的关键特性

那么，Doris有哪些关键特性去融合AI？

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCVypsH8R5PjH3eFzhUia2rbc6rGxXgtiaXoty34icADiaauqOrWQIynDJFQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

以上图为例，数据源经过各种数据集成和加工处理后，进入实时数据仓库 Doris 和离线湖仓（如 Hive、Iceberg、Hudi、Paimon），广泛应用于 OLAP 分析场景，同时也可以作为 LLM 上下游的数据底座。例如支撑 `LLM的Logs/ Events / Traces Analysis，Data Science，RAG或ChatBI等场景` 。

在这么一个生态链路中，Doris x AI 主要有以下几个关键特性：

##### 1\. 兼容 MySQL 协议

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCtWUqJZh7gz4Vu9cx46G3NjVehrIsKjtPrJgSlpCqvKsQsX4WUy9iaqw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Doris 采用 MySQL 协议，高度兼容 MySQL 语法，支持标准 SQL。用户可以通过各类客户端工具访问 Apache Doris，并支持与 `各类 LLM 项目及 BI 工具无缝集成` ，使得用户引入Doris时， `学习成本低` ，能够快速上手。

##### 2\. 支持 Arrow Flight SQL 协议

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCCqibb7S5icSWHf9mM1oaWicykE41bInX3Ho7NNxN4cmRzhCUWdOrjVGwg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

虽然 MySQL协议 具有良好兼容性和广泛的工具支持，但Doris默认是列式存储，而MySQL/JDBC/ODBC协议是通过行式传输，会导致与Doris进行数据传输时产生大量行/列的序列化与反序列化动作。在 `数据科学、机器学习等AI` 场景，也会使得FE 容易成为瓶颈、文本协议效率差。

引入 Arrow Flight SQL 协议，助力Doris实现高速数据读取。例如数据可以直接通过 BE 传递到 Pandas 客户端， `列式数据传输` 。

据实测：基于引入 Arrow Flight SQL 协议，Pandas（ `NLP预处理/模型训练` ） 测试 **数据吞吐提升 100 倍** ！

##### 3\. 极致的分析性能

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCNgWUtvAvJq8jJ77BAPDgvRKFou6YndqqPrbdkXHtIC4t43rhmibW1qg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

###### 3.1 执行引擎

Apache Doris 采用 `大规模并行处理（MPP）架构` ，支持节点间和节点内并行执行，以及多个大型表的分布式 Shuffle Join，从而更好地应对复杂查询。

使用 `Pipeline` 执行引擎，将查询分解为多个子任务并行执行，充分利用多核 CPU 的能力，同时通过限制查询线程数来解决线程膨胀问题。Pipeline 执行引擎减少数据拷贝和共享，优化排序和聚合操作，从而显著提高查询效率和吞吐量。

并且在查询引擎侧是 `向量化引擎` ，所有内存结构均按列式布局，可显著减少虚函数调用，提高缓存命中率，并有效利用 SIMD 指令。在宽表聚合场景下，性能是非向量化引擎的 5-10 倍。

###### 3.2 查询优化器

在优化器方面，Doris 采用 ` CBO、RBO 和 HBO 相结合的优化策略` 。RBO 支持常量折叠、子查询重写和谓词下推等优化，CBO 支持 Join Reorder 等优化，HBO 能够基于历史查询信息推荐最优执行计划。多种优化措施确保 Doris 能够在各类查询中枚举出性能优异的查询计划。

###### 3.3 缓存加速

Doris提供Data Cache和SQL Cache进行缓存加速：

1️⃣ Data Cache（数据缓存）通过缓存最近访问的 `远端存储系统` （HDFS 或对象存储）的数据文件到本地磁盘上，加速后续访问相同数据的查询。在频繁访问相同数据的查询场景中，Data Cache 可以避免重复的远端数据访问开销，提升热点数据的查询分析性能和稳定性。

2️⃣ SQL Cache 是 Doris 提供的一种 `查询优化机制` ，可以显著提升查询性能。它通过缓存查询结果来减少重复计算，适用于数据更新频率较低的场景。

###### 3.4 物化视图透明加速

物化视图根据 SQL 定义计算并存储数据，且根据策略进行周期性或实时性更新。物化视图 `可直接查询，也可以将查询透明改写` 。它可用于以下几个场景：

1️⃣ 查询加速

在决策支持系统中，如 BI 报表、Ad-Hoc 查询等，这类分析型查询通常包含聚合操作，可能还涉及多表连接。由于计算此类查询结果较为消耗资源、响应时间可能长达分钟级，且业务场景往往要求秒级响应，可以构建物化视图，对常见查询进行加速。

2️⃣ 轻量化 ETL（数据建模）

在数据分层场景中，可以使用物化视图的嵌套来构建 DWD 和 DWM 层，利用物化视图的调度刷新能力。

3️⃣ 湖仓一体

针对多种外部数据源，可以将这些数据源所使用的表进行物化视图构建，以此来节省从外部表导入数据到内部表的成本，并且加速查询过程。

目前Doris支持同步和异步物化视图：

`同步物化视图` 需要与基表的数据保持强一致性。

`异步物化视图` 与基表的数据保持最终一致性，可能会有一定的延迟。它通常用于对数据时效性要求不高的场景，一般使用 T+1 或小时级别的数据来构建物化视图。如果时效性要求高，则考虑使用同步物化视图。

###### 3.5 智能索引

数据库索引是用于查询加速的，为了加速不同的查询场景，Apache Doris 支持了多种丰富的索引：

**智能索引（自动创建）**

`前缀索引` ：Doris基于排序键自动为每1024行数据创建稀疏索引，直接定位数据块起始位置，加速排序键相关查询。仅需36字节即可触发索引，适合高频过滤场景。

`ZoneMap索引` ：自动维护每列的Min/Max/Null统计信息，快速跳过不满足条件的数据块，优化范围查询和NULL判断。

**倒排索引（手动创建）**

支持文本全文检索和数值/日期的高效过滤，通过值到行号的映射实现精准定位。

特别适合 `LLM日志分析场景` ：支持中文/英文分词（如parser="chinese"），可快速匹配关键词（如MATCH\_ANY查询）。

**全文检索与高级索引**

倒排索引替代旧版Bitmap索引，支持 `多条件组合查询和复杂分析` 。

BloomFilter系列：包括标准BloomFilter（高基数列等值查询）和NGram变种（LIKE模糊匹配），需手动配置。

##### 4\. 开放的湖仓一体

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCJibWmmmC6ib0ZLaTgPIyr6eMHVChXU3wGrocVJDVoJyKn62BD7Bsq1Rw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

Doris 通过 `可扩展的连接器框架、存算分离架构、数据生态开放性和极致的分析性能` ， 为用户提供了优秀的 **湖仓一体解决方案** ：

1️⃣ 可扩展的连接器框架：Doris 定义了标准的数据目录(Catalog)、库(Database)、表(Table)三个层级，帮助开发人员快速对接企业内部特有的数据源( `S3/HDFS：溯源分析/跨域模型训练` )，实现 `数据快速互通` 。

2️⃣ 存算分离架构：不同时间点使用不同规模的计算资源服务业务请求， `按需使用计算资源，节约成本` 。

3️⃣ 数据生态开放性：2.1 版本起，Doris 支持多种 `SQL 方言转换` ，如 Presto、Trino、Hive、PostgreSQL、Spark、Clickhouse 等等。

本文主要介绍以上4个特性，其它特性可具体查看Doris官方文档 🔗： `https://doris.apache.org/zh-CN/docs/dev/gettingStarted/what-is-apache-doris`

了解完Doris x AI的关键特性后，接下来，直接来看看Doris与AI的5个应用场景 👇

## Doris与AI的5个应用场景

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCic8KWjaBdzdS9dJRgPR8gmTOfxQBwiayY3F8rjaeTQEWHSHYt9L1yfPg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

##### 场景一：Doris × DataAgent - 数据有了自己的智能助手

工作中经常出现的这么一个场景：公司号突然被喷，评论区一片狼藉，客服电话被打爆，老板紧急召集会议，大家手忙脚乱却不知从何入手？

现在，有了Doris × DataAgent，一切都变得简单：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCBFWQS0WF7ghfL8fbtXxibjusiaKZ2L1h3eCKLS7BnqQiaDoZYnGHksEqQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

"最近我们产品在社交媒体上的评价怎么样？"

DataAgent接收到这个问题后： `自动连接到Doris数据库，扫描相关Schema，生成SQL查询，执行查询并获取结果，然后调用LLM（如DeepSeek）生成自然语言回答` ：

"过去一周，产品在社交媒体上获得了2,367条评论，总体情感倾向积极，NPS评分比上月提升12%。主要 **正面反馈** 集中在新UI设计和性能提升方面， **负面反馈** 主要关注某些高级功能的学习曲线较陡。 **建议** 重点关注用户B站ID:tech\_lover的长评，该评论获得了最高点赞量..."

这种实时、智能的数据分析能力，正改变着企业的决策方式。 `舆情分析` 、反欺诈决策等高价值场景，都能从这种技术组合中获益匪浅。

附 ⬇️ `Doris x AI舆情分析` 案例：

关注 重播 分享 赞

0 / 0

00:00 / 01:12  进度条，百分之0 [播放](https://mp.weixin.qq.com/s/) 00:00 / 01:1201:12 *全屏* 倍速播放中 <video src="https://mpvideo.qpic.cn/0b2ef4ab6aaah4aifnptbrtval6dd4xqahya.f10002.mp4?dis_k=a24cc66f3c7770e83dc470a07c5dcb80&amp;dis_t=1744336970&amp;play_scene=10120&amp;auth_info=aaWe5JZ7VBNM56npuFBNDTc1Sk1tZBFkYmMBbjAafBpVdCFGAkVuGBkBeRJOMA40OCEc&amp;auth_key=af0722714a3dd7f5dfca20b2ccb8bbfe&amp;vid=wxv_3933022903607672843&amp;format_id=10002&amp;support_redirect=0&amp;mmversion=false">您的浏览器不支持 video 标签</video>

继续观看

Apache Doris × AI 的5个应用场景（附完整案例）

<audio><source src="https://res.wx.qq.com/voice/getvoice?mediaid=MzA3MzA0MTAyNF8xMDAwMDI3Njk="></audio>

[视频详情](https://mp.weixin.qq.com/s/)

🔗 完整文字教程： [Doris x AI舆情分析](https://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487625&idx=1&sn=b92754f817b6675187192724d243d478&scene=21#wechat_redirect)

##### 场景二：Doris × RAG - 让大模型有据可依

" `大模型有时候真是不靠谱，编故事比我还厉害！` "

这是使用AI的企业常有的抱怨。知识的 `时效性、专业领域的局限性、幻觉问题` ，都困扰着AI应用落地。

Doris × RAG组合正是解决这一困境的良方：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCibZPXJicev3Qfhib4VM09m3NQqHLkE8qFxHC1icibHo35fK6YnDuzeQQb0Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1️⃣ 本地数据（如企业知识库文档）通过向量化存储到Doris中

2️⃣ 用户提问时，系统使用Doris高性能查询与 **distance向量函数** ，精准召回相关信息（预计6月份正式发布Doris向量语义搜索）

3️⃣ 大模型基于这些可靠信息生成答案

例如：一位法律顾问使用该系统查询特定案例时，系统不再凭空编造，而是从Doris存储的法律条文、案例库和历史咨询记录中检索出准确信息，然后生成带有明确引用来源的专业回答。

这好比给AI装上了"开卷考试"的能力，极大提升了回答的准确性与可靠性。

附 ⬇️ `Doris+DeepSeek搭建RAG知识库` 案例：

关注 重播 分享 赞

0 / 0

00:00 / 00:40  进度条，百分之0 [播放](https://mp.weixin.qq.com/s/) 00:00 / 00:4000:40 *全屏* 倍速播放中 <video src="https://mpvideo.qpic.cn/0bc3vqadaaaatmak3xptu5tvblgdgcwaamaa.f10002.mp4?dis_k=5336f7bd4aedbda66adc608c78c6da7d&amp;dis_t=1744336970&amp;play_scene=10120&amp;auth_info=O8S8lIdwURZLsKjp4QNNVmFnTU5iMEVlZTYEb2QYexgHJ3QSBktrHR5WeBIXYw5vbnMb&amp;auth_key=a4c355443dc838968294721ab2107952&amp;vid=wxv_3933023568723771397&amp;format_id=10002&amp;support_redirect=0&amp;mmversion=false">您的浏览器不支持 video 标签</video>

继续观看

Apache Doris × AI 的5个应用场景（附完整案例）

<audio><source src="https://res.wx.qq.com/voice/getvoice?mediaid=MzA3MzA0MTAyNF8xMDAwMDI3Njk="></audio>

[视频详情](https://mp.weixin.qq.com/s/)

🔗 完整文字教程： [Doris+DeepSeek搭建RAG知识库](https://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487577&idx=1&sn=6e7c50529a2c42cf3955570180b8a5d2&scene=21#wechat_redirect)

##### 场景三：Doris × ChatBI - 人人都能成为数据分析师

" `老板临时要一份上季度各地区销售额分析报告，还要漂亮的可视化图表，30分钟内！` "

这种紧急需求往往让业务人员手忙脚乱。而有了Doris × ChatBI，一切变得轻松自如：

用户只需用自然语言提问：" `分析上季度各地区销售额，按产品类别细分，并用柱状图展示前五名` "

Doris x ChatBI系统会：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCZjkIxYq1iadWADj01CveQS4ppFP3iacTGEfd9bR2jtncY9x5P3SPsT8Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1️⃣ 结合RAG技术进行相似度召回

2️⃣ 通过DSL规则生成Prompt

3️⃣ 大模型进行语义分析，生成规范查询

4️⃣ Doris快速执行查询，返回结果

5️⃣ 前端自动生成美观的可视化图表

从复杂的数据分析到漂亮的图表，一气呵成， `无需编写一行代码` 。

这种方式特别适合 **两类场景** ：标准化数据分析场景（ `Text2SQL` ）和企业特定业务场景（ `Text2DSL` ）。前者灵活性高，后者准确率和响应速度更有优势。

附 ⬇️ `0代码！教会你用Doris+DeepSeek+Dify搭建ChatBI系统（附完整DSL） ` 案例：

关注 重播 分享 赞

0 / 0

00:00 / 00:39  进度条，百分之0 [播放](https://mp.weixin.qq.com/s/) 00:00 / 00:3900:39 *全屏* 倍速播放中 <video src="https://mpvideo.qpic.cn/0bc3iqadkaaameafxtxkdvtvargdgvcaania.f10002.mp4?dis_k=1c5a39fa2ec264ca6ae88dd6732e17b2&amp;dis_t=1744336970&amp;play_scene=10120&amp;auth_info=GaLc4TkGQU62puG9BExZMWNMHmI2Qmc1NQNrPxouSwcgJEBTHjxKG1B2GktkD2A+dxo=&amp;auth_key=5f3cc39c34c08e383a49496f20d003b5&amp;vid=wxv_3922925796121264131&amp;format_id=10002&amp;support_redirect=0&amp;mmversion=false">您的浏览器不支持 video 标签</video>

继续观看

Apache Doris × AI 的5个应用场景（附完整案例）

<audio><source src="https://res.wx.qq.com/voice/getvoice?mediaid=MzA3MzA0MTAyNF8xMDAwMDI3Njk="></audio>

[视频详情](https://mp.weixin.qq.com/s/)

🔗 完整文字教程： [0代码！教会你用Doris+DeepSeek+Dify搭建ChatBI系统（附完整DSL）](https://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487687&idx=1&sn=1e34b95a0acbe4b4868db894d8affb3e&scene=21#wechat_redirect)

##### 场景四：Doris × MCP - AI能力的"万能转换器"

" `又要开发一个Doris AI应用接口？我的项目排期已经满了！` "

Doris技术团队在对接各种AI能力时，常常面临技术栈割裂、开发周期长的困境。MCP（模型上下文协议）犹如AI世界的" `USB转换器` "，让不同工具和数据源能无缝对接。

Doris × MCP为企业带来了全新的AI能力整合方式：

" **上线一个智能数据助手？半天搞定！** "

系统架构师小王乐呵呵地说。他只需：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSC1h9ZGpr7qr2ItfLAOIHt4U5TSLsTWHmpBnzUV0I8D5ichLCteuujZ7g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1️⃣ 使用兼容MCP Server的Client（SelectDB/Doris Studio规划中）

2️⃣ 连接到Doris MCP Server

3️⃣ 立刻获取多种AI能力： `NL2SQL、查询性能诊断、智能运维等`

某金融科技公司利用这种组合，将原本需要2周开发的 `Doris ChatBI功能，压缩到了1天内完成上线` 。系统还能智能分析SQL执行计划，提供定制化优化建议，可大幅度提升数据库性能。

Doris MCP协议标准化了AI与Doris数据之间的交互，使企业能以更低的成本、更快的速度构建AI应用，真正实现了" `即插即用` "的AI能力。

预计在4月份，正式发布 `Doris MCP MCP Server&Client` ，敬请期待！

##### 场景五：Doris × AI Observability - 大模型应用的"黑匣子"

"大模型应用昨晚2点突然失效了，用户投诉不断，但我们完全不知道发生了什么！"

随着AI应用在企业中的普及， **可观测性** 成为一大挑战。 `大模型调用链复杂，故障诊断困难` 。

Doris提供了高性能、低成本的可观测性解决方案：

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/fibMic00Uxz23icKYIK5Rbiaib8MvFfEIUPSCK0zMmKHF9zZgb4wDap98Ynwb7k1k49jfI2qMqMnxw2ia5RbKLnqIicRw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1️⃣ 存储和分析大量日志、Trace和指标数据

2️⃣ 与OpenTelemetry、ELK等生态集成

3️⃣ 提供标准SQL接口支持Grafana可视化

一个经典场景：某电商平台的AI推荐系统出现异常。运维团队通过Doris × AI Observability快速定位到问题：GPU资源在某时段被其他应用占用，导致推理延迟增加，进而影响了整个推荐链路。

**完整的调用链Trace和资源监控数据让诊断变得直观高效** 。

附 ⬇️ 【走进网易】基于 Doris/SelectDB 构建开放、高性能、低成本的可观测性平台 案例 ： https://www.bilibili.com/video/BV1yNX5YnEba/

## 结语

随着技术的不断演进，Doris与AI的融合还将向更深层次发展：

- 向量语义检索：更完善更精准的相似度检索
- 数据准备与特征存储：为AI模型训练提供高效数据支持
- 湖仓一体集成：无界对接更多的结构化和非结构化数据源
- ChatBI与Agent能力增强：更智能的数据分析体验
- Doris MCP Server&Client：预计在4月正式开源
- ......

这些演进方向正在重塑企业的数据分析与AI应用方式，让数据价值最大化。不仅解决了" `数据孤岛` "和" `AI幻觉` "等传统痛点，同时也开创了数据智能化的新范式。

无论你是数据工程师、数据分析师，还是业务决策者，这场数据与AI智能的共舞都值得你深度参与。


**完**

---

一臻数据致力于大数据AI时代的前沿内容分享，会持续分享更多有趣有用有态度的知识。同时也欢迎大家 **投稿，共建共进** ，帮助圈友们冲破认知壁垒，实现自我提升！

另外，整理了份 **一臻数据知识库** ，其中包含 **Apache Doris** 和 **Data+AI** **的学习资料、学习课程、白皮书、研究报告、行业标准** 和 **实践指南** 等内容，会持续更新，欢迎 **关注公众号，免费领取** 。

---

  

往期推荐

[

*走进* 开源，拥抱开源

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650483656&idx=1&sn=300e90f5017ebb3d97d3e98d26d52ff7&chksm=f374e9aec40360b85c87a26d9d1af93b2807ad1c54340676ce3173fb0508b3be7ca9595182f0&scene=21#wechat_redirect)

[

*大数据* 平台开发规范示例

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650482778&idx=1&sn=6a4a6b3bf16ab818aa38d222ce46fed6&chksm=f374ea3cc403632a0f6ef1a9728393b459c3d19926f8e9672467f278e9f56abb010b198d2b34&scene=21#wechat_redirect)

[

*大数据* 仓库开发规范示例

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650483237&idx=1&sn=824d2125280a009dddeec3f0aa60c4f6&chksm=f374e843c40361551cbbf48c7ad58fb054246a1abc5a60166a29aa7c7a547903848873149902&scene=21#wechat_redirect)

[

*0代码* ！教会你用Doris+DeepSeek+Dify搭建ChatBI系统（附完整DSL）

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487687&idx=1&sn=1e34b95a0acbe4b4868db894d8affb3e&chksm=f374f9e1c40370f7c4bd7996d0a18ee9bbf6e00194c56664488df1b031a638ce4f7e8ee9f41f&scene=21#wechat_redirect)

[

3分钟！教会你用Doris+ *DeepSeek* 搭建RAG知识库（喂饭级教程）

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487529&idx=1&sn=fb6a4c74e6d159d2695be7b8bf4e2b36&chksm=f374f88fc403719945a51d78fe56a2ebe8c264347cf8d56619d2757ffad77dec2a2972c7268a&scene=21#wechat_redirect)

[

3步！教会你用Doris+ *DeepSeek* 搭建ChatBI系统（保姆级教程）

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487577&idx=1&sn=6e7c50529a2c42cf3955570180b8a5d2&chksm=f374f97fc40370692ec22c265976448c1e90b69129cbe9a1802f824efec427aeafa56a89d8dd&scene=21#wechat_redirect)

[

99行代码！教会你用Doris+ *DeepSeek* 实现AI舆情分析

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487625&idx=1&sn=b92754f817b6675187192724d243d478&chksm=f374f92fc40370394c5a4494338b271142c753d44939db4cfe0cbaa32fecfeb71d90aa373271&scene=21#wechat_redirect)

[

*全网* 最 *全* Doris+DeepSeek使用手册（客服/图表/PPT/贺岁诗）！学会了Doris熟练度提高90%【建议收藏】

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487419&idx=1&sn=e06c84f7cfb006b7818aa572aa8a1b55&chksm=f374f81dc403710b0e5961a02f21fc7ae04d0fbf79ae6114acc07b47861cd9aae907e33148a8&scene=21#wechat_redirect)

[

都2025年了，Doris 和 *ClickHouse* 到底怎么选啊！

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650487648&idx=1&sn=c06b5db0631d0285b825392bbce6fb7e&chksm=f374f906c40370106a6dfccde58c33ef52b2343ca371dff024b2f281f9957009cb96f94e86fd&scene=21#wechat_redirect)

[

*深夜* 无需加班，Apache Doris让数据自己会跑

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650485454&idx=1&sn=a73a4a6e78b610cdc47d5e31293d871a&chksm=f374f0a8c40379be78b40cab31721c31f485af5272299ef7f8dbfdd30cff7dc6fcc27b49eb4e&scene=21#wechat_redirect)

[

我用 *X2Doris* 干翻了3000张表，老板还以为我组了个团队

](http://mp.weixin.qq.com/s?__biz=MzI3NjA1MTcyMQ==&mid=2650486392&idx=1&sn=f5bc442775d9478e64c13189f05c96e2&chksm=f374f41ec4037d084781c5072fe63b2338269b2530eb060091a136362d5f5c5a5716eba2302a&scene=21#wechat_redirect)

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

点击下方 蓝字 关注一臻数据

  

继续滑动看下一个

向上滑动看下一个 [知道了](https://mp.weixin.qq.com/s/) ： ， ， ， ， ， ， ， ， ， ， ， ， 。 视频 小程序 赞 ，轻点两下取消赞 在看 ，轻点两下取消在看 分享 留言 收藏 听过