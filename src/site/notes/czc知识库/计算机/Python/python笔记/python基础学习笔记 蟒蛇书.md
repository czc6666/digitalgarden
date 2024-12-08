---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python笔记/python基础学习笔记 蟒蛇书/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.906+08:00","updated":"2024-12-08T12:19:23.662+08:00"}
---



# 第二章  变量和简单数据类型

```python
# 将一条消息赋给变量并且将其打印出来  
a = 'you are very good'  
print(a)
```

```python
# 在字符串中使用变量↓  
# 把两个变量搞成一个变量要用ａ＝　ｆ＂｛ｘ｝｛ｙ｝＂  
  
first_name = '阿普杜拉'  
mid_name = '穆罕穆德'  
last_name = '克斯特洛夫斯基'  
full_name = f"sb→{first_name}·{mid_name}·{last_name}"  
print(f"hello,{full_name}")  
print("\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\thello")  
message = f"hello,{full_name}"  
print(message)  
  
# 添加空白用\n和\t  
# 删除空白用.strip()方法  
# 分为三种: 某某某.lstrip() 某某某.strip() 某某某.rstrip()
name = " sb "  
  
print(name.strip())  
print(name.lstrip())  
print(name.rstrip())

```

```python
"""  
用变量表示一个人的名字，再用小写，大写和首字母大写的方式显示人名  
"""  
a_name = 'apUdulAmuhanmuDe' # firstname  
b_name = 'kesiTeluoFUsiji' # lastname  
  
# lower  
print(f"{a_name.lower()}·{b_name.lower()}")  
  
# upper()  
print(f"{a_name.upper()}·{b_name.upper()}")  
  
# title()  
print(f"{a_name.title()}·{b_name.title()}")
```


# 第三章 列表
```python
# 3-1 将一些朋友的姓名存储在一个列表中，并将其命名为names。依次访问该列表中的每个元素，从而将每个朋友的姓名打印出来  
names = ['frank', 'fuck', 'framework']  
for n in names:  
print(n)  
  
# 3-2 问候语：继续使用3-1中的列表，但是不打印每个朋友的姓名，而为每人打印一条消息  
# 每条消息都包含相同的问候语，但抬头为朋友的姓名  
for name in names:  
print(f"hello {name.title()}, fuck you")  
  
# 3-3 自己的列表：想想你喜欢的通勤方式，如骑摩托车，并创建以一个包含多种通勤方式的列表。  
# 根据该列表打印一系列有关这些通勤方式的宣言，下面是一个例子  
# I would like to own a Honda motorcycle  
Commuting = ['bycycle', 'motorcycle', 'car']  
for way in Commuting:  
print(f"I would like to own a Honda {way}")  
  
################################################  
# 列表末尾添加元素：append()，例如a.append(b)  
# 列表第二个位置插入元素：a.insert(1,b)  
# 列表末尾弹出（类似于栈，删除）：a.pop()或x=a.pop()————也可以弹出任意位置的:x=a.pop(2)  
# 列表任意位置删除元素del a[0]  
# 根据值删除元素：a.remove('sb')————只删除列表中第一个指定的值  
################################################  
  
# 3-4 嘉宾名单  
guests = names  
for gg in guests:  
print(f"hi {gg}, please you attend my party")  
  
# 3-5 修改嘉宾名单  
no_lai = 'framework'  
print(f"{no_lai}来不了了")  
guests.remove(no_lai)  
guests.append('mike')  
for gg in guests:  
print(f"hi {gg}, please you attend my party")  
  
# 3-6 添加嘉宾  
guests.insert(0, "a")  
guests.insert(2, 'b')  
guests.append('c')  
for gg in guests:  
print(f"hi {gg}, please you attend my party")  
print(guests)  
  
# 3-7 缩减名单  
print('我只能邀请两个人了，其他人别来了')  
for i in range(4):  
print(f"sorry, i can`t 邀请你了，{guests.pop()}")  
i = 0  
for i in range(2):  
print(f"我还是邀请了你{guests[i]}")  
i += 1  
print(guests)  
for _ in range(2):  
del guests[0]  
print(guests)  
  
#############################################  
# a.sort() 永久按字母顺序排序  
# a.sort(reverse=True) 永久按字母逆序排序  
# a.reverse() 反转列表  
#  
# sorted(a) 临时按字母顺序排序  
# sorted(a, reverse=True) 临时按字母逆序排序 True!!!!!!!!!# len(a) 获取列表a的长度  
#############################################  
  
