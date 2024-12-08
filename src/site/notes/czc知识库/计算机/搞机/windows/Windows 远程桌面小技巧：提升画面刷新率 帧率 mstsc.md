---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/windows/Windows 远程桌面小技巧：提升画面刷新率 帧率 mstsc/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.083+08:00","updated":"2024-12-08T12:34:12.961+08:00"}
---


# [Windows 远程桌面小技巧：提升画面刷新率 - 玩客](https://wker.com/windows-rdp-refresh-rate/)


[Windows](https://wker.com/tag/windows/) 远程桌面默认的刷新率是 30 Hz，我们可以设置为 60 Hz，享受一下高刷新率，当然实际的效果取决于网络环境和客户端的设置，如果是局域网内，那效果应该还不错。

**提升 Windows 远程桌面帧率的办法：**

1、打开远程主机上的注册表编辑器（运行–>regedit），找到 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations` ，然后  
在空白处右击–>新建–>DWORD（32位）值，命名为 `DWMFRAMEINTERVAL`。

2、双击 DWMFRAMEINTERVAL，基数选择为十进制，数值数据填写 `15`。