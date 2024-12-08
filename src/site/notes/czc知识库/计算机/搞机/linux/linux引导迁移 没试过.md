---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/linux/linux引导迁移 没试过/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.008+08:00","updated":"2024-12-08T11:41:58.146+08:00"}
---



来源：[【万字详细教程】Linux to go——装在移动硬盘里的Linux系统（Ubuntu22.04）制作流程；一口气解决系统安装/引导文件迁移/显卡驱动安装等问题-CSDN博客](https://blog.csdn.net/m0_64545111/article/details/136131918)



> 将系统启动引导程序迁移到移动硬盘上
> 现在我们切换回Windows系统，使用Disk Genius查看移动硬盘的ESP区（注意到硬盘上的一些分区是无法像C盘、D盘这样直接被电脑的文件管理器访问的，需要为它们设置卷标，还必须有管理员权限，才能在文件管理器中进行访问和更改；这里推荐直接在Disk Genius中进行操作，即点击左侧目录即可直接访问和更改），发现其仍然是空的，没有我们的系统启动引导程序；实际上系统启动引导程序会被默认安装到主硬盘上：
> 
> 
> 
> 如果你不想每次开机都要选择一个系统（即使你没插上移动硬盘），不想让Linux to go对你原来的Windows系统产生影响；又如果你还想让Linux to go在不同的电脑上都能工作，那么就要考虑将系统的启动引导程序迁移到到移动硬盘上。
> 
> 这一步有使用boot-repair工具和手动迁移两种方法，我两种都尝试过，只有前者成功，并且前者也更加容易实现；这里就介绍第一种方法。
> 
> 再把一开始的启动U盘和移动硬盘都插到电脑上，开机重启，按下F12进入启动项选择界面，此时应该能看到一个ubuntu和一个linpus lite，前者就是我们刚安装好的ubuntu系统，后者则还是原来引导ubuntu安装的程序。选择linpus lite，进入安装界面，但这次选择“试用Ubuntu”。
> 
> 
> 
> 进入Ubuntu系统后，连接网络，打开终端输入下面的指令安装boot-repair软件：
> 
> sudo apt-add-repository ppa:yannubuntu/boot-repair
> sudo apt update
> sudo apt install boot-repair
> 1
> 2
> 3
> 安装完成后，输入命令运行该软件：
> 
> boot-repair
> 1
> 选择“Recommended repair”，等待程序运行完成即可。
> 
> 将系统启动引导程序成功迁移到移动硬盘后，可以通过DiskGenius软件在移动硬盘的ESP分区下看到如下的目录结构：
> 
> 此时就可以在Disk Genius中将主硬盘中对应的与ubuntu相关的系统引导启动程序文件删除，这样每次启动电脑，只有在插入移动硬盘时才能看到Ubuntu系统的启动项，在不插入移动硬盘时，电脑上就只有Windows一个启动项可以选择（不考虑其他特殊启动项）。
> 
> 至此，基本大功告成！不过需要说明的是Linux to go对电脑上原来的Windows系统也并不是完全没影响，在我的电脑上，每次使用完Ubuntu系统再切换回Windows系统，系统时间都会错乱，需要到系统中手动校准时间。
> ————————————————
>                             版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
> 
> 原文链接：https://blog.csdn.net/m0_64545111/article/details/136131918
