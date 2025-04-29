---
标题: "Contextual Retrieval in AI Systems"
链接: "https://www.anthropic.com/engineering/contextual-retrieval"
作者: "[[@AnthropicAI]]"
创建时间: "2025-04-29T15:42:28+08:00"
摘要: "Anthropic 提出了一种名为“上下文检索”的方法，通过结合上下文嵌入和上下文 BM25 技术，显著提高了 RAG 系统的检索准确性，减少了检索失败率。"
tags:
  - "clippings"
  - "AI"
  - "检索增强生成"
  - "上下文检索"
  - "效率"
  - "Anthropic"
字数: "2506"
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

For an AI model to be useful in specific contexts, it often needs access to background knowledge. For example, customer support chatbots need knowledge about the specific business they're being used for, and legal analyst bots need to know about a vast array of past cases.  
要使 AI 模型在特定上下文中有用，它通常需要访问背景知识。例如，客户支持聊天机器人需要了解它们所使用的特定业务知识，而法律分析机器人需要了解大量过去的案例。

Developers typically enhance an AI model's knowledge using Retrieval-Augmented Generation (RAG). RAG is a method that retrieves relevant information from a knowledge base and appends it to the user's prompt, significantly enhancing the model's response. The problem is that traditional RAG solutions remove context when encoding information, which often results in the system failing to retrieve the relevant information from the knowledge base.  
开发者通常使用检索增强生成（RAG）来增强 AI 模型的知识。RAG 是一种方法，它从知识库中检索相关信息并将其附加到用户的提示中，从而显著提高模型的响应。问题是，传统的 RAG 解决方案在编码信息时会删除上下文，这通常会导致系统无法从知识库中检索到相关信息。

In this post, we outline a method that dramatically improves the retrieval step in RAG. The method is called “Contextual Retrieval” and uses two sub-techniques: Contextual Embeddings and Contextual BM25. This method can reduce the number of failed retrievals by 49% and, when combined with reranking, by 67%. These represent significant improvements in retrieval accuracy, which directly translates to better performance in downstream tasks.  
在本文中，我们介绍了一种显著提高 RAG 检索步骤的方法。这种方法被称为“上下文检索”，并使用两种子技术：上下文嵌入和上下文 BM25。这种方法可以将检索失败的数量减少 49%，当与重排序结合使用时，可以减少 67%。这些代表检索准确性的显著提高，这直接转化为下游任务性能的提升。

