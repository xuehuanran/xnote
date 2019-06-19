### Binary Search

#### 整数集合上的二分

在单调递增序列$a$中查找 $>=x$ 的数中最小的一个($x$和$x$的后继)。
```cpp
while (l < r) {
    int mid = (l + r ) >> 1;
    if (a[mid] >= x) r = mid;
    else l = mid + 1;
}
return a[l];
```

在单调递增序列$a$中查找 $<=x$ 的数中最大的一个($x$和$x$的前驱)。

```cpp
while (l < r) {
    int mid = (l + r + 1) >> 1;
    if (a[mid] <= x) l = mid;
    else r = mid - 1;
}
return a[l];
```

第一段代码中，若$a[mid] >= x$，$mid$之后的数字不可能是答案，但$mid$本身可能是答案，因此令$r = mid$，同理，若$a[mid] < x$，则$mid$不可能是答案，因此令$l = mid + 1$。

第二段代码中，若$a[mid] <= x$，$mid$之前的数字不可能是答案，但$mid$本身可能是答案，因此令$l = mid$，同理，若$a[mid] > x$，则$mid$不可能是答案，因此令$r = mid - 1$。

注意第二段代码中$mid=(l + r + 1) >> 1$，这样才能保证退出条件为$l==r$，没有死循环的情况出现。

