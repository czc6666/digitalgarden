---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python学习/③python高级/312-关键字global和nonlocal/","dgPassFrontmatter":true,"created":"2024-12-02T21:34:50.138+08:00","updated":"2024-12-09T17:59:49.225+08:00"}
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
def outer():
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
def outer():
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



# 应用的栗子

```python
"""
假设你是一名网站开发者，你需要设计一个函数 login_counter()，用于统计用户登录的次数和最近一次登录的时间。

要求：
login_counter() 返回一个闭包 login()。
每次调用 login()，它将累加用户登录的次数，并记录最近一次登录的时间。
需要返回一个字典，包含累计的登录次数（total_count）和最近一次登录的时间（last_login_time）。
设计思路：

在 login_counter() 函数外部定义一个变量 count，用于记录累计的登录次数。
在 login_counter() 函数内部定义一个变量 last_login，用于记录最近一次登录的时间戳。
在 login() 函数内部更新 count 和 last_login 的值，并返回字典形式的结果。
"""

import time
count = 0

def login_counter():
    last_login = None
    def login():
        nonlocal last_login
        global count  # 这里count也可以写成nonlocal
        count += 1
        last_login = time.time()
        return {"total_count": count, "last_login_time": last_login}
    return login

# 调用示例
login_counter = login_counter()
print(login_counter())  
print(login_counter())  
```