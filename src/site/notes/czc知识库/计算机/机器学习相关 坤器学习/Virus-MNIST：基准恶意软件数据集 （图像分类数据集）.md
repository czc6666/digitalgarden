---
{"dg-publish":true,"permalink":"/czc知识库/计算机/机器学习相关 坤器学习/Virus-MNIST：基准恶意软件数据集 （图像分类数据集）/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:21.155+08:00","updated":"2024-12-08T12:21:39.541+08:00"}
---


简短的说明介绍了一个图像分类数据集，该数据集由 10 个可执行代码变体和大约 50,000 个病毒示例组成。恶意类包括 9 个计算机病毒家族和一个良性病毒集。可移植可执行文件 （PE） 的前 1024 个字节的图像格式反映了熟悉的 MNIST 手写数据集，因此之前探索的大多数算法方法只需稍作修改即可传输。恶意软件的 9 个病毒家族的指定源于对类标签的无监督学习;我们发现具有 KMean 聚类的家族，这些集群排除了非恶意示例。作为使用深度学习方法（MobileNetV2）的基准测试，我们发现，当包含beneware时，家庭病毒识别的总体准确率为80%。我们还发现，一旦发生阳性恶意软件检测（通过签名或启发式），将前 1024 个字节投影到缩略图中可以以 87% 的准确率对病毒类型进行分类。这项工作概括了其他恶意软件调查人员所证明的有前途的卷积神经网络，这些神经网络最初是为了解决图像问题而开发的，但应用于可执行文件中以像素字节为单位的新抽象域。该数据集可在 Kaggle 和 Github 上找到。

[Virus-MNIST: A Benchmark Malware Dataset | Papers With Code](https://paperswithcode.com/paper/virus-mnist-a-benchmark-malware-dataset)

数据集论文原文pdf：everything搜：
`VIRUS-MNIST_Noever_Noever.pdf`