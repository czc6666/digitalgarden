---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/windows/bat脚本类/bat脚本笔记/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.224+08:00","updated":"2024-12-08T12:34:13.006+08:00"}
---


>[!quote]- 代码
> ```
> 
> ```
## 开机自动启动某exe文件，以管理员权限
>[!quote]- 代码
> ```
> NET FILE 1>NUL 2>NUL
> if '%errorlevel%' == '0' (
>     echo Administrator rights confirmed.
> ) else (
>     echo Requesting administrator rights...
>     powershell Start-Process -FilePath "%0" -Verb RunAs
>     exit /b
> )
> 
> 
> 
> :: 直接运行PixPin.exe文件
> start "" "C:\Program Files (x86)\PixPin\PixPin.exe"
> ```
## 重启资源管理器
>[!quote]- 代码
> ```
> @echo off
taskkill /f /im explorer.exe
start explorer.exe
> ```
## 自动挂载bitlocker虚拟磁盘后自动解锁（命令行内输密码）脚本
>[!quote]- 代码
> ```
> NET FILE 1>NUL 2>NUL
> if '%errorlevel%' == '0' (
>     echo Administrator rights confirmed.
> ) else (
>     echo Requesting administrator rights...
>     powershell Start-Process -FilePath "%0" -Verb RunAs
>     exit /b
> )
>
>@echo off
set DiskFile=czchd.vhdx
set DiskLabel=czc的小新pro14
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
> echo czc的牛逼磁盘已挂载到 %DiskLabel%
> 
> :: 输入 BitLocker 密码
> echo 输入czc专用密码解锁这个隐藏在czcbook里的秘密磁盘
> manage-bde -unlock X: -password
> 
> :: 打开磁盘
> start X:\
> 
> :: 等待用户按下任意键
> echo 按任意键拔掉这个非常非常非常牛逼的磁盘
> pause
> 
> :: 卸载（弹出）虚拟磁盘
> echo 卸载虚拟磁盘 %DiskLabel%
> echo select vdisk file="%~dp0%DiskFile%" > temp_diskpart_script.txt
> echo detach vdisk >> temp_diskpart_script.txt
> diskpart /s temp_diskpart_script.txt
> del temp_diskpart_script.txt
> 
> echo 虚拟磁盘已从 %DiskLabel% 已卸载
> ```

## 自动启动某个目录下所有bat快捷方式
>[!quote]- 代码
> ```
>set "FolderToExecute=C:\czcVdisk\启动里的脚本会启动这里面的脚本\"
> 
> :: 检查指定文件夹是否存在
> if not exist "%FolderToExecute%" (
>     echo 文件夹不存在: "%FolderToExecute%"
>     pause
>     exit /b
> )
> 
> :: 进入指定文件夹
> cd /d "%FolderToExecute%"
> 
> :: 循环遍历文件夹内的所有快捷方式
> for %%f in (*.lnk) do (
>     echo 启动 %%~nf...
>     start "" "a in ('date /t') do (
>     set "currentDate=%%c-%%a-%%b"
> )
> 
> for /f "tokens=1-2 delims=: " %%a in ('time /t') do (
>     set "currentTime=%%a%%b"
> )
> 
> REM 构造目标文件夹名称
> set "targetFolder=%targetDir%\czc知识库_%currentDate%_%currentTime%"
> 
> REM 创建目标文件夹
> mkdir "%targetFolder%"
> 
> REM 复制文件
> xcopy "%sourceDir%\*" "%targetFolder%\" /E /Y
> 
> echo 复制完成！
> 
> REM 删除超过3天的备份
> forfiles /p "%targetDir%" /m czc知识库_* /d -3 /c "cmd /c if @isdir==TRUE rd /S /Q @file"
> 
> echo 删除超过7天的备份完成！
> 
> REM 设置倒计时3秒 
> timeout /t 3 
> exit
> ```

## vhdx 虚拟磁盘 压缩，记得修改磁盘文件名字
>[!quote]- 代码
> ```bat
> echo 提权ing
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
> echo 提权完成emmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm
> ::↑提权
> 
> 
> set DiskFile=sb.vhdx
> set DiskLabel=czc的牛逼盘
> 
> :: 创建一个包含diskpart命令的临时脚本文件
> echo select vdisk file="%~dp0%DiskFile%" > temp_diskpart_script.txt
> echo attach vdisk readonly >> temp_diskpart_script.txt
> 
> :: 运行diskpart来执行临时脚本
> diskpart /s temp_diskpart_script.txt
> 
> :: 删除临时脚本文件
> del temp_diskpart_script.txt
> 
> echo 磁盘已挂载（只读）到 %DiskLabel%
> 
> :: 创建 PowerShell 脚本文件
> echo Optimize-VHD -Path "%~dp0%DiskFile%" -Mode Full > OptimizeVHD.ps1
> 
> :: 运行 PowerShell 脚本
> powershell -ExecutionPolicy Bypass -File OptimizeVHD.ps1
> 
> :: 删除 PowerShell 脚本文件
> del OptimizeVHD.ps1
> 
> :: 卸载（弹出）虚拟磁盘
> echo 卸载虚拟磁盘 %DiskLabel%
> echo select vdisk file="%~dp0%DiskFile%" > temp_diskpart_script.txt
> echo detach vdisk >> temp_diskpart_script.txt
> diskpart /s temp_diskpart_script.txt
> del temp_diskpart_script.txt
> 
> echo 虚拟磁盘 %DiskLabel% 已成功压缩回收空间并卸载
> 
> ```
> 
> 





