

##### macbook优先使用homebrew方式安装python

##### 对于下载文件安装的方式，在删除3.9版本后

```
sudo rm -rf /Library/Frameworks/Python.framework/Versions/3.9
alias pip=pip3
alias python=python3
```

##### pycharm中处理interceptor

```
add interceptor
```

##### 需要把project  interceptor，system interceptor指向的python都做调整

##### 用命令永久移除配置：

```
PATH=$(echo $PATH | sed "s|:/Library/Frameworks/Python.framework/Versions/3.9/bin||g")
export PATH
```
