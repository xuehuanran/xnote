### Narrow versus Wide Transformations

在2012年RDD的文章中，对窄依赖的定义为，"父RDD的每个Partition至多只被一个子RDD的Partition所依赖”，宽依赖的定义为"子RDD的多个Partition可能依赖一个父RDD的Partition"。

下图是一个简单的例子关于窄依赖和宽依赖：

![Narrow_versus_Wide_Transformations_1](/Users/xuehuanran/repositories/xnote/Images/Narrow_versus_Wide_Transformations_1.png)

```scala
// Narrow dependency. Map the rdd to tuples of (x, 1)
val rdd2 = rdd1.map(x => (x, 1))
// Wide dependency groupByKey
val rdd3 = rdd2.groupByKey()
```

