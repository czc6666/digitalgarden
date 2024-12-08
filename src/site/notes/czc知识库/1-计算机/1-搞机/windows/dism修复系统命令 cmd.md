---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/windows/dism修复系统命令 cmd/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.029+08:00","updated":"2024-12-08T12:34:12.939+08:00"}
---


```
Dism /Online /Cleanup-image /Scanhealth
Dism /Online /Cleanup-Image /CheckHealth
Dism /Online /Cleanup-image /Restorehealth
sfc /scannow


1>>查看映像版本：Dism /online /Get-CurrentEdition。
3、然后就是进行扫描映像，注意的是查看映像是否有损坏：Dism /Online /Cleanup-Image /ScanHealth
4、然后就是进行查看损坏程度：Dism /Online /Cleanup-Image /CheckHealth。
5、最后一步就是进行修复系统映像文件了就完成了。Dism /Online /Cleanup-image /Restorehealth
```