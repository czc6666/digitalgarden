---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/windows/v1 老版/bat-自动挂载bitlocker虚拟磁盘后自动解锁（命令行内输密码）脚本.txt/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.278+08:00","updated":"2024-12-08T12:34:13.015+08:00"}
---


NET FILE 1>NUL 2>NUL
if '%errorlevel%' == '0' (
    echo Administrator rights confirmed.
) else (
    echo Requesting administrator rights...
    powershell Start-Process -FilePath "%0" -Verb RunAs
    exit /b
)




@echo off
set DiskFile=czchd.vhdx
set DiskLabel=czc的小新pro14

:: 创建一个包含diskpart命令的临时脚本文件
echo select vdisk file="%~dp0%DiskFile%" > temp_diskpart_script.txt
echo attach vdisk >> temp_diskpart_script.txt

:: 运行diskpart来执行临时脚本
diskpart /s temp_diskpart_script.txt

:: 删除临时脚本文件
del temp_diskpart_script.txt

echo czc的牛逼磁盘已挂载到 %DiskLabel%

:: 输入 BitLocker 密码
echo 输入czc专用密码解锁这个隐藏在czcbook里的秘密磁盘
manage-bde -unlock X: -password

:: 打开磁盘
start X:\

:: 等待用户按下任意键
echo 按任意键拔掉这个非常非常非常牛逼的磁盘
pause

:: 卸载（弹出）虚拟磁盘
echo 卸载虚拟磁盘 %DiskLabel%
echo select vdisk file="%~dp0%DiskFile%" > temp_diskpart_script.txt
echo detach vdisk >> temp_diskpart_script.txt
diskpart /s temp_diskpart_script.txt
del temp_diskpart_script.txt

echo 虚拟磁盘已从 %DiskLabel% 已卸载