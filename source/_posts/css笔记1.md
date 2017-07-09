---
title: css笔记1
date: 2017-04-12 20:23:21
tags:
  - css
categories: CSS
---

1. CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明：
> `p {color:red;text-align:center;}`
> CSS声明总是以分号(;)结束，声明组以大括号({})括起来:

2. HTML元素以id属性来设置id选择器,CSS 中 id 选择器以 "#" 来定义。
class 选择器在HTML中以class属性表示, 在 CSS 中，类选择器以一个点"."号显示：

2. CSS注释以 "/*" 开始, 以 "*/" 结束。

3. 插入样式表的方法有三种:
    1. 外部样式表：
    ```
    <head>
        <link rel="stylesheet" type="text/css" href="mystyle.css">
    </head>
    ```
    2. 内部样式表:
    ```
    <head>
    <style>
        p {margin-left:20px;}
    </style>
    </head>
    ```
    3. 内联样式:
    ```
    <p style="color:sienna;margin-left:20px">This is a paragraph.</p>
    ```
    4. 优先级：
    **内联样式 > 内部样式 > 外部样式 > 浏览器缺省设置**



4. 背景简写，背景颜色的简写属性为 "background"，属性顺序为：
    1. background-color
    1. background-image
    1. background-repeat
    1. background-attachment
    1. background-position
    2. `body {background:#ffffff url('img_tree.png') no-repeat right top;}`
5. 边框-简写属性：
    1. border-width
    1. border-style (required)
    1. border-color
    2. `border:5px solid red;`
6. 分组选择器，每个选择器用逗号分隔。
   嵌套选择器，每个选择器用空格分隔。

7. 隐藏元素
   * display:none，且隐藏的元素不会占用任何空间。
   * visibility:hidden可以隐藏某个元素，但隐藏的元素仍需占用与未隐藏之前一样的空间。

8. 元素定位position:
    * **Static 定位**，HTML元素的默认值，即没有定位，元素出现在正常的流中。
    * **Fixed 定位**，元素的位置相对于浏览器窗口是固定位置。Fixed定位使元素的位置与文档流无关，因此不占据空间。
    * **Relative 定位**，定位是相对其正常位置。可以移动的相对定位元素的内容和相互重叠的元素，它原本所占的空间不会改变。
    * **Absolute 定位**， 相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于`<html>`。Absolutely定位使元素的位置与文档流无关，因此不占据空间。

9. 响应式媒体查询
    1. 在 <head> 链接CSS文件时提供判断语句，选择性加载不同的CSS文件
    `<link rel="stylesheet" href="middle.css" media="screen and (min-width: 400px)">`
    2. 在CSS文件中分段书写不同设备的代码
        ```
        @media screen and (min-width: 600px) { /* CSS Code */ }
        @media screen and (max-width: 599px) { /* CSS Code */ }
        ```
    3. 媒体介质类型
        > all – 全部媒体类型
        > braille – 盲文触摸装置
        > embossed – 分页盲文打印机 （W3C的无障碍做的真细心……）
        > handheld – 小屏幕和流量有限的手持设备（注意！安装标准来说移动设备都应该使用这个介质类型，但是实际上安卓根本不理会这个介质，请使用 screen 结合媒体查询语句使用）
        > print – 提供给打印机的样式，最常用的介质类型，打印页面时获得适合阅读的效果
        > projection – 投影，给投影机使用（有人用？）
        > screen – 彩色屏幕，最常用的介质类型，一般和屏幕大小表达式联合使用
        > speech – 语音朗诵，用于屏幕阅读软件（和将来的Siri？）
        > tty – 固定间距字符网格，例如功能机那样的
        > tv – 智能电视设备（唔不知道我家的创维酷开支持如何……）
