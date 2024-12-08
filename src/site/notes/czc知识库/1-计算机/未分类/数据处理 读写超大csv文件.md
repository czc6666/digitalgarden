---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/未分类/数据处理 读写超大csv文件/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:21.132+08:00","updated":"2024-12-08T12:34:13.088+08:00"}
---



> [!NOTE] 什么是csv文件
> 我们平常使用最多的数据文件就是Excel了，如果你使用Excel处理过数据，你就会发现，对于Excel 97-2003 (.xls)，一张表最多只能存储65536行，对于Excel 2007+ (.xlsx)，最多可以存储1048576行。 
> 于是问题来了，那如果你要存储超过1048576行的数据用什么文件呢？
> csv格式的文件就是这个问题的解决方案之一。CSV是Comma-Separated Values的简称，是一种常见的文本文件格式，用于存储和交换简单的表格数据。CSV文件由纯文本组成，使用逗号（或其他分隔符）将不同的字段分隔开来。在CSV文件中，每一行表示一个数据记录，每个字段被逗号分隔。每个字段可以是文字、数字或其他类型的数据。CSV文件通常不包含任何格式化或样式信息，仅用于保存原始数据。

easyCSV
EasyCsv 是一个基于Java的简单、省内存的读写 csv 的开源项目。
[Java 读写 Csv 利器 EasyCsv-CSDN博客](https://blog.csdn.net/qq_43005544/article/details/122880887)

---
最终是用gpt写代码直接用pandas处理数据，好像是

---




> [!NOTE]- 垃圾，在此浪费了1小时生命
> b站看到的一个文章：[数据处理那些事｜如何读取一个128G的超大csv文件？ - 哔哩哔哩](https://www.bilibili.com/read/cv25171121/)
> 这个B人up给了个公众号输入csv发了个它自己写的？csv处理软件？（人文帮）
> [2023.06-CSV数据处理助手官方版下载丨最新版下载丨绿色版下载丨APP下载-123云盘](https://www.123pan.com/s/BXA9-kLj0d.html)
> - 实测是个垃圾，还要钱