---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/pytorch笔记/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.874+08:00","updated":"2024-12-08T12:27:33.516+08:00"}
---




## 入门

```python
import torch	//导入pytorch，***不是pytouch***

x = torch.arange(12)	//创建tensor([ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11])

x.shape	//显示张量的形状，比如上面的就是torch.Size([12])

x.numel()	//张量中元素总数	12

X = x.reshape(3, 4)	//改变张量形状→三行字列

torch.zeros((2, 3, 4))	//创建2x3x4的全0三维矩阵

torch.ones((2, 3, 4))	//创建2x3x4的全1三维矩阵

torch.randn(3, 4)	//创建3行4列，元素~N(0,1)的随机矩阵

torch.tensor([[2, 1, 4, 3], [1, 2, 3, 4], [4, 3, 2, 1]])	//手动创建矩阵

---

## 运算符

#### 按元素（elementwise）运算

命令：

x = torch.tensor([1.0, 2, 4, 8])

y = torch.tensor([2, 2, 2, 2])

x + y, x - y, x * y, x / y, x ** y	# **运算符是求幂运算

torch.exp(x)	#求幂

结果：

(tensor([ 3., 4., 6., 10.]), 

tensor([-1., 0., 2., 6.]), 

tensor([ 2., 4., 8., 16.]), 

tensor([0.5000, 1.0000, 2.0000, 4.00]), 

tensor([ 1., 4., 16., 64.]))

#### 线性代数运算

#### 多个张量连接在一起

X = torch.arange(6, dtype=torch.float32).reshape((2,3))

Y = torch.tensor([[2.0, 1, 3], [1, 2, 3]])

torch.cat((X, Y), dim=0), torch.cat((X, Y), dim=1)

输出：

(tensor([[0., 1., 2.],
     	   [3., 4., 5.],
  	      [2., 1., 3.],
  	      [1., 2., 3.]]), 
tensor([[0., 1., 2., 2., 1., 3.],
	        [3., 4., 5., 1., 2., 3.]]))

czc
```
