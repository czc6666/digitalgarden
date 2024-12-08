---
{"dg-publish":true,"permalink":"/czc知识库/4-硕士研究生/科研/1-文献阅读笔记/z-垃圾&归档文章&其他东西/3-其他相关东西/FAGnet的simpletex扫描pdf转latex： ConvertedMD/","dgPassFrontmatter":true,"created":"2024-08-08T15:51:34.874+08:00","updated":"2024-12-08T12:30:21.348+08:00"}
---


Knowledge-Based Systems 289(2024)111531

Contents lists available at ScienceDirect

Knowledge-Based Systems

journal homepage: wvww.elsevier.com/locate/knosys

M

$\therefore$

ELSEVIER

$\begin{array}{c}\text{Chack for}\\\text{updates}\end{array}$

FAGnet: Family-aware-based android malware analysis using graph
# neural network

Zhendong Wang, Kaifa Zeng $^*$, Junling Wang, Dahai Li

School of Information Engineering, Jiangxi Universiny $of$ Science and Technology, Ganzhou, Jiangxi 341000, China

ARTICLEINFO


Keywords.Android malware analysis
Malware family
Graph neural network Graph classificatiorn Static code analysis

ABSTRACT

Android malware family analysis is essential for building an efficient malware detection mechanism. In recent years, many graph representation learning-based malware detection and classification studies have been proposed, and many methods model malware as graph data to mine the behavioral semantics of malware. However, they do not consider the relationship at the sample (graph) level, and malware belonging to the same family has similar malicious behavior. The transformation of samples according to the Data Processing Inequality (DPI) will lead to the loss of mutual information transmission, which inspired us to consider the analysis of malware based on graph representation learning from this perspective. In this paper, we consider introducing the relationship between malware samples, inserting a family representation refinement component that is conducive to improving the family separability in the graph classification task, and propose a Eamily-Aware Graph neural network Android malware analysis (FAGnet). We use 4 backbones to perform extension experiments on 2 benchmark datasets and comprehensively compare some baseline methods. The experiments verify the effectiveness of FAGnet, which achieves 98.11 % accuracy on the Drebin dataset and 83.45 % and 72.76 % accuracy on the CICAndMal2017 category and family classification, respectively. In addition, FAGnet is evaluated with real-world data, and its satisfactory performance was maintained in real-world scenarios

## 1. Introduction

According to the McAfee Mobile Threat Report 2021 [1], the total amount of malware exceeded 400 million for the first time in the third quarter of 2021 and grew at an even faster rate in the fourth quarter. The additions surged from approximately 1.5 million in the third quarter to 3.4 million. While some malware are blocked by firewalls, there are still types that can bypass these security measures, compromising various devices such as computers, mobile phones, tablets, clouds, and IoT devices. With the proliferation of malware on the rise, there is an urgent need for effective and efficient detection and analysis methods to establish a secure network environment, safeguarding users and companies from these threats.
Malware family analysis aims to identify the characteristics of an individual malware family. Studies [2,3] have shown that Android malware has distinct family characteristics because malware creators often create malware by injecting similar malicious components into different popular applications. In other words, malware from the same family usually performs similar malicious behaviors. Family analysis is

similar to code clone detection [4,5], which aims to find similar pieces of code fragments. It identifies similar malicious components in malware samples from the same family, which allows experts to quickly and efficiently analyze malicious samples to design more robust detection mechanisms. Some machine learning-based methods usually use SVM, Naive Bayes, and Random Forest for classification based on features extracted from static analysis or dynamic analysis. For example, Drebin [6] extracts relevant features from the Manifest.xml, disassembles code by static analysis, and embeds them in S-dimensional vectors for classification using SVM. Taheri et al. [ 7] detect malware by static analysis of permissions and intent features extracted from the Manifest. xml and classify malware using dynamic network traffic and API call features, both using classifiers such as Random Forest. However, limited by the performance of these machine learning algorithms, researchers have improved and applied more novel algorithms to this field.
In recent years, Graph Neural Networks (GNN) have achieved very significant performance gains in numerous tasks, such as graph convolutional neural networks [8] (GCN), GraphSAGE [9], graph attention networks [10] (GAT) and graph isomorphic networks [11] (GIN), which

$\wedge$ Corresponding author.
$E$-mail address: zengkf@mail.jxust.ed

https://doi.org/l0.1016/j.knosys.2024.
Received 6 July 2023; Received in revised form 20 December 2023; Accepted 15 February 2024
Available online 16 February 2024
0950-7051/© 2024 Elsevier B.V. All rights reserved.

------------------------------------------------------------------

Z Wang et al.

analyze the structural features of gra about the neighborhood of graph nodes through a message passing mechanism. Therefore, many works are based on graph neural networks mechanism. Therefore, many works are based on graph neural networks stor stor st for malware analysis. GraphSAGE-JK [12] directly uses graph neural networks based on featureless FCGs and (JK) technique to solve the over-smoothing problem of GNNs. DMalNet [13] uses a GNN model based on dynamic API call graphs with API semantic information for malware detecti [14] maps Apps and Android APIs into a large heterogeneous graph, which is fed into the GNN model to generate information embeddings for classification. These works model malware as graphs and using GNN to generate graph representations for detection and classification of malware. However, despite their effect from three serious limitations:
Limitation 1: While malware exhibits p haviors, instances within the same family typically demonstrate similar behavioral semantics. These shared characteristics entail analogous or closely resembling behavioral patterns specific to the malware family, and leveraging these similarities can enhance malware family classification. To illustrate this point, consider Fig. 1, where instances of WannaCry and its variants manifest comparable malicious behaviors (such as linking to specified addresses, network access for propagation, registry modification, file permission adjustments, file encryption, etc.) via similar function calls. Exploiting the relationships within function call patterns among samples exhibiting identical or akin behavioral semantics can facilitate guided graph representation learning, yielding more distinctive feature representations. Regrettably, prevailing graphbased methodologies utilizing the GNN model treat each sample graph independently in graph representation generation. These methods solely capture the malicious behavior of individual components during the representation generation process, disregarding inter-component relationships. Deliberate attempts by malware creators to circumvent common antivirus mechanisms (e.g., whether the malware links to a specific address) and alterations in the implementation of malicious behavior (e.g., variant $\textcircled{1}$ omitting the step of linking to a speciffed address, variant $\textcircled{2}$ modifying the specified address) inevitably undermine the validity of models relying solely on the behavioral semantics of a single sample.
$Limitation2:$ In addition, each graph is treated separately in the loss calculation, and the relationships (similarities or differences) between different sample graphs are completely disregarded. According to the Data Process Inequality (DPI), the process of passing each sample through the node representation, graph representation, and then classification by the downstream classifier in the GNN is particularly lengthy. Therefore, when GNNs learn the graph representation of malware and use it for family classification, the effectiveness of the model is severely compromised, which urgently requires an excellent loss function to limit the embedding in the feature space.
Limitation 3: The Message Propagation Neural Network [15] is a generic framework for the working mechanism of graph neural networks and the strategy employed is neighbor aggregation. Taking the example of the node sendTextMessage O in Fig. 2, to update the information of the node, it is necessary to aggregate the information of its neighboring nodes. The more valuable information contained in the node features on the graph, the more valuable the node representation learned by the graph neural network. Therefore, the nodes in our source data (i.e, the graph) need to be populated with sufficiently robust and valuable information. Unfortunately, some work does not take full advantage of valuable information, such as GraphSAGE-JK [12] which merely normalizes graph centrality to graph node features instead of more valuable and relevant information about sensitive APIs (e.g. permissions, opcodes, parameters, etc.).
Considering the above limitations, this work considers the introduction of sample-level relationships in the graph representation learning process to improve the classification accuracy of malware families. To the best of our knowledge, this is the first work to introduce

Knowledge- Based Systems 289 (2024) III531

sample-level relationships in graph representation-based learning for malware analysis. We designed a family representation refinement component Family-Aware Refiner (FAR), which takes into account the relationships between samples and refines the same or similar malicious behaviors of each class of family samples into family features. The family representations of each family are refined according to the samples during the training process and these family representations are added to the graph representation of each sample to obtain better separability. To obtain more accurate family representations, a family loss function is proposed that takes into account both intra-family sample similarity and inter-family sample variability, which will simultaneously drive samples in the feature space to gather or disperse from each other (i.e., samelabeled samples gathered from each other and samples with different labels disperse from each other). The family loss function is used together with the classification loss function of the classifier for the supervised graph representation learning process to obtain better family separability. Finally, to assign more valuable node features to the nodes on the graph, inspired by MsDroid [16], we combine the permission and opcode features of the API as node information.
In this paper, the performance of FAGnet is evaluated with the Drebin [6] and CICAndMal 2017 [17] datasets, achieving accuracies of 98.11 % and $83.45\%$ for categories and 72.76 % for families, respectively. At the same time, several baseline models are compared and evaluated for testing accuracy, and a series of ablation studies are conducted to evaluate the effectiveness of each component.
The contributions of our work are as follows:

(1) A family-aware representation refinement component based on
sample-level relationships is proposed. The family-aware refinement component learns to refine the representations of different families from the sample and uses this representation to guide the graph representation learning process to learn more accurate graph representations to achieve higher analytical accuracy. Adding the family representation to the graph representation learned by the graph neural network will further increase the mutual information between the original graph and the graph representation, which will undoubtedly improve the model's performance.
(2) Construct a robust joint supervised loss function consisting of a
family loss based on the similarity of samples from the same family, a family loss based on the variability of samples from different families, and a cross-entropy loss in the classification stage, which acts jointly on the graph representation learning process to obtain better family separability.
(3) Experiments are conducted on 2 benchmark datasets using 4
backbone networks to validate the model, with the final FAGnet achieving 98.11 % accuracy on the Drebin dataset and $83.45\%$ (category) and 72.76 % (family) on the CICAndMal2017 dataset.


