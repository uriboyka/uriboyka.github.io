---
title: git遇到的问题
date: 2017-04-19 21:13:21
tags:
  - git
categories: Git
---

1. github push 提交代码时停止在writing objects怎么办？
  ```
  git config --global http.postBuffer 524288000
  git config --global sendpack.sideband false
  ```

2. git 修改地址？
  1. 1.修改命令git remote set-url origin [url]
  ```
  git remote set-url origin git@github.com:uriboyka/uriboyka.github.io.git
  ```
  2. 先删后加
  ```
  git remote rm origin
  git remote add origin [url]
  ```
  3. 修改配置文件
  ```
  $ vim .git/config
  ```
