---
{"dg-publish":true,"permalink":"/czc知识库/笔记/个人知识库构建/子文件夹/dataview插件教程笔记/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:22.369+08:00","updated":"2024-12-08T11:30:31.032+08:00"}
---



# 自己使用的dataview代码

````text

{ .block-language-dataview}
````

```text
| name | 标签 | 创建日期 |
| ---- | -- | ---- |

{ .block-language-dataview}

未完成任务汇总
```

{ .block-language-dataview}
可用在同一个文件内汇总完成和未完成任务
例如我自己写的：
[长期任务](长期任务.md)、[日程模板](日程模板.md)

# obsidian插件教程网站
[Obsidian 插件之 Dataview - 知乎](https://zhuanlan.zhihu.com/p/373623264)
[obsidian插件之dataview入门 - 知乎](https://zhuanlan.zhihu.com/p/409253101)
[Obsidian DataView 入门保姆级引导手册 - 知乎](https://zhuanlan.zhihu.com/p/614881764)
高阶玩法啊： [玩转 Obsidian 08：利用 Dataview 打造自动化 HomePage - 少数派](https://client.sspai.com/post/73958#!)
## 常用名字

|  |  |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- | ---- |
| file.name | Text | 文件名 |  |  |  |
| file.folder | Text | 所在文件夹 |  |  |  |
| file.path | Text | 完整路径 + 完整文件名 |  |  |  |
| file.ext | Text | 扩展名 |  |  |  |
| file.link | Link | 链接至本文件 |  |  |  |
| file.size | Number | 文件大小 (bytes) |  |  |  |
| file.ctime | Date Time | 创建时间 |  |  |  |
| file.cday | Date | 创建日期 |  |  |  |
| file.mtime | Date Time | 最后修改时间 |  |  |  |
| file.mday | Date | 最后修改日期 |  |  |  |
| file.tags | List | 文中的 \#标签 和 YAML 中的 tags |  |  |  |
| file.etags | List | 文中的 \#标签 和 YAML 中的 tags |  |  |  |
| file.inlinks | List | 反向链接 |  |  |  |
| file.outlinks | List | 正向链接 |  |  |  |
| file.tasks | List | 文中的任务列表 |  |  |  |
| file.lists | List | 文中的列表 (包含任务列表) |  |  |  |
| file.frontmatter | List | 文件中的 YAML 块内容 |  |  |  |
| file.starred | Boolean | 加星 |  |  |  |

