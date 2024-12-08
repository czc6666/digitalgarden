---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python学习/②面向对象/306-魔术方法：__dict__()/","dgPassFrontmatter":true,"created":"2024-12-02T18:08:44.450+08:00","updated":"2024-12-08T12:39:45.379+08:00"}
---


把对象转化为字典

把对象的属性转化为字典的键和值


例如，**把学生信息的对象转成列表后保存成列表再保存到文件**

```python
from Student import Student

students = []

s1 = Student('ZhangSan', 23, '10086')
s2 = Student('LiSi', 24, '10010')

students.append(s1)
students.append(s2)

students = [i.__dict__ for i in students]
print(students)
```