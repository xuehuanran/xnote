### Wide & Deep

#### Reference

Wide & Deep Learning for Recommender System, 2016 DLRS

#### Introduction

一个推荐系统可以被看作为一个搜索排序系统，其中输入的查询为用户以及上下文的信息(Context Information)，输出为Items的排序。给定一个查询，推荐系统的任务为依据相应的目标函数在数据库中找到相关的items。

#### The Wide Component

Wide Component实际上是一个线性模型$y = w^Tx + b$，其中特征既包括原始的特征，也包括转换后的特征，其中一个重要的特征transformation是对特征做cross-product，如下所示：
$$
t(\mathbf{x}) = \mathbf{x}_i^{c_k}
$$
其中，$c_k \in \left\{ 0,1 \right\}$，表示第$i$个特征是否被选中。

#### The Deep Component





