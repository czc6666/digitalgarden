---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/WSL/wsl虚拟磁盘空间压缩/","dgPassFrontmatter":true,"created":"2024-10-31T20:45:25.852+08:00","updated":"2024-12-08T12:34:13.054+08:00"}
---


[使用diskpart释放WSL2的磁盘空间\_wsl 空间释放-CSDN博客](https://blog.csdn.net/hzgaoshichao/article/details/125530763)

 `select vdisk file="C:\Users\CZC\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu22.04LTS_79rhkp1fndgsc\LocalState\ext4.vhdx"`

 `compact vdisk`
 