---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/windows/win11右键菜单默认显示更多选项，解决反人类 恢复传统右键的方法/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.072+08:00","updated":"2024-12-08T12:34:12.954+08:00"}
---


管理员cmd：
`reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve`
重启或者
重启资源管理器：`taskkill /f /im explorer.exe & start explorer.exe`





新找到的方法：[Windows 11 恢复传统右键的方法 - 玩客 (wker.com)](https://wker.com/windows-11-right-click/)





**1、临时恢复传统的右键菜单**

部分人喜欢新的样式，毕竟比较漂亮，部分选项要多点击一下才能出现，为了方便快捷，我们也可以在右击的时候按住 shift 键，这样就可以临时调出传统右键。

**2、永久恢复传统的右键菜单**

打开命令提示符（cmd），输入以下代码，然后重启电脑，就可以永久恢复到传统的右键菜单。

reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
