### 注册docker官网账号
在MacBook M1上安装Docker可以分为几个简单的步骤。Docker Desktop是Docker在桌面平台上的官方应用程序，它包含了运行Docker容器所需的所有组件。以下是具体的安装步骤：

### 步骤 1: 访问Docker官网
打开你的浏览器，访问Docker官网。在顶部菜单中找到“Products”，然后选择“Docker Desktop”。
登录或注册Docker账号（gmail账号）。

### 步骤 2: 下载适合M1的Docker版本
在Docker Desktop页面上，你会看到不同平台的下载选项。
选择适用于Mac M1芯片的版本（通常会自动检测到你的硬件类型）。

### 步骤 3: 安装Docker Desktop
下载完成后，打开你的下载目录，找到Docker Desktop的安装包。双击.dmg文件，它将打开一个安装窗口。将Docker Desktop图标拖放到你的“Applications”文件夹中。

### 步骤 4: 启动Docker Desktop
打开Finder，转到“Applications”文件夹，找到Docker Desktop。
双击Docker Desktop图标以启动它。
Docker Desktop首次启动时，可能需要几分钟的时间来初始化。

### 步骤 5: 配置国内镜像加速器（可选）
对于在中国大陆的用户，由于网络问题，可能需要配置国内的Docker镜像加速器。这可以通过Docker Desktop的设置来完成：
打开Docker Desktop。
点击右上角的Docker图标，选择“Preferences”（偏好设置）。
转到“Daemon”标签页。
点击“Edit”按钮以编辑Docker守护进程的JSON配置文件。
在配置文件中，找到或添加"registry-mirrors": ["http://mirror.example.com"]这一行，将http://mirror.example.com替换为你选择的国内镜像加速器地址。
保存并重启Docker Desktop。
### 步骤 6: 测试Docker是否安装成功
打开终端。
输入
```
docker --version
```
来验证Docker是否正确安装。
输入
```
docker run hello-world
```
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```
来测试Docker是否可以正常运行容器。
以上步骤应该可以帮助你在MacBook M1上顺利安装Docker Desktop。如果有任何问题，可以查阅Docker的官方文档或社区论坛以获取更多帮助。

## 配置信息
### 查看文件所在目录信息

```
docker info
```
