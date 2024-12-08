---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/编程/python笔记/python关键字：with/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.896+08:00","updated":"2024-12-08T12:19:23.657+08:00"}
---


[Python with 关键字 | 菜鸟教程](https://www.runoob.com/python3/python-with.html)


Python 中的 with 语句用于异常处理，封装了 try…except…finally 编码范式，提高了易用性。

**with** 语句使代码更清晰、更具可读性， 它简化了文件流等公共资源的管理。

有问题的代码，write没有执行的时候，close不会执行，文件不会关闭

```python
file = open('./test_runoob.txt', 'w')  
file.write('hello world !')  
file.close()
```

优化后的

```python
file = open('./test_runoob.txt', 'w')  
try:  
    file.write('hello world')  
finally:  
    file.close()
```

等价

```python
with open('./test_runoob.txt', 'w') as file:
    file.write('hello world !')
```