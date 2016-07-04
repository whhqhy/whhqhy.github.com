---
title: hexo 常用命令
categories: hexo
date: 2016-03-15 19:01:49
timestamp:
catAlias:
tags: [hexo]
keywords:
description: 第一次安装，需要经常使用的命令。
---

------
# 一、 安装git
- 从github上导出自己的网站仓库，仓库目录中打开命令行。
- 检查电脑是否已经有SSH keys ，`ls -al ~/.ssh`  如果没有，生成`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
- 将生成的id_rsa.pub里面的参数拷贝到github的SSH Keys栏目下

# 二、 安装node.js
官网下载nodejs [官网](https://nodejs.org/en/)

# 三、 安装hexo
安装hexo方法， [戳这里（转载）](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/)
通过npm命令完成hexo安装。
```bash
npm install hexo
```
```bash
npm install
```
安装上传github的插件
```bash
npm install hexo-deployer-git
```
- 如果第一次安装，需要执行`npm install -g hexo-cli`

# 四、 命令行推送到github
添加所有改变到暂存区    
```bash
git add --all
```
提交本地改变到仓库
```bash
git commit -m "..."
```
推送到github上blog分支
```bash
git push origin blog
```
执行hexo g -d生成网站并部署到GitHub上。

* [Hexo 官方文档](https://hexo.io/zh-cn/docs/)