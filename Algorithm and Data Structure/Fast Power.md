### Fast Power

#### Description 
在$O(n\log{n})$的时间复杂度计算$x^n$

#### Analysis
不断的除以2其实是进行2进制的表示，当n为奇数时说明该位为1，将连乘的结果累计起来。

#### Code
```cpp
double power(double x, int n) {
    long long res = 1, tmp = x;
    while (n) {
        if (y & 1) res *= tmp;
        tmp *= tmp;
        n >>= 1;
    }
    return res;
}
```

