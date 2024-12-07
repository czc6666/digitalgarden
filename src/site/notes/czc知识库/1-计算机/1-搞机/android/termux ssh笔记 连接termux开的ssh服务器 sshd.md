---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/1-搞机/android/termux ssh笔记 连接termux开的ssh服务器 sshd/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.886+08:00","updated":"2024-12-08T00:39:16.422+08:00"}
---




pkg install openssh
`sshd`启动ssh服务器
`passwd`设置ssh服务器密码  :::123456
用电脑连接：ssh <ip> -p <端口号>
ssh 192.168.213.229 -p 8022

确认ssh服务的监听端口

```text
netstat -ntlp | grep sshd
```

开启ssh的指令是：

```text
sshd
sshd -p 9000
```


