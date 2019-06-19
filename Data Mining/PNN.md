### PNN
#### Reference
Product-based Neural Networks for User Response Prediction, ICDM 2016

#### Introduction
在搜索推荐广告领域中，存在着大量的categorical类型的数据，一般是将这种数据进行One-Hot编码，转换成高维的稀疏数据。传统的机器学习模型，如线性模型，GBDT，FM等，对于这种高维稀疏数据处理的效果比较好，但是这些模型的缺点是需要大量的特征工程来发现high-order的特征。
基于Deep Learning的方法，在处理Categorical类型数据时，对于每个field进行一个embedding，但是缺点是模型的效果很受embedding初始化的影响。
这篇文章的主要贡献：
1) embedding layer不再是预训练，而是作为网络本身的参数。
2) 引入了一个product layer的概念，用来发现特征之间的关系。
3) 进一步探究了PNN的不同模式，包括两种作全连接的方式。

#### Product-based Neural Network

PNN的网络结构如下所示：

![PNN_Architecture](PNN_Architecture.png)

从上到下，网络的输出$\hat{y} \in (0, 1)$作为预测的CTR。
$$
\begin{aligned}
\hat{y} = \sigma(W_3l_2 + b_3)
\end{aligned}
$$
第二个hidden layer的输出$l_2$定义为：
$$
\begin{aligned}
l_2 &= relu(W_2l_1 + b2)
\end{aligned}
$$
其中$l_1 \in \mathbb{R}^{D_1}$为第一个hidden layer的输出，$W_2, b_2$为参数。
第一个hidden layer与product layer全连接在一起，输入有三部分组成，分别是$
l_p, l_z, b_1$，$l_1$的定义为：
$$
\begin{aligned}
l_1 = relu(l_z + l_p + b_1)
\end{aligned}
$$
定义Tensor间的内积：$A \odot B \triangleq \sum_{i,j} A_{i,j} B_{i,j}$，将两个shape相同的Tensor转化为一个标量。之后，定义$l_Z, l_p$分别为：
$$
\begin{aligned}
l_z = (l_z^1, l_z^2,...,l_z^n,...,l_z^{D_1}), \quad l_z^n = W_z^n \odot z \\
l_p = (l_p^1, l_p^2,...,l_p^n,...,l_p^{D_1}), \quad l_p^n = W_p^n \odot p \\
\end{aligned}
$$
其中$W_z^n, W_p^n$为product层的系数，其形状分别和$z,p$相同，$z$表示linear singal，$p$表示quadratic singal，定义如下：
$$
\begin{aligned}
&z = (z_1, z_2,...,z_N) \triangleq (f_1,f_2,...,f_N) \\
&p = \left\{ p_{i,j} \right\}, i = 1,...,N\ j = 1,...,N
\end{aligned}
$$
其中$f_i \in \mathbb{R}^M$为第$i$个特征所对应的embedding向量，$p_{i,j}=g(f_i,f_j)$为两两特征交互，PNN模型针对算子$g$有不同的定义方式。embedding向量通过如下方式计算：
$$
\begin{aligned}
f_i = W_0^ix[start_i:end_i]
\end{aligned}
$$
其中$x$为经过one-hot编码的向量，$W_0$代表embedding矩阵，$W_0^i \in \mathbb{R}^{M \times(end_i - start_i + 1)}$，对应第$i$个特征。

#### Inner Product-based Neural Network (IPNN)
在IPNN中，定义$g$为向量间的内积，$g(f_i,f_j) = <f_i, f_j>$，因此，$l_n^z$计算如下：
$$
\begin{aligned}
l_n^z = W_n^z \odot z = \sum_{i=1}^N\sum_{j=1}^M {(W_n^z)}_{i,j} z_{i,j}
\end{aligned}
$$
在计算$p$时，$g(f_i, f_j)$生成了一个方阵$p \in \mathbb{R}^{N \times N}$, 因此，$l_n^p = \sum_{i=1}^N\sum_{j=1}^N(W_n^p)_{i,j}p_{i,j}$。
上述操作能够增加神经网络的能力，但同时也会增加网络的复杂度，当计算$l_1$时，空间复杂度为$O(D_1N(M + N))$，时间复杂度为$O(N^2(D_1 + M))$
为了简化计算复杂度，采用矩阵分解的方法，令$W_n^p = \theta^n{\theta^n}^T$, 其中$\theta^n \in \mathbb{R}^N$。

#### Outer Product-based Neural Network (OPNN)
向量的内积运算输出为一个标量，而向量的外积运输输出为一个矩阵。在OPNN中，与IPNN唯一的一个不同点就是$g(f_i, f_j) = f_if_j^T$，因此$p$中的每一个元素都是一个方阵。
计算$l_1$的空间复杂度为$O(D_1M^2N^2)$，时间复杂度也为$O(D_1M^2N^2)$，然而这种操作在实际中是非常耗时的， 通过element-wise superposition的方法，我们可以减少时间复杂度。因此，重新定义$p$，如下所示：
$$
\begin{aligned}
p = \sum_{i=1}^N\sum_{j=1}^Nf_if_j^T=f_{\sum}(f_{\sum})^T, f_{\sum}=\sum_{i=1}^Nf_i
\end{aligned}
$$

