### Factorization Machines

#### Reference
Factorization Machines, ICDM 2010

#### Introduction
SVM是机器学习和数据挖掘中一种非常重要的模型，然而其不能很好的适用于大规模的稀疏数据。Factorization Machines (FM) 是一种类似SVM的模型，且能很好的适用于非常稀疏的数据，并且不需要进行对偶之类的操作，有着线性的时间复杂度。

#### Model Description

二阶FM模型可以用如下的公式表示：

$$
\begin{aligned}
\hat{y}(\mathbf{x}) := w_0 + \sum_{i=1}^nw_ix_i + \sum_{i=1}^n\sum_{j=i+1}^n<\mathbf{v}_i,\mathbf{v}_j>x_ix_j \qquad (1)
\end{aligned}
$$
其中 $w_0 \in \mathbb{R}, \mathbf{w} \in \mathbb{R}^n, \mathbf{V} \in \mathbb{R}^{n \times k}$ 为模型的参数，$\mathbf{V}$的第 $i$ 行 $\mathbf{v}_i$ 表示第 $i$ 个特征的 $k$ 个 factors，其实就是一个embedding。$\hat{w}_{i,j}:=<\mathbf{v}_i,\mathbf{v}_j>$ 描述了两个特征之间的交互关系。 

等式1的时间复杂度为 $O(n^2k)$，但是在FM中可以把复杂度降低为$O(kn)$。
$$
\begin{aligned}
&\quad\sum_{i=1}^n\sum_{j=i+1}^n <\mathbf{v}_i, \mathbf{v}_j>x_ix_j \\
&= \frac{1}{2}\sum_{i=1}^n\sum_{j=1}^n <\mathbf{v}_i, \mathbf{v}_j>x_ix_j - \sum_{i=1}^n <\mathbf{v}_i, \mathbf{v}_i>x_ix_i
\end{aligned}
$$

#### $d-way$ Factorization Machines





