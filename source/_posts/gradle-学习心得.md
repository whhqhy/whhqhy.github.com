---
title: gradle学习心得，记录
categories: Gradle
date: 2016-07-04 18:55:41
tags: [gradle,groovy]
keywords:
description: 
---
hook ,apply from
<!-- more -->

---
# 一、gradle工作流
具体描述有空再写

![gradle工作流](gradle work push.png)

## 读取manifest中versionName
``` groovy
def getVersionNameAdvanced(Project project){
    def xmlFile = project.file("AndroidManifest.xml")
    def rootManifest = new XmlSlurper().parse(xmlFile)
    return rootManifest['@android:versionName']
}
```

## 为所有子工程添加公共方法
```
subprojects{
    logger.log(LogLevel.INFO,'Config for '+project.name)
    apply from: rootProject.getRootDir().getAbsolutePath()+'/utils.gradle'
}

```

## 将依赖扩展和参数抽离到新的脚本
```
config.gradle

apply plugin: 'com.android.application'

def addExtendsDependencies(){
    dependencies {
        compile(name: 'CommonLib-1.0-release', ext: 'aar')
        compile(name: 'Drawer-1.0-release', ext: 'aar')

    }

    repositories{
        flatDir{
            dirs 'E:\\myAar'
       }
    }
}
//将函数设置为extra属性中去，这样，加载utils.gradle的Project就能调用此文件中定义的函数了
ext{
    addExtendsDependencies = this.&addExtendsDependencies
    appName = "天天斗地主真人版"
}

build.gradle

apply from: rootProject.getRootDir().getAbsolutePath()+"/gradle/${channelFlavors}Config.gradle"

dependencies {
    compile fileTree(dir: 'libs', include: '*.jar')
    addExtendsDependencies()
}
```

## 自定义渠道名称
```
productFlavors{
        "${channelFlavors}"{
            applicationId packageName
        }
    }
```

## xml添加，删除，更新，查询
```
def void updateManifestXml(def path){
    File file = new File(path)

    def doc = DOMBuilder.parse(new StringReader(file.text))
    def root = doc.documentElement
    use(groovy.xml.dom.DOMCategory) {
        //移除掉默认启动intent-filter 以及 基地标志的intent-filter
        removeIntentFilterByAction_Categroy(root,"android.intent.action.MAIN","android.intent.category.LAUNCHER")
        removeIntentFilterByAction_Categroy(root,"android.intent.action.CHINAMOBILE_OMS_GAME","android.intent.category.CHINAMOBILE_GAMES")


        // 根据不同启动Activity添加不同的操作
        if(hasLoginActivity){
            // LoginAcitivity 闪屏页启动
            // 1. 启动页横竖屏设置
            // 2. 启动页主题设置
            //def androidMap = ["android:screenOrientation":"landscape",
            //           "android:theme":"@style/GameTheme"]
            if(androidMap.size()>0){
                replaceActivityAttributes(root,androidMap)
            }
            // 3. LoginActivity 添加启动项 和 基地标志
            addMainIntentFilter(root,"com.zengame.basic.LoginActivity")
            addAndGameIntentFilter(root,"com.zengame.basic.LoginActivity")
        }else{
            // GameActivity 启动
            // 1. 移除掉LoginActivity
            removeActivityByName(root,"com.zengame.basic.LoginActivity")
            // 2. GameActivity 添加启动项 和 基地标志
            addMainIntentFilter(root,"com.zengame.basic.GameActivity")
            addAndGameIntentFilter(root,"com.zengame.basic.GameActivity")
        }

    }

    def result = XmlUtil.serialize(root)
    file.write(result,"UTF-8")
   // println result
}

def void addMainIntentFilter(def root,String name){
    root.getElementsByTagName("activity").each {node ->
        if(node.attributes.getNamedItem("android:name").nodeValue==name){
            org.w3c.dom.Element element = node.appendNode("intent-filter")
            element.appendNode("action",["android:name":"android.intent.action.MAIN"])
            element.appendNode("category",["android:name":"android.intent.category.LAUNCHER"])
        }
    }
}

def void addAndGameIntentFilter(def root,String name){
    root.getElementsByTagName("activity").each {node ->
        if(node.attributes.getNamedItem("android:name").nodeValue==name){
            org.w3c.dom.Element element = node.appendNode("intent-filter")
            element.appendNode("action",["android:name":"android.intent.action.CHINAMOBILE_OMS_GAME"])
            element.appendNode("category",["android:name":"android.intent.category.CHINAMOBILE_GAMES"])
        }
    }
}

def void removeActivityByName(def root,String name){
    root.getElementsByTagName("activity").each {node ->
        if(node.attributes.getNamedItem("android:name").nodeValue==name){
            node.parentNode.removeChild(node)
        }
    }
}

def void replaceActivityAttributes(def root,def map){
    root.getElementsByTagName("activity").each {node ->
        if(node.attributes.getNamedItem("android:name").nodeValue=="com.zengame.basic.LoginActivity"){
            map.each {key,value ->
                node.attributes.getNamedItem(key).setNodeValue(value)
            }
        }
    }
}

def void removeIntentFilterByAction_Categroy(def root,String actionValue,String categroyValue){
    root.getElementsByTagName("intent-filter").each {node ->
        boolean hasMain
        boolean hasLuancher
        node.childNodes.each { childNode ->
            if (childNode.nodeName == "action" && actionValue == childNode.attributes.getNamedItem("android:name").nodeValue) {
                hasMain = true
            }
            if (childNode.nodeName == "category" && categroyValue == childNode.attributes.getNamedItem("android:name").nodeValue) {
                hasLuancher = true
            }
        }
        if (hasMain && hasLuancher) {
            node.parentNode.removeChild(node)
        }
    }
}
```

