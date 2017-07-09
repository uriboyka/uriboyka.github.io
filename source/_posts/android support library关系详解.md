---
title: android support library关系详解
date: 2017-04-18 18:41:59
tags:
  - android
categories: Android
---

### 安卓官方为什么要提供支持包？
1. 向后兼容
2. 提供不适合打包进framework的功能
3. 为了支持不同形态的设备

### v4、v7、v13与安卓版本的关系
版本 | 级别
--|--
android1.6 |  4
android2.1 |  7
android2.3 |  9
andorid3.2 | 13

### v4 Support Libraries
* 官方在Support Library的第24.2.0版本（２０１6年8月发布）的时候移除了对Android 2.2 (API level 8)及其以下版本的支持，但是名字依然是v4。

* Gradle编译脚本中整个v4库的依赖语句如下`compile 'com.android.support:support-v4:24.2.1'`
* gradle中jar依赖语句格式如 **compile 'jar文件组（group/命名空间）:jar文件名（name）:jar文件版本（version）'**


### v7 Support Libraries
* 需要注意的24.2.0版本以后的v7支持库支持范围也是Android 2.3 (API level 9)及其以上版本了
* [怎么查看Support Library最新版本](https://developer.android.com/topic/libraries/support-library/revisions.html)？
* v7 appcompat library：支持UI设计样式、 material design相关，如ActionBar、AppCompatActivity、Theme等。

### ConstraintLayout是一个单独的支持包，所以需要在gradle中添加引用:
```
dependencies {
    compile 'com.android.support.constraint:constraint-layout:1.0.0-alpha'
}
```
* [怎么查看constraint-layout的最新版本](http://stackoverflow.com/questions/39534070/how-can-i-get-the-latest-version-of-constraintlayout-for-android)？

### Design Support Library:
    这个库现在使用的也比较多，它提供了material design设计风格的控件。如，navigation drawers、floating action buttons (FAB)、snackbars、tabs等。

### `com.android.support:design:25.3.1`[依赖关系](http://blog.csdn.net/zhangquanit/article/details/54291374)：
    1. `com.android.support:appcompat-v7:25.3.1`
        1. `com.android.support:support-v4:25.3.1`
    2. `com.android.support:support-v4:25.3.1`
        1. `com.android.support:support-compat:25.3.1`
        2. `com.android.support:support-media-compat:25.3.1`
        3. `com.android.support:support-core-utils:25.3.1`
        4. `com.android.support:support-core-ui:25.3.1`
        5. `com.android.support:support-fragment:25.3.1`
    3. `com.android.support:recyclerview-v7:25.3.1`
    4. `com.android.support:transition:25.3.1`
