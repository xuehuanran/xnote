### Topological Sort

#### 模板

```cpp
vector<int> topo_sort(const vector<vector<int>>& graph) {
    int n = graph.size();
    vector<int> d(n, 0); //d统计每个节点的入度
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < graph[i].size(); j++) {
            int v = graph[i][j];
            d[v]++;
        }
    }
    
    queue<int> q;
    for (int i = 0; i < n; i++) if (d[i] == 0) q.push(i);
    
    vector<int> order;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        order.push_back(u);
        for (int i = 0; i < graph[u].size(); i++) {
            int v = graph[u][i];
            d[v]--;
            if (d[v] == 0) {
                q.push(v);
            }
        }
    }
    
    return order;
}
```

