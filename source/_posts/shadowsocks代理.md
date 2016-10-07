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

## Linux安装
**安装图形版安hadowsocks**
1. 安装add-apt-repository，可执行`sudo add-apt-repository`,如果提示找不到命令可以试试`sudo apt-get install software-properties-common`
2. 安装shadowsocks-qt5，图形界面，可以扫描二维码添加代理，执行如下代码
`sudo add-apt-repository ppa:hzwhuang/ss-qt5`
`sudo apt-get update`
`sudo apt-get install shadowsocks-qt5`

**使用privoxy命令行穿墙**
1. 安装`sudo apt-get install privoxy` 
2. 配置`sudo vi /etc/privoxy/config`和windows版一样，打开socks5，`vi查找快捷键/字符串 n查找下一个`
3. 开启服务 `sudo  service  privoxy start`
4. 设置终端代理`export http_proxy='http://localhost:8118'`和`export https_proxy='https://localhost:8118'`
5. 测试 curl www.google.com

**chrome浏览器插件SwitchyOmega**
暂未实验，可参考[chrome代理与android SDK代理](https://blog.phpgao.com/privoxy-shadowsocks.html)

**curl安装**
1. 下载安装包 `wget http://curl.haxx.se/download/curl-7.20.0.tar.gz`
2. 解压到当前目录 `tar -zxf curl-7.20.0.tar.gz`,进入解压后的目录内`cd curl-7.20.0`
3. 配置，指定安装的目录 `./configure`
4. 编译 `make`
5. 安装 `sudo make install`


## 下载源码

参考官方文档[官方链接](http://source.android.com/source/downloading.html)
需要注意的点:
- 默认情况下，获得了Android源代码是匿名的。为了防止过量使用的服务器，每个服务器的IP地址与一个配额关联。

当与其他用户共享一个IP地址（例如访问来自超过了NAT防火墙的源库时），配额甚至可以触发常规使用模式（例如，如果许多用户同步来自同一IP地址的新客户在短期内）。

在这种情况下，有可能使用认证访问，然后使用单独的配额为每个用户，而不管IP地址。具体参考源码网站
- 出现error: unable to create file tests/P_str_escape/str\\escape.rs的解决办法[链接](http://blog.csdn.net/u013553529/article/details/50616725)
