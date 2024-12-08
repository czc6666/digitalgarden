---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/windows/端口转发笔记 windows/","dgPassFrontmatter":true,"created":"2024-10-31T20:45:26.198+08:00","updated":"2024-12-08T12:34:12.991+08:00"}
---


# 前置条件
### 注册表配置：
导航到HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters。
找到或创建一个名为IPEnableRouter的DWORD值，并将其设置为1。

### 防火墙添加入站规则

# 配置端口转发

netsh interface portproxy add v4tov4 listenaddress=192.168.25.25 listenport=8800 connectaddress=127.0.0.1 connectport=8800

**记得防火墙放开端口**


### 查看当前所有的转发规则
netsh interface portproxy show all

侦听 ipv4:                 连接到 ipv4:

地址            端口        地址            端口
--------------- ----------  --------------- ----------
127.0.0.1       3332        192.168.137.25  3332  ×
10.21.127.9     3332        192.168.137.25  3332  √

---


netsh interface portproxy add v4tov4 listenaddress=192.168.137.25 listenport=3332 connectaddress=127.0.0.1 connectport=3332

↑配置ssh的端口转发、



netsh interface portproxy add v4tov4 listenaddress=10.21.127.9 listenport=2200 connectaddress=192.168.137.25 connectport=2200

netsh interface portproxy delete v4tov4 listenaddress=192.168.137.25 listenport=2200


# 大模型对话记录

我现在有两台windows电脑a和b，a通过无线网卡连接了无线网络（ip地址是10.21.127.9，这也是我的也是公网ip），使用无线网卡共享网络给了有线网的那个网口，a电脑的有线网的网口的ip地址是192.168.137.1，然后我的b电脑通过网线连接a电脑，ip地址是192.168.137.25，现在我在b电脑上开了一个http服务器，端口号是3332，我该如何通过外网通过a机器访问到b机器的这个http服务器，我想通过访问10.21.127.9:3332网址就能进入我的http服务器

要通过外网访问位于B电脑上的HTTP服务器，您需要在A电脑上设置端口转发，将外部的HTTP请求从A电脑的公网IP地址（10.21.127.9）转发到B电脑的HTTP服务器（192.168.137.25:3332）。这可以通过使用Windows的netsh命令来实现端口转发。

### 步骤1: 设置端口转发

在A电脑上，您需要添加一个端口转发规则，使得所有发送到A电脑公网IP（10.21.127.9）上的3332端口的数据都会被转发到B电脑的3332端口。打开命令提示符（以管理员身份），然后输入以下命令：

Bash

Ask

Copy

Run

netsh interface portproxy add v4tov4 listenaddress=10.21.127.9 listenport=3332 connectaddress=192.168.137.25 connectport=3332

这个命令的参数解释如下：

- listenaddress=10.21.127.9：A电脑的公网IP地址。

- listenport=3332：外部访问时使用的端口号。

- connectaddress=192.168.137.25：B电脑的内网IP地址。

- connectport=3332：B电脑上HTTP服务器的端口号。

### 步骤2: 确保防火墙允许端口转发

您需要确保Windows防火墙允许从listenport（在本例中为3332）的流量。可以通过Windows防火墙的高级设置添加新的入站规则来允许此端口的流量。

1. 打开“控制面板” -> “系统和安全” -> “Windows Defender 防火墙”。

2. 在左侧选择“高级设置”。

3. 在“Windows Defender 防火墙与高级安全”窗口中，选择“入站规则”。

4. 在右侧点击“新建规则”。

5. 选择“端口”，然后点击“下一步”。

6. 选择“TCP”，指定“特定本地端口”，输入3332，然后点击“下一步”。

7. 选择“允许连接”，然后继续。

- 选择适用的配置文件（通常选择“域”，“私有”，“公共”），然后点击“下一步”。

9. 给规则命名，例如“HTTP Server Forwarding”，然后点击“完成”。

### 步骤3: 测试访问

从外网环境（非您家庭或办公网络）尝试访问您的HTTP服务器。在浏览器地址栏输入 http://10.21.127.9:3332。如果一切设置正确，您应该能够看到从B电脑上的HTTP服务器返回的页面。

### 注意事项

- 确保在执行这些命令时使用管理员权限的命令提示符。

- 考虑到安全因素，确保您的HTTP服务器已经进行了适当的安全配置，避免潜在的安全风险。

- 如果您在设置过程中遇到任何问题，检查所有设备的IP配置和防火墙设置是否正确。

我在a电脑上可以通过运行里输入\\192.168.137.25来访问的b主机的共享文件，我现在想能不能把这个也通过端口转发，让我能在外面也能通过\\10.21.127.9访问，因为我想当做一个网盘

要通过外网访问位于B电脑上的共享文件夹，您需要设置SMB（Server Message Block）协议的端口转发。然而，直接通过Internet公开SMB端口通常不推荐，因为这可能带来安全风险。如果确实需要远程访问文件，建议使用VPN（虚拟私人网络）或其他更安全的方法。但如果您仍然想通过端口转发来实现，以下是步骤：

### SMB端口

SMB通信通常使用以下端口：

- TCP 445 (SMB直接在TCP上)

- TCP 139 (如果通过NetBIOS在TCP上)

### 设置端口转发

1. 在A电脑上设置端口转发：

使用netsh命令在A电脑上为这两个端口设置端口转发。打开命令提示符（管理员），然后输入：

Bash

Ask

Copy

Run

   netsh interface portproxy add v4tov4 listenaddress=10.21.127.9 listenport=445 connectaddress=192.168.137.25 connectport=445

   netsh interface portproxy add v4tov4 listenaddress=10.21.127.9 listenport=139 connectaddress=192.168.137.25 connectport=139

