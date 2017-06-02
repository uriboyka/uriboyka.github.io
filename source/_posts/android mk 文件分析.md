---
title: android.mk文件分析
date: 2017-04-17 22:41:59
tags:
  - android
  - 源码分析
categories: android相关
---

### android 抽像 Makefile 语法，分三步：
#### 1. 清除旧变量
```
LOCAL_PATH:= $(call my-dir)
include $(CLEAR_VARS)
```
是因为Android.mk中所有的变量都是全局的，编译函数在编译时会调用这些变量。为了防止编译函数使用了编译其它模块时设置的变量。

#### 2. 设置新变量
```
LOCAL_SRC_FILES := $(call all-subdir-Java-files)
LOCAL_PACKAGE_NAME := AlarmClock
```
设置新变量就是把本次编译时用到的源码地址，包名等设置好。

#### 3. 调用编译函数
```
include $(BUILD_PACKAGE)
```
调用编译函数其实就是include一个固定的mk文件，这个mk文件会根据设置的变量提取出编译模块需要的target，Command等信息并执行固定的编译命令。
编译模块时，每一个include其实都是一次功能调用，或者对mk文件的调用，或者对变量和函数的调用。

### 代码详解

#### LOCAL_PATH := $(call my-dir)
一个Android.mk file首先必须定义好LOCAL_PATH变量。它用于在开发树中查找源文件。在这个例子中，宏函数‘my-dir’, 由编译系统提供，用于返回当前路径（即包含Android.mk file文件的目录）。


#### include $( CLEAR_VARS)
指定让GNU MAKEFILE为你清除许多LOCAL_XXX变量（例如 LOCAL_MODULE, LOCAL_SRC_FILES, LOCAL_STATIC_LIBRARIES, 等等...),除LOCAL_PATH 。


#### LOCAL_MODULE := helloworld
LOCAL_MODULE变量必须定义，以标识你在Android.mk文件中描述的每个模块。


#### LOCAL_SRC_FILES := helloworld.c
LOCAL_SRC_FILES变量必须包含将要编译打包进模块中的C或C++源代码文件。注意，你不用在这里列出头文件和包含文件，因为编译系统将会自动为你找出依赖型的文件；仅仅列出直接传递给编译器的源代码文件就好。
