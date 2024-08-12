##### 一、Ideal的Project下面Modules之间的关系种类
###### 1.1.使用Maven
> 如果你的项目使用Maven作为构建工具，你可以在pom.xml文件中通过<modules>标签来声明子模块，以及通过<dependency>标签来定义模块间的依赖关系。

###### 1.2.声明子模块
> 在顶级pom.xml文件中，你可以这样声明子模块

```
<project>
    <modules>
        <module>sub-module1</module>
        <module>sub-module2</module>
    </modules>
</project>
```

###### 1.3.定义依赖关系
> 在需要依赖其他模块的pom.xml文件中，你可以添加如下<dependency>标签：
这里的groupId和artifactId应当匹配目标模块的坐标，而version则通常与顶级pom.xml中的版本一致。

```
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>sub-module1</artifactId>
        <version>1.0.0</version>
    </dependency>
</dependencies>
```
###### 1.4.使用IntelliJ IDEA的模块设置
> 虽然通过构建工具的配置是最常见和推荐的方式来管理模块间的关系，但在IntelliJ IDEA中，你也可以直接在IDE中调整模块依赖。
1. 打开“Project Structure”对话框（File > Project Structure 或使用快捷键 Ctrl + Alt + Shift + S）。
1. 选择“Modules”选项卡。
1. 选择一个模块，然后点击“Dependencies”选项卡。
1. 点击“+”按钮，选择“Module Dependency”，然后选择你要添加的模块。
###### 通过这种方式，你可以在IDE层面直观地看到并调整模块间的依赖关系，不过更改通常会反映在对应的pom.xml或build.gradle文件中。

##### 二、Project Structure的Modules选项卡看不到同一个project中的其他modules

###### 2.1.module的排序问题，可能不是排在第一行,仔细搜索
###### 2.2.模块尚未添加到项目中：
>确保你已经将所有的模块添加到了项目中。你可以通过右键点击项目根目录，然后选择 "New" -> "Module..." 来添加新模块。 
