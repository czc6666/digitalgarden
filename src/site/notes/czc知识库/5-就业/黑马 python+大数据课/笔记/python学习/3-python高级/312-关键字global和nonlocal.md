---
{"dg-publish":true,"permalink":"/czc知识库/5-就业/黑马 python+大数据课/笔记/python学习/3-python高级/312-关键字global和nonlocal/","dgPassFrontmatter":true,"created":"2024-12-02T21:34:50.138+08:00","updated":"2024-12-07T17:35:51.304+08:00"}
---



global：全局变量，代表从这行代码开始，使用的变量都是全局中的变量
只能使用在函数里面
```python
num=10
def func():
	#尝试在局部作用域中修改全局变量
	global num
	num = 100
func()
print(num)
```

global只能修改全局变量
```python
num=1
def outer(）:
	#局部变量
	num = 10
	def inner():
	global num
		num = 100
	inner()
	print(num)  # 输出10
outer()
print(num)  # 输出100
```

nonlocal：离它最近的外层的局部变量
在内层函数里修改离他最近的外层**局部变量**


```python
num=1
def outer(）:
	#局部变量
	num = 10
	def inner():
	nonlocal num
		num = 100
	inner()
	print(num)  # 输出100
outer()
print(num)  # 输出1
```