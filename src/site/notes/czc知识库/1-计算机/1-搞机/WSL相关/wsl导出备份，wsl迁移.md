---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/WSL相关/wsl导出备份，wsl迁移/","dgPassFrontmatter":true,"created":"2024-11-19T13:51:53.815+08:00","updated":"2024-12-08T12:34:13.051+08:00"}
---


输入 `wsl --shutdown` 使其停止运行，再次使用`wsl -l -v`确保其处于stopped状态。

在D盘创建一个目录用来存放新的WSL，比如我创建了一个 `D:\Ubuntu_WSL` 。

①导出它的备份（比如命名为Ubuntu.tar)

```text
wsl --export Ubuntu-22.04 D:\Ubuntu_WSL\Ubuntu.tar
wsl --export Ubuntu-22.04 G:\Ubuntu.tar
```



②确定在此目录下可以看见备份Ubuntu.tar文件之后，注销原有的wsl

```text
wsl --unregister Ubuntu-22.04
```

③将备份文件恢复到`D:\Ubuntu_WSL`中去

```text
wsl --import Ubuntu-22.04 D:\Ubuntu_WSL D:\Ubuntu_WSL\Ubuntu.tar
```

这时候启动WSL，发现好像已经恢复正常了，但是用户变成了root，之前使用过的文件也看不见了。

## **3.恢复默认用户**

在CMD中，输入 `Linux发行版名称 config --default-user 原本用户名`

例如：

```bash
Ubuntu2204 config --default-user cham
```

请注意，这里的发行版名称的版本号是纯数字，比如Ubuntu-22.04就是Ubuntu2204。

这时候再次打开WSL，你会发现一切都恢复正常了。