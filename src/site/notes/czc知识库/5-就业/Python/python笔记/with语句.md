---
{"dg-publish":true,"permalink":"/czc知识库/5-就业/Python/python笔记/with语句/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.969+08:00","updated":"2024-12-08T12:19:23.729+08:00"}
---



`with`语句是Python中用于创建上下文管理器的关键字。它的作用是简化资源管理（如文件、网络连接、数据库连接等）的代码，确保在使用完资源后能够正确地关闭或释放资源，即使发生异常也能保证资源的正确处理。
```python
with expression as variable:
    # 使用变量进行操作
```


