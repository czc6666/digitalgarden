---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/windows/wsl-windows的linux子系统笔记/","dgPassFrontmatter":true,"created":"2024-11-16T21:01:14.932+08:00","updated":"2024-12-08T12:34:12.973+08:00"}
---



# WSL介绍

> [!NOTE] 微软官方的介绍
> 开发人员可以在 Windows 计算机上同时访问 Windows 和 Linux 的强大功能。 通过适用于 Linux 的 Windows 子系统 (WSL)，开发人员可以安装 Linux 发行版（例如 Ubuntu、OpenSUSE、Kali、Debian、Arch Linux 等），并直接在 Windows 上使用 Linux 应用程序、实用程序和 Bash 命令行工具，不用进行任何修改，也无需承担传统虚拟机或双启动设置的费用。

WSL（Windows Subsystem for Linux）是一个为在Windows 10和Windows 11上无缝运行Linux二进制可执行文件（ELF格式）而设计的兼容层。它允许开发者直接在Windows上运行Linux环境，包括大多数命令行工具、实用程序和应用程序，而无需设置传统的虚拟机或双重启动设置。

wsl1和wsl2没有绝对的哪个好，各有各的特点，按需选择

### WSL 1

WSL 1 是第一个版本的Windows Subsystem for Linux，它通过一个翻译层实现，这个翻译层将Linux系统调用转换为Windows系统调用。这种方法允许Linux程序在Windows上运行，而不需要Linux内核。
特点：
- 集成性好：与Windows系统高度集成，文件系统和进程间通信等方面表现优异。
- 资源占用低：不需要运行一个完整的Linux内核，因此资源占用相对较低。
- 兼容性问题：由于是通过系统调用转换实现，某些特定的Linux功能和系统调用可能不被支持，导致兼容性问题。

### WSL 2

WSL 2 是对WSL的重大更新，引入了真正的Linux内核，通过虚拟化技术运行在一个轻量级的虚拟机（VM）中。这提供了更完整的Linux系统调用兼容性，改善了性能，尤其是文件系统性能，同时保持了与WSL 1 相同的用户体验。
特点：
- 真实的Linux内核：WSL 2 使用真实的Linux内核，提高了与Linux应用的兼容性。
- 改进的性能：特别是在处理大量文件操作时，性能大幅提升。
- 完整的系统调用支持：由于使用了真实的Linux内核，几乎所有Linux系统调用都得到支持。
- 资源使用更高：虽然使用了虚拟化技术，但相比WSL 1，WSL 2 在启动和运行时会占用更多资源。
- 简化的网络配置：WSL 2 提供了更自然的网络配置，使得Linux和Windows应用之间的交互更加顺畅。

### WSL 1 与 WSL 2 的区别
- 内核差异：WSL 1 不包含Linux内核，而WSL 2 包含一个真实的Linux内核。
- 性能：WSL 2 在文件系统性能上有显著提升，尤其是在处理大量小文件时。
- 系统调用兼容性：WSL 2 提供了更完整的Linux系统调用支持。
- 资源占用：WSL 2 使用虚拟化技术，因此相对于WSL 1，其资源占用更高。

总的来说，WSL 2 在功能和性能上都有显著提升，特别是对于需要高度兼容Linux环境的开发者来说，WSL 2 是更好的选择。然而，对于那些对资源占用有严格限制或需要与Windows系统更紧密集成的场景，WSL 1 仍然是一个可行的选项。

# WSL的安装
[微软官方教程：安装 WSL | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install)

### 1. 启用 WSL 功能

打开开始菜单，在开始菜单中输入 `启用或关闭 Windows 功能`，在弹出的窗口中勾选 `虚拟机平台` 和 `适用于 Linux 的 Windows 子系统`，确定之后重启系统。

重启系统后，打开终端，在终端中输入：`wsl.exe --update`

即可安装 WSL 相关的组件，这一步可能需要几分钟的时间。

