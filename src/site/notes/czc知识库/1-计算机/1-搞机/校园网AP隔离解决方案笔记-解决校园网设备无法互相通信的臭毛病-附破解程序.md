---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/校园网AP隔离解决方案笔记-解决校园网设备无法互相通信的臭毛病-附破解程序/","dgPassFrontmatter":true,"created":"2024-11-17T00:01:50.894+08:00","updated":"2024-12-08T00:37:38.777+08:00"}
---



# 问题介绍 AC AP 隔离
两台电脑在同一楼层时触发了ap隔离，但是隔了距离跨ap是可以正常访问的，这就是原因

无线用户隔离

[华为 WLAN 维护宝典（V200）# 如何配置无线用户隔离？](https://support.huawei.com/enterprise/zh/doc/EDOC1000051014/54f784b4)

[Wifi隔离 （AP隔离）的原理及实现\_mtk noforwarding-CSDN博客](https://blog.csdn.net/xiao_yi_xiao/article/details/131899457)

>AP隔离非常类似有线网络的VLAN(虚拟局域网)，将所有的无线客户端设备之间完全隔离，是客户端只能访问AP接入的固定网络。通俗来讲，就是各个连接无线的客户机（如手机、电脑等）之间无法互相通讯的，即你无法在两台同时连接AP的电脑间使用类似共享文件等功能。因此，在开启该功能之后，可以保护不同用户间的数据安全，有利于抵御外部攻击。

---

[# 家庭无线漫游组网方案——AC+AP篇](https://zhuanlan.zhihu.com/p/235550377)


# 我们的目标是解决校内两设备无法互相通信的臭毛病
# 核心思想，自己重新设置路由规则
举个例子
- AP隔离就像"教室规定学生不能直接传纸条"
- 但学生都可以和老师（网关）通信
- 修改路由相当于"所有纸条都先交给老师转交"
- 这样就绕过了"学生之间不能直接传纸条"的限制


# linux 系统

[AP隔离的设备互相访问 - 王冰冰 - 博客园](https://www.cnblogs.com/wangbingbing/p/17931315.html)

# windows
查看当前路由表：`route print`
删除直连路由：`route delete 10.21.64.0 mask 255.255.192.0`
添加通过网关的路由：`route add 10.21.64.0 mask 255.255.192.0 10.21.64.1`
如果想要路由在重启后依然生效，使用：`route -p add 10.21.64.0 mask 255.255.192.0 10.21.64.1`



默认的
```
IPv4 路由表  
=========================================================================
活动路由:  
网络目标 网络掩码 网关 接口 跃点数  
0.0.0.0 0.0.0.0 10.21.64.1 10.21.127.9 46  
10.21.64.0 255.255.192.0 在链路上 10.21.127.9 301  
10.21.127.9 255.255.255.255 在链路上 10.21.127.9 301
```


---

# 让我用简单的方式解释AP隔离破解的原理：

1. 正常情况（有AP隔离）
	- AP隔离阻止了同一AP下设备之间的直接通信
	- 但所有设备都能和网关通信
```
设备A ←→ AP ←→ 设备B
        ❌
设备A ←→ 设备B
```


2. 修改路由后：
	- 删除直连路由，强制所有通信都经过网关
	- 网关成为"中转站"，帮助转发数据包
```
设备A → 网关 → 设备B
设备B → 网关 → 设备A
```

3. 具体原理：
	- 默认路由表让设备尝试在同一网段内直接通信
	- AP隔离阻止了这种直接通信
	- 修改路由后，即使是同网段通信也会发送到网关
	- 网关没有AP隔离限制，可以转发到目标设备

**就像**：
- AP隔离就像"教室规定学生不能直接传纸条"
- 但学生都可以和老师（网关）通信
- 修改路由相当于"所有纸条都先交给老师转交"
- 这样就绕过了"学生之间不能直接传纸条"的限制

# 破解工作原理

```
设备A ─→ 检测网关 ─→ 修改路由 ─┐
	                        ├─→ 可以互相访问
设备B ─→ 检测网关 ─→ 修改路由 ─┘
```



# ap隔离脚本程序

![windows 将ps、bat、py等脚本、代码编译成exe文件](windows%20将ps、bat、py等脚本、代码编译成exe文件.md)

代码上传github：

```powershell
# 自动请求管理员权限
if (-NOT ([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")) {
    Start-Process powershell -Verb RunAs -ArgumentList "-File `"$PSCommandPath`""
    exit
}

# 获取所有网络适配器
$adapters = Get-NetAdapter | Where-Object { $_.Status -eq "Up" } | ForEach-Object {
    $config = Get-NetIPConfiguration -InterfaceIndex $_.InterfaceIndex
    [PSCustomObject]@{
        Index = $_.InterfaceIndex
        Name = $_.Name
        Description = $_.InterfaceDescription
        IP = $config.IPv4Address.IPAddress
        Gateway = $config.IPv4DefaultGateway.NextHop
        Status = $_.Status
    }
}

# 显示适配器列表
Write-Host "`n所有活动的网络适配器：" -ForegroundColor Green

if ($adapters.Count -eq 0) {
    Write-Host "未找到任何活动的网络适配器！" -ForegroundColor Red
    Write-Host "`n按任意键退出..." -ForegroundColor Yellow
    $null = $Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
    exit
}

for ($i = 0; $i -lt $adapters.Count; $i++) {
    Write-Host "`n[$i] " -NoNewline -ForegroundColor Yellow
    Write-Host "$($adapters[$i].Name)" -ForegroundColor Cyan
    Write-Host "    描述: $($adapters[$i].Description)"
    Write-Host "    IP地址: $($adapters[$i].IP)"
    Write-Host "    网关: " -NoNewline
    if ($adapters[$i].Gateway) {
        Write-Host "$($adapters[$i].Gateway)" -ForegroundColor Green
    } else {
        Write-Host "无默认网关" -ForegroundColor Red
    }
    Write-Host "    状态: $($adapters[$i].Status)"
}

# 用户选择
do {
    Write-Host "`n请选择要配置的网络适配器 [0-$($adapters.Count - 1)]: " -NoNewline -ForegroundColor Green
    $choice = Read-Host
} while ($choice -notmatch '^\d+

将ps脚本编译成exe文件的方法
1. 以管理员身份打开 PowerShell
2. 运行: Install-Module ps2exe -Force
3. 运行: Invoke-ps2exe "route_config.ps1" "路由配置工具.exe" -or [int]$choice -lt 0 -or [int]$choice -ge $adapters.Count)

$selected = $adapters[[int]$choice]

# 检查选择的适配器是否有网关
if (-not $selected.Gateway) {
    Write-Host "`n错误：选择的网络适配器没有默认网关，无法配置！" -ForegroundColor Red
    Write-Host "请选择有默认网关的网络适配器。" -ForegroundColor Yellow
    Write-Host "`n按任意键退出..." -ForegroundColor Yellow
    $null = $Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
    exit
}

# 计算网段
$ipParts = $selected.IP.Split('.')
$networkID = "{0}.{1}.{2}.0" -f $ipParts[0], $ipParts[1], ($ipParts[2] -band 0xC0)

Write-Host "`n正在配置路由..." -ForegroundColor Green
Write-Host "选择的适配器: $($selected.Name)" -ForegroundColor Yellow
Write-Host "网关: $($selected.Gateway)" -ForegroundColor Yellow
Write-Host "网段: $networkID" -ForegroundColor Yellow

# 删除直连路由
Write-Host "`n删除直连路由..." -ForegroundColor Yellow
route delete $networkID mask 255.255.192.0

# 添加网关路由
Write-Host "添加网关路由..." -ForegroundColor Yellow
route -p add $networkID mask 255.255.192.0 $selected.Gateway

Write-Host "`n配置完成！" -ForegroundColor Green
Write-Host "`n按任意键退出..." -ForegroundColor Green
$null = $Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
```

将ps脚本编译成exe文件的方法
1. 以管理员身份打开 PowerShell
2. 运行: Install-Module ps2exe -Force
3. 运行: Invoke-ps2exe "route_config.ps1" "路由配置工具.exe"