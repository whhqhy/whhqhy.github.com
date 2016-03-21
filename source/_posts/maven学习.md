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


# **maven规范**
默认情况下，maven项目主代码位于src/main/java目录，测试代码位于src/test/java中，项目主代码和测试代码不同，项目主代码会被打包到最终的构件中，而测试代码只在运行测试时用到，不会被打包。

# **单元测试步骤**
一个典型的单元测试包含三个步骤：
1. 准备测试类及数据；
2. 执行要测试的行为；
3. 检查结果。

# **执行循序**
clean 清理输出目录target/
compile编译项目主代码


- mvn clean test执行顺序：
clean：clean、resources：resources、compiler:compiler、resources:testResources、compiler：testCompiler
先执行项目主资源处理、主代码编译、测试资源处理、测试代码编译


- maven主要命令： 
mvn clean compile 、mvn clean test、mvn clean package、mvn clean install。执行test之前会先执行compile，执行package之前会先执行test，执行install之前会先执行package。


