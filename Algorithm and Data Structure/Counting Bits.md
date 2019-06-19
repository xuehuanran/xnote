### Counting Bits

#### Description
给定一个非负整数 $num$，对于所有的 $i, 0≤i≤num$，计算出 $i$ 的二进制表示中1的个数。要求时间复杂度和空间复杂度都为$O(n)$。

#### Analysis
令`f[i]`表示 `i` 的二进制表示中的个数。则`f[i]`可以由`f[i/2]`转移过来，`i`的二进制表示和 `i/2` 的二进制表示除了最后一位都一样，所以递推方程为`f[i] = f[i/2] + (i&1)`。

#### Code
```cpp
vector<int> countBits(int num) {
    vector<int> f(num + 1, 0);
    for (int i = 1; i <= num; i++) {
        f[i] = f[i >> 1] + (i & 1);
    }
    return f;
}
```

