### 1.本地测试GraghRag
#### 环境搭建
##### ollamma提供LLM服务
```
ollama pull llama3
```
##### LM Studio提供Embednding服务
```
search ->  下载 nomic-embed-text-v1.5.Q4_K_M.gguf
Local server -> Embedding Model Settings -> 选择 Q4_K_M
Start Server 启动服务
```
#### 启动GraghRag
##### 初始化GraghRag环境
```
# 
pip install graphrag

# 在user目录下
mkdir -p ./ragtest/input

# copy of A Christmas Carol by Charles Dickens from a trusted source
curl https://www.gutenberg.org/cache/epub/24022/pg24022.txt > ./ragtest/input/book.txt

# 初始化目录，Since we have already configured a directory named .ragtest` in the previous step
python -m graphrag.index --init --root ./ragtest
```


##### 只需要配置GraghRag的Setting.yaml

```
# 访问本地 ollama提供的LLM服务
encoding_model: cl100k_base
skip_workflows: []
llm:
  api_key: ${GRAPHRAG_API_KEY}
  type: openai_chat # or azure_openai_chat
  model: llama3 # 选择LLM
  model_supports_json: true # recommended if this is available for your model.
  api_base: http://localhost:11434/v1 # Ollama服务


# 访问到本地的LM Studio提供的 Embedding服务
embeddings:
  ## parallelization: override the global parallelization settings for embeddings
  async_mode: threaded # or asyncio
  llm:
    api_key: lm-studio
    type: openai_embedding # or azure_openai_embedding
    # model: nomic-ai/nomic-embed-text-v1.5-GGUF/
    model: nomic-ai/nomic-embed-text-v1.5-GGUF/nomic-embed-text-v1.5.Q5_K_M.gguf # 注意：LM studio提供的URL较此少了/nomic-embed-text-v1.5.Q5_K_M.gguf
    api_base: http://localhost:1234/v1 # LM Studio服务
