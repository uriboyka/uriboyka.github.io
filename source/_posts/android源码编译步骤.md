---
title: android源码编译步骤
date: 2017-05-8 18:41:59
tags:
  - android
  - aosp
categories: Android
---

### android源码编译环境
```
sudo apt install vim git
sudo apt-get install ssh gitk
sudo apt-get install openjdk-7-jdk
sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip
```

### 编译命令
```
git clone git@192.168.1.194:crave1/p02.git

git clone git@192.168.1.194:crave1/p02.git

cd p02/

cd flycom35_m/

\. build/envsetup.sh

lunch

make clean -j8;make -j8 2>&1 | tee build.log
```

### 查看android源码的版本
1. 编译的时候在终端中一开始就会打印出来：`PLATFORM_VERSION：2.3.1`
2. 直接去make文件中去看：`build\core\version_defaults.mk  // 搜索该文件中的 PLATFORM_VERSION值`

### android 6.0 源码目录结构
* |-- Makefile
* |-- abi 应用程序二进制接口
* |-- art Android Runtime
* |-- bionic 系统底层库
    * |-- libc  C库，如stdio、stdlib、string
    * |-- libdl  动态链接库访问接口
    * |-- libm 数学函数库，提供常见的数序运算和浮点运算
    * |-- libstd 标准C++库
    * |-- libthreaddb 线程调试库，可利用此库对多线程程序进行调试
    * |-- linker 链接器
* |-- bootable 启动引导相关代码
* |-- build 编译Android系统、Android SDK、及相关文档
* |-- cts Android兼容性测试套件标准
* |-- dalvik 一个应用对应一个单独的Dalvik虚拟机实例
* |-- developers 开发者目录
* |-- development 提供开发所需的工具、例程
* |-- device Android源码中对产品的描述文件夹
* |-- docs 介绍开源相关文档
* |-- external android使用的一些开源的模组
* |-- frameworks 核心框架——java及C++语言
* |-- hardware 硬件抽象层，部分厂家开源的硬解适配层HAL代码
* |-- libcore  运行库
* |-- libnativehelper JNI用到的库
* |-- ndk ndk相关
* |-- packages 应用程序包
    * |-- app 蓝牙、浏览器、计算器、日历、相机、联系人通讯录、桌面闹钟、拨号器、Email、相册、登录启动项（显示图片框架等图形界面、负责应用的调度）、音乐播放器、安装/卸载应用、设置、录音机等系统默认应用（出厂时安装应用）
    * |-- inputmethods 输入法
    * |-- providers 提供应用界面所需的数据、如日历、联系人等
    * |-- services 彩信、来电
    * |-- wallpapers 基础壁纸、动态壁纸等
* |-- pdk google用来减少碎片化的东西
* |-- platform_testing
* |-- prebuild 预编译
* |-- sdk sdk及模拟器
* |-- system 底层文件系统库、应用及组件——C语言
* |-- tool
