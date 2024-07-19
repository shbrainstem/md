## 安装Ollama

### 下载Ollama
<html>
https://ollama.com/download
</html>

### 安装Ollama

```
双击*dmg文件，拖入Application图标
```
### 运行Ollama，打开terminal

```
ollama serve
```
### 加载模型
#### 以下地址查找模型，页面有加载模型的命令，注意观察版本
<html>
https://ollama.com/library
</html>

### 执行模型加载

```
ollama run qwen2:1.5b
```
##### 上面的命令完成后，在>>> 后面就可以输入问题了
##### 文件保存地址通过访达->前往->前往文件夹，可以看到模型文件在/Users/yourusername/.ollama/models/ 目录下

## 浏览器访问

<html>
API地址：http://localhost:11434/api/tags
文档地址：https://github.com/ollama/ollama/blob/main/docs/api.md
</html>

### API调用

```
curl http://localhost:11434/api/generate -d '{
  "model": "qwen2:1.5b",
  "prompt":"Why is the sky blue?"
}'

curl http://localhost:11434/api/chat -d '{
  "model": "qwen2:1.5b",
  "messages": [
    { "role": "user", "content": "为什么天空是蓝色的?" }
  ]
}'
```


<html>
老牛同学
Ollama完整教程：本地LLM管理、WebUI对话、Python/Java客户端API应用</html>


```
Ollama的安装过程，与安装其他普通软件并没有什么两样，安装完成之后，有几个常用的系统环境变量参数建议进行设置：

OLLAMA_MODELS：模型文件存放目录，默认目录为当前用户目录（Windows 目录：C:\Users%username%.ollama\models，MacOS 目录：~/.ollama/models，Linux 目录：/usr/share/ollama/.ollama/models），如果是 Windows 系统建议修改（如：D:\OllamaModels），避免 C 盘空间吃紧
OLLAMA_HOST：Ollama 服务监听的网络地址，默认为127.0.0.1，如果允许其他电脑访问 Ollama（如：局域网中的其他电脑），建议设置成0.0.0.0，从而允许其他网络访问
OLLAMA_PORT：Ollama 服务监听的默认端口，默认为11434，如果端口有冲突，可以修改设置成其他端口（如：8080等）
OLLAMA_ORIGINS：HTTP 客户端请求来源，半角逗号分隔列表，若本地使用无严格要求，可以设置成星号，代表不受限制
OLLAMA_KEEP_ALIVE：大模型加载到内存中后的存活时间，默认为5m即 5 分钟（如：纯数字如 300 代表 300 秒，0 代表处理请求响应后立即卸载模型，任何负数则表示一直存活）；我们可设置成24h，即模型在内存中保持 24 小时，提高访问速度
OLLAMA_NUM_PARALLEL：请求处理并发数量，默认为1，即单并发串行处理请求，可根据实际情况进行调整
OLLAMA_MAX_QUEUE：请求队列长度，默认值为512，可以根据情况设置，超过队列长度请求被抛弃
OLLAMA_DEBUG：输出 Debug 日志标识，应用研发阶段可以设置成1，即输出详细日志信息，便于排查问题
OLLAMA_MAX_LOADED_MODELS：最多同时加载到内存中模型的数量，默认为1，即只能有 1 个模型在内存中
```