注意：这一步需要保证 Windows Update，Windows 防火墙等功能可以正常使用，如果这一步报错Ox80072ee2 可看下一步的解决方法。

### 2. 安装Ubuntu
打开微软商店里下载Ubuntu发行版：[安装 WSL | Microsoft Learn](https://aka.ms/wslstore)
由于网络因素，无法下载，就用本地安装方法，下面找了一堆下载地址

- [Ubuntu](https://aka.ms/wslubuntu)
- [Ubuntu 24.04](https://wslstorestorage.blob.core.windows.net/wslblob/Ubuntu2404-240425.AppxBundle)
- [Ubuntu 22.04 LTS](https://aka.ms/wslubuntu2204)
- [Ubuntu 20.04](https://aka.ms/wslubuntu2004)
- [Ubuntu 20.04 ARM](https://aka.ms/wslubuntu2004arm)
- [Ubuntu 18.04](https://aka.ms/wsl-ubuntu-1804)
- [Ubuntu 18.04 ARM](https://aka.ms/wsl-ubuntu-1804-arm)
- [Ubuntu 16.04](https://aka.ms/wsl-ubuntu-1604)
- [Debian GNU/Linux](https://aka.ms/wsl-debian-gnulinux)
- [Kali Linux](https://aka.ms/wsl-kali-linux-new)
- [SUSE Linux Enterprise Server 12](https://aka.ms/wsl-sles-12)
- [SUSE Linux Enterprise Server 15 SP2](https://aka.ms/wsl-SUSELinuxEnterpriseServer15SP2)
- [SUSE Linux Enterprise Server 15 SP3](https://aka.ms/wsl-SUSELinuxEnterpriseServer15SP3)
- [openSUSE Tumbleweed](https://aka.ms/wsl-opensuse-tumbleweed)
- [openSUSE Leap 15.3](https://aka.ms/wsl-opensuseleap15-3)
- [openSUSE Leap 15.2](https://aka.ms/wsl-opensuseleap15-2)
- [Oracle Linux 8.5](https://aka.ms/wsl-oraclelinux-8-5)
- [Oracle Linux 7.9](https://aka.ms/wsl-oraclelinux-7-9)
- [Fedora Remix for WSL](https://github.com/WhitewaterFoundry/WSLFedoraRemix/releases/)


## 升级WSL2
[旧版 WSL 的手动安装步骤 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4%E2%80%94download-the-linux-kernel-update-package)
网上下载msi安装包安装即可（或者找我要安装包）

### 设置WSL2为默认版本
打开 PowerShell，然后在安装新的 Linux 发行版时运行以下命令，将 WSL 2 设置为默认版本：

```powershell
wsl --set-default-version 2
```

# 下面是使用中遇到的常见问题👇👇👇
# WSL与windows的文件互通问题

在WSL（Windows Subsystem for Linux）中，Windows和Linux之间的文件互通是一个重要的功能，它允许用户在两个系统之间无缝地访问和操作文件。以下是关于如何在WSL中访问Windows文件，以及在Windows中访问WSL文件的方法和特点。

### WSL 访问 Windows 文件

在WSL中访问Windows文件系统是相对直接的。Windows的驱动器在WSL中自动挂载，并且可以通过`/mnt/<drive>`路径访问，其中`<drive>`是Windows中的驱动器字母（例如C、D等）。

访问方式：

1. 打开WSL终端。
2. 使用cd命令进入挂载的Windows文件系统，例如：

```powershell
   cd /mnt/c
```

3. 现在你可以使用Linux命令来浏览和操作Windows文件系统中的文件。

特点：

- 易用性：直接挂载，易于访问和操作。

- 性能：在WSL 1中，文件操作性能可能不如原生Windows操作，但在WSL 2中得到了显著提升。

- 文件权限：在WSL中操作Windows文件时，可能会遇到文件权限和元数据支持的限制。

### Windows 访问 WSL 文件

#### 常规访问文件方法

此电脑（资源管理器、explorer.exe）左边栏中有个linux，点开里面就是wsl的所有文件

#### 程序员角度的访问文件

在Windows中访问WSL的文件系统则稍微复杂一些，但Windows 10的更新版已经提供了更为直接的方法。

访问方式：

1. 在文件资源管理器中，输入\\wsl$，然后按回车。这将显示所有已安装的Linux发行版。

- 选择你想要访问的发行版，然后浏览其文件系统。

或者，你可以直接使用特定发行版的路径，例如：

`\\wsl$\Ubuntu\home`

这里，“Ubuntu”是Linux发行版的名称，home是Linux文件系统中的一个目录。

特点：
- 直接访问：通过文件资源管理器直接访问WSL文件系统。
- 适用性：适用于文件浏览和传输，但编辑WSL文件时应谨慎，因为Windows应用可能不正确处理Linux文件的权限和元数据。
- 性能：访问速度合理，但可能不适合高强度的文件操作任务。


# WSL中的GPU直连（nvidia的cuda）

[在WSL中使用GPU：WSL2 + Ubuntu 18.04 + CUDA + Gnome图形界面环境配置](https://blog.csdn.net/Ashken/article/details/108974058)

- 新版的gpu驱动里自动集成wsl的cuda，不用另外安装，在wsl的python环境可直接使用cuda


# WSL网络的clash代理

[在 WSL2 中使用 Clash for Windows 代理连接 - East Monster 个人博客](https://eastmonster.github.io/2022/10/05/clash-config-in-wsl/)

> WSL [2.3.11 版本](https://github.com/microsoft/WSL/releases/tag/2.3.11)新增了图形化配置界面 (WSL Settings)，在**网络 > 网络模式**处选择 `Mirrored` 即可：

至于WSL1，我没用过，我不知道

注意：开关代理后需要重启WSL才可生效

# WSL开ssh服务器局域网其他设备连接

[Win11将WSL做SSH服务器，实现通过局域网SSH远程连接到WSL上，并且开机自动启动，手把手教学\_wsl ssh-CSDN博客](https://blog.csdn.net/q4616756/article/details/131842814)

## 使用ssh服务器你可能需要设置端口转发来实现局域网或外网访问
[powershell设置端口转发](powershell设置端口转发.md)

> [!NOTE] ## 端口转发设置方法：
> 
> 
> 命令都是在管理员权限的 `powershell` 中执行
> 
> 
> # 创建端口转发规则的命令：
> ```cobol
> netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=22 connectaddress=127.0.0.1 connectport=222
> ```
> 
> 意思是系统检测（监听）到内部或者是外部有对 ip: `0.0.0.0` 的 `22` 端口 的访问，就把他转发到
>  ip: `127.0.0.1` 的 `222`端口去
> 
> # 删除端口转发规则的命令：
> 
> ```cobol
> netsh interface portproxy delete v4tov4 listenport=22 listenaddress=0.0.0.0
> ```
> 
> 删除对 ip: `0.0.0.0` 的 `22` 端口的监听规则
> 
> # 使用以下命令列出当前的所有端口转发规则：
> 
> ```kotlin
> netsh interface portproxy show all
> ```


## wsl导致系统不能休眠、睡眠解决方案

### 大概率失效方法：

[windows装了wsl子系统后不能正常休眠的问题\_虚拟机监控程序不支持此待机状态-CSDN博客](https://blog.csdn.net/qq_21444067/article/details/129938003)

命令行里输入三行命令

`powercfg -a`

`bcdedit -set hypervisorlaunchtype off`

`bcdedit -set hypervisorlaunchtype auto`

### 自己遇到后的解决方法

下载windows系统镜像，右键挂载后打开setup.exe，进去选择保留全部文件的重装即可（放心，软件设置文件配置等等等全部都在，不会变一点！）

