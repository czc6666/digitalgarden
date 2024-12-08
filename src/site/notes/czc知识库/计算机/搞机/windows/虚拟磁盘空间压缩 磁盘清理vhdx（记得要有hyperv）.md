---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/windows/虚拟磁盘空间压缩 磁盘清理vhdx（记得要有hyperv）/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.194+08:00","updated":"2024-12-08T12:34:12.998+08:00"}
---


磁盘管理里挂载为只读
powershell管理员
`Optimize-VHD -Path "D:\czc仓库盘\czc仓库盘(挂载f盘).vhdx" -Mode Full`
>[!note]- 网上的
>3.对NTFS文件，用Windows Server PowerShell里面的Optimize-VHD小命令（cmdlet），操作如下：a.先在磁盘管理工具里面“操作-附加VHD”，记得勾选“read-only”（必不可少）b.打开PowerShell，输入Optimize-VHD -Path C:\YourVHDX.vhdx -Mode Full。运行后很快就OK了，磁盘文件显著变小了。关于Optimize-VHD详细一点的说明可参考：https://docs.microsoft.com/zh-tw/powershell/module/hyper-v/optimize-vhd?view=win10-ps
>
>用这个命令需要先有hyper-v！！！！！！！！！！！！
>`Optimize-VHD -Path D:\Vdisk\sb\sb.vhdx -Mode Full`
