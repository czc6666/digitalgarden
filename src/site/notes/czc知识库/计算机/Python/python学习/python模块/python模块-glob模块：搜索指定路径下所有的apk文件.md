---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python学习/python模块/python模块-glob模块：搜索指定路径下所有的apk文件/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.914+08:00","updated":"2024-12-08T12:19:23.668+08:00"}
---


ChatGPT介绍glob模块：
> `glob` 是 Python 标准库中的一个模块，用于在文件系统中搜索匹配指定模式的文件路径。它提供了一个名为 `glob` 的函数，用于执行文件路径的模式匹配。
> 
> 具体来说，`glob.glob(pattern)` 函数接受一个字符串 `pattern` 作为参数，这个字符串是一个文件路径的模式，可以包含通配符 `*` 和 `**`。函数会根据这个模式在文件系统中搜索匹配的文件路径，并返回匹配到的文件路径列表。
> 
> 例如，`glob.glob('*.txt')` 会搜索当前目录下所有以 `.txt` 结尾的文件，并返回这些文件的路径列表；`glob.glob('**/*.txt', recursive=True)` 则会递归搜索当前目录及其所有子目录中的所有以 `.txt` 结尾的文件。
> 
> `glob` 模块通常用于文件查找、文件路径匹配等场景，非常方便用于处理文件系统中的大量文件。

自己遇到的实例：
```python
import glob
files = glob.glob(self._data_path + '/**/*.apk', recursive=True)  
n_files = len(files)
```
ChatGPT:
- `self._data_path` 是指定的数据路径，代码会在这个路径下搜索 APK 文件。
-  `'/**/*.apk'` 表示匹配任意深度的子目录（包括当前目录），并且文件名以 `.apk` 结尾。
	- `'/'`：斜杠表示从当前目录开始匹配。
	- `**`：双星号表示递归匹配任意深度的子目录，即匹配当前目录及其所有子目录。
		- 如果要限定只在二级目录下查找 APK 文件，可以使用类似这样的模式字符串：`'/*/*.apk'`。这样表示只匹配直接子目录（二级目录）下的 APK 文件。
	- `*.apk`：星号和点号组合表示匹配任意文件名以 `.apk` 结尾的文件。
- `recursive=True` 参数告诉 `glob` 函数递归搜索子目录。
因此，这行代码的意思是在指定的数据路径 `self._data_path` 及其所有子目录中查找所有的 APK 文件












