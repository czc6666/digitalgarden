---
{"dg-publish":true,"permalink":"/czc知识库/计算机/Python/python笔记/python windows反斜杠的问题/","dgPassFrontmatter":true,"created":"2024-12-07T08:39:46.889+08:00","updated":"2024-12-08T12:19:23.655+08:00"}
---




> [!NOTE]+ 路劲反斜杠被当作转义字符
> 这个错误是因为Python中的字符串转义问题导致的。在Windows路径中，反斜杠`\`是转义字符，而在Python中，字符串中的反斜杠也会被解释为转义字符。因此，如果想要在字符串中表示一个反斜杠，需要使用两个反斜杠`\\`来表示。
> 
> 在你的代码中，路径中的反斜杠没有被正确处理，导致了Unicode编码错误。要解决这个问题，可以将路径中的单个反斜杠改为双反斜杠，或者使用原始字符串表示法（在字符串前面加上`r`）来避免转义字符的影响。
> 例如，将这行代码：
> ```python
> with open('C:\a\first_test\Drebin_Dictionary.pkl', 'rb') as f:
> ```
> 修改为
> ```python
> with open(r'C:\a\first_test\Drebin_Dictionary.pkl', 'rb') as f:
> ```
> 或者
> ```python
> with open('C:\\a\\first_test\\Drebin_Dictionary.pkl', 'rb') as f:
> ```
> 自己总结：
> 项目文件中的相对路径可以直接用‘/’或‘\\’，pycharm会识别到正确路径
> 绝对路径部分就会是被成转义字符
> ```python
> with open('../first_test/Drebin_Dictionary.pkl', 'rb') as f:
> ```


