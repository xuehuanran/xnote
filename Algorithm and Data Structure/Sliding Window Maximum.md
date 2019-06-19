### Sliding Window Maximum

#### Reference

LeetCode 239. Sliding Window Maximum

#### Description

给定一个数组$nums$，有一个大小为$k$的滑动窗口从数组最左边向右滑动，每次移动一个数字，输出每次滑动窗口中的最大值。

#### Analysis

一道非常经典的用单调队列的算法。使用单调队列是一个普通的dequeue，即队头和队尾都可以添加和删除元素，假设队列的队尾为队列的最大元素所在下标，从队头至队尾元素单调递增。

#### Code

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
  int n = nums.size();
  vector<int> res;
  deque<int> q;
  for (int i = 0; i < n; i++) {
    while (!q.empty() && i - q.back() >= k) q.push
  }
}
```



