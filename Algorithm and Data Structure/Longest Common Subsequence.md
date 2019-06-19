### Longest Common Subsequence

#### Reference
POJ 1458 Common Sequence

#### Description
给定两个序列$s1,s2$，求出两个字符串最长的公共子序列。

#### Analysis
非常经典的动态规划问题，递推方程如下(这里序列的下标从1开始，编码时要注意下标从0还是1开始)：
$$
\begin{aligned}
f[i][j] = 
\left\{
             \begin{array}{lr}
             f(i - 1, j - 1) + 1, \quad  if \ s1[i] = s2[j]  \\
             \max(f[i][j - 1], f[i - 1][j]), \quad if \ s1[i] \neq s2[j]\\
             
             \end{array}
\right.
\end{aligned}
$$

#### Code
```cpp
int lcs(const string& s1, const string& s2) {
    int n1 = s1.size(), n2 = s2.size();
    vector<vector<int>> f(n1 + 1, vector<int>(n2 + 1, 0));
    for (int i = 1; i <= n1; i++) {
        for (int j = 1; j <= n2; j++) {
            if (s1[i - 1] == s2[j - 1]) f[i][j] = f[i - 1][j - 1] + 1;
            else f[i][j] = max(f[i - 1][j], f[i][j - 1]);
        }
    }
    return f[n1][n2];
}
```


$$

$$

