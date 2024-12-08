---
{"dg-publish":true,"permalink":"/czc知识库/5-就业/Python/python学习/3-python高级/330-html基础（前端）/","dgPassFrontmatter":true,"created":"2024-12-03T16:45:28.769+08:00","updated":"2024-12-08T12:39:45.397+08:00"}
---


html网页框架
css对网页美化

# HTML
## HTML概念与作用

### html定义
HTML 的全称为：HyperText Mark-up Language,指的是**超文本标记语言**。标记：就是标签，<标签名称></标签名
称>，比如:`<html></html>`、`<h1></h1>`等，标签大多数都是成对出现的。

所谓超文本，有两层含义：
1、因为网页中还可以图片、视频、音频等内容(超越文本限制)
2、它还可以在网页中跳转到另一个网页，与世界各地主机的网页链接(超链接文本(`<a></a>`))

### html作用
最简单的脚本语言（python是最简单的编程语言）
html是用来开发网页的，它是开发网页的语言。

## html基本结构

```html
<!DOCTYPE html>  # 文档声明
<html lang="en">  # 告诉浏览器使用英语，网页从这里开始，到</html>结束
    <head>  # 网页的头，负责对网页进行设置标题、编码格式等
        <meta charset="UTF-8">  # 告诉浏览器使用UTF-8编码
        <title>Title</title>  # 网页的标题
    </head>
    <body>  # 网页的主体，负责网页的内容
        网页显示内容
    </body>
</html>
```

网页文件的后缀是.html或者.htm，一个html文件就是一个网页，html文件用编辑器打开显示的是文本，可以用文本的方式编辑它，如果用浏览器打开，浏览器会按照标签描述内容将文件渲染成网页。


## VScode
推荐使用vscode来写html代码

