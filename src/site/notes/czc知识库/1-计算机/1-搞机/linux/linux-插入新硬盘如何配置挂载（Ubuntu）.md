---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/linux/linux-插入新硬盘如何配置挂载（Ubuntu）/","dgPassFrontmatter":true,"created":"2024-11-21T10:07:26.302+08:00","updated":"2024-12-08T11:41:26.603+08:00"}
---



相关查看命令：
lsblk
df -h

```bash
# 1. 首先检查磁盘是否已经格式化，查看是否有分区表
sudo fdisk -l /dev/sda

如果显示如下信息说明未格式化，要继续下面的格式化操作：
Disk /dev/sda：3.64 TiB，4000787030016 字节，7814037168 个扇区
Disk model: ST4000NM024B-2TF
单元：扇区 / 1 * 512 = 512 字节
扇区大小(逻辑/物理)：512 字节 / 4096 字节
I/O 大小(最小/最佳)：4096 字节 / 4096 字节

# 2. 如果磁盘未格式化，需要先格式化
# 创建分区表
sudo fdisk /dev/sda
# 在 fdisk 中：
# 输入 n 创建新分区
# 输入 p 创建主分区
# 分区号按默认回车
# 起始扇区按默认回车
# 结束扇区按默认回车
# 输入 w 保存并退出

# 3. 格式化分区为 ext4 文件系统
sudo mkfs.ext4 /dev/sda1

# 4. 创建挂载点（假设要挂载到 /mnt/data）
sudo mkdir -p /mnt/data

# 5. 挂载磁盘
sudo mount /dev/sda1 /mnt/data

# 6. 检查挂载是否成功
df -h

# 7. 设置开机自动挂载，编辑 /etc/fstab 文件
sudo nano /etc/fstab
或者
sudo vim /etc/fstab
建议用vim，具体使用方法如果没用过请另外搜索，不难

# 在文件末尾添加以下行
/dev/sda1    /mnt/data    ext4    defaults    0    2
❗一个分区只能挂载到一个地方，不能同时挂载两个地方哦，要多个地方访问就去创建快捷方式！！。。11！！
	# . 创建符号链接
	ln -s /mnt/data /home/czc/mnt·
	
# 8. 设置目录权限（假设要给当前用户权限）
sudo chown -R $USER:$USER /mnt/data
```




如何查看硬盘的型号

```bash
# 方法1：使用 lsblk 命令加 -d 参数
lsblk -d -o name,model,size

# 方法2：使用 hdparm 命令（可能需要安装）
sudo apt install hdparm  # 如果没有安装
sudo hdparm -I /dev/sda  # 查看 sda 硬盘详细信息

# 方法3：使用 smartctl 命令（需要安装 smartmontools）
sudo apt install smartmontools  # 安装
sudo smartctl -i /dev/sda      # 查看 sda 硬盘信息

# 方法4：查看系统日志
sudo dmesg | grep -i 'sda\|nvme'

# 方法5：查看硬件信息
sudo lshw -class disk
```