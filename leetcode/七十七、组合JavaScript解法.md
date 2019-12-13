## 组合
给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

示例:

输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

思路：回溯

执行用时 :104 ms, 在所有 javascript 提交中击败了99.45%的用户  
内存消耗 :40.9 MB, 在所有 javascript 提交中击败了87.10%的用户

```
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function(n, k) {
    // 去除不符合条件的
    if (n <= 0 || k <= 0 || k > n) return [];
    let res = [];
    findCombinations(1, k, n, [], res);
    return res;
};
function findCombinations (start, k, n, pre, res) {
    // 当前找到的组合存储在pre中，需要从start开始搜索新的元素
    // 在第k层结算
    if (pre.length === k) {
        res.push(pre.slice());
        return false
    }
    for (let i = start; i < n+1; i++) {
        pre.push(i);
        findCombinations(i+1, k, n, pre, res);
        // 回溯，状态重置
        pre.pop();
    }
}
```