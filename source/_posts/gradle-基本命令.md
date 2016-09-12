---
title: gradle基本，记录
categories: Gradle
date: 2016-03-16 16:04:41
timestamp:
catAlias:
tags: [gradle,groovy]
keywords:
description: 
---
gradle的目录结构，使用中copy，delete方法记录 
<!-- more -->

---
# 一、基本目录
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

# 二、使用的方法
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
显示文件列表
```gradle
task echoDirListViaAntBuilder() {
    description = 'Uses the built-in AntBuilder instance to echo and list files'
    //Docs: http://ant.apache.org/manual/Types/fileset.html
    
    //Echo the Gradle project name via the ant echo plugin
    ant.echo(message: project.name)
    ant.echo(path)
    ant.echo("${projectDir}/samples")
    
    println 'test'

    //Gather list of files in a subdirectory
    ant.fileScanner{
        fileset(dir:"samples")
    }.each{
        //Print each file to screen with the CWD (projectDir) path removed.
        println it.toString() - "${projectDir}"
    }
}

echo :
$ bash run-example.bsh
[ant:echo] ant-antbuilder
[ant:echo] :echoDirListViaAntBuilder
[ant:echo] E:\github\oreilly-gradle-book-examples\ant-antbuilder/samples
test
\samples\one.txt
\samples\three.txt
\samples\two.txt
:echoDirListViaAntBuilder UP-TO-DATE

```
依赖关系
```gradle
$ cat build.gradle
ant.importBuild 'build.xml'

defaultTasks = ['antStandAloneHello', 'afterTheAntTask']

task beforeTheAntTask << {
    println "A Gradle task that precedes the Ant target"
}

task afterTheAntTask(dependsOn: "antHello") << {
    println "A Gradle task that precedes the Ant target"
}

Administrator@whhqhy /cygdrive/e/github/oreilly-gradle-book-examples/ant-antdependsongradle
$ cat build.xml
<project>
  <target name="antStandAloneHello">
    <echo message="A stand-alone hello from an Ant target"/>
  </target>

  <target name="antHello" depends="beforeTheAntTask">
    <echo message="A dependent hello from the Ant target"/>
  </target>
</project>


echo:
$ gradle
:antStandAloneHello
[ant:echo] A stand-alone hello from an Ant target
:beforeTheAntTask
A Gradle task that precedes the Ant target
:antHello
[ant:echo] A dependent hello from the Ant target
:afterTheAntTask
A Gradle task that precedes the Ant target

BUILD SUCCESSFUL

```