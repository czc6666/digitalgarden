---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/windows/v1 老版/bat脚本-bat提权代码汇总 管理员权限.txt/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.297+08:00","updated":"2024-12-08T12:34:13.022+08:00"}
---


> 为何不试试买笔记本送的驱动文件夹里的setup.cmd里的提权代码呢？
> 
> ---
> 
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
> ```
> 
> ---
> =======================================
> 
> ```
> @echo off
> :: Check if the script is already running with admin rights
>nul 2>&1 "%SYSTEMROOT%\System32\cacls.exe" "%SYSTEMROOT%\System32\config\system"
> 
> :: If the errorlevel is 0, then the script is running as administrator
> if %errorlevel% == 0 (
>     echo Script is running with administrator rights.
> ) else (
>     echo Script is not running with administrator rights.
>     echo Requesting administrator rights...
> 
>     :: The following line will prompt the UAC (User Account Control) dialog for admin privileges
>     :: This line will cause the script to restart with admin rights
>     powershell -command "Start-Process '%0' -Verb RunAs"
>     exit
> )
> ```
> 
> ---


> [!note] ===================================
> ```
> @echo off
> NET FILE 1>NUL 2>NUL
> if '%errorlevel%' == '0' (
>     echo Administrator rights confirmed.
> ) else (
>     echo Requesting administrator rights...
>     powershell Start-Process -FilePath "%0" -Verb RunAs
>     exit /b
> )
> ```


