---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/机器学习相关 坤器学习/TF-IDF：一种用于信息检索与数据挖掘的常用加权技术/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:20.735+08:00","updated":"2024-12-08T12:25:39.531+08:00"}
---


terms frequency-inverse doc-ument frequency

网上随便找的两个教程：
[机器学习：生动理解TF-IDF算法 - 知乎](https://zhuanlan.zhihu.com/p/31197209)
[用通俗易懂的方式讲解：TF-IDF算法介绍及实现 - 知乎](https://zhuanlan.zhihu.com/p/592645536)


[tf-idf - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/Tf-idf)

**tf-idf**（英语：**t**erm **f**requency–**i**nverse **d**ocument **f**requency）是一种用于[信息检索](https://zh.wikipedia.org/wiki/%E8%B3%87%E8%A8%8A%E6%AA%A2%E7%B4%A2 "信息检索")与[文本挖掘](https://zh.wikipedia.org/wiki/%E6%96%87%E6%9C%AC%E6%8C%96%E6%8E%98 "文本挖掘")的常用加权技术。tf-idf是一种统计方法，用以评估一字词对于一个文件集或一个[语料库](https://zh.wikipedia.org/wiki/%E8%AA%9E%E6%96%99%E5%BA%AB "语料库")中的其中一份[文件](https://zh.wikipedia.org/wiki/%E6%96%87%E4%BB%B6 "文件")的重要程度。字词的重要性随着它在文件中出现的次数成[正比](https://zh.wikipedia.org/wiki/%E6%AD%A3%E6%AF%94 "正比")增加，但同时会随着它在语料库中出现的频率成反比下降。tf-idf加权的各种形式常被[搜索引擎](https://zh.wikipedia.org/wiki/%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E "搜索引擎")应用，作为文件与用户查询之间相关程度的度量或评级。除了tf-idf以外，互联网上的搜索引擎还会使用基于链接分析的评级方法，以确定文件在搜索结果中出现的顺序。

[GCNs论文用到这个方法：](202305.13.GCNs_AMD：基于%20GCN%20增强函数调用图中节点特征差异的%20Android%20恶意软件检测方法%20An%20Android%20Malware%20Detection%20Approach%20to%20Enhance%20Node%20Feature%20Differences%20in%20a%20Function%20Call%20Graph%20Based%20on%20GCNs.md#^f2fe9b)

GAT_AMD也用了（结合LSO）


tf-idf是一种统计方法，用以评估一字词对于一个文件集或
一个语料库中的其中一份文件的重要程度。它是一种用于
信息检索与文本挖掘的常用加权技术。