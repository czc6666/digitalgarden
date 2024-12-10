---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python学习/③python高级/361-HTTP协议/","dgPassFrontmatter":true,"created":"2024-12-10T20:21:08.388+08:00","updated":"2024-12-10T21:08:20.378+08:00"}
---



# HTTP协议

## 1、HTTP 协议的介绍


- HTTP协议的全称是(HyperTextTransferProtocol)，翻译过来就是**超文本传输协议**。
- 超文本是超级文本的缩写，是指超越文本限制或者超链接，比如:图片、音乐、视频、超链接等等都属于超文本。
- HTTP协议的制作者是**蒂姆·伯纳斯-李**（物理学家），1991年设计出来的，**HTTP协议设计之前目的是传输网页数据的，现在允许传输任意类型的数据**。
- **传输HTTP协议格式的数据是基于TCP传输协议的，发送数据之前需要先建立连接**。

## 2、HTTP的作用

HTTP规定了浏览器和Web服务器通信数据的格式，也就是说浏览器和web服务器通信需要使用http协议。


## 3、浏览器访问Web服务器的通信过程

![361-HTTP协议_image.png](/img/user/czc%E7%9F%A5%E8%AF%86%E5%BA%93/9-%E6%97%A0%E5%A5%87%E4%B8%8D%E6%9C%89/9-%E9%99%84%E4%BB%B6/%E9%99%84%E4%BB%B6/361-HTTP%E5%8D%8F%E8%AE%AE_image.png)



# 查看HTTP协议的通信过程

掌握：
http如何去服务器请求资源
http协议如何相应数据

## 开发者工具的使用
大部分浏览器里按f12（苹果用alt+command+i），打开开发者工具，点击network，可以看到http请求的通信过程。

元素：查看网页的html结构
控制台：用于写js代码调试
网络：**查看http请求的通信过程**
源代码：查看网页的源代码

