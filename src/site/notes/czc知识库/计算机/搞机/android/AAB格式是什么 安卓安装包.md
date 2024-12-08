---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/android/AAB格式是什么 安卓安装包/","dgPassFrontmatter":true,"created":"2024-08-11T18:38:42.878+08:00","updated":"2024-12-08T00:38:33.576+08:00"}
---



[AAB-CSDN博客](https://blog.csdn.net/liuxiaofeng1991/article/details/108443647)


传统的 Android Package Kit (APK) 包含应用支持的所有设备的代码和资源 (布局文件、图像等)。因此，您在安装 APK 时可能装上了一些您永远不会用到的资源。您的屏幕尺寸不会改变，您的 CPU 也不会; 您通常不会说应用所支持的所有语言。很明显，APK 里的内容的比您要求的更多，占用的空间也比实际需要的更多。

Android App Bundle 是什么？
Android App Bundle 是一种发布格式 —— 精确地说，是一个带有 .aab 扩展名的 zip 文件。它包含应用支持的所有设备的代码和资源，例如 DEX 文件、本地代码库、清单文件、各种资源文件等。一旦上传用于发布，Google Play 就会处理 APK 的签名和生成，这个过程称为动态交付 (Dynamic Delivery)。动态交付的用途是，根据用户的设备配置为用户生成优化的 APK。那么这究竟是怎么做到的？
