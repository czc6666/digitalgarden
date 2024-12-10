---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python学习/python模块/python模块-pyinstaller 编译 打包python成exe文件/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.929+08:00","updated":"2024-12-08T12:19:23.704+08:00"}
---


[【Python教程】保姆版教使用Pyinstaller 打包python成exe文件-CSDN博客](https://blog.csdn.net/flyskymood/article/details/123668136)

常用参数 含义  
-i 或 -icon 生成icon  
-F 创建一个绑定的可执行文件  
-w 使用窗口，无控制台  
-C 使用控制台，无窗口  
-D 创建一个包含可执行文件的单文件夹包(默认情况下)  
-n 文件名

---

pyinstaller --noconsole --onefile 哔哔哔.py
pyinstaller --onefile 嘀嘀嘀.py
