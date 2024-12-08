---
{"dg-publish":true,"permalink":"/czc知识库/笔记/85-做笔记笔记/1-obsidian笔记/css代码片段 自定义obsidian snippets插件/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:22.312+08:00","updated":"2024-12-08T11:23:05.270+08:00"}
---



border主题中文件列表行间距，我想调小，gpt给我了个方法：css文件放进snippets文件夹，在obsidian中启用这个css文件
```css
/* 调整文件列表项的上下间距 */
.nav-file-title {
    margin-top: -10px; /* 上间距 */
    margin-bottom: -1px; /* 下间距==调这个好像没用== */
}

/* 调整文件夹列表项的上下间距 */
.nav-folder-title {
    margin-top: -8px; /* 上间距 */
    margin-bottom: 1px; /* 下间距==调这个好像没用== */
}
```