2. 配置Windows防火墙：

在A电脑上，允许TCP端口445和139的入站连接。可以通过“Windows Defender 防火墙”的“高级设置”添加新的入站规则。

### 考虑安全性

- 使用VPN：建议设置VPN，让外部设备安全地连接到您的内部网络，然后像在本地网络一样访问共享文件。

- 使用更安全的文件共享服务：考虑使用如Nextcloud、Google Drive等服务，这些服务为远程文件访问提供了更好的安全性和易用性。

### 测试访问

从外网环境尝试访问您的共享文件夹。在文件资源管理器地址栏输入 \\10.21.127.9 看是否能访问到共享文件夹。

### 注意事项

- 直接通过Internet公开SMB端口可能会使您的系统面临安全风险，如勒索软件攻击等。

- 确保进行适当的安全配置，包括使用强密码、定期更新系统和软件等。

总之，虽然技术上可以通过端口转发实现这一功能，但出于安全考虑，强烈建议使用VPN或其他安全的远程访问解决方案。

我现在有一台c主机，是linux系统，内网ip地址是192.168.137.3，开启了ssh服务，端口号是22，我想端口转发到10.21.127.9的2203端口

要将位于C电脑（Linux系统）上的SSH服务（默认端口22）通过A电脑（作为网关）转发到外网的特定端口（例如2203），您可以在A电脑上设置端口转发。这样，任何到A电脑公网IP（10.21.127.9）上的2203端口的SSH请求都会被转发到C电脑的22端口。以下是详细的设置步骤：

### 步骤1: 在A电脑上设置端口转发

在A电脑上，您需要使用netsh命令来添加端口转发规则。请以管理员权限打开命令提示符，然后输入以下命令：

Bash

Ask

Copy

Run

netsh interface portproxy add v4tov4 listenaddress=10.21.127.9 listenport=2203 connectaddress=192.168.137.3 connectport=22

这个命令的参数解释如下：

- listenaddress=10.21.127.9：A电脑的公网IP地址。

- listenport=2203：外部访问时使用的端口号。

- connectaddress=192.168.137.3：C电脑的内网IP地址。

- connectport=22：C电脑上SSH服务的端口号。

### 步骤2: 确保防火墙允许端口转发

您需要确保Windows防火墙允许从listenport（在本例中为2203）的流量。可以通过Windows防火墙的高级设置添加新的入站规则来允许此端口的流量。

1. 打开“控制面板” -> “系统和安全” -> “Windows Defender 防火墙”。

2. 在左侧选择“高级设置”。

3. 在“Windows Defender 防火墙与高级安全”窗口中，选择“入站规则”。

4. 在右侧点击“新建规则”。

5. 选择“端口”，然后点击“下一步”。

6. 选择“TCP”，指定“特定本地端口”，输入2203，然后点击“下一步”。

7. 选择“允许连接”，然后继续。

- 选择适用的配置文件（通常选择“域”，“私有”，“公共”），然后点击“下一步”。

9. 给规则命名，例如“SSH Forwarding to C”，然后点击“完成”。

### 步骤3: 测试SSH连接

从外网环境尝试通过SSH连接到您的C电脑。在SSH客户端中，使用以下命令：

Bash

Ask

Copy

Run

ssh -p 2203 username@10.21.127.9

其中username是您在C电脑上的用户名。如果一切设置正确，您应该能够成功连接到C电脑。

### 注意事项

- 确保在执行这些命令时使用管理员权限的命令提示符。

- 考虑到安全因素，确保您的SSH服务已经进行了适当的安全配置，例如使用密钥认证代替密码认证，以及定期更新系统和软件。

- 直接通过Internet公开SSH端口可能会使您的系统面临安全风险，建议使用更安全的方法，如VPN。

---

如果您的A电脑充当软路由器，并且外网可以直接访问A电脑，您需要在A电脑上设置端口转发，以便将外部的HTTP请求转发到B电脑上的HTTP服务器。在Windows系统中，您可以使用netsh命令来设置端口转发。
步骤1：开启IP转发
首先，确保A电脑已经开启了IP转发功能。这可以通过编辑注册表来完成：
打开“运行”对话框（Win + R），输入regedit，按Enter打开注册表编辑器。
导航到HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters。
找到或创建一个名为IPEnableRouter的DWORD值，并将其设置为1。
重启A电脑以应用更改。
步骤2：使用netsh命令设置端口转发
在A电脑上打开命令提示符（以管理员身份），然后使用以下命令设置端口转发：
Bash
这里的参数解释如下：
listenport=3332：A电脑监听的端口。
listenaddress=192.168.137.1：A电脑的IP地址。
connectport=3332：B电脑上HTTP服务器的端口。
connectaddress=192.168.137.25：B电脑的IP地址。
步骤3：确保防火墙设置允许端口转发
您需要确保Windows防火墙允许从listenport（在本例中为3332）的流量。可以通过Windows防火墙的高级设置添加新的入站规则来允许此端口的流量。
步骤4：测试端口转发
从另一台不在您本地网络中的电脑上，尝试访问http://[A电脑的公网IP]:3332。如果设置正确，您应该能够看到从B电脑上的HTTP服务器返回的内容。
注意事项
确保A电脑的公网IP是固定的，或者使用DDNS服务，以便从外网可靠地访问。
考虑到安全因素，确保您的HTTP服务器已经进行了适当的安全配置，避免潜在的安全风险。
如果您在设置过程中遇到任何问题，检查所有设备的IP配置和防火墙设置是否正确。