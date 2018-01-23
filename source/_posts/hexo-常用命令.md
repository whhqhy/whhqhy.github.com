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

# 五、 使用本地图片
1. 首先确认 _config.yml 中有 post_asset_folder: true
2. npm install hexo-asset-image --save
```
Example
MacGesture2-Publish
├── apppicker.jpg
├── logo.jpg
└── rules.jpg
MacGesture2-Publish.md
Make sure post_asset_folder: true in your _config.yml.

Just use ![logo](MacGesture2-Publish/logo.jpg) to insert logo.jpg.
```
* [Hexo 官方文档](https://hexo.io/zh-cn/docs/)


# 六、 BlueLake主题安装需要插件
```
cnpm install hexo-renderer-jade@0.3.0 --save
cnpm install hexo-renderer-stylus --save
cnpm install hexo-generator-json-content@2.2.0 --save
```
[BlueLake主题](http://chaoo.oschina.io/2016/12/29/BlueLake%E5%8D%9A%E5%AE%A2%E4%B8%BB%E9%A2%98%E7%9A%84%E8%AF%A6%E7%BB%86%E9%85%8D%E7%BD%AE.html)

如果出现报错
```
(node:9488) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated.
ERROR Plugin load failed: hexo-renderer-sass
Error: Cannot find module 'node-sass'
```
可尝试安装 `cnpm install node-sass@latest`