## 添加声明周期hook，替换构建apk中资源文件
```
project.tasks.whenTaskAdded { task ->
    if(task.name.contains('AndroidTest')){
        task.enabled = false
    }
    android.applicationVariants.all{ variant ->
        if(task.name.contains("Debug")){
            logger.log(LogLevel.INFO,"Debug task过滤${task.name}");
        }else if(task.name=="merge${variant.name.capitalize()}Assets"){
            logger.quiet("^^^^^^^^^^^^^^merge${variant.name.capitalize()}Assets")
            task.doLast {
                println "cowboy " +buildDir.absolutePath
                String path =buildDir.absolutePath+"\\intermediates\\assets\\"+variant.name.capitalize()-"Release"+"\\release"
                logger.quiet("^^^^^^^^^^^^^^${project.name} assemble projectDir ${project.projectDir.absolutePath}")
                if(new File(path).exists()) {
                    copyFile("${channelFlavors}_build_app.properties","build_app.properties",rootProject.getRootDir().getAbsolutePath()+"/gradle", path)
                }
            }
        }else if(task.name=="merge${variant.name.capitalize()}Resources"){
            logger.quiet("^^^^^^^^^^^^^^merge${variant.name.capitalize()}Resources")
            task.doFirst {
                String valuePath = projectDir.absolutePath+"\\res\\values\\strings.xml"
                File valueFile =new File(valuePath);
                if(valueFile.exists()){
                    def text =valueFile.text.replaceAll("<string name=\"app_name\">.*</string>","<string name=\"app_name\">"+appName+"</string>")
                    valueFile.write(text,"UTF-8")
                }
            }
//            task.doLast {
//                String path = buildDir.absolutePath+"\\intermediates\\res\\merged\\zenGame\\release\\drawable-xxhdpi-v4";
//                logger.quiet("^^^^^^^^^^^^^^${project.name} assemble projectDir ${project.projectDir.absolutePath}")
//                if (new File(path).exists()) {
//                    copyFile("ic_launcher.png","ic_launcher.png","E:\\ssd", path)
//                }
//            }
        }else if(task.name == "process${variant.name.capitalize()}Manifest"){
            task.doLast {
                String str = buildDir.absolutePath+"\\intermediates\\manifests\\full\\"+variant.name.capitalize()-"Release"+"\\release\\AndroidManifest.xml"
                logger.quiet("^^^^^^^^^^^^^^${project.name} cowboy ${variant.name.capitalize()}Manifest")
                File valueFile =new File(str)
                if(valueFile.exists()){
                    def text = valueFile.text;
                    map.each {key,value ->
                        text =text.replaceAll("START_REPLACE_"+key+"_END_REPLACE",value)
                    }
                    valueFile.write(text,"UTF-8")

                    updateManifestXml(str)
                    println "cowboy to stop"
//                    throw new GradleException("cowboy to stop ")
                }
            }
        }


    }
}
```