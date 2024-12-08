---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/WSL相关/wsl中挂载硬盘、分区ext4磁盘/","dgPassFrontmatter":true,"created":"2024-10-24T23:27:39.072+08:00","updated":"2024-12-08T12:34:13.049+08:00"}
---


# 挂载命令记录

```
我现在需要挂载很多个盘符到wsl2中：  
(base) czc@czc-pc:~/mnt$ ls hc310 hc320 wzd0 wzd1 wzd2 wzd3  
我已经创建好了挂载的文件夹  
盘符对应关系如下：  
F → hc320  
G → hc310  
R → wzd1  
S → wzd2  
Z → wzd3  
W → wzd0

sudo mount -t drvfs 'F:' /home/czc/mnt/hc320
sudo mount -t drvfs 'G:' /home/czc/mnt/hc310
sudo mount -t drvfs 'R:' /home/czc/mnt/wzd1
sudo mount -t drvfs 'S:' /home/czc/mnt/wzd2
sudo mount -t drvfs 'Z:' /home/czc/mnt/wzd3
sudo mount -t drvfs 'W:' /home/czc/mnt/wzd0
```

## 测试挂载分区读写性能

```顺序
fio --name=seqwrite --ioengine=libaio --rw=write --bs=1M --numjobs=1 --size=1G --iodepth=1 --runtime=60 --directory=/home/czc/mnt/wzd2 --group_reporting
fio --name=seqread --ioengine=libaio --rw=read --bs=1M --numjobs=1 --size=1G --iodepth=1 --runtime=60 --directory=/home/czc/mnt/wzd2 --group_reporting
```

```随机
fio --name=randwrite --ioengine=libaio --rw=randwrite --bs=4k --numjobs=1 --size=500M --iodepth=32 --runtime=60 --directory=/home/czc/mnt/hc310 --group_reporting
fio --name=randread --ioengine=libaio --rw=randread --bs=4k --numjobs=1 --size=500M --iodepth=32 --runtime=60 --directory=/home/czc/mnt/wzd2 --group_reporting
```

# windows完整硬盘挂载进wsl↓
# [在Windows中使用WSL访问EXT4分区的完整指南](https://blog.csdn.net/redparrot2008/article/details/142484372)


## Linux和WSL操作笔记

### 1. Linux中挂载和卸载分区
- **挂载分区**:
  ```bash
  sudo mount /dev/sda1 /mnt
  ```
- **卸载分区**:
  ```bash
  sudo umount /mnt
  ```

### 2. WSL中挂载和卸载Windows中的分区或文件夹
- **挂载分区**:
  ```bash
  sudo mount -t drvfs C: /mnt/c
  ```
- **卸载分区**:
  ```bash
  sudo umount /mnt/c
  ```

### 3. 创建和删除快捷方式
- **创建快捷方式** (符号链接):
  ```bash
  ln -s /usr/bin/python3 ~/bin/python
  ```
- **删除快捷方式**:
  ```bash
  rm ~/bin/python
  ```

以上是在Linux和WSL环境中管理文件系统和快捷方式的基本操作。