# 3-8 放眼世界  
I_want_to_travel_somewhere = ['LaSa', 'XiAn', 'GuiLin', 'NeiMengGu', 'MaLaiXiYa']  
print(I_want_to_travel_somewhere)  
print(f'临时字母排序:{sorted(I_want_to_travel_somewhere)}')  
print(I_want_to_travel_somewhere)  
print(f'临时反字母排序:{sorted(I_want_to_travel_somewhere, reverse=True)}')  
print(I_want_to_travel_somewhere)  
I_want_to_travel_somewhere.reverse()  
print(I_want_to_travel_somewhere)  
I_want_to_travel_somewhere.reverse()  
print(I_want_to_travel_somewhere)  
print('已经完成两次反转')  
print('顺序排序：')  
I_want_to_travel_somewhere.sort()  
print(I_want_to_travel_somewhere)  
print('逆序排序：')  
I_want_to_travel_somewhere.sort(reverse=True)  
print(I_want_to_travel_somewhere)  
  
# 3-9 晚餐嘉宾  
print(f'我想去的地方一共有{len(I_want_to_travel_somewhere)}处')  
  
# 3-10 尝试使用各个函数  
# 略  
  
# 3-11 不要引发索引错误  
# 例如，列表里有3个元素，你访问第四个元素 a.[3]
```

# 第四章 列表操作

```python
# 4-1 比萨  
pizzas = ["a", 'b', 'c']  
for pizza in pizzas:  
print(f'i like {pizza} pizza')  
print('i really love pizza')  
  
# 4-2 动物  
# 略  
  
####################  
# for _ in range(6):  
# numbers = list(range(1,6,2))  
# min(a) max(a) sum(a)  
# 列表解析，squares = [value**2 for value in range(1,11)]  
####################  
  
# 4-3 数到20  
for i in range(1, 21):  
print(i)  
  
# 4-4 一百万 打印1到一百万  
yi_bai_wan = list(range(1, 1000001))  
# for i in yi_bai_wan:  
# print(i)  
  
# 4-5 一百万求和  
print(f'列表最小数为：{min(yi_bai_wan)},列表最大数为：{max(yi_bai_wan)},列表所有数的和为：{sum(yi_bai_wan)}')  
  
# 4-6 奇数  
odd_number = list(range(1, 20, 2))  
for i in odd_number:  
print(i)  
  
# 4-7 3的倍数  
number3 = list(range(0, 30, 3))  
for i in number3:  
print(i)  
  
# 4-8 立方 1到10的立方打印出来  
for i in range(1,11):  
print(i**3)  
  
# 4-9 立方解析 用列表解析生成  
number333 = [number**3 for number in range(1,11)]  
print(number333)
```

# 第五章 if语句
```python
# 5-1 条件测试 略  
# 5-2 更多条件测试 略  
"""  
if ---:  
---  
elif ---:  
---  
else:  
---  
"""  
# 5-3 外星人颜色  
alien_color = 'yellow'  
if alien_color == 'green':  
print('你得了5分')  
  
# 5-4 外星人颜色2  
if alien_color == 'green':  
print('5point')  
else:  
print('10print')  
  
# 5-5 外星人颜色3  
if alien_color == 'green':  
print('5point')  
elif alien_color == 'yellow':  
print('10print')  
else:  
print('15point')  
  