You can easily deploy your own Contextual Retrieval solution with Claude with [our cookbook](https://github.com/anthropics/anthropic-cookbook/tree/main/skills/contextual-embeddings).  
您可以使用我们的食谱轻松部署自己的上下文检索解决方案。

### A note on simply using a longer prompt关于简单地使用更长的提示的注意事项

Sometimes the simplest solution is the best. If your knowledge base is smaller than 200,000 tokens (about 500 pages of material), you can just include the entire knowledge base in the prompt that you give the model, with no need for RAG or similar methods.  
有时候，最简单的解决方案才是最好的。如果你的知识库小于 200,000 个 token（大约 500 页材料），你只需将整个知识库包含在提供给模型的提示中，无需 RAG 或类似方法。

A few weeks ago, we released [prompt caching](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) for Claude, which makes this approach significantly faster and more cost-effective. Developers can now cache frequently used prompts between API calls, reducing latency by > 2x and costs by up to 90% (you can see how it works by reading our [prompt caching cookbook](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/prompt_caching.ipynb)).  
几周前，我们为 Claude 发布了提示缓存功能，这使得这种方法变得更加快速和成本效益。开发者现在可以在 API 调用之间缓存频繁使用的提示，通过> 2 倍减少延迟，并将成本降低高达 90%（你可以通过阅读我们的提示缓存食谱了解其工作原理）。

However, as your knowledge base grows, you'll need a more scalable solution. That’s where Contextual Retrieval comes in.  
然而，随着你的知识库增长，你需要一个更可扩展的解决方案。这就是上下文检索的作用所在。

## A primer on RAG: scaling to larger knowledge basesRAG 入门：扩展到更大的知识库

For larger knowledge bases that don't fit within the context window, RAG is the typical solution. RAG works by preprocessing a knowledge base using the following steps:  
对于不适合在上下文窗口内的大型知识库，RAG 是典型的解决方案。RAG 通过以下步骤对知识库进行预处理：

1. Break down the knowledge base (the “corpus” of documents) into smaller chunks of text, usually no more than a few hundred tokens;  
	将知识库（文档的“语料库”）分解成更小的文本块，通常不超过几百个标记；
2. Use an embedding model to convert these chunks into vector embeddings that encode meaning;  
	使用嵌入模型将这些块转换为编码意义的向量嵌入；
3. Store these embeddings in a vector database that allows for searching by semantic similarity.  
	将这些嵌入存储在允许通过语义相似性进行搜索的向量数据库中。

At runtime, when a user inputs a query to the model, the vector database is used to find the most relevant chunks based on semantic similarity to the query. Then, the most relevant chunks are added to the prompt sent to the generative model.  
在运行时，当用户向模型输入查询时，向量数据库会根据与查询的语义相似度找到最相关的片段。然后，将这些最相关的片段添加到发送给生成模型的提示中。

While embedding models excel at capturing semantic relationships, they can miss crucial exact matches. Fortunately, there’s an older technique that can assist in these situations. BM25 (Best Matching 25) is a ranking function that uses lexical matching to find precise word or phrase matches. It's particularly effective for queries that include unique identifiers or technical terms.  
虽然嵌入模型擅长捕捉语义关系，但它们可能会错过关键的确切匹配。幸运的是，有一种较老的技术可以协助这些情况。BM25（最佳匹配 25）是一种排名函数，它使用词汇匹配来找到精确的单词或短语匹配。它特别适用于包含唯一标识符或技术术语的查询。

BM25 works by building upon the TF-IDF (Term Frequency-Inverse Document Frequency) concept. TF-IDF measures how important a word is to a document in a collection. BM25 refines this by considering document length and applying a saturation function to term frequency, which helps prevent common words from dominating the results.  
BM25 通过在 TF-IDF（词频-逆文档频率）概念的基础上工作。TF-IDF 衡量一个词在文档集合中对文档的重要性。BM25 通过考虑文档长度并应用饱和函数到词频来改进这一点，这有助于防止常见词汇主导结果。

Here’s how BM25 can succeed where semantic embeddings fail: Suppose a user queries "Error code TS-999" in a technical support database. An embedding model might find content about error codes in general, but could miss the exact "TS-999" match. BM25 looks for this specific text string to identify the relevant documentation.  
这里是 BM25 如何成功而语义嵌入失败的情况：假设用户在技术支持数据库中查询“错误代码 TS-999”。嵌入模型可能会找到关于错误代码的一般内容，但可能会错过确切的“TS-999”匹配。BM25 会寻找这个特定的文本字符串来识别相关的文档。

RAG solutions can more accurately retrieve the most applicable chunks by combining the embeddings and BM25 techniques using the following steps:  
RAG 解决方案可以通过以下步骤结合嵌入和 BM25 技术，更准确地检索最相关的片段：

1. Break down the knowledge base (the "corpus" of documents) into smaller chunks of text, usually no more than a few hundred tokens;  
	将知识库（文档的“语料库”）分解成更小的文本块，通常不超过几百个标记；
2. Create TF-IDF encodings and semantic embeddings for these chunks;  
	为这些片段创建 TF-IDF 编码和语义嵌入；
3. Use BM25 to find top chunks based on exact matches;  
	使用 BM25 根据精确匹配查找顶级块；
4. Use embeddings to find top chunks based on semantic similarity;  
	使用嵌入向量根据语义相似度查找顶级块；
5. Combine and deduplicate results from (3) and (4) using rank fusion techniques;  
	结合并去重（3）和（4）的结果，使用排名融合技术；
6. Add the top-K chunks to the prompt to generate the response.  
	将顶级块添加到提示中生成响应。

By leveraging both BM25 and embedding models, traditional RAG systems can provide more comprehensive and accurate results, balancing precise term matching with broader semantic understanding.  
通过利用 BM25 和嵌入模型，传统的 RAG 系统可以提供更全面、更准确的结果，在精确的词匹配与更广泛的语义理解之间取得平衡。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F45603646e979c62349ce27744a940abf30200d57-3840x2160.png&w=3840&q=75)

A Standard Retrieval-Augmented Generation (RAG) system that uses both embeddings and Best Match 25 (BM25) to retrieve information. TF-IDF (term frequency-inverse document frequency) measures word importance and forms the basis for BM25. 一个同时使用嵌入和最佳匹配 25（BM25）来检索信息的标准检索增强生成（RAG）系统。TF-IDF（词频-逆文档频率）衡量词的重要性，并构成 BM25 的基础。

