### Union Find

#### 模板

```cpp
int parent[N], height[N] n;

void init() {
  for (int i = 1; i <= n; i++) {
    parent[i] = i;
    height[i] = 0;
  }
}

int find(int x) {
  if (parent[x] == x) return x;
  return parent[x] = find(parent[x]);
}

bool is_same(int x, int y) {
  return find(x) == find(y);
}

void merge(int x, int y) {
  x = find(x), y = find(y);
  if (x == y) return;
  if (height[x] < height[y]) {
    parent[x] = y;
  } else {
    parent[y] = x;
    if (height[x] == height[y]) height[x]++;
  }
}
```

