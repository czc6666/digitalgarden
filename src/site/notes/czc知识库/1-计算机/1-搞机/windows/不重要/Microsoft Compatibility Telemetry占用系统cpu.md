---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/windows/不重要/Microsoft Compatibility Telemetry占用系统cpu/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.375+08:00","updated":"2024-12-08T12:34:13.042+08:00"}
---


[Microsoft Compatibility Telemetry占用系统cpu-CSDN博客](https://blog.csdn.net/liuyukuan/article/details/119426976)

关闭它的方法如下：
Microsoft Compatibility Telemetry是微软下的一个监测数据收集服务，如果加入microsoft 客户反馈改善计划，该服务就会在监测系统异常并收集反馈到微软。

一般我们肯定要保证系统运行的流畅，所有建议大家禁止该服务。

打开程序搜索框，输入计划任务，找到计划任务工具

打开计划任务后如下图所示。依次展开左侧列表。

Microsoft---Windows---Application Experience，依次找到Application Experience列表

在Application Experience列表点击，右侧菜单列表中，找到Microsoft Compatibility Telemetry Microsoft服务。右击弹出快捷菜单，点击禁用