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

## cygwin添加代理
找到cygwin安装目录，home下的.bashrc文件，在里面添加如下代理即可
```
export HTTP_PROXY='http://localhost:8118'
export FTP_PROXY="$HTTP_PROXY" 
export HTTPS_PROXY="$HTTP_PROXY" 

export http_proxy="$HTTP_PROXY" 
export ftp_proxy="$FTP_PROXY" 
export https_proxy="$HTTPS_PROXY" 
```

## windowws cmd 添加代理
使用set http_proxy方式直接设置代理即可
```
C:\Users\Administrator>set http_proxy=http://localhost:8118

C:\Users\Administrator>set https_proxy=https://localhost:8118

C:\Users\Administrator>curl www.google.com
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>302 Moved</TITLE></HEAD><BODY>
<H1>302 Moved</H1>
The document has moved
<A HREF="http://www.google.co.jp/?gfe_rd=cr&amp;ei=D3_sV9OANNKQ8QfqoqXQAw">here<
/A>.
</BODY></HTML>
```