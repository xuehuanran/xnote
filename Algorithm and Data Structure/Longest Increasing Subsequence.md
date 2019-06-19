### Longest Increasing Subsequence

#### Reference
《挑战程序设计竞赛》

#### Description
有一个长为$n$的数列$a_0,a_1,...,a_{n-1}$。求出这个序列中最长的上升子序列的长度。

#### Analysis
这个问题是被称作最长上升子序列（LIS, Longest Increasing Subsequence）的著名动态规划问题。首先建立递推关系。
定义$f[i]$，以$a_i$为末尾的最长上升子序列的长度。则很容易得出递推方程：
$$
\begin{aligned}
f[i] = \max\left\{1, f[j] + 1 | j < i, a_j < a_i \right\}
\end{aligned}
$$
时间复杂度为$O(N^2)$

#### Code
```cpp
int lis(const vector<int>& a) {
    int n = a.size(), res = 0;
    vector<int> f(n, 1);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (a[j] < a[i]) f[i] = max(f[i], f[j] + 1);
        }
        res = max(res, f[i]);
    }
    return res;
}
```

#### Improvement of Time Complexity $O(n\log{n})$
还可以定义其它的递推关系将时间复杂度优化到$O(n\log{n})$，定义$f[i]$为长度为$i + 1$的上升子序列中末尾元素的最小值，

代码实现如下：
```cpp
int lis(const vector<int>& a) {
    int n = a.size();
    vector<int> f(n, INT_MAX);
    for (int i = 0; i < n; i++) {
        *lower_bound(a.begin(), a.end(), a[i]) = a[i];
    }
    return lower_bound(a.begin(), a.end(), INT_MAX) - a.begin();
}
```