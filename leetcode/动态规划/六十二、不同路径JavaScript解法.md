## 不同路径

### 解题思路
杨辉三角形，每个位置的路径 = 该位置左边的路径 + 该位置上边的路径

执行用时 :68 ms, 在所有 javascript 提交中击败了61.73%的用户
内存消耗 :33.7 MB, 在所有 javascript 提交中击败了75.15%的用户

```
/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */
var uniquePaths = function(m, n) {
    const cur = new Array(n);
    cur.fill(1);
    for (let i=1; i<m; i++) {
        for (let j = 1; j < n; j++) {
            cur[j] += cur[j-1]
        }
    }
    return cur[n-1]
};
```