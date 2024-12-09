---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/WSL/WSL/","dgPassFrontmatter":true,"created":"2024-12-08T22:41:53.411+08:00","updated":"2024-12-09T00:25:07.375+08:00"}
---


# WSL 是什么？

WSL 是 Windows Subsystem for Linux 的缩写，它是一个在Windows 10/11上能够运行原生Linux二进制可执行文件的兼容层。简单来说，它让你能在Windows系统上运行Linux环境



# 我用WSL的动机

- 之前在很多代码中花了大量的时间来解决windows系统和linux系统的差异导致的代码无法运行的问题。
- 最近在研究WSL（Windows Subsystem for Linux），我发现这是一个完美的解决方案，wsl2已经有完整linux内核，和原生linux系统已经几乎没有差异
- 上英伟达也对wsl2做了驱动层面的适配，这样就可以在wsl中直接调用gpu跑深度学习模型。
- 对比传统的虚拟机，wsl启动快，运行效率很高，无缝集成在windows中，使用我熟悉的生产工具和环境来进行开发，例如vscode和pycharm都能直接打开wsl里的python项目和linux终端
	- 目前的问题，windows的文件系统是ntfs，linux的文件系统是ext4，由于文件系统差异， /mnt 下挂载的 Windows 磁盘因为改成通过网络协议进行交互，所以读写性能比较低，尤其是在大量小文件读写的时候，比如传输apk数据集
		- 可能的解决方法：专门拿一个硬盘出来用ext4分区存我的数据，然后直接挂载到wsl中。或者创建vhdx虚拟磁盘挂载进去

# 相关笔记


- [[czc知识库/计算机/搞机/WSL/wsl导出备份，wsl迁移\|wsl导出备份，wsl迁移]]
- [[czc知识库/计算机/搞机/WSL/wsl虚拟磁盘空间压缩\|wsl虚拟磁盘空间压缩]]
- [[czc知识库/计算机/搞机/WSL/wsl中安装ssh服务\|wsl中安装ssh服务]]
- [[czc知识库/计算机/搞机/WSL/wsl中挂载硬盘、分区ext4磁盘\|wsl中挂载硬盘、分区ext4磁盘]]


