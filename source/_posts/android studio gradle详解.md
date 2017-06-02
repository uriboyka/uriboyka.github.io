---
title: android studio gradle详解
date: 2017-04-15 19:41:59
tags:
  - android
  - gradle
categories: android相关
---

1. gradle包的版本,在项目的gradle/wrapper目录下面有个gradle-wrapper.properties中有如下内容：
`distributionUrl=https\://services.gradle.org/distributions/gradle-2.2.1-all.zip`
    >团队中人员A,B,C，每个人都有自己的电脑和配置，如何能保证A,B,C使用同一个版本得gradle来编译项目呢，gradle wrapper就用来干这个

2. gradle插件的版本,是android studio为了方便使用gradle进行配置和编译而开发的插件,项目的根目录下的build.gradle中会配置如下代码:
    ```
    buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.0'
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
    }
    ```
3. gradle 与 gradlew: W意思是wrapper，它是一个用bash命令包装过的gradle编译启动脚本，里面会进行环境变量检测和设置。最终进行编译的还是gradle;Gradlew是包装器，自动下载包装里定义好的gradle 版本，保证编译环境统一，gradle 是用本地的gradle

4. [gradle插件与包版本对应相关](https://developer.android.com/studio/releases/gradle-plugin.html)如下：
    > Plugin version 2.0.0 - 2.1.2 ----> Gradle version 2.10 - 2.13
    > Plugin version 2.1.3 - 2.2.3 ----> Gradle version 2.14.1+
    > Plugin version 2.3.0+ ----> Gradle version 3.3+


5. 导入其它项目时修改gradle版本问题：
    > 1. 修改gradle插件的版本，在项目根目录下的build.gradle中修改
    > ```
    > dependencies {
    >    classpath
    > 'com.android.tools.build:gradle:2.2.3'
    > }
    > ```
    > 2. 修改gradle的版本，在项目的gradle/wrapper目录下面有个gradle-wrapper.properties中修改
    > `distributionUrl=https\://services.gradle.org/distributions/gradle-2.14.1-all.zip`
    > 3. 查看当前系统安装了哪些版本的gradle，`C:\Users\suyf\.gradle\wrapper\dists`


6. 手动安装gradle版步骤：
    > 1.下载对应版本的[gradle zip](https://services.gradle.org/distributions)包.
    > 2. 把zip放到相应目录，不需要解压`C:\Users\suyf\.gradle\wrapper\dists\gradle-2.14.1-all\8bnwg5hd3w55iofp58khbp6yv`
    > 3. 这个目录最好先让android studio 自己生成好后，取消自己fetch文件，然后自己去下载好gradle-xxx-all-zip文件，放到对应的目录下.

7. Eclipse有个打开文件就自动展开目录的功能，在IntelliJ里从Project左边栏的齿轮上选择Autoscroll to Source和Autoscroll from Source都勾选上即可。
