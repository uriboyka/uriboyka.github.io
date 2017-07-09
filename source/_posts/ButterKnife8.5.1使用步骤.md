---
title: ButterKnife8.5.1使用步骤
date: 2017-06-12 20:23:21
tags:
  - android
  - butterknife
categories: Android
---


### 在根目录build.gradle添加如下代码
```
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.2'
        classpath 'com.jakewharton:butterknife-gradle-plugin:8.5.1'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
```

### 在模块目录build.gradle中添加插件代码（可选）：
```
apply plugin: 'com.android.application'
apply plugin: 'com.jakewharton.butterknife'
```

### 在Module的dependencies添加如下代码：
```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:25.3.1'
    compile 'com.android.support.constraint:constraint-layout:1.0.2'
    testCompile 'junit:junit:4.12'

    compile 'com.jakewharton:butterknife:8.5.1'
    annotationProcessor 'com.jakewharton:butterknife-compiler:8.5.1'
}
```
