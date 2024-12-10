---
{"dg-publish":true,"permalink":"/czc知识库/计算机/坤器学习/GNN 图神经网络/","dgPassFrontmatter":true,"created":"2024-06-24T12:21:09.792+08:00","updated":"2024-12-08T17:30:09.471+08:00"}
---



学习网站：
-[深度学习学习网站 信息](深度学习学习网站%20信息.md))
- [不愧是公认最好的【图神经网络GNN/GCN教程】，从基础到进阶再到实战，一个合集全部到位！-人工智能/神经网络/图神经网络/深度学习。\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1184y1x71H)

# 应用领域
- 最大层面，芯片设计
- 场景分析、问题推理
- 系统推荐相关（个性化推荐）
- 欺诈检查、风控相关
- 知识图谱
- 道路交通，动态流量预测（竞赛热门）
- 自动驾驶，无人机等场景
- 化学，医疗领域（未来趋势方向）
- 物理模型相关：新能源电池设计，ai自动找分子组合方案做实验

图的基本组成
- **V** 顶点 Vertex (or node) attributes
- **E** Edge (or link) attributes and directions
- **U** Global (or master node) attributes

图神经网络要做啥：无论事整的多么复杂，我们利用图神经网络的目的就是整合特征（整合点的、边的和全局的特征，全面）
- Vertex (or node) embedding
- Edge (or link) attributes and embedding
- Global (or master node) embedding

embedding：词嵌入

图的邻接矩阵
邻接矩阵：描述节点的邻居有哪一些
无向图的邻接矩阵是对称的

为什么CV和NLP中应用GNN很少
- 传统NN模型输入**格式**固定，
- 因为图像和文本数据的**格式都贼固定**，想一想咱们的预处理
- 有图像resize成固定大小，然后进行卷积操作得到特征，**格式很固定**
- 文本固定长度和词向量大小，然后也是这么个事，**不需要特殊的邻接矩阵**

GNN，输入数据不规则，不同数据结构完全不同 
社交网络人物关系，这种邻接矩阵很庞大

GNN三种级别的人物：
点：Node与Edge级别任务
边：
图：Graph级别任务

邻接矩阵：一般邻接矩阵表达形式如下，并不是一个N\*N的矩阵，而是保存source,target

例如：
```
Nodes [0,1,1,0,0,1,1,1]
Edges [2,1,1,1,2,1,1]
Adjacency List [[1,0],[2,0],[4,3],[6,2],[7,3],[7,4],[7,5]]
Global 0
```