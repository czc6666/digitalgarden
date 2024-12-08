---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/windows/开关休眠功能 cmd命令/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.167+08:00","updated":"2024-12-08T12:34:12.986+08:00"}
---


除了通过操作系统的菜单来关闭休眠功能，我们还可以使用命令行工具禁用它。
以管理员身份打开命令提示符，输入
powercfg -h off
并按回车键，即可禁用休眠功能。如果想重新启用，只需输入
powercfg -h on
即可。