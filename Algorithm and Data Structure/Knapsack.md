### Knapsack Problem

#### 01背包
01背包问题的模型如下：
给定$N$个物品，其中第$i$个物品的体积为$v_i$，价值为$w_i$。有一体积为$V$的背包，要求选择一些物品放入背包，使得物品总体积不超过$V$的前提下，物品的总价值最大。
背包问题中的递推方程如下，对于每个物品都可以选择加还是不加：
$$
\begin{aligned}
F[i,j] = 
\left\{
             \begin{array}{lr}
                F[i-1, j] \\
                F[i-1, j - v_i] + w_i, \ if\ j >= v_i
             \end{array}
\right.
\end{aligned}
$$
代码如下(注意在实际中f一般从1开始，而v和w要考虑下标是从1还是0开始的)：
```cpp
memset(f, -1, sizeof(f));
f[0][0] = 0;
for (int i = 1; i <= N; i++) {
    for (int j = 0; j <= V; j++) 
        f[i][j] = f[i - 1][j];
    for (int j = v[i]; j <= V; j++)
        f[i][j] = max(f[i][j], f[i - 1][j - v[i]] + w[i]);
}
return f[N][V];
```

01背包问题可以使用倒序循环的方法优化空间复杂度，使从$O(NV)$降到$O(V)$，代码如下所示：
```cpp
int f[N + 1];
memeset(f, 0, sizeof(f);
for (int i = 1; i <= N; i++) {
    for (int j = V; j >= v[i]; j--) {
        f[j] = max(f[j], f[j - v[i]] + w[i]);
    }
}
return f[V];
```

#### 完全背包
完全背包问题中，每个物品都有无数个，其它条件和01背包相同。
完全背包的模板和01背包相同，由于每件物品可以选择无数次，因此，从前向后遍历。
```cpp
int f[N + 1];
memeset(f, 0, sizeof(f);
for (int i = 1; i <= N; i++) {
    for (int j = v[i]; j <= v[i]; j++) {
        f[j] = max(f[j], f[j - v[i]] + w[i]);
    }
}
return f[V];
```

#### 多重背包
多重背包问题中，每个物品有$n_i$个。思路是针对每种物品，$v_i \cdot n_i >= V$，则对这种采用完全背包的思路，否则，采用01背包的思路，这种情况，不能一件件物品去试试，效率比较低，而是应该用二进制把$n_i$分解，从而时间复杂度从$O(V\sum n_i)$降到$O(V\sum \log n_i)$。

#### 三种背包的通用模板
```cpp
//主函数
int main() {
    for (int i = 1; i <= N; i++) {
        //invoke functions...
    }
}

// 01背包
void zero_one(int v, int w) {
    for (int i = V; i >= v; i++)
        f[i] = max(f[i], f[i - v] + w);
}

// 完全背包
void complete(int v, int w) {
    for (int i = v; i <= V; i++) 
        f[i] = max(f[i], f[i - v] + w);
}

// 多重背包, n为物品数量
void multiply(int v, int w, int n) {
    if (v * n >= V) complete(v, w);
    else {
        int k = 1;
        while (k < n) {
            zero_one(k * v, k * w);
            n -= k;
            k *= 2;
        }
        zero_one(v * n, w * n);
    }
}

```

