---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Android/Android/","dgPassFrontmatter":true,"created":"2024-12-08T22:39:40.446+08:00","updated":"2024-12-08T22:44:33.578+08:00"}
---

# 相关笔记

- [[czc知识库/计算机/搞机/Android/安卓 电池 电量 锂电池 管理机制\|安卓 电池 电量 锂电池 管理机制]]
- [[czc知识库/计算机/搞机/Android/安卓搞机笔记\|安卓搞机笔记]]
- [[czc知识库/计算机/搞机/Android/刷机工具\|刷机工具]]
- [[czc知识库/计算机/搞机/Android/AAB格式是什么 安卓安装包\|AAB格式是什么 安卓安装包]]
- [[czc知识库/计算机/搞机/Android/android studio安装\|android studio安装]]
- [[czc知识库/计算机/搞机/Android/AndroidManifest.xml文件\|AndroidManifest.xml文件]]
- [[czc知识库/计算机/搞机/Android/AndroidX是什么\|AndroidX是什么]]
- [[czc知识库/计算机/搞机/Android/AOSP 安卓开放源代码项目\|AOSP 安卓开放源代码项目]]
- [[czc知识库/计算机/搞机/Android/api和库的区别\|api和库的区别]]
- [[czc知识库/计算机/搞机/Android/smali代码是什么\|smali代码是什么]]
- [[czc知识库/计算机/搞机/Android/termux ssh笔记 连接termux开的ssh服务器 sshd\|termux ssh笔记 连接termux开的ssh服务器 sshd]]
- [[czc知识库/计算机/搞机/Android/termux笔记\|termux笔记]]






> [!NOTE] apk文件组成 Android application package (APK) 
> Android 平台 上用于安装 Android 应用程序的文件是一个后缀名为.apk 的压缩文件, 其内包含 Android 应用所有的 数据和资源文件。通过解压.apk 文件可以得到以下结构:
> 
> assets: 用于存放需要打包到 apk 中的**静态文件**
> 
> lib: 存放应用程序依赖的 **native 库文件**, 一般是用 C/C++语言编写
> 
> res: 存放**资源文件**。如存放 Android 应用布局xml 文件
> 
> META-INF: 保存应用的**签名信息**, 签名信息**可以验证 APK 文件的完整性**
> 
> AndroidManifest.xml: Android 应用的**配置文件**。声明应用所申请的权限信息、硬件信息、SDK版本、包信息等; 描述应用的各个组件(activity、service、broadcast receiver 和 content provider), 向Android 系统告知有关组件以及可以启动这些组件的条件的信息
> 
> classes.dex: Android 应用程序的**可执行文件**。java 代码首先会被编译成.class 文件, 得到的类文件被翻译成 Dalvik 字节码, 最终合并为一个或多个可执行 dex 文件。
> 
> resources.arsc: 记录资源文件和资源 ID 之间的映射关系, 用来根据资源 ID 寻找资源
> 
> 由于 AndroidManifest.xml 含有 Android 应用程序的配置信息, classes.dex 文件是 Android 应用程序的可执行文件, 均与应用行为特征关系及恶意程度紧密相关。因此 Android 的恶意软件检测模型通常以上述两个文件为重点进行特征的分析和选择。
> 
> ———————————————————
> 
> 原文链接：https://blog.csdn.net/qq_45378281/article/details/127294441
> 

## 安卓API
为了使应用程序与开发人员更方便地访问安卓系统的特定例程, 而无需访问源码或理解系统内部的实现 细节, 安卓定义了一些函数并提供外部接口, 这些函数就是安卓 API. API 相较于权限而言是一种粒度更细的 特征.

## 安卓源代码：[[czc知识库/计算机/搞机/Android/AOSP 安卓开放源代码项目\|AOSP 安卓开放源代码项目]]