# 5-6 人生的不同阶段 略  
# 5-7 喜欢的水果  
favorite_fruits = ['banana', 'apple', 'ZhiYin']  
# 5-8 以特殊方式跟管理员打招呼  
users = ['admin', 'a', 'b', 'c', 'd']  
for user in users:  
if user == 'admin':  
print(f"Hello {user}, would you like to see a status report?")  
else:  
print(f"Hello {user}, thank you for logging in again")  
# 5-9 处理没有用户的情形  
users.clear()  
if users:  
for user in users:  
if user == 'admin':  
print(f"Hello {user}, would you like to see a status report?")  
else:  
print(f"Hello {user}, thank you for logging in again")  
else:  
print('We need to find some users')  
# 5-10 检查用户名  
current_users = ['A', 'b', 'C', 'd', 'E']  
print(current_users)  
XiaoXie_current_users = [item.lower() for item in current_users] # !!!!好好学习这句 复制出一个全部是小写的列表  
print(XiaoXie_current_users)  
new_users = ['D', 'B', 'v', 'x', 'z']  
for new_user in new_users:  
if new_user.lower() in current_users:  
print(f'{new_user}:需要使用其他用户名')  
else:  
print(f'{new_user}:这个用户名暂时未被使用')  
# 5-11 序数  
numbers = list(range(1, 10))  
for number in numbers:  
if number == 1:  
print(f'{number}st')  
elif number == 2:  
print(f'{number}nd')  
else:  
print(f'{number}th')
```
# 第六章 字典
```python
# 6-1 人  
ren = {'first_name': 'tony', "last_name": 'chen', 'age': '99', 'city': 'SanYa'}  
print(ren)  
# 6-2 喜欢的数  
# 6-3 词汇表  
dictionary = {'a': 'fuck', 'b': 'frank', 'c': 'fastbook', 'd': 'fastboot', 'e': 'bootloader'}  
for a, b in dictionary.items():  
print(f'{a}:{b}')  
# 6-4 词汇表2  
dictionary['f'] = '盖林柏林'  
dictionary['g'] = '脖子→拧'  
dictionary['h'] = '我叫磁力泵'  
dictionary['i'] = 'engineer'  
dictionary['j'] = '哈哈哈哈哈'  
for a, b in dictionary.items():  
print(f'{a}:{b}')  
# 6-5 河流  
HeLiu = {'黄河': '中国', '长江': '中国', '赣江': '中国'}  
for key, value in HeLiu.items():  
print(f'The {key} runs through {value}')  
for He in set(HeLiu.keys()):  
print(He)  
for GuoJia in set(HeLiu.values()):  
print(GuoJia)  
# 6-6 调查  
print('================')  
favorite_languages = {'jen': 'python', 'sarah': 'c', 'edward': 'ruby', 'phil': 'python'}  
people_list = ['jen', 'sarah', 'phil', 'frank', 'fastbook']  
for people in people_list:  
if people in favorite_languages.keys():  
print('thank you')  
else:  
print('I invite you to participate in this survey')  
print('========================')  
favorite_languages = {'jen': 'python', 'sarah': 'c', 'edward': 'ruby', 'phil': 'python'}  
people_list = {'jen', 'sarah', 'phil', 'frank', 'fastbook'}  
for people in people_list:  
if people in favorite_languages.keys():  
print(f'thank you, {people}')  
else:  
print(f'{people}, I invite you to participate in this survey')  
# 6-7 人们  
ren2 = {'first_name': 'sb', "last_name": '2b', 'age': '88', 'city': '北金'}  
ren3 = {'first_name': '牛逼', "last_name": '铸币', 'age': '77', 'city': '上海'}  
people__ = [ren, ren2, ren3]  
for sb in people__:  
for a, b in sb.items():  
print(a + " 和 " + b)  
# 6-8 宠物  
# 6-9  
# 6-10  
# 6-11  
# 6-12
```
# 第七章 用户输入和while循环
```python
"""  
# 7-1 汽车租赁  
a = input('你要租什么车\n')  
print(f'Let me see if i can find you a {a}')  
# 7-2 餐馆订位  
YongCanRenShu = int(input('有他妈多少个人用餐？？\n'))  
if YongCanRenShu > 8:  
print('没有空桌')  
else:  
print('有空桌')  
# 7-3 10的倍数  
b = int(input('输入一个数\n'))  
if b % 10 == 0:  
print('这就是10的倍数')  
else:  
print('这不是10的倍数')  
# 7-4 披萨配料  
active = True  
while active:  
c = input('请输入你要加入的配料，输入0退出循环')  
if c == '0':  
active = False  
else:  
print(f'已添加{c}')  
# 7-5 电影票  
age = int(input('请输入年龄以计算票价:\n'))  
while 1:  
if age == 0:  
break  
else:  
if age < 3:  
print('免费')  
elif 3 <= age <= 12:  
print('10美元')  
else:  
print('15美元')  
# 7-6 三种出路 略  
# 7-7 无线循环 略  
"""  
# 7-8 熟食店  
sandwich_orders = ['pastrami', 'a', 'pastrami', 'b', 'pastrami', 'c']  
finished_sandwiches = []  
while sandwich_orders:  
sandwich = sandwich_orders.pop()  
print(f'I made your {sandwich} sandwich')  
finished_sandwiches.append(sandwich)  
for a in finished_sandwiches:  
print(f'{a} sandwich is finished')  
# 7-9 五香烟熏牛肉卖完了  
print('===========================')  
sandwich_orders = ['pastrami', 'a', 'pastrami', 'b', 'pastrami', 'c']  
print('Our pastrami is sold out')  
while 'pastrami' in sandwich_orders:  
sandwich_orders.remove('pastrami')  
print(sandwich_orders)  
# 7-10 梦想的度假胜地  
dream_destination = {}  
while 666:  
name = input('please enter your name')  
if name == 'exit':  
break  
destination = input('please enter your dream destination')  
dream_destination[name] = destination  
for a, b in dream_destination.items():  
print(f"{a}'s dream destination is {b}")
```
# 第八章 函数
```python
# printing_fuctions.py
def print_models(unprinted_designs, completed_models):  
"""  
模拟打印每个设计，直到没有打印的设计为止  
打印每个设计后，都将其移到列表completed_models中  
:param unprinted_designs::param completed_models::return:  
"""  
while unprinted_designs:  
current_design = unprinted_designs.pop()  
print(f"Printing model: {current_design}")  
completed_models.append(current_design)  
  
  
def show_completed_models(completed_models):  
"""  
显示打印好的所有模型  
:param completed_models::return:  
"""  
print('\nThe following models have been printed:')  
for completed_model in completed_models:  
print(completed_model)
```
```python
# printing_models.py
from printing_functions import *  
  
unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']  
completed_models = []  
  
print_models(unprinted_designs, completed_models)  
show_completed_models(completed_models)
```
```python
# main.py
# 8-1 消息 8-2 喜欢的图书  
def display_message():  
print('In this chapter I am going to learn about functions')  
  
  
def favorite_book(title):  
print(f"One of my favorite books is {title}")  
  
  
favorite_book('The old man and the sea')  
display_message()  
  
  
# 8-3 T恤  
def make_shirt(size, character):  
print(f"The size of the T-shirt is {size}, and the pattern of the T-shirt is {character}")  
  
  
make_shirt('a', 'b')  
make_shirt(size='sb', character='2b')  
  
  
# 8-4 大号T恤  
def make_shirt(size, character='I love Python'):  
print(f"The size of the T-shirt is {size}, and the pattern of the T-shirt is {character}")  
  
  
make_shirt('large')  
make_shirt('medium')  
make_shirt('999', 'bbb')  
  
  
# 8-5 城市  
def describe_city(name='深圳', country='China'):  
print(f"{name} is in {country}")  
  
  
describe_city()  
describe_city('1', '2')  
describe_city('ss')  
  
  
# 8-6 城市名  
def city_country(city_name, country):  
return f'"{city_name}, {country}"'  
  
  
print(city_country('a', '1'))  
print(city_country('b', '2'))  
print(city_country('c', '3'))  
  
  
# 8-7 专辑 # 8-8 用户的专辑 略  
def make_album(singer_name, album_title, number=None):  
b = {singer_name: album_title}  
if number:  
b['number'] = number  
return b  
  
  
print(make_album('a', 'b', 10))  
print(make_album('c', 'd'))  
print(make_album('e', 'f'))  
  
  
# 8-9 消息  
messages = ['111', '222', '333']  
  
  
def show_messages(b):  
for message in b:  
print(message)  
  
  
show_messages(messages)  
print('=================')  
  
  
# 8-10 发送消息  
sent_messages = []  
  
  
def send_messages(a, b):  
while a:  
message = a.pop()  
print(message)  
b.append(message)  
  
  
send_messages(messages, sent_messages)  
print(messages)  
print(sent_messages)  
  
  
# 8-11 消息归档  
print('--------------------------------------------')  
messages = ['111', '222', '333']  
sent_messages = []  
  
  
def send_messages(a, b):  
while a:  
message = a.pop()  
print(message)  
b.append(message)  
  
  
send_messages(messages[:], sent_messages) # ！！！切片在这里切，不是在函数定义的地方切！！！  
print(messages)  
print(sent_messages)  
  
  
# 8-12 三明治  
def sandwich(*sb):  
print('这个sb要求的配料有这些：')  
for a in sb:  
print(f'--{a}')  
  
  
sandwich('1', '2', '3')  
sandwich('sss', 'vvv')  
sandwich('aaa')  
  
  
# 8-13 用户简介  
def build_profile(first, last, **user_info):  
user_info['first_name'] = first  
user_info['last_name'] = last  
return user_info  
  
  
user_profile = build_profile('czc', 'czc', location='GanZhou', country='China')  
print(user_profile)  
  
  
# 8-14 汽车  
def make_car(manufacturer, model, **car_info):  
car_info['manufacturer'] = manufacturer  
car_info['model'] = model  
return car_info  
  
  
car = make_car('subaru', 'outback', color='blue', tow_package=True)  
print(car)
```
# 第九章 类
```python
class User:  
	def __init__(self, name, age, location):  
		self.name = name  
		self.age = age  
		self.location = location  
  
	def print_user_information(self):  
		print(self.name + self.age + self.location)


class Privileges:  
	def __init__(self):  
		self.privileges = ['can add post', 'can delete user', 'can ban user']  
	  
	def show_privileges(self):  
		print(self.privileges)  
  
  
class Admin(User):  
	def __init__(self, name, age, location):  
		super().__init__(name, age, location)  
		self.privileges = Privileges()


czc_admin = admin.Admin('czc', '23', "China")  
czc_admin.privileges.show_privileges()
```
# 第十章 文件和异常
布响学！

# 第十一章 测试代码
布响学！

