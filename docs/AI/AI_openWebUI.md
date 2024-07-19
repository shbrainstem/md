### 基于docker安装open-webui

#### 文档地址

<html>
https://docs.openwebui.com/</html>

##### 执行命令
```
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```
##### 打印内容
```
main: Pulling from open-webui/open-webui
***
```

### 配置webui到ollama的模型

```
需要从左下角进入用户的Admin Panel->settings
```
#### 配置指向的模型
```
settings->connections 
-----在Ollama API 中增加一项http://localhost:11434 右下角点save
```
```
settings->models 
-----在Manage Ollama Models的拉下项中可以看到上一步添加的http://localhost:11434
----Pull a model from Ollama.com
直接在webui执行 拉取模型
```
#### 选择模型
```
settings->documents->Embedding Model
这里需要先在terminal执行了
ollama run qwen2:1.5b
才能有选项
需要点击右下角save保存
```
## 使用
左上角 new chat打开新的对话窗口
在新窗口左上角选择 模型名称
然后就可以对话
