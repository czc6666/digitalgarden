---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/1-收藏大宝贝/Everything：windows系统无敌文件搜索工具/","dgPassFrontmatter":true,"created":"2024-12-03T19:25:04.493+08:00","updated":"2024-12-08T00:37:11.057+08:00"}
---



原理介绍：[Everything原理及个人实现 - 玄虚233 - 博客园](https://www.cnblogs.com/xuanxu233/p/16083526.html)
作者自己写的一个类似的程序：[GitHub - XUANXUQAQ/File-Engine: An app launcher && efficiency tool](https://github.com/XUANXUQAQ/File-Engine)
# Everything原理及实现

网上找了很多的资料，还是没有很清楚的了解Everything这款软件。所以自己研究了以下，并记录下来。

Everything是一个搜索文件速度超快的软件，相比Windows自带的搜索功能，Everything可以做到在数十万文件中做到秒搜。

本文来分析一下Everything背后的原理以及自己实现一个Everything。

## Everything的工作原理

Everything在第一次打开程序时会扫描整个磁盘，并建立一个索引库。需要注意的是，Everything并不是像Windows文件夹遍历那样一个文件一个文件的搜索并记录。而是通过NTFS文件系统的特性，MFT和USN journal。这也是Everything仅支持NTFS文件系统的原因。

**Master File Table (MTF)**

在NTFS文件系统中，有一个特殊的表，称为MTF表。所有文件夹和文件的名称都被存储在该表中，Everything通过遍历这个表的所有内容，实现在不遍历文件系统就能获取当前磁盘中的所有文件的名称和路径。

**USN journal**

NTFS的日志功能。所有对文件系统的修改操作都被记录在了一个journal日志文件中。Everything通过监控这个日志文件实现对文件修改的监控。

**文件查找**

通过字符串匹配算法从之前建立的索引中对字符串进行匹配，并显示文件名称和路径。