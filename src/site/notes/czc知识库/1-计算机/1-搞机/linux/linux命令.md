---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/linux/linux命令/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.647+08:00","updated":"2024-12-08T11:41:39.208+08:00"}
---


、
```
mkdir  # 创建目录
rmdir
rm  # 删文件
lsblk  # 查看已连接设备
sudo mkdir /mnt/usb  # 创建挂载点
sudo mount /dev/sdb1 /mnt/usb  # 挂载U盘
sudo umount /mnt/usb  # 卸载U盘
ln -s 目标文件 链接名称  # 创建超链接
```

[Linux 利用mount挂载移动硬盘（亲测有效）\_linux mount 挂载移动硬盘-CSDN博客](https://blog.csdn.net/qq_52302919/article/details/137552864)



```linux
sudo fuser -m -u /dev/sda2
sudo kill 2280
sudo mount -t ntfs-3g /dev/sda2 Disk4T/
bash Anaconda-1.4.0-Linux-x86_64.sh
export PATH=anaconda/bin/:$PATH

conda config --set show_channel_urls yes
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes

conda create --name datasetdownload python=3.9
```


[linux系统挂载（卸载）U盘（文件系统）\_linux挂载u盘-CSDN博客](https://blog.csdn.net/stay_zezo/article/details/80715761)
[anaconda的安装和使用（管理python环境看这一篇就够了）-CSDN博客](https://blog.csdn.net/tqlisno1/article/details/108908775)


![[vim编辑器使用 linux](vim%E7%BC%96%E8%BE%91%E5%99%A8%E4%BD%BF%E7%94%A8%20linux.md)

实时查看linux内存使用情况命令
`watch -n 0.5 -d free -m`