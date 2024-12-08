---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/windows/v1 老版/bat脚本-开机自动挂载虚拟磁盘方法.txt/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.306+08:00","updated":"2024-12-08T12:34:13.025+08:00"}
---


> ```
> @echo off
> :: BatchGotAdmin
> ::-------------------------------------
> REM  --> Check for permissions
>nul 2>&1 "%SYSTEMROOT%\system32\cacls.exe" "%SYSTEMROOT%\system32\config\system"
> 
> REM --> If error flag set, we do not have admin.
> if '%errorlevel%' NEQ '0' (
>     echo Requesting administrative privileges...
>     goto UACPrompt
> ) else ( goto gotAdmin )
> 
> :UACPrompt
>     echo Set UAC = CreateObject^("Shell.Application"^) > "%temp%\getadmin.vbs"
>     echo UAC.ShellExecute "%~s0", "", "", "runas", 1 >> "%temp%\getadmin.vbs"
>     "%temp%\getadmin.vbs"
>     exit /B
> 
> :gotAdmin
>     if exist "%temp%\getadmin.vbs" ( del "%temp%\getadmin.vbs" )
>     pushd "%CD%"
>     CD /D "%~dp0"
> 
> ::以上是提权代码，不用以管理员权限运行也可以提权到管理员权限
> 
> 
> 
> @echo off
> set DiskFile=czchd.vhdx
> set DiskLabel=MyVirtualDisk
> 
> :: 创建一个包含diskpart命令的临时脚本文件
> echo select vdisk file="%~dp0%DiskFile%" > temp_diskpart_script.txt
> echo attach vdisk >> temp_diskpart_script.txt
> 
> :: 运行diskpart来执行临时脚本
> diskpart /s temp_diskpart_script.txt
> 
> :: 删除临时脚本文件
> del temp_diskpart_script.txt
> 
> echo 磁盘已挂载到 %DiskLabel%
> 
> :: 等待用户按下任意键
> pause
> 
> 
> :: 卸载（弹出）虚拟磁盘
> echo 卸载虚拟磁盘 %DiskLabel%
> echo select vdisk file="%~dp0%DiskFile%" > temp_diskpart_script.txt
> echo detach vdisk >> temp_diskpart_script.txt
> diskpart /s temp_diskpart_script.txt
> del temp_diskpart_script.txt
> 
> echo 虚拟磁盘 %DiskLabel% 已卸载
> ```
