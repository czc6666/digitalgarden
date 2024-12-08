---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/windows/v1 老版/bat-自动启动某个目录下所有bat快捷方式/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.267+08:00","updated":"2024-12-08T12:34:13.012+08:00"}
---


> set "FolderToExecute=C:\czcVdisk\启动里的脚本会启动这里面的脚本\"
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
> for ~nf...
>     start "" "%%f"
> )

echo 所有快捷方式已启动
timeout /t 3 /nobreak >nul 2>&1