---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/编程/python笔记/python：检查路径是否存在，不存在就递归创建此路径/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.964+08:00","updated":"2024-12-08T12:19:23.722+08:00"}
---



```python
if not os.path.exists(self._working_path):  
	os.makedirs(self._working_path)
```
>chatgpt:这段代码首先使用`os.path.exists()`函数检查指定路径`self._working_path`是否存在。如果该路径不存在，`os.makedirs()`函数会递归地创建这个路径及其上级目录，以确保在后续操作中可以正常存储文件。这样的操作通常用于确保工作目录或文件存储路径在使用之前是存在的，避免因路径不存在而导致的错误。
