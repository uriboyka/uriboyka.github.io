---
title: github page hexo博客同步源文件与静态文件方法
date: 2017-04-17 23:03:30
tags:
  - git
  - hexo
categories: Git
---


### 搭建流程
1. 在github上创建仓库 uriboyka.github.io.
2. 创建两个分支：master 与 hexo.
3. 设置 hexo 为默认分支，保存源文件.
4. git clone hexo 分支到本地，执行：
  ```
  hexo init
  npm install
  npm install hexo-deployer-git --save
  ```
5. 修改站点目录 _config 中的 deploy 参数，分支为：master
6. 依次执行下列命令，提交修改的源文件：
  ```
  git add .
  git commit -m ""
  git push origin hexo
  ```
7. 发布网站到 master 分支上：`hexo g -d`

### 日常改动流程
1. 将源文件改动推送到github上：
  ```
  git add .
  git commit -m ""
  git push origin hexo
  ```
2. 将html文件发布到master分支：
  ```
  hexo g -d
  ```
