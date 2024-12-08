---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Windows/右键菜单添加新建选项添加自定义项目 typora 右键新建md文件/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.114+08:00","updated":"2024-12-08T12:34:12.975+08:00"}
---


https://zhuanlan.zhihu.com/p/325845278
在计算机`\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Discardable\PostSetup\ShellNew`文件夹中双击编辑Classes文件，添加.vsdx
↑必须要有常用软件绑定的格式才能用↑
↓添加右键新建.md文件教程
https://blog.csdn.net/qq_43564374/article/details/109471694
绑定typora。注册表脚本👇
```注册表脚本
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\.md]
@="Typora.exe"
[HKEY_CLASSES_ROOT\.md\ShellNew]
"NullFile"=""
[HKEY_CLASSES_ROOT\Typora.exe]
@="czc的md笔记"
```