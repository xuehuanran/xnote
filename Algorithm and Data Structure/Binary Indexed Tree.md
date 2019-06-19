### Binary Indexed Tree

树状数组(Binary Indexed Tree)是能够完成下列操作的数据结构：

$\bullet$ 给定$i$，计算$a_1+a_2+...+a_i$

$\bullet$ 给定$i$和$x$，执行$a_i=a_i + x$	



#### 树状数组的实现

```cpp
int bit[N + 1], n;

int sum(i) {
    int s = 0;
    while (i > 0) {
        s += bit[i];
        i -= i & -i;
    }
    return s;
}

void add(int i, int x) {
    while (i <= n) {
				bit[x] += x;
      	i += i & -i;
    }
}
```