The rest of the paper is organized as follows: Section 2 defines the malware family classification problem and introduces the overall framework of FAGnet, Section 3 details the design methodology of our approach, Section 4 evaluates the performance of our proposed approach, Section 5 introduces the related work of malware and graph neural network, and Section 6 concludes the paper and future work.

2. Problem definition and framework overview

# 2.1. Problem definition

Malware family classification is the classification of malware into specified families. Graph-based classification of Android malware families requires first converting the app to a graph.Given an app, the program semantics are extracted into a function call graph (Fig. 2) represented as$G=(V,E)$,where each node represents an API in the call graph, and$A\in\mathbb{R}^n\times n$is the adjacency matrix of the nodes in the graph.

2

------------------------------------------------------------------

Z Wang et al

Knowledge- Based Systems 289 (2024) III53I

![](https://img.simpletex.net/pdf/BzBdZhZh/fTROUVwimGrUTRM5S17OzlsFhV6tSOcD6.png)

Fig. 1. A sketch of how the ransomware WannaCry and its variants work. The WannaCry controls subsequent behaviors by linking to a specified address, if it succceeds in linking to that address it simply exits, otherwise it starts loading resources and begins to spread. Subsequently, it obtains access to all files the registry and encrypts all files to ransom users. Variant © deletes the step of linking to the specified address, while variant $\textcircled{\text{modifiesthespecifiedadd}}$
$$f:M\to\mathcal{Z}\to L,f(\Phi(G_i))=Y_i,G_i=\mathrm{T}(m_i)$$
(1)

Here $f$ denotes the feature mapping, T denotes the sample transformation, and $Y_i$ denotes the model's predictive labelling for $m_\mathrm{i}.$ In our approach,$f$ consists of a combination of graph representation and family representation.

### $2. 2. \textit{ Framework overview}$

![](https://img.simpletex.net/pdf/BzBdZhZh/fRMAxIVwcGnylyOdskaSn5NV5EXbcOOKy.png)

Fig. 2. FCG examples from the FakeInstaller family.$^{11}$

Fig. 3 illustrates the overview architecture of FAGnet, which consists
of the following three major components
Android malware feature extr feature extraction in this work is divided into two steps. (1) decompile: Android apps are generally written in Java and compiled into Dalvik code stored in classes.dex file. The compiled code and the various resources needed for the execution of the program are packaged into an Android application package file (APK). Between feature extraction, the APK needs to be decompressed into a dex file, which is not readable. Therefore, we need to convert it into a readable Samli file, which can be done with the help of some common disassemble tools such as Apktool [18].(2) FCG Generation: FCG can model the behavior of the program in order to preserve the semantics of the program and to weaken the impact of obfuscation techni consider the combination of API Permission and Opcode information as node features to compensate 
Graph representation learning. This does not require time consuming graph matching algorithms. FAGnet uses four basic graph neural networks GCN, GraphSAGE, GAT, and GIN as a backbone. This phase requires learning two representations.(1) For each graph, the backbone network is used to automatically learn graph embeddings

The node set of graph G is represented as$V_G(|V_G|=n).e=(\nu_1$, $v_2)\in E$denotes the call relationship $\mathbb{R}^{n\times c}$ denotes the feature matrix and the feature vector dimension of each node is c.
Given a set of Android malware $M=\{m_i\}$ with corresponding family labels $L=\{l_i\}$, transform it into a set of graphs $\mathscr{C}=\{G_i\}.$ For each sample graph$G_i\in\mathscr{F}$,we intend to learn its d-dimensional graph representation$hg_{G_i}^d$ and then refine it using the family representation $hc_i.$ This makes each sample graph representation resilient to polymorphism in malicious behavior by including more significant family features. We aim to learn a model:

![](https://img.simpletex.net/pdf/BzBdZhZh/fcvURr2sWthE12p6w6YkLyHAr33k1xCND.png)

Fig. 3. The architecture of FAGnet

3

------------------------------------------------------------------

Z Wang et al.

from multi-hop relationships between nodes on the graph, converting the high-dimensional graph to a low-dimensional vector representation. (2) Based on the low-dimensional graph representations learnt in the previous stage, different family representations are generated using FAR according to different families. Finally, the graph representation is combined with the family representation to generate the final graph representation $hg_G^{\prime}.$ In this way, the final graph representation $hg_G^{\prime}$ has both its own behavioral semantics and the behavioral semantics shared by its family.
Familial classification of Android malware. After learning $hg_G^{\prime}$, this step predicts these malware samples from known and unknown families and adjusts the quality of the graph representation and family representation learned in the graph representation learning phase based on the prediction results. This motivates the FAR to generate more distinctive family representations thus further motivating the model performance.

# 3. Methodology

In this section, we introduce the details of FAGnet, including Android malware feature extraction, graph representation learning, and family classification.

# 3.1. Feature extraction

## 3.1.1. Pre-processing For an APK, the classes.dex file is first converted to a Smali file (an

interpreted language that is syntactically close to pure source code) by Apktool. Subsequently, the call graph is extracted by scanning all Smali files to identify the 'invoke-' in them. In the call graph, each node represents the API, and the source and target nodes of the directed edges represent the caller and the callee, respectively, which reflect the invocation relationship between the APIs. For example, a user-defined functionncalls getSystemService() to use the system service and calls getNetworkInfo() to obtain network information. Then, we add a directed edge from nodento node getSystemService() in the FCG, indicating that functionncalls getSystemService(). Similarly, a directed edge from nodenis added to node getNetworkInfo(). Therefore, all call relationships in the app are organized into FCGs by identifying them to characterize the behavior of the app.

# 3.1.2. Semantic collection To fill the missing node features in FCGs, some studies have encoded

the names of APIs as node features, but this is susceptible to code obfuscation and results in very weak node features. Therefore, we consider introducing more robust properties, the permission and opcode of the API, as node features in the FCG. Privacy- and security-related access to the Android API is controlled by the app's permission system, which largely solves the security problem. However, if the software is installed with excessive requests for permissions from the user (e.g., weather software requesting access to SEND SMS or adware requesting access to BROADCAST STICKY), this can cause significant security problems. On the other hand, introducing the permissions involved in malware into the classification and detection will also improve robustness. Opcode is used to describe the part of a machine language instruction that specifies the part of the machine code that is to perform a certain operation. The Dalvik bytecode generated by decompiling the APK provides access to the opcode of each API, which presents the execution logic of the code. Therefore, we also consider the opcode attribute of the API as a node feature to be included in the FCG as a

Knowledge- Based Systems 289 (2024) III531

supplement.
The following describes the method for extracting the permission

and opcode attributes of the API in the FCG:
Permission: To extract permission-related (i.e, sensitive) APIs$\nu_\mathrm{per}\in V$from the call graph, two widely used API-Permission mappings are used (PSCout [19], Axplorer [20]). For$\forall v\in G$,if it is a sensitive API, the permissions involved are calculated based on the mapping, and a binary vector is generated based on this (i.e., set to 1 and 0, respectively, based on whether the API requires certain permission). For non-sensitive APIs, it is a 0 vector.
Opcode: Opcode histograms are generated by traversing all Smali files, i.e., counting the frequency of occurrence of each opcode. In addition, in some API sections, opcodes occur much more frequently than others (e.g.,“const/4’,“invoke-direct'), so we consider implementing a normalization of opcode frequencies to eliminate the effect of scale between indicators
As shown in Fig. 4, there are directed edges pointed to node $Land-$ $roid/os/AsyncTask;-><init>OV^{\prime}$ by node 'toy exampleO’in the FCG to which it belongs. The node features of node“toy example()’are generated according to the API-Permission mapping, while$\nu_\mathrm{qc}$is generated by counting the opcode frequency. An example of$\nu_\mathrm{per}$and$\nu_\mathrm{opc}$is shown in Fig. 5, and feature generation is shown in Algorithm 1.
Finally, the node features are a combination of$\nu_\mathrm{per}$and$\nu_\mathrm{opc},[H_\mathrm{per}|H_\mathrm{opc}].$ The resulting call graph with node features can then be fed into the GNN to generate a vector of graph representations, while the FAR generates a representation of each family.

# 3.2. Graph representation learning

# $3. 2. 1. \textit{ Graph embedding generation}$
Graph representation learning has excellent performance in graph

data-related tasks, such as natural language processing [21,22], recommendation systems [23-25], computer vision [26,27], and biomedicine [28,29]. They broadly adopt the recursive neighbor node messaging paradigm,which is a paradigm for aggregating neighbor node information to update central node information. Consider a multilayer GCN with the following layer-by-layer propagation rule:
$$H^{(l+1)}=\sigma\bigg(\tilde{D}^{-\frac{1}{4}}\tilde{A}\tilde{D}^{-\frac{1}{4}}H^{(l)}W^{(l)}\bigg)$$
(2)

where$H^(l+1)$denotes the features of thel+1-layer in the network,Adenotes the adjacency matrix of the graph,$\tilde{D}=\sum_j\tilde{A}_{ij}$, and$W^(l)$is the trainable parameter on thel-layer. $\sigma(\cdot)$are activation functions, such as tanh and ReLu.
The graph classification task differs from the node classification and link prediction tasks in that it requires a readout function to obtain a representation of the graph. Common readout functions include sum, mean, max, MLP, GRU, etc. Therefore, after learning the feature repre- sentation of the nodes in the graph via graph neural networks, average pooling is used as a readout function in this paper as follows:

(3)
$$H_G=a\nu g(H_\nu|\nu\in G)$$
$H_G$is the feature representation of graph$G.$ In the graph classification task, the feature representation of the graph obtained by the readout function is then classified by the classifier to obtain the result.

# 3.2.2. Family-Aware Refiner However, disregarding the relationship between the samples is sub-

optimal. Therefore, we introduce FAR to refine each cluster graph representation for better performance. The FAR is co-trained with the graph neural network and can be inserted directly into the neural network, which is a plug-and-play component, as shovn in the dotted box section in Fig. 6. FAR consists of three components: 
Subgraph Generator. The components within a malware sample responsible for executing malicious behaviors constitute a relatively

$\frac{1\text{ SHA-25}}{6:}$
011able277 af208d7c369781696abf9c05052cabf36-
b592e2dd452c6dc3a9a51. The red nodes are examples of sensitive APIs, such
as the node sendTextMessage(), which involves the permission SEND SMS.

------------------------------------------------------------------

9(2024)1153

Z Wang et al

![](https://img.simpletex.net/pdf/BzBdZhZh/fCNt4OLoczgMtKAPVZhHxlz0Yw2ggahg4.png)
Fig. 4. A toy example of the smali code.


![](https://img.simpletex.net/pdf/BzBdZhZh/fSlyLrKvwZo8SlFYKNYrWYBOWL1gzDeZ8.png)


Fig. 5. An example of$\nu_\mathrm{per}$ and $\nu_\mathrm{qq\epsilon}.$

![](https://img.simpletex.net/pdf/BzBdZhZh/fRQZZ1tbzIkgeFDy244pxWMMr2Uc0pV1N.png)
Fig.6. Graph Convolutional Network Architecture with FAR.

small fraction of the overall code. Moreover, the subset of these behaviors that display characteristics shared among malware families is even more limited. Consequently, utilizing the complete graph representation for generating family representations proves highly inefficient. To address this, the process involves selecting crucial subgraphs from the entire graph that hold significant importance and ample discriminatory features to enhance the quality of family representation. In order to streamline the graph by eliminating redundant information, we contemplate the utilization of SAGPool [30],a hierarchical pooling methodology founded on the self-attention mechanism of graph convolution. This approach leverages graph features and topology to compute attention scores, thereby producing pooling results aligned with the graph's characteristics. SAGpool distinguishes nodes that should be maintained based on each node's attention scorez$\in Z:$
(4)
$$idx=top-rank(Z,[kA^{\prime}]),Z_{mask}=Z_{idx}$$
SAGPool sets the number of nodes to be parameter pooling ratek$\in(0,1),top$-rank returns thekindexes of the largest self-attention score inZ,and$Z_mnsk$is the attention mask. In this work, we use graph convolution to learn the attention score z of each node of the original graph and then use TopKPooling to select the K nodes with maximum attention score. Fi by graph pooling operation.
Subgraph Clustering. When subgraph representations are obtained, these subgraph representations need to be clustered in order to obtain family representations. Note that in the training phase, each subgraph representation is used to update its cluster. However, during the validation and testing phase, as the true label of the sample is not known, a pseudolabel$\tilde{y}_G$is predicted based on the subgraph representation$hg_G^\mathrm{sub}$of the sample, and the graph representation of the sample is refined based on the family representation of the pseudolabel family. Here, the

5

------------------------------------------------------------------

Z Wang et al

pseudolabel$\bar{y}_G$is predicted based on the cosine similarity between the
subgraph representation and the family representation:

(5)
$$\overline{y}_{G}=argmax\bigl(cos_sim\bigl(hg_{G}^{sab},hc_{i}\bigr)\bigr)$$
In addition, all clusters stop being updated during the validation and
testing phases.
Set Encoder. The FAR maintains a per-cluster subgraph representation$E_\mathrm{i}$during training, where each sample is identified and added to a cluster based on its label, and the subgraphs in each cluster belong to the same family. Encoding subgraphs in a cluster into a family representation requires mapping a set into a vector, which requires satisfying Permutation-Invariant (PI), meaning that the order of the subgraphs in the cluster must not affect the final family representation. PI is used as a function $f:\mathscr{X}\to\mathscr{Y}$ on a set for any permutation$\pi$, which has:

(6)
$$f(\{x_1,...,x_M\})=f(\{x_{\pi(1)},...,x_{\pi(M)}\})$$
According to Deep sets [31], PI is satisfied if and only if the function$f:X{\to}Y$can be decomposed into the form of$\rho(\sum_x\in X\Phi(x))$, where- $\rho$andФrepresent any function. For example, the functionfwith permutation invariance from the three subgraphs labelediin Fig.7 should satisfy the condition that f $[ \textcircled {1}, \textcircled {2}, \textcircled {3}] = \mathbb{f} [ \textcircled {3}, \textcircled {2}, \textcircled {1}]$ when the subgraphs in the cluster are in the $[\textcircled{1},\textcircled{2},\textcircled{3}]$ or $[\textcircled{3},\textcircled{2},\textcircled{1}]$ order.
Fig.7 aggregates the set of subgraphs in the cluster labeledito obtain a family representation of this family, and according to Deep sets [31] has the aggregation functionz
$$hc_i=\sigma\left(\sum_{hg_G^{*}}\Phi\left(hg_G^{*ab}\right)\right)$$
(7)

where$\sigma$is the multilayer perceptron (MLP) whose activation function is ReLu,Ф$(h\text{g}_G^{\mathrm{sub}})=h\text{g}_G^{\mathrm{sub}}/|E_i|$, and$h\text{g}_G^\mathrm{sub}$is a representation of the subgraph generated by graph G from SAGPool. After the FAR generates the family representation$hc_\mathrm{i}$, it is used to refine each sample with the label$i:$
$$hg_G^{'}=\sigma([hg_G|hc_i])(y_G=i)$$
(8)

refines the similarities and differences between samples to generate the family representation$hc_1with$ significant differentiation. The family representation $hc_i$ is combined with the original graph representation $hg_G$ as the final graph representation $hg_G^{\prime}$ thereby enhancing the performance of the downstream classification task.

3.2.3. Joint supervised loss function
In classification tasks, a superior loss function is critical to the clas-

sification performance of the model. In sample sets characterized by intricate distributions, particularly in multi-class tasks, it is advantageous for samples not only to exhibit separability among different classes in the feature space but also to maintain compactness within individual classes. This attribute enables the model to yield more resil-

Knowledge- Based Systems 289 (2024) III53I

ient outcomes, especially when handling samples from classes exhibiting substantial variations in distribution. The Center loss [32] maintains a class center in the feature space for each class of the training set and constrains the distance between the samples and the class center to make the intra-class distance smaller during the training process. A family representation with high distinguishability requires not only that different family representations are sparser in the sample space, but also that samples of the same family are more clustered in the sample space. Given this, this work designs a loss function$\mathscr{Z}_\text{famijy}$that drives the family representation learned by the FAR to be more distinguishable, which consists of intra-family and inter-family losses. The intra-family loss$Z_\text{intra}$is defined as the similarity of the subgraph representation in the cluster:
$$\mathcal{I}_{mana}=\underset{i\in\mathscr{Y}}{\operatorname*{avg}}\Bigg(\underset{y_G=i}{\operatorname*{avg}}\big(cos_sim\big(hc_i,hg_G^{nab}\big)\big)\Bigg)$$
(9)

The$\mathscr{I}_\text{inre}$measures the similarity of the subgraphs in the cluster to the family representation through cosine similarity and constrains the distance of the samples within the family from the family center by minimizing the intra-family loss.$\mathscr{I}_\text{srter}$is defined as the similarity of family representations in different clusters2

(10)
$$\mathcal{L}_{inter}=\underset{i\in V}{\operatorname*{avg}}\Bigg(\underset{j\neq i,j\in V}{\operatorname*{avg}}\big(cos_sim\big(hc_i,hc_j\big)\big)\Bigg)$$
The$\mathscr{I}_\text{mur}$measures the similarity of family representations of different families through cosine similarity and controls the distance between family centers by maximizing inter-family loss to make them more distant and distinguishable in the feature space. In summary, the objective of training the FAR is to maximize intra-family loss$\mathscr{L}_iwra$and minimize inter-family loss$\mathscr{Z}_\text{ouer. Thus, the family loss function in this}$ paper is defined as:

(11)
$$\mathcal{L}_{\mathrm{fandy}}=\log(\exp(\mathcal{L}_{\mathrm{inter}}-\mathcal{L}_{\mathrm{intra}}))$$
The family representation$hc_\mathrm{obtained}$ by the FAR and the graph representation$h$g$_\mathrm{\omega}$generated by the graph neural network are composed into the final graph representation$hg_G^{\prime}$,which is then passed through the
In summary, to bridge the gap of inter-sample relationships, FAR classiffer forfinal classiffication$tg_{G}$,which is then passed through the fines the simila
classifier is chosen from the commonly used cross-entropy loss functionz

(12)
$$\mathcal{L}_{\mathrm{col}}=\sum_{G\in\mathcal{S}}y_{G}\mathrm{log}\bigg(\hat{y}_{G}\bigg)$$
$\overset{\wedge}{\operatorname*{\hat{y}}}_{G}$is the graph G prediction label. In graph representation learning, the$\mathscr{L}_\text{family}$and$\mathscr{L} _\text{cel}$joint supervisions are integrated, and the joint su- pervision loss function is as follows:

(13)
$$\mathcal{L}=\mathcal{L}_{\mathrm{cel}}+\lambda*\mathcal{L}_{\mathrm{fawily}}$$
$where\lambda is the hyperparameter that balances the classification loss and$
family loss.

![](https://img.simpletex.net/pdf/BzBdZhZh/fGZs60ny8DWwTC4AFMtvQPUIINeGlSdwM.png)


Fig. 7. Example of a subgraph

6

------------------------------------------------------------------

Z Wang et al

Knowledge- Based Systems 289 (2024) III53I

In family analysis, the number of families is relatively large compared to the two categories of the detection task, so this paper considers the introduction of family loss to control the feature representation of the samples to make the feature representation of the same family more compact in the feature space and the feature representation of different families sparser in the feature space to improve the classification accuracy.
The pseudocode of the FAR is shown in algorithm 2.

# 4. Experiment

experiment is set to 500, the initial learning rate is set to 1e-3, and the early stop criterion is used (i.e, when the validation accuracy is not further improved within 20 epochs, the learning rate is reduced by twice until it reaches 1e-6 and the training is stopped). $\lambda$in equation (11) is set to 1 by default, andkin equation (3) is set to 0.5. The model is trained using the Adam optimizer [36], and the hidden size of the network is set to 128. Using the self-loop trick during training showed a performance improvement in [37]. In addition, according to the data statistics in Table 1, there is a significant difference in the number of nodes and edges between the Drebin dataset and the CICAndMal2017 dataset. The average number of nodes and edges in CICAndMal2017 is nearly 5 times that of Drebin, which is limited by the GPU's memory. Therefore, the batch size of CICAndMal2017 is set to 8, while that of Drebin is set to 32.
Finally, the feature dimension of permission is 248, and the feature dimension of opcode is 224, i.e., the node permission and opcode features are combined to give a feature dimension of 472, which is redundant for learning graph neural networks, and there are dimensions with all zero values, which is meaningless for training the network Therefore, from time and space considerations, non-all-0 feature dimensions were filtered as node features, and the final node feature embedding dimension was 255 for the Drebin dataset and 249 for the CICAndMal2017 dataset. To reduce the uncertainty caused by data division, the experiments in this paper all used 10-fold cross-validation to take the mean and standard deviation of 10 experiments as the final result.

In this section, the dataset and experimental steps are introduced, and then a series of experiments are designed to answer the following research questions:
RQ 1. How does the model perform for malware family analysis?
RQ 2. Does FAGnet outperform the existing baseline?
RQ 3. How does the FAR contribute to the model?
RQ 4. How do the statically extracted permission and opcode as node
features contribute to the classification?
RQ 5. How does the joint supervised loss function contribute to the
model?
RQ 6. How does FAGnet perform in real-world scenarios?

## 4.1. Dataset

## 4.2.3. Metrics This paper evaluates model performance using the metrics in

Table 2, including Accuracy, Precision, Recall, and F1-Score, where TP, TN, FP, and FN denote true positive, true negative, false positive, and false negative, respectively. In a multiclassification task, it is often desirable to have a higher accuracy and a greater F1-Score.

Two datasets, Drebin [6] and CICAndMal2017 [17] were used in this work: Drebin contains 5560 Android malware samples from 179 families and CICAndMal2017 contains 429 samples from 42 families in 4 categories. The statistics of the datasets used in the study are shown in tabtle 1.
Due to the extreme sample imbalance problem in the Drebin dataset (such as the existence of families with only 1 sample), this paper selects 4,765 samples from the top 24 families (excluding families with sample sizes less than 20) for the experiment (Fig. 8(a)). In addition, Drebin and CICAndMal2017 both have samples that cannot be decompiled by Apktool, so a total of 424 samples from CICAndMal2017 were selected, with category and family statistics as in Fig. 8(b) and (c). In the experiments, the training set, validation set, and test set were randomly divided according to the ratio of 80%, 10%, and 10%.

# 4.3. Experimental results

The experiments were first conducted on the two datasets using different backbone networks. Fig. 9 shows the classification results for the 10-fold cross-validation on each backbone network. Fig. 10 shows the confusion matrix generated on the test set of the two datasets using the model with the backbone network as the GCN.
This section performs the family classification task on the large Drebin dataset (4765 samples) and the category and family classiffcation

# 4.2. Experimental setup

## $4.2.1.Environment$ The experiments were conducted using Ubuntu 18.04 and an Intel(R)

## Table 1
Summary statistics of the experimental datasets

Xeon(R) Platinum 8255C CPU@2.50 GHz and a 40G RAM machine with an NVIDIA RTX 3080 GPU. The proposed method was implemented using Python and several packages (Apktool [18], Deep Graph Library [33],PyTorch [34], Scikit-learn [35]).

<table>
	<tbody>
		<tr>
			<th>Dataset</th>
			<th>十 Apps</th>
			<th>Call graph A Graphs</th>
			<th>$Avg\#$ Nodes</th>
			<th>$Avg\#$ Edges</th>
			<th>Families</th>
		</tr>
		<tr>
			<td>Drebin</td>
			<td>5560</td>
			<td>4765</td>
			<td>2346.45</td>
			<td>5234.81</td>
			<td>24</td>
		</tr>
		<tr>
			<td>CICAndMal2017</td>
			<td>429</td>
			<td>424</td>
			<td>11,371.26</td>
			<td>26,111.58</td>
			<td>42</td>
		</tr>
	</tbody>
</table>

## 4.2.2. Implementation Details The backbone in the model was selected from 3 layers of GCN,

GraphSAGE, GAT, and GIN. The maximum number of epochs in the

![](https://img.simpletex.net/pdf/BzBdZhZh/fT1Gkzp4DrUzk5XcSynMlsPdmdeCYZOLa.png)



(b)CICAndMal2017-Category

(a)Drebin

(c)CICAndMal2017-Family


Fig. 8. Statistics on the number of datasets

7

------------------------------------------------------------------

Z Wang et al

Knowledge- Based Systems 289 (2024) III53I

Table 2
Descriptions of the metrics.


<table>
	<tbody>
		<tr>
			<th>Metric</th>
			<th>Definitiom</th>
		</tr>
		<tr>
			<td>Accuracy</td>
			<td>$TP+TN$</td>
		</tr>
		<tr>
			<td>Precision</td>
			<td>$TP+TN+FP+FN$ $TP$</td>
		</tr>
		<tr>
			<td>Recall</td>
			<td>$TP+FP$ $77P$</td>
		</tr>
		<tr>
			<td>Fl-Scare</td>
			<td>$TP+FN$ $2Prectsion+Recall$</td>
		</tr>
		<tr>
			<td rowspan="1">Fl-Scare</td>
			<td>Precision+Recall</td>
		</tr>
	</tbody>
</table>

component, by 3.05% and 2.08%, respectively).
The confusion matrix in Fig. 10(a) shows that the majority of samples from the test set were correctly classified, with only a very small number of samples being incorrectly classified; for example, three samples from Adrd, BaseBridge, and Geinim From the perspective of the FAR, when using equation (7) to calculate the pseudolabels of these three samples, the pseudolabels were calculated as GinMasters, thus injecting the family representation of GinMasters into its graph representation, leading the classifier to incorrectly classify these three samples as GinMasters. Similarly, most of the samples in the category and family classification tasks on the CICAndMal2017 dataset in Fig. 10(b) and (c) can be correctly classified, while there are also some misclassified samples. Especially in the family classification task, due to the small number of samples contained in each family, the minimum family has only 4 samples (selfmite family), which makes learning extremely difficult. The generalization ability of a model in a small number of samples is an important issue, especially in the context of privacy, security, and the high cost of obtaining sample labels, and how to enable machine learning systems to efficiently learn and generalize from a small number of samples. However, the model in this article can still classify samples to a certain extent correctly with a small number of samples
Answer to RQ 1 and RQ 5: The model achieved a family classification accuracy of 98.1132% for 4765 samples from 24 families in the Drebin dataset and achieved improved performance in the category and family classification tasks of the CICAndMal2017 dataset. Moreover, compared to using only the backbone, FAR has improved effectiveness, and in the 10-fold cross-validation, the standard deviation of the classification results is smaller, which means that the model's classiffication effect is more stable.

tasks on the small CICAndMal2017 dataset (424 samples). As seen from the experimental results in Fig. 9, the ability of FAR to learn family representations with certain distinguishability due to the constraint of the family loss function in the joint supervisory function drives the final graph representation generated by the model to be highly separable, and the strong features resulting from the family representation make the model more stable (smaller standard deviation).
In the family classification task on the Drebin dataset, the model achieved 98.1132±0.6867% and 97.4843±0.7906% accuracy when using GCN and GIN as the backbone network, respectively, which is $1.11\%$ and $1.53\%$ higher than that when FAR is not used. In the category classification task of the CICandMal2017 dataset, the model achieved $83.4520\pm6.1242\%$ and $82.3477\pm6.3530\%$ accuracy when GCN and GraphSAGE were used as backbone networks, respectively, which were $3.01\%$ and $7.33\%$ higher than when FAR was used. In the family classification task of the CICandMal2017 dataset, the model achieved $74. 4925\pm 5. 2483\%$ and $73. 8567\pm 6. 2415\%$, respectively, when GraphSAGE and GIN were used as backbone networks, which are improvements of 6.59% and 6.53%, respectively, compared to when FAR was not used.
Conversely, the validity of the model was compromised if the family representation learned from the FAR di family characteristics (e.g., when using the GAT as the backbone, both category and family classifications from CICAndMal2017 were less accurate with the insertion of the family representation refinement

## 4.4. Comparison experiments

Since this work adopts the analysis method based on graph representation learning, we first consider the method based on graph representation learning and second consider the dataset used by the method when selecting the baseline. For the Drebin dataset, this paper selects

![](https://img.simpletex.net/pdf/BzBdZhZh/fiGt2tU4kgK7ykAryVsy8H4WwiGdZT8gm.png)

(a)Drebin

(c)CICAndMal2017-Family

(b)CICAndMal2017-Category
Fig.9. 10-fold cross-validation classification results

![](https://img.simpletex.net/pdf/BzBdZhZh/fYFhTLwNzhXAV8idQNgSfdU4eyUGuqUMq.png)
(a)Drebin
(b)CICAndMal2017-Category

(c)CICAndMal2017-Family

Fig. 10. Confusion matrix of the Drebin and CICAndMal2017 datasets

------------------------------------------------------------------

Z Wang et al

Knowledge- Based Systems 289 (2024) III53I

Table 4
Comparison of category classification with other baselines on the CICAnd-

Mal2017 dataset
<table>
	<tbody>
		<tr>
			<th>Model</th>
			<th>Feature(s)</th>
			<th>Precision</th>
			<th>Recall</th>
		</tr>
		<tr>
			<td>Lashkari et al.[17]</td>
			<td>Dynamic+Network Traffic</td>
			<td>49.9%</td>
			<td>48.596</td>
		</tr>
		<tr>
			<td>Taheni et al. 1.[7]</td>
			<td>(17)+Dynamic API call</td>
			<td>83.396</td>
			<td>81%</td>
		</tr>
		<tr>
			<td>Abuthawabeh et al. [40]</td>
			<td>Conversation-level Network Traffic</td>
			<td>BO.20%</td>
			<td>79.6496</td>
		</tr>
		<tr>
			<td>FAGnet</td>
			<td>Static+FCG</td>
			<td>83.7296</td>
			<td>$83.72\%$</td>
		</tr>
	</tbody>
</table>

Table 5

Comparison of family classification with other baselines on the CICAndMal2017

dataset.
<table>
	<tbody>
		<tr>
			<th>Model</th>
			<th>Feature(s)</th>
			<th>Precision</th>
			<th>Recall</th>
		</tr>
		<tr>
			<td>Lashkari et al.[17]</td>
			<td>Dynamic+Network Traffie</td>
			<td>27.596</td>
			<td>25.596</td>
		</tr>
		<tr>
			<td>Taheri et al. (7)</td>
			<td>[17]+Dynamic API call</td>
			<td>59.796</td>
			<td>$61.2^{96}$</td>
		</tr>
		<tr>
			<td>FAGnet</td>
			<td>Static+FCG</td>
			<td>74.4196</td>
			<td>$74.41\%$</td>
		</tr>
	</tbody>
</table>

## datasets.

## 4.5. Time Efficiency

several machine learning-based approaches as baselines for comparison (Table 3). CANDYMAN [38] uses Markov chains to dynamically model malware behavior and uses machine learning methods for classification. GDroid [14] models the call relationship between APPs and APIs with API usage patterns as a heterogeneous graph and uses graph convolutional neural networks for analysis. GSFDroid [39] uses static analysis to construct sensitive API calls to FCG, uses GCN to learn graph representations, and employs MLP classifiers for classification tasks on known families. Drebin [6] used static analysis to extract relevant sensitive information from manifest files and decompiled the dex code of APIs and networks as feature vectors for classification using machine learning methods. GraphSAGE~JK[12] used FCG as data, where node-filled graph centrality was used as a feature, and GNN vith Jumping-Knowledge for analysis. Since no source code has been made available, we report the scores provided by the respe
The experimental results in Table 3 demonstrate that FAGnet achieved the highest performance among all baselines on the Drebin dataset $(98.11\%$ accuracy and 98.26% F1-score).It is worth noting that GraphSAGE-JK[12] differs from FAGnet in that it uses graph centrality in FCG as node features and uses jumping knowledge graph neural networks, whereas FAGnet uses the permission and opcode attributes of the API in FCG as node features and uses FAR to enhance the representational power of graph neural networks.
For the CICAndMal2017 dataset, this paper conducts separate malware category and family classification experiments. For category classification experiments, Lashkari et al.[17] collected network traffic features (e.g., source IP, target IP, source port, target port, protocol, etc.) and processed them accordingly to perform classification using a machine learning system. Taheri et al.[7] set up different frameworks based on detection and classification tasks, where the classification framework uses dynamic API calls and network traffic features. Abuthawabeh et al.[40] proposed collecting conversation-level network traffic as features and using machine learning methods for classification based on [17]. For family classification experiments, Lashkari et al. [17] and Taheri et al. [7] were used for comparison. The comparison results are shown in Tables 4 and 5.
The experimental results in Tables 4 and 5 demonstrate that the model achieved the best performance of FAGnet across all baseline methods on the CICAndMal2017 dataset. FAGnet achieved an accuracy of 83.72% in category classification and 74.41% in family classification. Dynamic analysis to obtain network traffic characteristics is theoretically more robust but relies on more resource consumption, and in the case of event-driven Android simulations running software, capturing the network traffic characteristics of all malicious actions performed by the malware requires more complex moderation of the triggering method and considerable time consumption. The static analysis used in this paper, however, only requires feature extraction for static code, with the largest time consumption being in the extraction of API permission and opcode features, but this is very efficient compared to dynamic analysis. Therefore, FAGnet only needs to achieve similar or even better results than the baseline approach with minimal resource consumption.
Answer to RQ 2: FAGnet outperforms existing methods for malware family classification, achieving the highest accuracy and recall and lowest false positives on both large (i.e., Drebin) and small (i.e., CICAndMal2017)

From Section 4.3, it can be seen that the introduction of FAR brings an increase in accuracy to the model, but at the same time, it needs to be considered whether the additional components and the loss function drastically sacrifice the efficiency of the backbone. The number of epochs and the average time taken per epoch for FAGnet with GCN and GraphSAGE as backbones are reported in Table 6.In most scenarios, FAGnet doesn't notably impact the efficiency of the backbone networks. The discernible increase in time per epoch emerges solely in the family classification task on CICAndmal2017, as compared to the baseline backbone performance. We analyzed the experiments and found that this phenomenon arises with an increase in the number of classes to be categorized, as evidenced by the differences when carrying out the category (4 classes) versus family categorization (42 families) tasks on the CICAndMal2017 dataset shown in Table 6. However, this time is acceptable when the model is trained offline and then deployed to a mobile device, for example, in the Drebin dataset, it only took 1.84 hours to train when using GraphSAGE.

## 4.6. Ablation Studies

Two ablation studies are designed to demonstrate the effect of different node features and joint supervised loss functions on model performance.

## 4.6.1. Node features Consider the classification of node features into four cases: combined

permission and opcode $([H_{per}|H_{opc}])$, opcode $(H_{qpc})$, permission$H_\mathrm{per}$, and consider only graph centrality $(H_\mathrm{gc})$ in FCG rather than sample API semantics, which is a common structural node feature on attributeless graphs.
This paper considers the collection of combinations of the following
graph centralities as node features in the FCG:

Table 3
Comparison with other baselines on the Drebin dataset

<table>
	<tbody>
		<tr>
			<th>Model</th>
			<th>Feature(s)</th>
			<th>Accuracy</th>
			<th>Precision</th>
			<th>Recall</th>
			<th>Fl-Score</th>
		</tr>
		<tr>
			<td>[38] CANDYMAN</td>
			<td>Dynamic+Markov chain</td>
			<td>81.8</td>
			<td>0.807</td>
			<td>0.818</td>
			<td>0.802</td>
		</tr>
		<tr>
			<td>GDroid [14]</td>
			<td>Static+API</td>
			<td>96.98</td>
			<td>0.969</td>
			<td>0.959</td>
			<td>0.960</td>
		</tr>
		<tr>
			<td>GSFDroid [39]</td>
			<td>Static+FCG</td>
			<td>91.10</td>
			<td> </td>
			<td> </td>
			<td> </td>
		</tr>
		<tr>
			<td>Drebin [6]</td>
			<td>SIA mde</td>
			<td>93</td>
			<td> </td>
			<td> </td>
			<td> </td>
		</tr>
		<tr>
			<td>GraphSAGE-JK :[12]</td>
			<td>Static+FCG</td>
			<td>96.88</td>
			<td>0.9701</td>
			<td>0.9688</td>
			<td>0.97</td>
		</tr>
		<tr>
			<td>FAGnet</td>
			<td>Static+FCG</td>
			<td>98.11</td>
			<td>0.9841</td>
			<td>0.9811</td>
			<td>0.9826</td>
		</tr>
	</tbody>
</table>

------------------------------------------------------------------

Z Wang et al

Knowledge- Based Systems 289 (2024) IIII53I

Table 6

seconds

Time efficiency of FAGnet and backbones. The unit of Time/epoch
<table>
	<tbody>
		<tr>
			<th rowspan="2">Model</th>
			<th> </th>
			<th rowspan="2">Drebin $Epoch\pm s.d.$</th>
			<th rowspan="2">Time/epoch</th>
			<th colspan="2">torr</th>
			<th colspan="2">CICAndMal2017- Family</th>
		</tr>
		<tr>
			<th> </th>
			<th>Epoch$\pm$s. d. </th>
			<th>Time/epoch</th>
			<th>Epoch $\pm s.d.$</th>
			<th>Time/epoch</th>
		</tr>
		<tr>
			<td rowspan="2">$GCN$</td>
			<td>Vanilla</td>
			<td>$234.1\pm32.6$</td>
			<td>13.3407</td>
			<td>$209.0\pm42.1$</td>
			<td>5.5583</td>
			<td>$210.8\pm26.8$</td>
			<td>5.0103</td>
		</tr>
		<tr>
			<td>FAGnet</td>
			<td>$2429\pm29.2$</td>
			<td>28.9879</td>
			<td>$214.2\pm38.9$</td>
			<td>6.9265</td>
			<td>$224.5\pm22.8$</td>
			<td>17.3832</td>
		</tr>
		<tr>
			<td rowspan="2">GraphSAGE</td>
			<td>Vanilla</td>
			<td>$256.7\pm20.3$</td>
			<td>14.8310</td>
			<td>$199.8\pm22.3$</td>
			<td>5.2338</td>
			<td>$199.4\pm16.9$</td>
			<td>5.3508</td>
		</tr>
		<tr>
			<td>FAGnet</td>
			<td>$236.2\pm27.1$</td>
			<td>27.9146</td>
			<td>$209.7\pm26.6$</td>
			<td>6.6509</td>
			<td>$203.5\pm16.2$</td>
			<td>17.7851</td>
		</tr>
	</tbody>
</table>

2) PageRank: PageRank was originally used to calculate the importance
of Internet pages and was defined as a function on a collection of web pages to indicate the importance of a web page. Based on the idea that highly linked pages are also more important, the PageRank of each function in the FCG is calculated to reflect its importance. PageRank is defined as follows:

node feature in the family classification task of the CICAndMal2017 dataset. From this perspective, it can be shown that there is some overlap in the permissions involved in the relevant APIs in the different family samples, especially when the sample size is small, which confounds the model. In addition, using the centrality feature of the graph as a node feature can make the sample somewhat distinguishable, but its effectiveness is greatly reduced when classifying categories and families in the small CICAndMal2017 dataset.
Answer to RQ 4: Ablation studies on the GCN and GraphSAGE backbones basedonfour different node features. The experimental results show that the permission and opcode extracted in this paper provide a good boost to the model, and it is found that the opcode feature provides the greatest boost to the malware family classification task compared to permission.
$$PR(v_i)=d\left(\sum_{v_j\in B(v_i)}\frac{PR(v_j)}{L(v_j)}\right)+\frac{1-d}{N}$$
(14)

wheredis the damping factor, and$B(v_i)$is the set of nodes in the FCG that link node$v_i.L(\nu_j)$is the number of edges with$\nu_\mathrm{j}$as the source node, and N is the total number of nodes.

## 4.6.2. Loss functions This section designs an ablation study on the effect of jointly su-

pervised loss functions on the model, considering four different combi-
nations of loss functions:

3) Degree: The in-degree and out-degree of nodes in the FCG.
4) Node closeness centrality: closeness centrality is the reciprocal of the
average shortest path toufor all n-1 reachable nodes and is scaled according to its proportion in the overall graph, which is defined as.

(15)
$$C_{MF}(u)=\frac{n-1}{N-1}\:\frac{n-1}{\sum_{\nu=1}^{n-1}d(\nu,u)}$$
$1)\mathscr{L}_{\mathrm{cel}}{:\text{Using only the cross-entropy loss function, i.e., equation}}$
(11).
$2)\mathscr{L}_{cd}+\mathscr{L}_{intra}{:\text{Using cross-entropy loss functions and intra-family}}$
loss functions.
$3)\mathscr{L}_{cel}+\mathscr{L}_{itter}{:\text{Using cross-entropy loss functions and inter-family}}$
loss functions.
$4) \mathscr{L} {: \text{Using the entire joint supervisory loss function, i. e. , equation}}$
(12).

4) Node degree centrality: degree centrality indicates that the greater
the degree of a node is, the more important it is. The assumption behind this metric is that an important node has many connections. The normalized degree centrality of nodes with degree n is defined as
$$C_D(v_i)=\frac{d_i}{N-1}$$
(16)


Similarly, GCN and GraphSAGE are used as the backbone in this section to conduct experiments to compare the performance of four different loss functions.
The results in Fig. 12 demonstrate that the joint supervised loss function$\mathscr{I}$proposed in this paper achieves the best results. Under the constraint of joint supervised loss, the FAR learns that a more familyspecific family representation drives the model to generate a more distinguishable graph representation. In contrast, in some cases, when only intra-family loss and classification loss or only inter-family loss and classification loss are used, the resulting family representation introduces a perturbation into the graph representation generated by the model that affects the classification effect of the model. A family representation with significant family characteristics needs to be generated under certain constraints. Our family loss function takes into account both the similarity of samples within a family and the variability between samples from different famillies. This helps constrain the generation of a family representation with significant family characteristics

whereNis the number of nodes in the graph.
Collect the above five graph centrality node features to form$H_\mathrm{gc}.$ This section compares the performance of four different node features in a model using GCN and GraphSAGE as the backbone, and the results are shown in Fig. 11.
The results in Fig. 11 shows that the node feature$[H_{per}|H_{opc}]$collected in this paper, consisting of the API's permission and opcode, achieved the best performance, followed by the opcode feature$H_{apc}$, while the permission feature$H_\mathrm{per}$was too weak for family classification and even performed less well than the method using only graph centrality as the

![](https://img.simpletex.net/pdf/BzBdZhZh/f522KetZzGruHYiyFWasPMwgI85Ew1UKC.png)

(b)CICAndMal2017-Category

(c)CICAndMal2017-Family


(a)Drebin

Fig. 11. Ablation study on node features

10

------------------------------------------------------------------

Z Wang et al

Knowledge- Based Systems 289 (2024) III53I

![](https://img.simpletex.net/pdf/BzBdZhZh/fFHHnr2iGGDXVaaG2PG9vZuNMl1OC2zq2.png)







Fig. 12. Ablation study on loss functions

Algorithm 1
Feature generatior

Answer to RQ 5: This section analyses the performance of the joint supervised loss function on both the GCN and GraphSAGE backbones. The experimental results have shown that the joint supervised loss function prompts the generation of more accurate family representations to improve performance, while the generation of inaccurate family representations reduces the effectiveness of the analysis.

## 4.7. Deployment

![](https://img.simpletex.net/pdf/BzBdZhZh/fQZpN4PqCDaVBlfLMxUTUQKXOzspPHOUO.png)

Algorithm
<table>
	<tbody>
		<tr>
			<th>Tr:</th>
			<th>aining of Family-Aware Refiner</th>
		</tr>
		<tr>
			<td>In</td>
			<td>$\textbf{put: hg}_G^\mathrm{aab},hg_G$and $y_G;$</td>
		</tr>
		<tr>
			<td>On</td>
			<td>stput:he.y $\therefore\angle AC=\angle AC$ andy</td>
		</tr>
		<tr>
			<td>1 $a$ ·</td>
			<td>for each G$\in\mathscr{E}$do</td>
		</tr>
		<tr>
			<td>2:</td>
			<td>usehg$_G^\mathrm{mb}$update the$E_(y_G=i);$</td>
		</tr>
		<tr>
			<td>3:</td>
			<td>usehg$_G^\mathrm{q\vartheta}$updatehc$_i$by Eq.(5);</td>
		</tr>
		<tr>
			<td>4:</td>
			<td>usehg$_{GG}^\mathrm{q\vartheta}$andhe$_{\epsilon}$calculate$h_G^{\prime}$by Eq.(6);</td>
		</tr>
		<tr>
			<td>5:</td>
			<td>TR $9mr$</td>
		</tr>
		<tr>
			<td>6:</td>
			<td>end for</td>
		</tr>
		<tr>
			<td>7:</td>
			<td>retum Istres</td>
		</tr>
	</tbody>
</table>

We achieved high performance for Android malware classification performed in an experimental environment. In this subsection, we discuss the performance of FAGnet on a real-world dataset.
The performance of the model in a real-world scenario is more indicative of the model's performance than in an experimental environment. Therefore, we consider capturing data from the real world and validating the performance of FAGnet in this scenario. VirusShare [41] is a large malware repository containing not only Android malware but also malware for other platforms such as Linux and Windows. Furthermore, it is still being updated regularly with some of the latest captured malware, so we considered obtaining malware samples from this malware repository for real-world scenarios. We also determined the family tag and timestamp of each malware sample at VirusTotal [42] to ensure that it was still active since 2020. Ultimately, we selected 1,000 samples from the Adware, Banking, Riskware, and SMSware families from VirusTotal's family reports and timestamp reports.
The experimental results are shown in Table 7, where it should be noted that the slight decrease in performance in real-world scenarios compared to the experimental setting is acceptable, especially since the samples in Drebin and CICAndMal2017 were collected from 6-9 years ago (although they are still widely used in recent work). Finally, from the results in Table 7, we can conclude that FAGnet still achieves a generally satisfactory performance and that our model can perform better in classifying malware in real-world scenarios.
Finally, we try to simulate the deployment effect using Google Pixel 7 Pro in Android Studio. Limited by the space of the simulator, we used 100 samples (from each of the four families mentioned above) for our experiments and studied the model runtime and accuracy (Fig.13).We found that the feature processing time in the whole classification process is extremely large (close to 97.5%), which is similar to when we run it on the server. However, because the hardware level of mobile devices is so much lower compared to servers, the overall time is close to 100 times more. The accuracy of the model quantized and deployed to different platforms is more influenced by the sample (e.g., conceptual drift), which is similar to the case of the real-world dataset studied above CTable 7).
However, as shown in Fig. 13, the time for feature processing on the simulation device is too long relative to the inference time, and such computational costs will affect the effectiveness of model deployment to


some extent. Therefore, in real devices, multi-threading techniques can be considered for I/O-intensive operations in the feature processing phase. For example, processes such as converting APKs to graphs, and extracting Permission and Opcode of nodes are implemented multithreaded using Python's Threading module to improve CPU efficiency. In addition, we can consider using the Androguard$^2$ tool to convert APK to graph directly instead of using Apktool to convert APK to Smali file and then traverse all the files to generate a graph. And use the relevant methods in the androguard analyze module to generate node features for the graph. These solutions to shorten the feature processing time can solve the computational cost problem on real devices to some extent.
Answer to RQ 6: FAGnet can achieve satisfactory results in malware
classification tasks in real-world scenarios.

Table 7
The performance of FAGnet for familial classification on real-world data

<table>
	<tbody>
		<tr>
			<th>Backbone</th>
			<th>Accuracy</th>
			<th>Precision</th>
			<th>Recall</th>
			<th>Fl.Scorem</th>
		</tr>
		<tr>
			<td>$GCN$</td>
			<td>9496</td>
			<td>$92.55\%$</td>
			<td>$95.42\%$</td>
			<td>93.796</td>
		</tr>
		<tr>
			<td>GraohsAGE</td>
			<td>9376</td>
			<td>$92.3\%$</td>
			<td>93.91%</td>
			<td>92.8196</td>
		</tr>
	</tbody>
</table>

https://github.com/androguard/androguard

11

------------------------------------------------------------------

Z Wang et al


![](https://img.simpletex.net/pdf/BzBdZhZh/fqhbDyeUfZrlDD3goRQ27cbdNnVel1RDP.png)
Fig. 13. Deployment of the model on the simulator.

## 5. Related work

### 5.1. Malware family classification

There has been a significant amount of work focused on the family analysis of Android malware. Characterizing malware families can help improve the malware detection process and understand patterns of $\hat{\text{malware evolution, which is equally important for maintaining a secure}}$ network environment. Similar to malware detection, recent family classification studies often use multilevel features from static or dynamic analysis. Static analysis mines a sample for static features rather than executing it. Feng et al.[3] use static analysis to generate a new high-level representation of an Android app called an inter-component call graph (ICCG) to determine whether the app matches the control flow properties specified in the signature. Fan et al.[43] use a TF-IDF-like approach to assign different weights to sensitive API calls and generate FCG to represent the app based on the decompiled code to generate a sensitive API call related graph (SARG) to transform the malware family classification problem into a graph clustering problem. Dynamic analysis requires the collection of relevant features during the runtime of a sample. Martín et al. [38] used a Markov chain to model dynamic behavior using information about where the sample was executed on a DroidBox. Then, a machine learning algorithm was used to perform family classification. Li et al. [13] executed samples on a Cuckoo SandBox, collected relevant features to form API call sequences, and embedded API name and parameter features to perform detection and classification tasks using graph learning algorithms.
In addition, several studies have used network traffic-based detection methods. Lashkari et al.[17] extracted and computed over 80 network traffic features and used machine learning algorithms such as Random Forests, K-Nearest Neighbors, and Decision Trees to perform detection and classification tasks. Taheri et al.[7] extended Lashkari et al. [17] by adding Permission and Intent static features and API call dynamic features using the same machine learning algorithm to significantly improve detection and classification. Network traffic usually contains a large amount of information. To enhance the fusion, extraction, and analysis of heterogeneous threat data from multi-sources, Qi et al.[44] constructed a network security knowledge graph based on the knowledge of known attacks and introduced it into compound attack detection to automatically mine the attack chain. This also helps to uncover malware distribution and attack chains.

Knowledge-Based Systems 289 (2024) III53I

## 5.2. Graph neural network

Graph data are widely available due to their powerful representation of relative relationships, and many learning tasks require solving graph data problems, such as modeling physical systems, predicting protein properties, web link analysis, recommender systems, traffic prediction, and fake news detection. Unlike other fields of data, it is crucial to construct a reasonable graph model based on the structural information in the graph. Graph neural networks capture the structural information of a graph by passing messages through nodes in the graph. In recent years, many variants of graph neural networks, such as GCN, GraphSAGE, GAT, and GIN, have achieved good performance in many deep learning tasks. Below is a brief introduction to the four variants mentioned above.
The basic idea of GCN is to reduce the high-dimensional neighbor node information of a node in the graph to a low-dimensional representation. This is a model that directly operates on graph-structured data. It uses a first-order approximation to simplify calculations based on spectral graph convolution and proposes a simple and effective layer propagation method. However, GCN is a transductive learning method with limited scalability when dealing with large images in the field of engineering practice. Therefore, to solve the problem of transductive learning, GraphSAGE proposes an inductive learning method that utilizes both node feature information and structural information to obtain a map of graph embedding. Compared with the results after the GCN saves the map, GraphSAGE saves the generated embedding map, which has stronger scalability. GAT assumes that the neighbors of nodes in the graph have different importance to the nodes, which is different from GCN predetermination and not the same as GraphSAGE. Instead, attention mechanisms are used in the node aggregation process to determine the importance of each neighboring node to the central node, and multi-head attention methods can be combined to enhance the expression ability. GIN considers graph convolution operations from a spatial domain perspective, and Message Passing Neural Network (MPNN) [15] outlines a general framework for spatially based convolutional neural networks, which treats graph convolution as a message-passing process where information is passed directly along a node in the graph to another node. GIN argues that the graph embeddings generated in the information transfer neural network framework do not effectively distinguish between graph structures. To correct this shortcoming, GIN adjusts the weights of the central nodes utilizing a learnable parameter$\varepsilon^k$and demonstrates that the sum aggregation approach outperforms the average and max aggregation approaches. 5.3. Graph-based malware analysis


The topological structure of graph data can effectively model the behavioral semantics of malware, so there have been many recent works on graph-based malware analysis. Especially for API-related graphs, the relationship between nodes in the graph well describes the API call relationship. He et al.[16] extracted FCGs and collected semantic information from APIs to construct behavioral subgraphs non-redundantly representing the behavioral semantics of malware and used GIN for behavioral subgraph classification. Li et al.[39] used FCG as a base graph model to describe the program semantics of malware and GCN to automatically learn graph data features for malware family analysis. In addition, a simple graph feature normalization method based on Z-score is proposed to mitigate the performance of downstream tasks caused by different scales due to the random initialization and propagation strategies of the GCN. Lo et al. [12] directly use FCG, where graph centrality is standardized to node features in the graph, and it uses graph neural networks with jumping knowledge to perform detection and classification tasks. Yumlembam et al. [45] considered malware on IOT devices based on API graphs with centrality features and Permission and Inten and employed GNN-generated graph embedding along with the VGAE-MalGAN method to retrain the model, thus maintaining high

12

------------------------------------------------------------------

Z Wang et al

accuracy in the face of generating adversarial sample attacks.
Yan et al.[46] extract a Control Flow Graph (CFG) from malware, where nodes in the CFG represent base blocks that contain a sequence of codes, and edges between nodes indicate jumps in the code blocks with some code and structural attributes added to the nodes. A Deep Graph Convolutional Network (DGCNN) is used to learn to obtain graph representations for downstream tasks. Gao et al.[14] built 'APP-API' and 'API-API' edges to construct heterogeneous graphs based on API invocation relationships and usage patterns, converting the original problem into a node classification problem. Herath et al.[47] designed an attribute CFG-based family classification model with interpretability, which extracts key subgraphs of classification results in the CFG and ranks the importance of nodes in the subgraphs.
However, none of the above methods consider sample-level relationships. Samples in the same family usually exhibit similar malicious behavior (i.e., relationships between samples are crucial for malware family analysis). Therefore, this paper considers introducing relationships between samples in the malware analysis process as a way to improve the performance of malware analysis.

# 6. Conclusions and future work

Given the excellent performance of graph neural networks for graph data analysis, this work has modelled malware as graph data and uses graph neural networks for analysis. Prior studies have established the FCG's ability to capture substantial behavioral semantics in characterizing malware. However, the FCG lacks specific features. To address this limitation, we have introduced API permission and opcode semantics into the FCG. This additional semantic information significantly enhances our ability to delineate the distinct characteristics within the FCG. However, existing work neglects the relationships between samples, and those from the same family often exhibit very similar behaviors. To fill this gap, the FAR proposed in this work considers introducing sample-level relationships and learning the unique representation of the family based on the family labels of the samples. It is envisioned that the learning of the family representation guided graph neural network can achieve better family separability. To obtain more accurate family representations, a joint supervised loss function was introduced. Experiments have shown that under the control of a suitable loss function, FAR can obtain family representations with high distinguishability, and the inclusion of family representations in the graph representation of samples also improves classification accuracy.
This article conducted a large number of experiments to verify the effectiveness of the model. The experimental results showed that FAGnet can classify malware families with high accuracy and recall, even when facing small datasets, which has made certain improvements for some baseline methods. In addition, ablation studies were designed to validate the contribution of the node features extracted in this work and the joint supervised loss function to the effective improvement achieved by the model.
There is further scope for improvement on the semantic features of nodes according to MsDroid [16], which found that byte-based semantic information embedding is relatively too simple and susceptible to confusion and conceptual drift. In future work, we can consider introducing more robust API semantic information embedding, such as API usage mode [14], API parameter information, and category [48,49]. In the FAR of this paper, some detailed improvements can also be attempted, such as the introduction of attention mechanisms and ranking pooling in the aggregation of subgraph clusters. In graph clustering algorithms, the introduction of multi-view graph learning-based clustering [50] can be considered, e.g., simultaneously considering the FCG, CFG, and behavior subgraph or modifying the node features in the same topological graph. In the case of subgraph generation, i.e., graph pooling methods, ranking nodes can be introduced in different views using different contextual graph information to identify more important subsets of nodes or to consider graph topology information. Deploying

Knowledge- Based Systems 289 (2024) III53I

real-time environments, abstracting malware attacks into graph streams, and using graph stream summarization algorithms for fast graph querying is a worthwhile direction, such as the continuous graph stream summarization algorithm proposed by Jia et al. [51] for efficient and effective graph querying processing. Finally, some more advanced graph neural networks can be considered as a backbone for mining graph data to obtain more generalized models.

CRediT authorship contribution statement

Zhendong Wang: Writing- review & editing, Supervision, Project administration, Funding acquisition. Kaifa Zeng: Writing- review & editing, Writing - original draft, Validation, Software, Methodology, Formal analysis, Conceptualization. Junling Wang: Supervision. Dahai Li: Supervision, Resources, Funding acquisition.

## Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Data availability

The experimental data of this paper are from this website (https ://www.unb.ca/cic/datasets/andmal2017.html, https://www.sec.cs. tubs.de/-danarp/drebin/index.html)

## Acknowledgments

This work is supported by the Natural Science Foundation of China (62062037,61562037,72261018) and the Natural Science Foundation of Jiangxi Province (20212BAB202014,20171BAB202026).

## References

( 1) McAlee. McAfee Mobile Threat Report. 2021; Available from: https://www.mcafee
com/.
( 2) Y. Zhou, X. Jiang, Dissecting android malware: characterization and evolution, in: 
2012 IEEE symposiurr
security and privacy, IEEE, 2012.
$\{3\}$ Y.Feng, et al., Apposcopy: semantics-based detection of android malware through
static analysis, in: Proceedings of the $222nd$ ACM SIGSOFT international symposium
on foundations of software engineering, 2014.
$\{4\}$ H.Sajnani, et al., Sourcerercc: scaling code clone detection to big-code, in
engineering, 2016.[6] D. Arp, et al., Drebin: effective and explainable detection of android malware in
Ndss, 2014.
your pocket
$\{7\}$ L. Taheri, A.F.A. Kadir, A.H. Lashkari, Extensible android malware detection and
family classification using network-flows and API-calls, in: 2019 International
Carnahan Conference on Security Technology (ICCST), IEEE, 2019.
[ 8] T. N. Kipf and M. Welling, Semi- supervised classification with gruph comvolutiona
nerworks. arXiv preprint arXiv:1609.02907, 2016.
[9] W.Hamilton, Z. Ying, J. Leskovec, Inductive representation learning on large graphs, Adv. Neural Inf. Process. SysL.(2017) 30.[10] P. Veličković, et al $\begin{array}{cc}[10]&\text{P.Veličković, et al.,Gruph attention networks.arXiv preprint arXiv:1710.10903}\\&\text{2017}\end{array}$
2017.
( 11)  K.  Xu,  et al. ,  How powerful are graph netural networks?  arXiv preprint arXiv: 
1810.00826,2018
( 12)   W.W. Lo, et al, Graph neural network-based android malware classification with
jumping knowledge, in: 2022 IEEE Conference on Dependable and Secure
Computing (DSC), IEEE, 2022.
$\{13\}$ C.Li, et al., DMalNet: dynamic malware analysis based on API feature engineering
and graph learning, Comput. Secur. 122(2022)102872.
(14) H.Gao, S. Cheng, W. Zhang, GDroid: android malware detection and classificatior mithamab analutional atunol cotunole Commant Some 105(2001) TOPPEA
with graph convolutional network, Comput. Secur. 106 (2021) 102264.
Internationa
(15) J. Gilmer, et al., Neural message passing for quantum chemistry
conference on machine learning, 2017. PMLR
$\{16\}$ Y.He, et al., MsDroid: identifying malicious snippets for android malware
detection, IEEE Trans. Dependable Secure Comput. (2022).
[17] AH. Iashkari, et al., Toward developing a systematic approach to generate benchmark android malware datasets and classification, in: 2018 Intemationa
Carnahan Conference on Security Technology (ICCST), IEEE, 2018

13

------------------------------------------------------------------

Z Wang et al


[18] Apktool. Apktool: $a$ tool for reverse engineering android apk files. 2016; Available
from: https//ibotpeaches.github.io/Apktool/.
Security, 2012.
[20] M.Backes, et al., On demystifying the Android application framework: re-visiting
Android permission specification analysis, in: USENIX Security Symposium, 2016. $\{21\}$ A. Bordes, et al., Translating embeddings for modeling multi-relational data, Adv.
Neural Inf. Process. Syst.(2013) 26
(22) X. Wang, Y. Ye, A. Gupta, Zero-shot recognition via semantic embeddings and
knowledge graphs, in: Proceedings of the IEEE conference on computer vision and
pattern recognition, 2018.
[23] X.He, et al, Lightgcn: simplifying and powering graph convolution network for
recommendatior
Proceedings oí the 43rd International ACM SIGIR conference
research and development in Information Retrieval, 2020
[24] L. Wu, et al., A neural influence difusion model for social recommendation, in.
Proceedings of the 42nd international ACM SIGIR conference on research and
development in information retrieval, 2019.
[25] H. Wang, et al., Knowledge graph convolutional networks for recommenden
systems, in: The world wide web conference, 2019.
[26] A. Mohamed, et al., Social-stgcnn: a social spatio-temporal graph convolutional
neural network for human trajectory prediction, in: Proceedings of the IEEE/CVE
conference on computer vision and pattern recognition, 2020
[27] K. Han, et al., Vistion grın: an image ís worth graph of nodex. arXiv preprint arXiv:
2206.00272,2022
$\{28\}$ Z. Hao, et al., ASGN: an active semi-supervised graph neural network for moleculan
property prediction, in: Proceedings of the 26th ACM SIGKDD International
Conference on Knowledge Discovery & Data Mining, 2020
[29] M. Zhang, et al, Hierarchical attention propagation for healthcare representation learning, in: Proceedings of the 26th ACM SIGKDD International Confer
Knowledge Discovery & data Mining, 2020.
(30) J. Lee, I. Lee, J. Kang, Self-attention graph pooling. International Conference On
Machine Learning, PMLR, 2019
(31) M. Zaheer, et al., Advances in neural information processing systems, Deep sets
(2017)30.
(32) Y. Wen, et al., A discriminative feature learning approach for deep face
recognition, in: Computer Vision- ECCV2016:14th European Conference,
Amsterdam, The Netherlands, Springer, 2016. October 11-14,2016, Proceedings,
Part VII I4.
(33) M.Y. Wang, Deep graph library: towards efficient and scalable deep learning on
graphs, in: ICLR workshop on representation learning on graphs and manifolds, 2019.

Knowledge-Based Systems 289 (2024) III53I

[34] A. Paszke, et al., Pytorch: an imperative style, high-performance deep leaming library, Adv. Neural Inf. Process. Syst. ( 2019) 32. [ 35] Scikit- learn. scikit- learn: machine learning in Python. 2021; Available from: https
/scikie-learn.org-
(36) D.P. Kingma and J. Ba, Adam: $a$ method for stochastic $optimization.$ arXiv preprint
arXiv:1412.6980, 2014
Simplifying graph convolutional networks, in: Intemationa
$[37]F.VVu$,
conference on machine learning, PMLR, 2019.
( 38) A. Martin, V. Rodr$\acute{ı }$guez- Fern$\acute{a}$ndez, D. Camacho, CANDYMAN: classifying Android
malware families by modelling dynamic traces with Markov chains, Eng. Appl.
Artif. Intell. 74 (2018) 121-133
[39] Q. Li, et al., Semi-supervised two-phase familial analysis of Android malware with
normalized graph embedding, Knowl. Based. Syst. 218(2021)106802 [40] M.K.A. Abuthawabeh, K.W. Mahmoud, Android malware detection and
categorization based on conversation-level network traffic features, in: 2019 International Arab Conference on Information Technology (ACTT), IEEE, 2019.
[41] VirusShare. Available from: https://virusshare.com/.
[42] VirusTotal. Available from: https://www.virustotal.com/
Fan, et al., Android malware familial classification and representative sample
[43]
selection via frequent subgraph analysis, IEEE Trans. Inf. Forensics Secur. 13 (8)
(2018)1890-1905.
[44] Y. Qi, et al, Cybersecurity knowledge graph enabled attack chain detection for
cyber-physical systems, Comput. Electr. Eng. 108 (2023) 108660
$\{45\}$ R.Yumlembam, et al., Iot-based android malware detection using graph neural
network with adversarial defense, IEEE Internet. Things. J.(2022)
(46) J.Yan,G.Yan, D. Jin, Classifying malware represented as control flow graphs using
deep graph convolutional neural network, in: 2019 49th annual IEEE/IFIF
international conference on dependable systems and networks (DSN), IEEE, 2019 $\begin{aligned}\text{[47]J.D. Herath, et al, CFGExplainer: explaining graph neural network-based malware classification from control flow graphs, in: 2022 52nd Annual IEEE/IFIP}\end{aligned}$ [48]M. Zhang, et al., Semantics-aware android malware classification using weighted
contextual api dependency graphs, in: Proceedings of the 2014 ACM SIGSAC
conference on computer and communications security, 2014
[49] Z.Zhang, P. Qi, W. Wang, Dynamic malware analysis with feature engineering and
feature learning, in: Proceedings øí the AAAl conference on artificial intelligence,
2020.
(50) U. Fang, et al., A Comprehensive Survey on Multi-view Clustering, IEEe Trans
Knowl. Data Eng.(2023)
(51) Y. Jia, et al., Persistent graph stream summarization for real-time graph analytics
World Wide Web.(2023) 1-21

14