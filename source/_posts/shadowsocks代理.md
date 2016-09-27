---
title: shadowsocks代理
date: 2016-09-28 00:07:23
categories:
tags: [shadowsocks]
keywords:
description: shadowsocks代理下载google源码
---

# 需求
  办理了shadowsocks账号，但是一直以来没搞清楚如何使用shadowsocks下载源码，最近空闲，所以特意尝试了下，走了一些误区（如想要代理windows终端，实际上只需要代理git就好了），但是总算还是达到自己下载源码的需求了

# 实现步骤
## 关于代理软件安装
1. 安装privoxy，选择options-> edit main configuration 找下下面这行 去掉前面的#        forward-socks5t   /               127.0.0.1:1080 .
2. 重启privoxy
3. 查看privoxy默认监听的8118端口是否已经打开：`netstat -an | grep 8118`

## git添加代理
1. **添加代理**
	* git config --global --add http.proxy localhost:8118  
	* git config --global --add http.proxy localhost:8118
2. **git使用shadowsocks代理**
	* 方法一
		找到user/用户名/.gitconfig，手动添加如下
		```
		[http]
			proxy = 'socks5://127.0.0.1:1080'
			proxy = localhost:8118 // 添加代理所加内容
		[https]
			proxy = 'socks5://127.0.0.1:1080'
			proxy = localhost:8118 // 添加代理所加内容
		```
	* 方法二
		* git config --global http.proxy 'socks5://127.0.0.1:1080' 
		* git config --global https.proxy 'socks5://127.0.0.1:1080'
3. **取消git代理设置**
	* 方法一
		找到user/用户名/.gitconfig 删除添加的选项
	* 方法二
		* git config --global --unset http.proxy 
		* git config --global --unset https.proxy