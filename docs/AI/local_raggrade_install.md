<!-- TOC -->
* [TOC]
:toc:

### 下载和说明地址：

>https://microsoft.github.io/graphrag/posts/get_started/

### 安装命令

//安装 graphrag
pip3 install graphrag
//配置setting文件中的的大模型KEY
export GRAPHRAG_API_KEY=<CHATGTP-KEY>

### 执行
> 1.运行索引器
mkdir -p ./ragtest/input
> 2.下载数据集
curl https://www.gutenberg.org/cache/epub/24022/pg24022.txt > ./ragtest/input/book.txt
> 3.配置工作区变量
python3 -m graphrag.index --init --root ./ragtest

  这将在目录中创建两个文件：.env和。settings.yaml./ragtest
.env包含运行 GraphRAG 管道所需的环境变量。如果检查文件，您将看到已定义的单个环境变量。 GRAPHRAG_API_KEY=<API_KEY>这是 OpenAI API 或 Azure OpenAI 端点的 API 密钥。您可以将其替换为您自己的 API 密钥。

settings.yaml包含管道的设置,会读.env文件的环境变量。您可以修改此文件以更改管道的设置。

>4.运行索引管道
python3 -m graphrag.index --root ./ragtest
执行日志信息在下面文件中

output\{run_id}\reports\logs.json
使用本地LM-studio运行的模型

###  参考的settings.ymal文件

encoding_model: cl100k_base
skip_workflows: []
llm:
  api_key: lm-studio
  type:  openai_chat # or azure_openai_chat
  model: Qwen/Qwen2-7B-Instruct-GGUF
  model_supports_json: true # recommended if this is available for your model.
  #max_tokens: 4000
  #request_timeout: 180.0
  api_base: http://localhost:1234/v1/
  #......
  
embeddings:
  ##parallelization: override the global parallelization settings for embeddings
  async_mode: threaded # or asyncio
  llm:
    api_key: lm-studio
    type: openai_embedding # or azure_openai_embedding
    model: text-embedding-3-small
    # api_base: https://<instance>.openai.azure.com

### 调用服务
