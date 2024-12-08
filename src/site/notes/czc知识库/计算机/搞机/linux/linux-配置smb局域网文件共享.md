---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/linux/linux-配置smb局域网文件共享/","dgPassFrontmatter":true,"created":"2024-11-21T10:19:39.118+08:00","updated":"2024-12-08T11:41:31.700+08:00"}
---



### linux下操作：
```bash
# 1. 安装 Samba

sudo apt update

sudo apt install samba

  

# 2. 创建共享目录（如果还没有）

# 假设使用之前挂载的 /mnt/data

sudo chmod 777 /mnt/data

  

# 3. 添加 Samba 用户（通常使用你的 Linux 用户名）

sudo smbpasswd -a czc  # 设置 Samba 密码

  

# 4. 编辑 Samba 配置文件

sudo nano /etc/samba/smb.conf

  

# 在文件末尾添加以下配置：

[data]

    path = /mnt/data

    browseable = yes

    read only = no

    create mask = 0777

    directory mask = 0777

    valid users = czc

    force user = czc

    force group = czc

  

# 5. 重启 Samba 服务

sudo systemctl restart smbd

sudo systemctl restart nmbd

  

# 6. 如果有防火墙，需要开放相关端口

sudo ufw allow samba

```

### Windows 访问方式：

- 打开文件资源管理器

- 在地址栏输入：\\你的Linux主机IP

- 输入用户名（czc）和密码（你设置的 Samba 密码）

### macOS 访问方式：

- 在 Finder 中点击"前往" -> "连接服务器"

2. 输入：smb://你的Linux主机IP

- 输入用户名和密码


### 配置说明

```bash
[data]                      # 共享名称
    path = /mnt/data        # 共享目录路径
    browseable = yes        # 是否可见
    read only = no          # 允许写入
    create mask = 0777      # 新建文件权限
    directory mask = 0777   # 新建目录权限
    valid users = czc       # 允许访问的用户
    force user = czc        # 强制文件所有者
    force group = czc       # 强制文件组
```

### 检查服务状态

```bash
# 检查 Samba 服务状态
sudo systemctl status smbd

# 查看共享列表
smbclient -L localhost -U czc

# 检查配置文件语法
testparm
```

### 常见问题

```bash
# 如果访问被拒绝，检查 SELinux
sudo setenforce 0  # 临时关闭 SELinux

# 如果需要永久关闭 SELinux
sudo nano /etc/selinux/config
# 将 SELINUX=enforcing 改为 SELINUX=disabled

# 检查日志文件
sudo tail -f /var/log/samba/log.smbd
```