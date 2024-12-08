---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Android/AOSP 安卓开放源代码项目/","dgPassFrontmatter":true,"created":"2024-06-27T17:22:52.460+08:00","updated":"2024-12-08T00:39:01.866+08:00"}
---



AOSP：Android Open Source Project
[android笔记 安卓](android笔记%20安卓.md)

# 总结
百度网盘下别人提取好的源码


### AOSP 概述

AOSP 安卓开源项目（**Android Open Source Project**），是一项旨在指导Android移动平台开发的计划 。

Android 是一个适用于移动设备的开源操作系统，也是由 Google 主导的对应开源项目。作为一个开源项目，Android 的目标是避免出现任何集中瓶颈，即没有任何行业参与者可一手限制或控制其他任何参与者的创新。为此，Android 被打造成了一个适用于消费类产品的完整高品质操作系统，并配有可自定义并运用到几乎所有设备的源代码，以及所有用户均可访问的公开文档（英文网址：[source.android.com](https://link.juejin.cn?target=https%3A%2F%2Fsource.android.google.cn%2F%3Fhl%3Dzh-cn "https://source.android.google.cn/?hl=zh-cn")；简体中文网址：[source.android.google.cn](https://link.juejin.cn?target=https%3A%2F%2Fsource.android.google.cn%2F%3Fhl%3Dzh-cn "https://source.android.google.cn/?hl=zh-cn")）。
[【视频文稿】车载Android应用开发与分析 - AOSP的下载与编译 - 掘金](https://juejin.cn/post/7202826051541532727)
> 👆从这发现的可以在清华源里下源码tar压缩包

# AOSP源码网站：
https://source.android.google.cn/docs/setup/download/downloading
[https://github.com/aosp-mirror](https://github.com/aosp-mirror)
[cs.android.com](https://cs.android.com)👉这里可以快速搜索源代码里的代码和文件
http://aospxref.com

# 下载方法
- 使用初始化压缩包
中科大和清华大学提供了AOSP源码的压缩包，现在的包大约有60GB左右，可以使用命令行或迅雷等下载工具下载。优点：下载速度快，支持断点续传。缺点：不贴近工作环境，实际项目中不使用这种方式。
- 清华大学文档：https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/
- 源码压缩包：https://mirrors.tuna.tsinghua.edu.cn/aosp-monthly/aosp-latest.tar
中科大文档 : https://mirrors.ustc.edu.cn/help/aosp.html
- 使用repo 直接同步
使用repo直接同步源码，是Android官方文档中使用的方式。优点：更贴近工作环境。在实际项目中也是使用这种方式同步Android源码。缺点：源码太大，外网不稳定、速度很慢，容易同步失败（实际项目中，使用公司内网不会存在这个问题）。
官方文档：
[下载源代码  |  Android Open Source Project](https://source.android.google.cn/docs/setup/download/downloading)


- 上面都是狗屁，太难了
- 直接百度网盘下载： [Android (包含1.6到14)AOSP源码下载(百度网盘)\_android 10源码百度网盘-CSDN博客](https://blog.csdn.net/zwc456baby/article/details/108594712)


# 实际安装笔记
参考网站：
[git-repo | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/git-repo/)
[repo安装与简单使用](https://blog.csdn.net/xuanwolanxue/article/details/104678027)
[【视频文稿】车载Android应用开发与分析 - AOSP的下载与编译 - 掘金](https://juejin.cn/post/7202826051541532727)

清华源下载`aosp-latest.tar`，解压`tar xf aosp-latest.tar`
安装`repo`
```linux命令
mkdir ~/bin
wget https://storage.googleapis.com/git-repo-downloads/repo -P ~/bin/
chmod a+x ~/bin/repo export 
PATH=~/bin:$PATH
如第三步一样，在~/.bashrc 文件的最末尾添加如下内容： 
export REPO_URL=https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/
这里使用的是清华大学的镜像源
```
重启shell
`repo init`
`cd aosp`
`repo sync`
等待同步，输出进度：`Fetching:  9% (128/1402) 7:21 | 4 jobs | 0:49 platform/prebuilts/rust @ prebuilts/rust`

