### 字典树

#### 字典树简介
Trie（字典树）是一种用于字符串快速检索的多叉树结构，Trie的每个节点都有若干个字符指针。

字典树的数组实现如下，参考李煜东《算法竞赛进阶指南》：

```cpp
//初始化，空间复杂度为O(NC) 
int trie[N][C], tot = 1; // 每当有新的节点时，tot加1，从1开始是为了判断某节点的孩子是否为空
bool end[N];

void insert(char* str) {
    int len = strlen(str), p = 1;
    for (int k = 0; k < len; k++) {
        int ch = str[k] - 'a';
        if (trie[p][ch] == 0) trie[p][ch] = ++tot;
        p = trie[p][ch];
    }
    end[p] = true;
}

bool search(char* str) {
    int len = strlen(str), p = 1;
    for (int k = 0; k < len; k++) {
        int ch = str[k] - 'a';
        if (trie[p][ch] == 0) return false;
        p = trie[p][ch];
    }
    return end[p]; //判断是否为一个单词的终止
}

// 与search基本相同，除了返回true
bool startWith(char *str) {
    int len = strlen(str), p = 1;
    for (int k = 0; k < len; k++) {
        int ch = str[k] - 'a';
        if (trie[p][ch] == 0) return false;
        p = trie[p][ch];
    }
    return true; // 判断是否为前缀
}
```

