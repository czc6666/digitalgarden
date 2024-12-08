---
{"dg-publish":true,"permalink":"/czc知识库/1-计算机/未分类/子中子/IoT 恶意软件进化谱系研究 1/","dgPassFrontmatter":true,"created":"2024-06-18T17:45:21.049+08:00","updated":"2024-12-08T12:27:44.667+08:00"}
---


[IoT 恶意软件进化谱系研究 ](https://mp.weixin.qq.com/s/xXYFcVOXA6lZfhign0BJlg)

Avenger [威胁棱镜](javascript:void(0);) *2021-09-09 09:00*

## 工作来源

IEEE Internet of Things Journal（March 2021）

## 工作背景

由于很多物联网恶意软件披露了源代码，这导致相关的变种快速增长，且这些变种在大多数情况下包含多个家族的特征，这给分类、标记、谱系分析和作者归属带来了挑战。（注：恶意软件谱系是指原始家族与其后代、版本或变种之间的家族演化关系。）

已有研究多针对特定 IoT 恶意软件展开，都忽略了每个家族的系统演化情况，导致对恶意软件发展趋势的分析不完整不是全局视野。研究需要挖掘家族之间的血缘关系，形成对恶意软件的家族归类和谱系推断的能力。

## 工作设计

系统整体架构如下所示：
![](/img/user/czc知识库/9-无奇不有/9-附件/附件/网安信息收集_image.png)

### 情报收集

BlackHat 的演讲（Iot malware: Comprehensive survey, analysis framework and case studies）中总结了至少 60 个 IoT 恶意软件家族，涵盖了 2012 年至 2018 年的主要家族。从这些家族名称的初始关键字列表开始。通过在 Google 上搜索初始关键词，得到了 10214 条相关结果作为初始文章库。

对于别名可以通过正则表达式捕获，这些匹配模式是通过从收集的文章中进行的大量手动分析工作总结出来的。这样总共收集到了 138 个家族别名（覆盖 72 个家族）。

![](/img/user/czc知识库/9-无奇不有/9-附件/附件/网安信息收集_image-1.png)

进一步使用这些家族别名和固定短语“IoT 恶意软件/僵尸网络”来搜索在线文章并抓取所有结果，包括安全报告、技术博客文章等。然后删除重复的和不相关的文章。最后，可使用 17857 篇 IoT 恶意软件相关文章进行分析。虽然定义的别名模式可能无法涵盖所有可能的用法，但由于收集的文章数量众多，这些模式足以收集常用的别名。

### 特征挖掘

恶意软件特征挖掘阶段包括两个任务：恶意软件行为提取和基于提取行为的特征工程。

#### 行为提取

首先获取每个家族的高频行为列表，用于后续的特征关联。恶意软件行为提取主要分两步提取：收集和行为加权。

使用斯坦福类型依赖解析器来分析每个句子的主要成分并提取行为。通过 WordNet 合并具有相似含义的相同词性的单词以减少单词变体。最后从 17857 篇文章中生成了 62424 个独特的行为。

![](/img/user/czc知识库/9-无奇不有/9-附件/附件/网安信息收集_image-2.png)

收集所有行为中的动词和名词，以预测单词和家族之间的语法关系。根据 FeatureSmith（Featuresmith: Automatically engineering features for malware detection by mining the security literature）的方法定义每个单词和家族之间的相关性分数。

选择 ATT&CK 中与 Linux 相关的战术阶段，并将提取的行为映射到特定的战术阶段，以便与可提取的特征进一步关联。根据统计分析，高权重行为在相应家族的在线文章中出现更为频繁。最终得到每个家族前 5400 种行为被映射为 7 种战术阶段，如下所示。

![](/img/user/czc知识库/9-无奇不有/9-附件/附件/网安信息收集_image-3.png)

#### 特征工程

特征工程是要将 5400 个行为映射到对应的特征上。前人研究证明可执行二进制文件中的文件元信息、段、系统调用和用户命令可以反映不同家族的行为特征。本工作也利用文件元数据、系统调用和库函数作为潜在的物联网恶意软件分类特征。

用作分类特征的文件元数据包括二进制文件大小、编译期间的安全选项（例如 Canary 和 NX）、操作环境（例如 OS、架构和 MMU（内存管理单元支持））和各种编译选项。共选择了 18 个可执行二进制文件的属性作为分类特征，如下所示。

![](/img/user/czc知识库/9-无奇不有/9-附件/附件/网安信息收集_image-4.png)

在基于 Linux 的系统下有两种操作的方式：系统调用和库函数。系统调用提供了操作系统和进程之间的接口，这是进入内核系统的唯一入口点。库函数作为应用程序编程接口用于应用程序开发。恶意行为可能与一个或多个特定的系统调用或库函数相关联。用系统调用和库函数来生成物联网恶意软件检测的潜在特征。总的来说，共有 7422 个库函数和 500 个系统调用。

要分三步将行为和特征关联起来，前五个特征如下所示：

![](/img/user/czc知识库/9-无奇不有/9-附件/附件/网安信息收集_image-5.png)

总共获得了 165 个系统调用和 1278 个库函数可用作特征，这些特征可以很容易地从可执行文件中提取出来。

### 家族谱系推断

与传统恶意软件相比，IoT 恶意软件家族进化速度更快，派生关系更加复杂，变种家族数量众多。

首先删除包含少于两个不同家族名称的句子，它们不太可能表达出可用的谱系相关信息。采用简单的 SVM 模型来区分出包含谱系关系表达的句子。选择 SVM 是因为在数据量较小时相比其他同类算法决策树、KNN 等具有更好的分类准确率，并且训练更加轻量级。

谱系关系表达的词汇是 “new”、“same”、“evolution”、“likely”、“common”、“offspring”、“later”、“derived”、“variant”、“beyond”、“faster”、“similar”、“merge”、“followed”、“like”、“from”、“version”、“fusion”。

提取出 9002 句与谱系关系有关的句子，使用别名库合并过滤。最后有 280 个句子可以表示恶意样本的谱系关系。

### 分类模型

集成学习使用多种基本学习算法（又名弱模型）来获得比任何弱模型更好的分类性能。弱模型的设计如下所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwokjPe6xdool2RjIibibiaWMQFicVyvc8q5mIDoongwg1qj67PWBDVrP1icg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在准确性和效率之间进行权衡考虑后，提出四种类型的弱模型：即 Double 模型、Simple 模型、Black-White 模型和 Total 模型。对收集的 23 个家族进行了模型训练，涉及的弱模型总数为 253 个。最终的检测结果由每个模型的线性加法加权投票决定。

进行 10 折交叉验证测试，选择 f-measure 作为集成模型的投票权重（注：f-measure 是 precision 和 recall 的调和平均值）。Black-White 模型首先用于检测给定样本是良性还是恶意。之后，其他弱模型同时进行进一步检测。异构弱模型针对不同特征的识别可以提高整个集成模型的鲁棒性，每一个绕过集成模型的意图都可能影响每个弱模型的输出，从而极大地增加攻击成本。

### 谱系分析

恶意软件谱系分析难以验证分析结果。让基于 NLP 的谱系分析和基于样本的分析得到的结果相互印证。

基于系统调用与恶意软件行为相关。恶意软件经过变种改进后，主要的恶意特征仍然保留。这一发现表明系统调用可以检测派生谱系。此外，即使是新的变种，其恶意意图也与原始变种相似。因此，可以通过系统调用有效地识别新的变体。

将每个特征作为词向量处理，得到每个家族排名靠前的频繁向量（也可称为频繁串）。为了计算每个家族的谱系纯度，定义了七个变量。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwavSA93KQYXdr803Ugic2ynhQq2l74by6NPYYYCia4tZhCU4xIqGSicDTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 工作准备

设计了四种收集样本的蜜罐，如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwkWwgKiboHMsIPIrlDYHparssrWvVqN2FnSIg6fJ5uWmxUx1vBg7LbXg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 第一种类型的蜜罐模拟嵌入 Web 服务的设备，主要包括 Goahead、BOA、AppWeb、Thttpd、Apache 等。
- 第二种类型的蜜罐模拟流行的 CVE 存在的物联网设备。
- 第三种类型的蜜罐模拟通用协议捕获物联网恶意软件家族的 courie 蜜罐。
- 第四种类型的蜜罐模拟物联网相关协议的物联网恶意软件家族。

蜜罐覆盖 15 国家/地区的 20 个 VPN 上部署，拥有动态 IP 地址。大部分被捕获的家族是 Mirai 和 Gafgyt，另外也从其他来源补充了数据集。

家族标签由 AVClass 确定。但 VirusTotal 中的引擎并未针对 IoT 进行定制，这导致许多 IoT 恶意软件样本被标记为传统恶意软件家族。

最终的恶意软件数据集由两部分组成：第一部分包括从 Ubuntu Core 18 系统 AMD 64 位、RIOT-OS-2020.04 和 Contiki-NG-3.0 的可执行文件中收集的 16752 个良性样本，这些样本是专门为物联网设备设计的。第二部分是基于 Cowrie 蜜罐和商业交换收集到的 36 个恶意软件家族的 39004 个物联网恶意样本。如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwKOia7eOZebsDcyAYfSXKIMR2Tfr65ndkkMqNnzDu1ICIGhqz9da6HcA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

样本数据集以及其他一些内容开源在 https://github.com/IoMafelt/IoMafelt。

### 架构

如下显示了样本的架构分布情况，可以为蜜罐提供指导。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycw1nRnFvIVzM2Oq7254JWyhg7Y6utNyQ7KGcNiavrjTK1wI8NEv87cKTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### 大小

一些家族在其二进制文件中嵌入了硬编码的弱口令列表，这导致文件大小变大。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwps1v5uPkyhlQpZwcwQ8TkB0THofEA0NkW9xd57gKsOYfqEl133ic5eA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwXibeMCeflF5XZwWoryZt5VZNfYChfkd0kM8xS2ePqtH2UxibpBribOZ6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### Bit

只有 1381 个 64 位可执行文件。

### 系统调用

许多家族通过使用名为 gethostname 的系统调用来获取主机名。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwibLZwC7b4rQyelzaldPwgkG5sXVS6kLoypx7yjOjiap28j11icy9yNENw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### 加壳

尝试从段名、熵值、函数数量推断可执行文件是否加壳。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycw4wMwa1Wd3bk6ruhHK2CtlHSU4y1Hic91rCqcr8f4tuicndHsV7eviaTTw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwabpjUu6DAuwMCWjChh7a8krZ6XGDXcbswMfZ92biayHDfn2wF3tOESA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwialFVgw6gSVv08vaDWNC1TXOrURcroRMSO98fUEIPjbOaiaOlY2vZAYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 工作评估

### 基本环境

少于 10 个样本的家族在训练时不予考虑，最终总共使用了 23 个家族的 38963 个 IoT 恶意软件样本进行训练。

基于 Detux 改进了沙盒，并使用 QEMU 根据样本的架构分布为各种 CPU 架构模拟运行环境。为了保证样本能够正确执行，提前在不同的分析环境中安装了 uClibc、musl、glibc。为每个样本保留了 10 分钟的执行时间，在运行时跟踪并获取样本调用的系统调用。在动态分析之后，通过 r2dare 提取相关静态特征。

实验使用 Intel(R) Xeon(R) CPU E5-2667 v4 @ 3.20 GHz、503 GB 内存，运行 Ubuntu 14.04.4 操作系统。

### 模型分类

使用梯度提升决策树（GBDT）、NB（朴素贝叶斯）、SVM、LR（逻辑回归）和 KNN 模型进行评估，使用网格搜索法为每个模型选择每个参数的最佳值。最后，每个模型得到一个参数的最优组合。不同算法的比较结果如下所示，最终选择 GBDT 作为默认分类器。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwJjV4OJkOdE3C28xhAJ4ia8Q3121QicRhvf4y1majUShY4CCwpiaeGBmDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过 GBDT 模型比较了四种弱模型和集成模型的检测精度。结果如下所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwMDiaVIUgnHViay7GjUo8GcFAnAAkqlFeLxrQ4ibfwWXhib8YZeb9ML1nuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

集成模型是优于四种弱模型的，将弱模型集成到集成模型中后，弱模型低准确率的模型被赋予较低的权重以提高每个家族的整体准确率。

### 横向对比

这是第一个针对 23 个恶意软件家族的 IoT 恶意软件分类研究，与 VirusTotal 提供的其他安全产品（例如 McAfee、Avast 和 F-Secure）进行比较，以横向验证有效性。通过哈希检索每个样本的 VirusTotal 报告，然后使用 AVClass 处理最终结果。

选取蜜罐收集的恶意样本加上 16752 个良性样本作为测试数据集，结果如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycw0zvfo9jcibhO7a35RpT6oFpodqAqMRKD9aP7WiaKlDN2PdpVWtj3UAsg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

每个样本的检测平均耗时 20 s，包括特征提取。检测率相比之下会更好，这些产品在很多家族上会产生很高的误报。推测这些产品的检测率低是因为缺乏签名。

### 特征评估

通过互信息度量评估单个特征对模型性能的贡献。特征包括文件元数据、系统调用和库函数，前五个特征如下所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwuaAIl2HdQPdGlZYGgMkkQE9vUacRtY6HIlLvqzGTSaqPNMKga8zSew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一共选出 146 个特征，包括 18 个文件元数据特征、72个系统调用和56个库函数。

大约 20% 的样品是加壳的。二进制文件的段由加壳程序插入一个随机名称，这些名称很可能被规则解析，例如相同的前缀或段名称的长度。

### 谱系分析

如下显示了按衍生谱系因子排名的前 5 个家族的覆盖精度：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwOiaVuVYDRiaaibhhdaVWZhSm4t8CM7pSQ7qnibuWlOR0QOz83QIY9Jgz8Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当 X 从 2 变为 3 时，准确度显著增加并在 3 后趋于平缓。所以在谱系分析中，给定的样本包含得分在前 3 位的家族特征，而得分低的家族对谱系分析的贡献很小。

给定一个家族，就可以通过样本之间的平均得分来推断一个家族和另一个家族之间是否存在谱系关系。结果如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwXAljY7VWycgStXJBjFo5mlZCRZyRu0drbnUjvficpibsoP9oT4vokuLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

选择了 1600 作为阈值，只有分数高于阈值的关系，才相信它是确实存在的。有了这个假设，我们发现了五个新的谱系，并验证了此前获得的 12 个谱系。完整谱系图如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwdxFxV5DRGXqa0flJ9ZGG8Ze2phVgMjUPlFHRwoGV49Dj5Wico0BR3bg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### 案例分析- NewAidra

NewAidra，也被称为 IRCTelnet，是 Mirai、Aidra 和 BASHLITE 的组合。但是，能够收集到的 NewAidra 样本很少。因此，这个家族从训练集中被移除，变成了一个“未知”的恶意家族，用这个家族的样本来展示评估谱系的可检测性。

该样本内置了一个基于 telnet 协议的扫描工具。其中函数 sockprint() 首先在 Gafgyt 的源代码中使用，用于维护与远程服务器的 C&C 信道。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycw8l3tuj7CDKHFRTbtaRoK4G9e9Lr9HEFaIDjCKuVibMXdDFky2APjyEA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

凭据列表是从 Mirai 复制的，如下所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwcMKI2hVR4YdtIJ9cvdWu7GZpzmiaoYBG1ScGVMy3MwULnGNeIV7PAnw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

家族检测结果是 Aidra。在衍生谱系分析中，前三个衍生谱系因子分别是 Aidra（1950.8）、Mirai（1720.1）和 Qbot（1661.5）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwoicCzINJArSEaVNHpHyibJocU2KSLlDvOBnTGaTHKDwibNULTtlLePV9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### 案例分析- Mirai

Mirai 是历史上最臭名昭著的恶意软件之一，占数据集的近 37%。Mirai 使用硬编码命令（例如 cat /proc/version、cat /proc/cpuinfo）来获取有关设备的信息。根据观察，Mirai 是变种数量最多的家族。

其两种主要变种：第一类变种侧重于传播，包括 ADBMiner、Okiru 和 Wicked。第二类变种是功能的定制修改，攻击者重新开发源代码以删除或改进某些功能。例如，OMG 和 JenX 使用开源工具包 3proxy 删除 Mirai 中的扫描组件。

### 案例分析- Gafgyt

Gafgyt（也称为 BASHLITE）是一种用 C 编写的恶意软件，占到数据集的近 27%。Gafgyt 示例的源代码由三部分组成：下载器、扫描器和 DDoS 模块。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwyHLSHYQGl77KMia6cquVhTeXKISjVzART1h9licK1Rv1lVs7WNHAEh7w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可用于识别 Gafgyt 通信流量的部分特征如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwsIQkdia51l4hic4p25f9MUsae9icQeZE5ianydcRpdR4YUfzstTtbX8vbg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Gafgyt 具有明显的 BaaS（僵尸网络即服务）特征，Gafgyt 实现了从传统的销售攻击流量的获利模式向通过云平台提供僵尸网络托管服务的转变。这样的销售方式，降低了攻击组织的成本，其攻击势必会蔓延到各个领域。

### 整体趋势

对收集到的样本进行了大量逆向分析。分析结果表明，Mirai 变体（如 MIORI 和 SORA）的数量大幅度增加。根据观察，这些变种会首先执行命令 “/bin/busybox SORA” 来确定受害者是否已被感染，然后根据系统反馈再决定下一步行动。这种谨慎的行为可以提高攻击效率。

Gafgyt 和 Mirai 贡献了大部分攻击行为。总体而言，DDoS 部分的特征没有显著变化，例如攻击目标和 C&C 分布。从 2019 年 6 月开始，倒是发现了越来越多的无文件挖矿攻击。

## 工作思考

该研究通过广泛部署的蜜罐收集了 36 个恶意软件家族的 38963 个 IoT 恶意软件样本，最终构建了 72 个 IoT 恶意软件家族的谱系图，已被纳入绿盟科技公司的威胁感知系统实际使用。其整体的架构全貌在 GitHub 中有体现，实际上更为清楚，但在正文中没有使用。

![图片](https://mmbiz.qpic.cn/mmbiz_png/dlhiccJOdNYYFTKcHWum5c5ib9baseZycwTBpkQo2dXibn2EjkZ14EJ8oHrhVmzrC8A2XhpdNZSlGvhXXj5vPIlNQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

IoT 恶意软件的相关研究越来越多，传统杀软对于此类的威胁检出并不一定划分成为更高级的家族概念，而是根据家族特征进行输出，很多恶意软件都会被判定为 Mirai，但是由 Mirai 所衍生出来的其他变种家族则难以进行划分。此类集成学习的方法倒是可以广泛应用在其他应用场景当中，用于提升使用效果，但此类方法的可解释性在实际应用中可能会因为应用场景的不同的而有不同的重要性。在开放数据集中运营“智能”的方法可能会为分析人员带来更大的压力与挑战，找到各种的平衡点是很有技巧的。