全拼是Visual StudioCode(简称VSCode）是由微软研发的一款**免费、开源**的**跨平台**代码编辑器，目前是前端(网页)
使用最多的一款软件开发工具。


### 插件：
open in browser：右击在浏览器打开html
vscode-icons：美化文件图标

## 常用的html标签
了解单标签和双标签

### html中的注释
`<!-- 双标签、六级标题 -->`

### 常见的双标签
#### 标题标签`<h1>标题</h1>`
一共有六级标题
可嵌套
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Title</title>
</head>
<body>
    <!-- 双标签、六级标题 -->
    <h1>一级标题</h1>
    <h2>二级标题</h2>
    <h3>三级标题</h3>
    <h4>四级标题</h4>
    <h5>五级标题</h5>
    <h6>六级标题</h6>
</body>
</html>
```
#### 段落标签`<p1>内容</01>`
每段都是个段落
#### 布局标签`<div></<div>`
负责整个网页的结构
div+css专门用来做网页布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Title</title>
</head>
<body>
    <!-- div布局标签，负责整个网页结构，可嵌套 -->
    <div>
        <h1>div布局标签，负责整个网页结构，可嵌套</h1>
        <p>
            段落标签，这里放文字
        </p>
    </div>
</body>
</html>
```

#### 有序列表`<ol></ol>`
会自动添加序号，类似于md的“`1.`”
#### 无序列表`<ul></ul>`
自动添加“·”，类似与md 的“`- `”

```html
    <!-- 列表标签：有序列表和无序列表 -->
    <ol>
        <li>有序列表</li>
        <li>有序列表</li>
        <li>有序列表</li>
    </ol>
    <ul></ul>
        <li>无序列表</li>
        <li>无序列表</li>
        <li>无序列表</li>
    </ul>
```

#### 超文本链接标签
一种双标签，从一个页面跳转到另一个页面
```html
<a href="URL">content</a>
```
### 常见的单标签
 只有开始标签没有结束标签

#### 换行标签`<br>`
文本的换行需要通过换行标签来实现，否则就在一坨
一个换行标签不行就两个换行标签，换两行

#### 水平线标签`<hr>`

#### 图片标签（img标签）`<img src="a.jpg">`
标签里有属性
`<!--img标签，图片标签=><img 属性=属性值>-->`


两个参数↓
```html
<img src="图片地址" alt="当图片无法显示时，所提示的文字信息">
```
图片地址可以来源网络

### 表格标签`<table></table>`
```html
    <table border="1"(边框宽度)>
        <tr></tr>
            <td>表头1</td>
            <td>表头2</td>
        </tr>
        <tr></tr>
            <td>内容1</td>
            <td>内容2</td>
        </tr>
    </table>
```
### 表单标签（双标签）`<form></form>`
表单用于**搜集**不同类型的**用户输入**（用户输入的数据），然后可以把用户数据提交到web服务器（Python）。（前端到后端）

下面的代码包括：标签，输入框，单选框，复选框，下拉菜单选择，文本输入框，提交和重置按钮
```html
    <form></form>
        <label for="username">用户名：</label>
        <input type="text" id="username" placeholder="请输入用户名">
        <br>
        <label for="password">密码：</label>
        <input type="password" id="password" placeholder="请输入密码">
        <br>
        <label for="gender">性别：</label>
        <input type="radio" id="gender" name="gender" value="男">男
        <input type="radio" id="gender" name="gender" value="女">女
        <br>
        <label for="hobby">爱好：</label>
        <input type="checkbox" id="hobby" name="hobby" value="篮球">篮球
        <input type="checkbox" id="hobby" name="hobby" value="足球">足球
        <input type="checkbox" id="hobby" name="hobby" value="乒乓球">乒乓球
        <br>
        <label>日期：</label>
        <select name="date" id="date">
            <option value="1">1999</option>
            <option value="2">2000</option>
            <option value="3">2001</option>
            </select>
        <br>
        <textarea name="textarea" id="textarea" cols="30" rows="10">ss</textarea>
        <input type="submit" value="提交">
        <input type="reset" value="重置">
    </form>
```

#### 表单的提交
提交路径和方式

```
<form>标签表示表单标签，定义整体的表单区域
action属性设置表单数据提交地址
method属性设置表单提交的方式，一般有“GET"方式和“POST"方式，不区分大小写
```

它们定义了表单的行为和数据的处理方式
action：表单发送的URL，例如↓
```html
<form action="submit_form.php">
```
method：数据发送到服务器时应使用的HTTP方法，有post和get
	get：将表单数据附加到action URL后面，并在浏览器的地址栏中显示这些数据
	post：将表单数据包含在HTTP请求的主体中，不会在浏览器地址栏中显示这些数据
例如↓
```html
<form method="post">
```
name：为表单元素指定一个名称
```html
<input type="text" name="username">
```
value：为表单元素定义初始值
```html
<input type="submit" value="Submit">
```

表单的一个栗子
提交到baidu.com，提交方法是post
```html
    <form action="http://www.baidu.com" method="post">
        <label for="username">用户名：</label>
        <input type="text" id="username" name="username" placeholder="请输入用户名">
        <br>
        <label for="password">密码：</label>
        <input type="password" id="password" name="password" placeholder="请输入密码">
        <br>
        <input type="submit" value="提交">
        <input type="reset" value="重置">
    </form>
```
## html中的路径问题

### 绝对路径
windows下：`C:\Python\dog.png`
不适合迁移
### 相对路径
相对于这个html文件
#### 同级关系
直接使用文件名或者 `./文件名`
#### 上级关系
`../一层`
`../../两层`
#### 下级关系
`文件夹/ll.jpg`



## input标签的属性合集

```html
    <!-- 文本输入 -->
    <label>普通文本：</label>
    <input type="text" placeholder="请输入文本">
    <br>

    <!-- 密码输入 -->
    <label>密码：</label>
    <input type="password" placeholder="请输入密码">
    <br>

    <!-- 数字输入 -->
    <label>数字：</label>
    <input type="number" min="0" max="100">
    <br>

    <!-- 邮箱输入 -->
    <label>邮箱：</label>
    <input type="email" placeholder="请输入邮箱">
    <br>

    <!-- 单选按钮 -->
    <label>性别：</label>
    <input type="radio" name="gender" value="male">男
    <input type="radio" name="gender" value="female">女
    <br>

    <!-- 复选框 -->
    <label>爱好：</label>
    <input type="checkbox" name="hobby" value="reading">阅读
    <input type="checkbox" name="hobby" value="sports">运动
    <input type="checkbox" name="hobby" value="music">音乐
    <br>

    <!-- 文件上传 -->
    <label>上传文件：</label>
    <input type="file">
    <br>

    <!-- 日期选择 -->
    <label>日期：</label>
    <input type="date">
    <br>

    <!-- 颜色选择 -->
    <label>颜色：</label>
    <input type="color">
    <br>

    <!-- 范围滑块 -->
    <label>音量：</label>
    <input type="range" min="0" max="100">
    <br>

    <!-- 搜索框 -->
    <label>搜索：</label>
    <input type="search" placeholder="请输入搜索内容">
    <br>

    <!-- 提交按钮 -->
    <input type="submit" value="提交">

    <!-- 重置按钮 -->
    <input type="reset" value="重置">
```