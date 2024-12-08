---
{"dg-publish":true,"permalink":"/czc知识库/计算机/搞机/linux/vim编辑器使用 linux/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.666+08:00","updated":"2024-12-08T11:42:05.973+08:00"}
---





```
i //编辑模式

:q  
//退出
:q! 
//退出且不保存（:quit!的缩写）
:wq
//保存并退出
:wq!
//保存并退出即使文件没有写入权限（强制保存退出）
:x
//保存并退出（类似:wq，但是只有在有更改的情况下才保存）
:exit
//保存并退出（和:x相同）
:qa
//退出所有(:quitall的缩写)
:cq
//退出且不保存（即便有错误）

```

[vim命令大全 - 知乎](https://zhuanlan.zhihu.com/p/61515833)