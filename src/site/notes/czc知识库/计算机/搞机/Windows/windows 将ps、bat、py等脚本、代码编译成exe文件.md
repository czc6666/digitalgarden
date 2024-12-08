---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Windows/windows 将ps、bat、py等脚本、代码编译成exe文件/","dgPassFrontmatter":true,"created":"2024-11-17T00:01:50.836+08:00","updated":"2024-12-08T12:34:12.957+08:00"}
---


# powershell脚本：`.ps1`文件
1. 以管理员身份打开` PowerShell`
2. 运行: `Install-Module ps2exe -Force`
3. 运行: `Invoke-ps2exe "route_config.ps1" "路由配置工具.exe"`


❗❗❗❗
如果需要编译出的exe文件执行许需要管理员权限可以用这条命令编译：

```bash
Invoke-ps2exe "route_config.ps1" "校园网通信限制破解.exe" -requireAdmin
```


[校园网AP隔离解决方案笔记-解决校园网设备无法互相通信的臭毛病-附破解程序](校园网AP隔离解决方案笔记-解决校园网设备无法互相通信的臭毛病-附破解程序.md)

# bat脚本

1. 按 Win+R，输入 iexpress
2. 选择 "Create new Self Extraction Directive file"
3. 点击 Next
4. 选择 "Extract files and run an installation command"
5. 填写包名称
6. 选择是否显示提示
7. 选择是否显示许可证
8. 添加你的 BAT 文件
9. 设置安装程序命令（通常是你的 BAT 文件名）
10. 选择显示模式
11. 完成设置并生成 EXE

# python程序（脚本）
这里简单说

用pyinstaller

```bash
# 1. 安装 PyInstaller
pip install pyinstaller

# 2. 基本打包命令
pyinstaller your_script.py

# 3. 常用的打包选项
pyinstaller --onefile --windowed --icon=your_icon.ico your_script.py
```

常用参数：

```bash
--onefile        # 打包成单个文件
--windowed       # 不显示控制台窗口
--icon=file.ico  # 添加图标
--name=NAME      # 指定输出文件名
--clean          # 清理临时文件
--add-data "src;dst"  # 添加额外文件
--hidden-import MODULENAME  # 添加隐藏的依赖
```