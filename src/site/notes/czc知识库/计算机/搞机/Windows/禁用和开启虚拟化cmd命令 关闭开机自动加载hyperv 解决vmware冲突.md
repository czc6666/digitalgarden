---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Windows/禁用和开启虚拟化cmd命令 关闭开机自动加载hyperv 解决vmware冲突/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.176+08:00","updated":"2024-12-08T12:34:12.988+08:00"}
---


bcdedit /set hypervisorlaunchtype off
关
bcdedit /set hypervisorlaunchtype auto
开？
完美解决方案是把vmware更新到16以上。还有冲突，那就是肯定是别人的问题
old：最新版vmware可以运行在windows虚拟化的平台上，老的vmware是运行在cpu的硬件虚拟化平台上，和windows的虚拟化平台冲突（也是运行在cpu虚拟的平台上）