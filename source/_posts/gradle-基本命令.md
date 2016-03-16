---
title: gradle 基本命令
categories: Gradle
date: 2016-03-16 16:04:41
timestamp:
catAlias:
tags: [gradle,groovy]
keywords:
description: 
---
gradle部分知识点 
<!-- more -->

---
# 一、 基本目录

| 目录类型	| Eclipse	| IDEA（Android Studio）
| --------   | -----:  | :----:  |
| 代码根目录	| /	| src/main
| adil文件	| /src	| [代码根目录]/aidl
| java文件	| /src	| [代码根目录]/java
| assets文件	| /assets	| [代码根目录]/assets
| jni文件	| /jni	| [代码根目录]/jni
| jnilibs文件	| /libs	| [代码根目录]/jniLibs
| res文件	| /res	| [代码根目录]/res
| AndroidMainfest.xml	| AndroidMainfest.xml	| [代码根目录]/AndroidMainfest.xml

# 二、 使用的方法
复制目录
```gradle 
def copyTargetDir(){
    copy{
        from 'myCopy'
        into 'copyTarger/files'
    }
}

task executeTask<<{
    copyTargetDir()
}
```
删除目录
```gradle 
def deleteTargetDir(){
    File file = file("${project.rootDir}/copyTarger/files")
    println file.getAbsolutePath()
    if(file.exists()){
        file.deleteDir()
    }
}

task executeTaskCopy<<{
    deleteTargetDir()
}
```