
###### 安装虚拟环境模块
```
pip install virtualenv
```
###### 创建虚拟环境
```
python3 -m venv myenv
```
######  激活虚拟环境
```
source myenv/bin/activate
```

> 调整Python的虚拟环境只会影响当前的终端（Terminal）会话。当你在终端中激活一个虚拟环境时，环境变量如PATH、VIRTUAL_ENV等会在当前会话中被修改，这样当你在这个终端中运行Python相关的命令时，它们会指向虚拟环境中的Python解释器和库，而不是系统的全局Python环境。

- 在同一个终端窗口中打开的新标签页或分屏也将会继承这些环境变量的更改，因此也将使用同一个虚拟环境。
- 如果你在另一个终端窗口或者新的终端会话中运行Python相关的命令，那么这些命令将不会受到之前激活的虚拟环境的影响，除非你也在那个新会话中激活相同的虚拟环境。
- 当你退出当前的终端会话或使用deactivate命令时，环境变量将恢复到激活虚拟环境之前的值，即回到系统的全局Python环境状态。
