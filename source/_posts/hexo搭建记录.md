---
title: hexo搭建记录
date: 2017-04-17 23:03:30
tags:
  - hexo
categories: Git
---

### 安装配置hexo
1. 下载安装hexo
    ```
    npm install -g hexo-cli
    ```
2. 初始化博客
    ```
    // 建立一个博客文件夹，并初始化博客，<folder>为文件夹的名称，可以随便起名字
    $ hexo init <folder>
    // 进入博客文件夹，<folder>为文件夹的名称
    $ cd <folder>
    // node.js的命令，根据博客既定的dependencies配置安装所有的依赖包
    $ npm install
    ```
3. 配置博客，修改_config.yml文件。注意：**每一项的填写，其:后面都要保留一个空格**
    1. 目录结构
        ```
        .
        ├── .deploy       #需要部署的文件
        ├── node_modules  #Hexo插件
        ├── public        #生成的静态网页文件
        ├── scaffolds     #模板
        ├── source        #博客正文和其他源文件, 404 favicon CNAME 等都应该放在这里
        |   ├── _drafts   #草稿
        |   └── _posts    #文章
        ├── themes        #主题
        ├── _config.yml   #全局配置文件
        └── package.json
        ```
    1. 配置部署
        ```
        deploy:
            type: git
            repo: https://github.com/uriboyka/uriboyka.github.io.git
            branch: master
        ```


### 遇到问题
1. 如果发布的时候出现错误：`ERROR Deployer not found: git` 意思就是用来发布文章的git没有安装，执行命令 `npm install hexo-deployer-git --save`就可以解决了
