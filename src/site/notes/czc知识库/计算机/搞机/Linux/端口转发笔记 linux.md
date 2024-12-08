---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/Linux/端口转发笔记 linux/","dgPassFrontmatter":true,"created":"2024-11-05T17:46:15.091+08:00","updated":"2024-12-08T11:41:18.583+08:00"}
---



> [!NOTE] gpt4turbo对话记录
> 在windows中配置端口转发用这个目录：  
> netsh interface portproxy add v4tov4 listenaddress=192.168.137.3 listenport=2205 connectaddress=192.168.137.5 connectport=2205  
> 那么在linux中如何配置端口转发呢？  
> 一般来说时windows做软路由同时配置各种端口转发规则容易高效还是linux更合适？
> 
> 在Linux中配置端口转发，你可以使用iptables命令来实现。以下是一个基本的示例，用于设置类似于你在Windows中提到的端口转发规则：
> ```
> sudo iptables -t nat -A PREROUTING -p tcp --dport 2205 -j DNAT --to-destination 192.168.137.5:2205
> sudo iptables -t nat -A POSTROUTING -p tcp -d 192.168.137.5 --dport 2205 -j MASQUERADE
> ```
> 这里的命令做了两件事：
> 
> 1. -A PREROUTING 将所有目标端口为2205的TCP流量重定向到192.168.137.5的2205端口。
> 
> 2. -A POSTROUTING 确保从192.168.137.5发出的数据包看起来像是从原始的Linux服务器发出的，这是通过伪装（MASQUERADE）完成的。
> 
> 关于Windows和Linux哪个更适合作为软路由并配置端口转发，这主要取决于你的具体需求和环境：
> 
> - Linux 通常被认为在网络服务和路由方面更加灵活和强大。它支持广泛的网络工具和自定义脚本，适合需要高度定制的环境。
> 
> - Windows 的配置可能更加直观，特别是对于那些习惯于图形用户界面的用户。但是，它可能不如Linux那样灵活，特别是在高级网络功能和自动化方面。
> 
> 如果你需要高度可定制的解决方案，或者是在寻找一个能够支持复杂网络配置的系统，Linux可能是更好的选择。如果你寻求易用性并且环境主要是Windows，那么使用Windows也是合理的选择。


配置笔记

由于ip中包含137，win的局域网其他设备访问会出问题，czc-pc局域网内只能ssh到wzd-1服务器，所以我在wzd-1服务器中配置端口转发

sudo iptables -t nat -A PREROUTING -p tcp --dport 2205 -j DNAT --to-destination 192.168.137.5:2205
sudo iptables -t nat -A POSTROUTING -p tcp -d 192.168.137.5 --dport 2205 -j MASQUERADE

！！！
不对，这样还是没有用！！！

看来要指定访问端口也不行，那我只有在软路由上开ssh服务器，中转访问.5
这样可以，用wzd-0做ssh中转