This approach allows you to cost-effectively scale to enormous knowledge bases, far beyond what could fit in a single prompt. But these traditional RAG systems have a significant limitation: they often destroy context.  
这种方法可以使您以成本效益的方式扩展到庞大的知识库，远远超出单个提示所能容纳的范围。但是，这些传统的 RAG 系统有一个显著的局限性：它们通常会破坏上下文。

### The context conundrum in traditional RAG传统 RAG 中的上下文难题

In traditional RAG, documents are typically split into smaller chunks for efficient retrieval. While this approach works well for many applications, it can lead to problems when individual chunks lack sufficient context.  
在传统 RAG 中，文档通常被分割成更小的块以实现高效的检索。虽然这种方法对许多应用来说效果很好，但当单个块缺乏足够的上下文时，可能会导致问题。

For example, imagine you had a collection of financial information (say, U.S. SEC filings) embedded in your knowledge base, and you received the following question: *"What was the revenue growth for ACME Corp in Q2 2023?"*  
例如，假设您有一个包含在您的知识库中的财务信息集合（例如，美国证券交易委员会的文件），并且您收到了以下问题：“ACME 公司 2023 年第二季度的收入增长是多少？”

A relevant chunk might contain the text: *"The company's revenue grew by 3% over the previous quarter."* However, this chunk on its own doesn't specify which company it's referring to or the relevant time period, making it difficult to retrieve the right information or use the information effectively.  
一个相关的片段可能包含以下文本：“公司的收入在上个季度增长了 3%。”然而，这个片段本身并没有指定是哪家公司或相关的时间段，这使得检索正确的信息或有效地使用信息变得困难。

## Introducing Contextual Retrieval介绍上下文检索

Contextual Retrieval solves this problem by prepending chunk-specific explanatory context to each chunk before embedding (“Contextual Embeddings”) and creating the BM25 index (“Contextual BM25”).  
上下文检索通过在每个片段前添加特定的解释性上下文（“上下文嵌入”）并创建 BM25 索引（“上下文 BM25”）来解决此问题。

Let’s return to our SEC filings collection example. Here's an example of how a chunk might be transformed:  
让我们回到我们的 SEC 文件集合示例。以下是一个片段可能被转换的例子：

```
original_chunk = "The company's revenue grew by 3% over the previous quarter."

contextualized_chunk = "This chunk is from an SEC filing on ACME corp's performance in Q2 2023; the previous quarter's revenue was $314 million. The company's revenue grew by 3% over the previous quarter."
```

It is worth noting that other approaches to using context to improve retrieval have been proposed in the past. Other proposals include: [adding generic document summaries to chunks](https://aclanthology.org/W02-0405.pdf) (we experimented and saw very limited gains), [hypothetical document embedding](https://arxiv.org/abs/2212.10496), and [summary-based indexing](https://www.llamaindex.ai/blog/a-new-document-summary-index-for-llm-powered-qa-systems-9a32ece2f9ec) (we evaluated and saw low performance). These methods differ from what is proposed in this post.  
值得注意的是，过去已经提出了其他使用上下文来改进检索的方法。其他提议包括：向片段添加通用的文档摘要（我们进行了实验，发现收益非常有限）、假设性文档嵌入和基于摘要的索引（我们进行了评估，性能较低）。这些方法与本文中提出的方法不同。

### Implementing Contextual Retrieval实现上下文检索

Of course, it would be far too much work to manually annotate the thousands or even millions of chunks in a knowledge base. To implement Contextual Retrieval, we turn to Claude. We’ve written a prompt that instructs the model to provide concise, chunk-specific context that explains the chunk using the context of the overall document. We used the following Claude 3 Haiku prompt to generate context for each chunk:  
当然，手动标注知识库中的数千甚至数百万个片段将是一项庞大的工作。为了实现上下文检索，我们转向 Claude。我们编写了一个提示，指示模型提供简洁的、针对每个片段的上下文，该上下文使用整个文档的上下文来解释该片段。我们使用了以下 Claude 3 Haiku 提示来为每个片段生成上下文：

```
<document> 
{{WHOLE_DOCUMENT}} 
</document> 
Here is the chunk we want to situate within the whole document 
<chunk> 
{{CHUNK_CONTENT}} 
</chunk> 
Please give a short succinct context to situate this chunk within the overall document for the purposes of improving search retrieval of the chunk. Answer only with the succinct context and nothing else.
```

The resulting contextual text, usually 50-100 tokens, is prepended to the chunk before embedding it and before creating the BM25 index.  
结果上下文文本，通常为 50-100 个标记，在将其嵌入并创建 BM25 索引之前，被添加到块之前。

Here’s what the preprocessing flow looks like in practice:  
实际中预处理流程是这样的：

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F2496e7c6fedd7ffaa043895c23a4089638b0c21b-3840x2160.png&w=3840&q=75)

