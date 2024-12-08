---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Windows/powershell设置端口转发/","dgPassFrontmatter":true,"created":"2024-10-13T16:19:22.626+08:00","updated":"2024-12-08T12:34:12.941+08:00"}
---



`netsh interface portproxy add v4tov4 listenport=2222 listenaddress=0.0.0.0 connectport=22 connectaddress=172.28.140.245`





增加转发的命令：

```cobol
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=22 connectaddress=127.0.0.1 connectport=22
```

删除转发的命令：

```cobol
netsh interface portproxy delete v4tov4 listenport=22 listenaddress=0.0.0.0
```

使用以下命令列出当前的端口转发规则：

```kotlin
netsh interface portproxy show all
```

测试连接的命令：

```typescript
ssh username@ip -p 22
```

