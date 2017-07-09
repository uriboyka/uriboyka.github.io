---
title: git笔记1
date: 2017-04-12 21:13:21
tags:
  - git
categories: Git
---

1. 安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置.

2. 创建仓库，通过git init命令把这个目录变成Git可以管理的仓库。
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

3. 添加文件到Git仓库，分两步：
> 第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；
> 第二步，使用命令git commit，完成。

4. 要随时掌握工作区的状态，使用git status命令。
如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

5. 在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

6. 版本回退
> HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
> 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
> 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

7. 工作区和暂存区
> 前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
> 第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
> 第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。
> 因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
> 你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

8. 管理修改,每次修改，如果不add到暂存区，那就不会加入到commit中。

9. 撤销修改:
    1. 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
    2. 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。
    3. 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

10. 删除文件，在文件管理器中把没用的文件删了，然后就用命令`git rm`删掉，并且`git commit`。

11. 添加远程仓库：
    1. 要关联一个远程库，使用命令`git remote add origin git@github.com:uriboyka/learngit.git`；
    2. 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
    3. 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

12. Git分支：
    * 查看分支：`git branch`
    * 创建分支：`git branch <name>`
    * 切换分支：`git checkout <name>`
    * 创建+切换分支：`git checkout -b <name>`
    * 合并某分支到当前分支：`git merge <name>`
    * 删除分支：`git branch -d <name>`

13. 多人协作：
    * 查看远程库信息，使用git remote -v；
    * 本地新建的分支如果不推送到远程，对其他人就是不可见的；
    * 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
    * 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
    * 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
    * 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