Contextual Retrieval is a preprocessing technique that improves retrieval accuracy. 上下文检索是一种提高检索准确性的预处理技术。

If you’re interested in using Contextual Retrieval, you can get started with [our cookbook](https://github.com/anthropics/anthropic-cookbook/tree/main/skills/contextual-embeddings).  
如果您想使用上下文检索，可以从我们的食谱开始。

### Using Prompt Caching to reduce the costs of Contextual Retrieval使用提示缓存以降低上下文检索的成本

Contextual Retrieval is uniquely possible at low cost with Claude, thanks to the special prompt caching feature we mentioned above. With prompt caching, you don’t need to pass in the reference document for every chunk. You simply load the document into the cache once and then reference the previously cached content. Assuming 800 token chunks, 8k token documents, 50 token context instructions, and 100 tokens of context per chunk, **the one-time cost to generate contextualized chunks is $1.02 per million document tokens**.  
Claude 在低成本的条件下实现了独特的上下文检索，这得益于我们上面提到的特殊提示缓存功能。使用提示缓存，您无需为每个片段传递参考文档。只需将文档加载到缓存中一次，然后引用之前缓存的內容。假设 800 个令牌片段、8k 个令牌文档、50 个令牌上下文指令和每个片段 100 个令牌的上下文，生成上下文化片段的一次性成本为每百万文档令牌 1.02 美元。

#### Methodology 方法论

We experimented across various knowledge domains (codebases, fiction, ArXiv papers, Science Papers), embedding models, retrieval strategies, and evaluation metrics. We’ve included a few examples of the questions and answers we used for each domain in [Appendix II](https://assets.anthropic.com/m/1632cded0a125333/original/Contextual-Retrieval-Appendix-2.pdf).  
我们在各个知识领域（代码库、小说、ArXiv 论文、科学论文）、嵌入模型、检索策略和评估指标上进行了实验。我们在附录 II 中包含了每个领域使用的几个问题和答案的示例。

The graphs below show the average performance across all knowledge domains with the top-performing embedding configuration (Gemini Text 004) and retrieving the top-20-chunks. We use 1 minus recall@20 as our evaluation metric, which measures the percentage of relevant documents that fail to be retrieved within the top 20 chunks. You can see the full results in the appendix - contextualizing improves performance in every embedding-source combination we evaluated.  
下面的图表显示了所有知识领域内平均性能，以及表现最佳的嵌入配置（Gemini Text 004）和检索前 20 个片段。我们使用 1 减去召回率@20 作为评估指标，该指标衡量了在顶部 20 个片段中未能检索到的相关文档的百分比。您可以在附录中查看完整结果——在评估的每个嵌入源组合中，上下文化都提高了性能。

#### Performance improvements 性能提升

Our experiments showed that:  
我们的实验表明：

- **Contextual Embeddings reduced the top-20-chunk retrieval failure rate by 35%** (5.7% → 3.7%).  
	上下文嵌入将顶部 20 个片段检索失败率降低了 35%（5.7% → 3.7%）。
- **Combining Contextual Embeddings and Contextual BM25 reduced the top-20-chunk retrieval failure rate by 49%** (5.7% → 2.9%).  
	结合上下文嵌入和上下文 BM25 降低了前 20 个片段检索失败率 49%（5.7% → 2.9%）。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F7f8d739e491fe6b3ba0e6a9c74e4083d760b88c9-3840x2160.png&w=3840&q=75)

Combining Contextual Embedding and Contextual BM25 reduce the top-20-chunk retrieval failure rate by 49%. 结合上下文嵌入和上下文 BM25 降低了前 20 个片段检索失败率 49%。

#### Implementation considerations实现考虑因素

When implementing Contextual Retrieval, there are a few considerations to keep in mind:  
在实现上下文检索时，有一些考虑因素需要记住：

1. **Chunk boundaries:** Consider how you split your documents into chunks. The choice of chunk size, chunk boundary, and chunk overlap can affect retrieval performance <sup>1</sup>.  
	块边界：考虑如何将文档分割成块。块大小、块边界和块重叠的选择会影响检索性能 <sup>1</sup> 。
2. **Embedding model:** Whereas Contextual Retrieval improves performance across all embedding models we tested, some models may benefit more than others. We found [Gemini](https://ai.google.dev/gemini-api/docs/embeddings) and [Voyage](https://www.voyageai.com/) embeddings to be particularly effective.  
	嵌入模型：虽然上下文检索提高了我们测试的所有嵌入模型的性能，但某些模型可能比其他模型受益更多。我们发现 Gemini 和 Voyage 嵌入特别有效。
3. **Custom contextualizer prompts:** While the generic prompt we provided works well, you may be able to achieve even better results with prompts tailored to your specific domain or use case (for example, including a glossary of key terms that might only be defined in other documents in the knowledge base).  
	定制上下文提示：虽然我们提供的通用提示效果良好，但您可能能够通过针对特定领域或用例定制的提示获得更好的结果（例如，包括知识库中其他文档中可能定义的关键术语词汇表）。
4. **Number of chunks:** Adding more chunks into the context window increases the chances that you include the relevant information. However, more information can be distracting for models so there's a limit to this. We tried delivering 5, 10, and 20 chunks, and found using 20 to be the most performant of these options (see appendix for comparisons) but it’s worth experimenting on your use case.  
	块数量：将更多块添加到上下文窗口中会增加包含相关信息的可能性。然而，更多信息可能会对模型造成干扰，因此存在一个限制。我们尝试了 5、10 和 20 个块，发现使用 20 个块在这些选项中性能最佳（参见附录中的比较），但值得在您的用例中进行实验。

**Always run evals:** Response generation may be improved by passing it the contextualized chunk and distinguishing between what is context and what is the chunk.  
始终运行评估：通过传递上下文化的片段并区分上下文和片段，可以改进响应生成。

## Further boosting performance with Reranking进一步通过重排序提升性能

In a final step, we can combine Contextual Retrieval with another technique to give even more performance improvements. In traditional RAG, the AI system searches its knowledge base to find the potentially relevant information chunks. With large knowledge bases, this initial retrieval often returns a lot of chunks—sometimes hundreds—of varying relevance and importance.  
在最后一步，我们可以将上下文检索与其他技术相结合，以获得更多的性能提升。在传统的 RAG 中，AI 系统会搜索其知识库以找到可能相关的信息片段。随着知识库的增大，这种初始检索通常会返回大量——有时是数百——不同相关性和重要性的片段。

Reranking is a commonly used filtering technique to ensure that only the most relevant chunks are passed to the model. Reranking provides better responses and reduces cost and latency because the model is processing less information. The key steps are:  
重排序是一种常用的过滤技术，以确保只有最相关的片段被传递给模型。重排序可以提供更好的响应，并减少成本和延迟，因为模型处理的信息更少。关键步骤包括：

1. Perform initial retrieval to get the top potentially relevant chunks (we used the top 150);  
	执行初始检索以获取最有可能相关的片段（我们使用了前 150 个）；
2. Pass the top-N chunks, along with the user's query, through the reranking model;  
	将前 N 个片段以及用户的查询通过重排序模型进行传递；
3. Using a reranking model, give each chunk a score based on its relevance and importance to the prompt, then select the top-K chunks (we used the top 20);  
	使用重排序模型，根据每个片段与提示的相关性和重要性为其评分，然后选择前 K 个片段（我们使用了前 20 个）
4. Pass the top-K chunks into the model as context to generate the final result.  
	将前 K 个块作为上下文输入到模型中，以生成最终结果。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F8f82c6175a64442ceff4334b54fac2ab3436a1d1-3840x2160.png&w=3840&q=75)

Combine Contextual Retrieva and Reranking to maximize retrieval accuracy. 结合上下文检索和重排序以最大化检索准确性。

### Performance improvements 性能提升

There are several reranking models on the market. We ran our tests with the [Cohere reranker](https://cohere.com/rerank). Voyage [also offers a reranker](https://docs.voyageai.com/docs/reranker), though we did not have time to test it. Our experiments showed that, across various domains, adding a reranking step further optimizes retrieval.  
市场上存在多种重排序模型。我们使用 Cohere 重排序器进行了测试。Voyage 也提供重排序器，但我们没有时间对其进行测试。我们的实验表明，在各个领域，添加重排序步骤可以进一步优化检索。

Specifically, we found that Reranked Contextual Embedding and Contextual BM25 reduced the top-20-chunk retrieval failure rate by 67% (5.7% → 1.9%).  
具体来说，我们发现重排序上下文嵌入和上下文 BM25 将前 20 个片段检索失败率降低了 67%（5.7% → 1.9%）。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F93a70cfbb7cca35bb8d86ea0a23bdeeb699e8e58-3840x2160.png&w=3840&q=75)

Reranked Contextual Embedding and Contextual BM25 reduces the top-20-chunk retrieval failure rate by 67%. 重新排序的上下文嵌入和上下文 BM25 将前 20 个片段检索失败率降低了 67%。

#### Cost and latency considerations成本和延迟考虑

One important consideration with reranking is the impact on latency and cost, especially when reranking a large number of chunks. Because reranking adds an extra step at runtime, it inevitably adds a small amount of latency, even though the reranker scores all the chunks in parallel. There is an inherent trade-off between reranking more chunks for better performance vs. reranking fewer for lower latency and cost. We recommend experimenting with different settings on your specific use case to find the right balance.  
重新排序的一个重要考虑因素是对延迟和成本的影响，尤其是在对大量片段进行重新排序时。因为重新排序在运行时增加了一个额外的步骤，即使重新排序器并行地对所有片段进行评分，这也不可避免地增加了一小部分延迟。在重新排序更多片段以获得更好的性能与重新排序较少片段以降低延迟和成本之间存在着固有的权衡。我们建议您针对特定的用例进行实验，以找到合适的平衡点。

## Conclusion 结论

We ran a large number of tests, comparing different combinations of all the techniques described above (embedding model, use of BM25, use of contextual retrieval, use of a reranker, and total # of top-K results retrieved), all across a variety of different dataset types. Here’s a summary of what we found:  
我们进行了一系列大量测试，比较了上述所有技术（嵌入模型、使用 BM25、使用上下文检索、使用重排器以及检索到的总 top-K 结果数量）在不同数据集类型上的不同组合。以下是我们的发现总结：

1. Embeddings+BM25 is better than embeddings on their own;  
	嵌入+BM25 比单独使用嵌入效果更好；
2. Voyage and Gemini have the best embeddings of the ones we tested;  
	在我们测试过的嵌入中，Voyage 和 Gemini 的嵌入效果最佳；
3. Passing the top-20 chunks to the model is more effective than just the top-10 or top-5;  
	将前 20 个片段传递给模型比只传递前 10 个或前 5 个更有效。
4. Adding context to chunks improves retrieval accuracy a lot;  
	为片段添加上下文可以显著提高检索准确性；
5. Reranking is better than no reranking;  
	重新排序优于不进行重新排序；
6. **All these benefits stack**: to maximize performance improvements, we can combine contextual embeddings (from Voyage or Gemini) with contextual BM25, plus a reranking step, and adding the 20 chunks to the prompt.  
	所有这些好处都可以叠加：为了最大化性能提升，我们可以将上下文嵌入（来自 Voyage 或 Gemini）与上下文 BM25 相结合，再加上重新排序步骤，并将 20 个片段添加到提示中。

We encourage all developers working with knowledge bases to use [our cookbook](https://github.com/anthropics/anthropic-cookbook/tree/main/skills/contextual-embeddings) to experiment with these approaches to unlock new levels of performance.  
我们鼓励所有与知识库合作的开发者使用我们的食谱来尝试这些方法，以解锁新的性能水平。

Below is a breakdown of results across datasets, embedding providers, use of BM25 in addition to embeddings, use of contextual retrieval, and use of reranking for Retrievals @ 20.  
以下是结果在数据集、嵌入提供者、BM25 与嵌入结合使用、使用上下文检索以及使用重排序进行检索@20 的分解。

See [Appendix II](https://assets.anthropic.com/m/1632cded0a125333/original/Contextual-Retrieval-Appendix-2.pdf) for the breakdowns for Retrievals @ 10 and @ 5 as well as example questions and answers for each dataset.  
请参阅附录 II，其中包含检索@10 和@5 的分解以及每个数据集的示例问题和答案。

![](https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F646a894ec4e6120cade9951a362f685cd2ec89b2-2458x2983.png&w=3840&q=75)

1 minus recall @ 20 results across data sets and embedding providers. 1 减去检索@20 的数据集和嵌入提供者的召回率结果。