```
##### 完成配置后的
```
# Running the Indexing pipeline
python -m graphrag.index --root ./ragtest
```
###### Running the Query Engine
```
# Here is an example using Global search to ask a high-level question:
python -m graphrag.query \
--root ./ragtest \
--method global \
"What are the top themes in this story?"
```
```
# Here is an example using Local search to ask a more specific question about a particular character:
python -m graphrag.query \
--root ./ragtest \
--method local \
"Who is Scrooge, and what are his main relationships?"
```



### 2.关于GraghRag的说明
#### RAG 检索增强生成
> （Retrieval-Augmented Generation）技术是一种先进的自然语言处理（NLP）方法，它结合了信息检索和生成式语言模型的优点，以提高模型回答复杂问题的能力。
 RAG技术的核心思想是在生成模型的上下文中整合外部知识，这样可以提升生成内容的准确性和可靠性。

#### 有效利用GraphRAG的关键考虑因素
 
> 信息提取技术以推断和生成分块数据之间的联系、用于存储和检索的知识索引以及用于生成图形查询的模型，例如 Cypher 生成模型。随着新技术的不断涌现。
 

#### GraphRag的挑战

> GraphRAG 与 RAG 一样，具有明显的局限性，包括如何形成图形、生成查询这些图形的查询，以及最终决定根据这些查询检索多少信息。
主要挑战是“查询生成”、“推理边界”和“信息提取”。
#### 关于RAG的问题
##### 问题
> 主要的原因是对用户意图的误解，导致获取不相关的信息
##### 解决方案很简单：
> 准确理解用户的意图并提供“相关”信息。
##### 改善这一状况的努力涉及多种方法，主要分为四类：
 
> 1. 从零开始构建大模型----这种模型从一开始就可以获得清晰的数据上下文，但构建成本较高。
> 2. 优选模型+特定领域训练----采用“训练有素”的大型语言模型，并在特定领域进一步训练它们，这种方法具有成本效益且相对准确，但在模型上下文和领域特定上下文之间保持平衡却具有挑战性。
>3. 既有大模型+提示工程----按原样使用大型语言模型，但为用户查询添加额外的上下文，这虽然具有成本效益，但在上下文提供方面存在主观性和潜在偏见的风险。
>4. 既有大模型+响应优化----保留大型语言模型，同时在响应过程中提供“相关信息”的额外上下文，这允许提供最新的、具有成本效益的响应，但在识别和集成相关文档方面涉及复杂性。
 
##### 评价优化效果的角度

> 成本、准确性、特定领域术语、最新响应、透明度和可解释性。      
 
##### 处理过程出现的问题

> - 内容缺失：第一个限制是无法索引与用户查询相关的文档，因此无法使用它们来提供上下文。尽管认真预处理数据并正确将数据存储在数据库中，但无法利用这些数据是一个重大缺陷。
>- 错过排名靠前的文档：第二个问题出现在检索到与用户查询相关的文档但相关性极低时，导致答案无法满足用户的期望。这主要源于在过程中确定要检索的“文档数量”的主观性，突出了一个主要限制。因此，有必要进行各种实验来正确定义这个 k 超参数。
>- 不在上下文中 — 合并策略限制：从数据库中检索到包含答案的文档，但无法将其包含在生成答案的上下文中。当返回大量文档时会发生这种情况，并且需要合并过程来选择最相关的信息。
>- 未提取：第四个是 LLM（大型语言模型）的基本限制，它倾向于检索“近似”值而不是“精确”值。因此，获取“近似”或“类似”值可能会导致不相关的信息，从而因未来响应中的微小噪音而造成重大影响。
>- 格式错误：第五个问题似乎与指令调整密切相关，指令调整是一种通过使用指令数据集微调 LLM 来提高零样本性能的方法。当提示中的附加指令格式不正确时，就会发生这种情况，导致 LLM 产生误解或误读，从而产生错误的答案。
>- 特异性不正确：第六个问题涉及未充分利用用户查询信息或过度使用查询信息，导致在考虑查询的重要性时出现问题。当输入和检索输出的组合不合适时，很可能会发生这种情况。
>- 不完整：第七个限制是，尽管能够使用上下文来生成答案，但缺失的信息会导致对用户查询的响应不完整。

##### 上述问题分析。这三个因素凸显了 RAG 中的关键因素，并提出了如何改进这些问题的问题。
 
>1. 索引 — 检索与用户查询相关的文档，
>2. 在生成答案之前正确提供信息，
>3. 输入和检索前/后过程的适当组合。
 
#### 技术差异分析
##### RAG和本地搜索引擎的差异

```
在处理本地知识库方面，RAG 与搜索引擎提供的查询服务存在以下主要差异：

1. 信息来源

RAG 从本地知识库中检索信息，该知识库可以包含来自各种来源的数据，例如文本文档、数据库、表格等。
搜索引擎从互联网上检索信息，该信息通常包含网页、新闻文章、社交媒体帖子等。
2. 信息粒度

RAG 通常检索与查询相关的文档或段落，并将其作为输入提供给生成模型。
搜索引擎通常检索完整的网页，用户需要自行浏览网页以找到所需信息。
3. 信息质量

本地知识库中的信息通常经过人工审核和整理，因此质量相对较高。
互联网上的信息质量参差不齐，用户需要自行判断信息的准确性和可靠性。
4. 信息完整性

本地知识库通常包含特定领域或主题的完整信息。
互联网上的信息可能不完整或分散，用户需要从多个来源收集信息。
5. 信息呈现

RAG 可以生成与查询相关的文本摘要或答案，用户可以直接阅读。
搜索引擎通常以列表形式呈现检索结果，用户需要自行浏览网页以找到所需信息。
总而言之，RAG 处理本地知识库的优势在于信息来源可靠、信息粒度细、信息质量高、信息完整性强、信息呈现直观。

特性    	RAG	搜索引擎
结构化程度	高	低
完整性   	高	低
准确性	    高	中等
定制化    	高	低

```



