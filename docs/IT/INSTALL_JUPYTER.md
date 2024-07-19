

### CentOS 9 安装

```
pip3 install notebook
pip3 install notebookjupyter notebook --generate-config
```
### 创建配置文件
```
jupyter notebook --generate-config
```
### 修改配置文件-外网访问，端口，访问密码

```
 vi ~/.jupyter/jupyter_notebook_config.py
```
#### hashed_password内容来自jupyter_server_config.json
```
c.NotebookApp.ip = '0.0.0.0' 
c.NotebookApp.port = 8888
c.NotebookApp.allow_remote_access = True
c.NotebookApp.password ="argon2:$argon2id$v=19$m=10240,t=10,p=8$vMAvLra0Yz+P2lMNrVzjbw$NbmZW1YXuqF5Mbwx0T6mjYmrXQatw1g6Yp4PTbVbRDk" 
c.NotebookApp.allow_root = True
```
### 配置外网访问密码/输入密码
```
jupyter notebook password
```
#### 生产新的文件
```
vi /root/.jupyter/jupyter_server_config.json
```
```
{
  "IdentityProvider": {
    "hashed_password": "argon2:$argon2id$v=19$m=10240,t=10,p=8$vMAvLra0Yz+P2lMNrVzjbw$NbmZW1YXuqF5Mbwx0T6mjYmrXQatw1g6Yp4PTbVbRDk"
  }
}
```
### 启动jupyter
```
nohup jupyter notebook &
```
### 远程访问
```
http://IP:8888/
```

##### 服务器未pip install 包的处理方式
```
!pip install <package_name>
```

