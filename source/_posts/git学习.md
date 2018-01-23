---
title: git学习
categories: git
date: 2016-03-17 13:40:55
timestamp:
catAlias:
tags: [git,命令]
keywords:
description: 一些git命令的记录，方便以后翻看
---

# 一、git使用片段
* 初始化 `git init`

* 查看仓库状态 `git status`

* 查看log日志 `git log  || git log --pretty=oneline`

* 还原仓库 `git reset --hard HEAD^`

* 查看历史id `git reflog 查看commit_id`

* 可以丢弃工作区的修改 `git checkout -- file`

* 回到最近一次git commit或git add时的状态 `git checkout -- readme.txt`

* 把暂存区的修改撤销掉（unstage），重新放回工作区：`git reset HEAD readme.txt`

* 删除指定文件 `git rm test.txt`

* 查看改变 `git diff`

* 查看文本内容 `cat readme.txt`

* 查看分支 `git branch`

* 创建分支 `git branch <name>`

* 切换分支 `git checkout <name>`

* 创建+切换分支 `git checkout -b <name>`

* 合并某分支到当前分支 `git merge <name>`

* 删除分支 `git branch -d <name>`


# 二、实际操作
<p>
git init
git add README.md || git add \-\-all
git commit -m "first commit"
git remote add origin https://github.com/whhqhy/git.git
git push -u origin master
git pull origin master
git clone git@github.com:whhqhy/buildApk.git
</p>
