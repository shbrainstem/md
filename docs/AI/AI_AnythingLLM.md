#### 安装

<html>
https://useanything.com/
</html>

#### anythingLLM选择远程服务
可以选择远程服务，可能需要收费，一般选择本地ollamma服务


#### anythingLLM集成ollama
首页->左边栏最下面的扳手->进入“设置”->LLM首选项->LLM 提供商->选择“ollama"->选择qwen7b
->右上角选"save change" 完成

#### 配置agent skill

```
Generate & save files to browser
```
##### 允许模型生成的数据或输出直接在用户的浏览器中保存为文件。这项功能对于那些需要模型生成复杂数据结构、长文本、表格、代码片段或其他类型文件的用户非常有用。

```
Generate charts
```
##### 从数据集中自动创建视觉化表示的过程，生成excel，csv等文件

```
Web Search
```
##### 允许模型在回答问题时访问互联网上的实时信息。这个功能特别有用，因为模型可以获取到最新的数据、新闻、研究结果或其他在线资源，从而提供更准确、更及时的答案。

```
SQL Connector
```
##### 可以直接与SQL数据库进行交互，从而访问存储在数据库中的结构化数据。这种能力对于那些需要从历史数据中提取信息、分析趋势或执行复杂查询的应用场景非常有用。
```
RAG & long-term memory
```
##### 该选项不能关闭， RAG（Retrieval-Augmented Generation）和long-term memory配置项是两个关键功能，它们有助于增强模型的性能，特别是在处理需要背景知识或长期记忆的任务时

```
View & summarize documents
```
##### 该选项不能关闭，来帮助用户管理和理解大量文档的功能。

```
Scrape websites
```
##### 该选项不能关闭，允许模型或相关应用程序从网页上自动提取数据。
