---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/linux/杂/linux 修改屏幕分辨率 自定义/","dgPassFrontmatter":true,"created":"2024-07-23T16:20:14.150+08:00","updated":"2024-12-08T11:39:54.020+08:00"}
---



[Linux操作系统修改屏幕分辨率方法--centos、ubuntu等均适用\_centos failed to get size of gamma for output defa-CSDN博客](https://blog.csdn.net/weixin_42092278/article/details/83869114)

```
xrandr

xrandr --newmode "1920x1080_60.00" 173.00 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync

xrandr --addmode VGA-1 "1920x1080_60.00"

xrandr -s <分辨率序号>
```

