---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python学习/①python基础/211-递归删除文件夹-shutil模块/","dgPassFrontmatter":true,"created":"2024-11-12T13:06:28.819+08:00","updated":"2024-12-08T12:39:45.343+08:00"}
---


`import shutil`
**使用慎重！**

非空目录不能删除文件夹，要强行删除就要用：
`shutil.rmtree('data')`
进目录一个一个删掉后再删除目录