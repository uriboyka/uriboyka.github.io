---
title: java编程思想笔记
date: 2017-04-19 22:19:20
tags:
  - java
categories: java相关
---

### 一切都是对象
* 创建了一个引用，就希它能与一个对象相关联。new操作符的意思是：“给我一个对象”。
* 基本类型存储到**堆栈**。
* 对象类型存储到**堆**。
* java基本类型所占存储空间大小是不变的:

基本类型 | 大小 | 包装器类型
--|---|--
void | - | Void
boolean | - | Boolean
byte | 8 bits | Character
char | 16 bits| Character
short | 16 bits | Short
int | 32 bits | Integer
long | 64 bits | Long
float | 32bits| Float
double | 64 bits | Double
