---
title: idea使用记录
date: 2017-04-13 19:23:21
tags:
  - idea
categories: idea相关
---

1. Idea 把"Mark Directory As..."的文件夹都加入CLASSPATH。

2. Facets 表示这个module有什么特征，比如 Web，Spring和Hibernate等；

3. Artifact 是maven中的一个概念，表示某个module要如何打包，例如war exploded、war、jar、ear等等这种打包形式；
一个module有了 Artifacts 就可以部署到应用服务器中了！

4. 在给项目配置Artifacts的时候有好多个type的选项，exploed是什么意思：
> 1. explode 在这里你可以理解为展开，不压缩的意思。也就是war、jar等产出物没压缩前的目录结构。建议在开发的时候使用这种模式，便于修改了文件的效果立刻显现出来。
> 2. 默认情况下，IDEA的 Modules 和 Artifacts 的 output目录 已经设置好了，不需要更改，打成 war包 的时候会自动在 WEB-INF目录 下生产 classes目录，然后把编译后的文件放进去。

5. Java artifact是什么意思，maven一直用，但是不明白中文意思？
> artifact你把它理解成“生成的东西”就差不多了。这个词强调的是这是你软件生产过程中某一步的产生物，不像程序本身，或者是配置文件这些，是你手写出来的。

6. 当点击运行tomcat时，Idea开始做以下事情：
> 1. 运行server前会做一次编译。编译后class文件存放在指定的项目编译输出目录下.
> 2. 根据artifact中的设定对目录结构进行创建.
> 3. 拷贝web资源的根目录下的所有文件到artifact的目录下.
> 4. 拷贝编译输出目录下的classes目录到artifact下的WEB-INF下.
> 5. 拷贝lib目录下所需的jar包到artifact下的WEB_INF下.
> 6. 运行server，运行成功后，如有需要，会自动打开浏览器访问指定url.

7. 文件编码设置（Ctlr+Alt+S): **Editor**->**Code Style**->**File Encodings**,三个地方编码都设为UTF-8.

8. 实时代码模板**Live Templates**：可以补全如 System.Out.Println之类的语句。
> 1. 调用。调用常规的实时代码模板主要是通过两个快捷键：Tab 和 Ctrl + J。如：sys+tab
> 2. 设置。**Editor**->**Code Style**->**Live Templates**。

9. 文件代码模板**File and Code Templates**:可以设置在新建文件时的文件描述、作者等信息。
> 设置。**Editor**->**Code Style**->**File and Code Templates**。

10. 后缀代码模板**Postfix Completion**：比实时代码模板更加便捷一点点的补全，功能本质上也是代码模板。
> 1. 使用。输入`o.notnull`按**Tab**键，代码就会变为`if (o != null)`
> 设置。**Editor**->**General**->**Postfix Completion**。

11. IntelliJ IDEA 对插件进行了很好的分类：
    * All plugins 显示所有插件。
    * Enabled 显示当前所有已经启用的插件。
    * Disabled 显示当期那所有已经禁用的插件。
    * Bundled 显示所有 IntelliJ IDEA 自带的插件。
    * Custom 显示所有我们自行安装的插件，如果你自己装了很多次插件的话，这个选项会用得比较多。

12. Debug 常用快捷键:
    * F7 : 进入下一步，进入方法体。
    * F8 ：进入下一步，不进入方法体。
    * F9 ：恢复程序运行，但是如果该断点下面代码还有断点则停在下一个断点上


### 常用快捷键
快捷键  |   介绍
--|--
 Ctrl + Alt + S |  格式化代码，可以对当前文件和整个包目录使用 （必备）
 Ctrl + Alt + O |  优化导入的类，可以对当前文件和整个包目录使用 （必备）
 Ctrl + Alt + T |  对选中的代码弹出环绕选项弹出层 （必备）
 Ctrl + F |  在当前文件进行文本查找 （必备）
 Ctrl + Shift + F | 根据输入内容查找整个项目 或 指定目录内文件 （必备）
 Ctrl + E |  显示最近打开的文件记录列表 （必备）
 Ctrl + N	 |  根据输入的 类名 查找类文件 （必备）
 Ctrl + Shift + N | 通过文件名定位 / 打开文件 / 目录，打开目录需要在输入的内容后面多加一个正斜杠 （必备）
 Ctrl + P |  方法参数提示显示 （必备）
 Ctrl + Shift + Alt + S |  打开当前项目设置 （必备）
 Alt + F7 | 查找光标所在的方法 / 变量 / 类被调用的地方
 Ctrl + Shift + A | 可以查找所有Intellij的命令，并且每个命令后面还有其快捷键
 Ctrl + W | 递进式选择代码块。可选中光标所在的单词或段落，连续按会在原有选中的基础上再扩展选中范围 （必备）
 Shift + Shift |  在项目的所有目录查找，包括类、资源、配置项、方法等等
