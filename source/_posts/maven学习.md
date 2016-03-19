---
title: maven学习
categories: maven
date: 2016-03-19 22:31:45
timestamp:
catAlias:
tags: [maven]
keywords:
description: maven学习
---

# **Maven安装目录分析**
maven目录结构
	
	bin
	boot
	conf
	lib
	LICENSE.txt
	NOTICE.txt
	README.txt


- bin：该目录包含了mvn运行的脚本，这些脚本用来配置java命令，准备好classpath和相关的java系统属性，然后执行java命令。mvn.bat是基于Windows平台的bat脚本。在命令行输入任何一条mvn命令时，实际上就是在调用这些脚本。


- boot：该目录只包含一个jar文件plexus-classworlds，是一个类加载器框架，相当于默认的java类加载器。


- conf：该目录包含settings.xml文件，修改该文件就能够在机器上全局的定制maven行为。一般情况下，我们复制该文件置于~/.m2/目录下（~表示用户目录）。


- lib：该目录包含了所有的maven运行时需要的java类库。


# **~/.m2**
该目录下方法maven的本地仓库，所有的maven构建都被存储到该仓库中，以方便重用。