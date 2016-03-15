---
title: hexo 常用命令
categories: hexo
date: 2016-03-15 19:01:49
timestamp:
catAlias:
tags: [hexo,命令行]
keywords:
description: 博客第一版
---

------
# 一、 安装hexo
　　安装hexo方法， [戳这里（转载）](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/)

# 二、 移植到其它机器
通过npm命令完成hexo安装。
```bash
npm install hexo
```
生成网站文件
```bash
npm install
```
安装上传github的插件
```bash
npm install hexo-deployer-git
```
# 三、 命令行推送到github
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