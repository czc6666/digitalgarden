---
{"dg-publish":true,"permalink":"/czc知识库/笔记/85-做笔记笔记/1-obsidian笔记/obsidian插件/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:22.321+08:00","updated":"2024-12-08T17:15:03.070+08:00"}
---


#obsidian插件
# 自动添加路标插件 waypoint 
- 生成一个文件夹的目录树（实时更新）在一个文件中
- [自动添加路标 Waypoint ｜ Obsidian神插件\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1zb421H71s)
- 在文件夹下同名文件中**手敲**     \%\% Waypoint \%\%    然后就能自动生成实时更新的目录树
- 不能在知识库的根目录搞这个

# 远程多端同步插件
- remotely-save

# 热力图插件（基于dataview）：
- Contribution Graph
# 实用小部件插件（基于dataview）：
- Contribution Widget

# 未分类插件列表：
- Paste image rename：自动重命名拖进来的图片
- clear unused images：清除笔记中不再使用的图像以节省空间
- quiet outline：更丰富的大纲，目录
- kanban：添加看板。例如3个: to do; doing; done
- mind map：目录自动生成思维导图
- commander：在任何你想要的地方位置添加命令按钮
- File Explorer Note Count：统计文件夹下的文件数量
- editing toolbar：添加文本编辑功能（类OneNote，会卡用下面的这个轻量级的编辑插件）
- cmenu：轻量级文本编辑（不会用）
- Icon Folder(iconize)：给文件夹换图标（自己在设置里下载图标）
- File Color：给文件夹上颜色（需要自己在设置里添加颜色）
- surfing：直接在obsidian里打开网页链接当浏览器用
- Obsidian42 - BRAT：Easily install a beta version of a plugin for testing. 装未发布的插件
- Bartender：允许重新排列状态栏和侧边栏中的元素，[Bartender插件+BRAT插件——实现Obsidian目录文件手动排序](https://blog.csdn.net/m0_72265583/article/details/132005345)
- **dataview**：[dataview教程](dataview插件教程笔记.md)，最大的好处是自动更新，减少手动改的麻烦，数据库查询语法，难

- Day Planner：使用增强的时间块功能，从Markdown笔记中的任务列表中规划一天。（精确每小时安排，用不上，不用）
- style setting：设置当前主题的参数，标题颜色等等。（编辑主题的css文件）
- **banners**：开头**自定义图片页面背景**（原理也是特殊语法写在页面前面，可能和其他头语法产生冲突（实测没有冲突，现在的ob会把头语法（yaml）显示成可视化的属性，编辑模式下看不了，切换阅读模式可以看图））（卡的乱七八糟，不用了他妈的）
	- [PKMer\_Obsidian 插件：Obsidian Banners 为你的笔记添加头图](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/obsidian-banners/)
	- 
- Multi-Column Markdown：分栏，命令搜column插入就行（可配合dataview实现数据分栏可视化）
- Tag Wrangler：快速管理obsidian标签，[Tag Wrangler——快速管理 Obsidian 标签 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/587111398)
- heat：日常活跃热力图，还没装，要写代码 **垃坤**
- 3d graph：3d显示关系图谱，很炫？

- pandoc：很强大的导出工具？我试试看，（要提前安装pandoc软件）配置方法：[在Obsidian中实现 Pandoc Plugin 的插件配置 - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/9626)，，狗屁，不能导出pdf？？？我直接卸载
- callout manager：自定义callout样式和看现有样式，无脑方便不敲代码（有问题）

- DB Folder：辅助dataview，给文件批量添加属性

- Contribution Graph：真正能用的**热力图**，Generate a interactive heatmap graph to visualize and track your productivity

# 遇到问题去的解决方案插件

- Update Relative Links：
{ #05e012}

	- 移动文件的时候更新文件里的链接，重新按照相对路径写一遍链接
	- ctrl+p：Update all relative links：刷新所有文件的链接
- Consistent attachments and links：（没试过）
	- 自动移动笔记附件并更新链接
{ #043752}

- advanced URI：给每个文件附加一个唯一的UID，用这个来管理每个文件（创建文件链接代替obsidian原本的文件链接，原本的文件链接在文件数量很大以后修改文件，相关文件里的链接可能不会跟着修改）



- （废）obsidian-proxy-github-master：解决每次需要梯子才能访问商店的问题，obsidian网络代理，傻逼垃圾，**只支持0.14版本以前**