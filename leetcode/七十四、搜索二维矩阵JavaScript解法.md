## 搜索二维矩阵

思路：
m*n的矩阵可以视为长度为m*n的有序数组
有序数组中的位置idx = 矩阵中row = idx / n, col = idx % n。

步骤：
1、初始化左右序号
left = 0和right = m x n - 1.
2、While left < right:
选取虚数组最中间的序号作为中间序号:pivot_idx = (left + right) / 2.<br>
该序号对应于原矩阵中的row = pivot_idx // n行, col = pivot_idx % n列，由此拿到中间元素pivot_element。该元素将虚数组分为两部分。<br>
比较pivot_element与target以确定在哪一部分进行进一步查找<br>

执行用时 :68 ms, 在所有 javascript 提交中击败了59.03%的用户<br>
内存消耗 :34.2 MB, 在所有 javascript 提交中击败了65.91%的用户

```
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function(matrix, target) {
    let m = matrix.length;
    if (m === 0) return false;
    let n = matrix[0].length;

    let left = 0, right = m * n - 1;
    let pivotIdx, pivotElement;
    while (left <= right) {
        pivotIdx = ((left + right) >>> 1) >>> 0;
        pivotElement = matrix[pivotIdx / n >>> 0][pivotIdx % n];
        if (target === pivotElement) return true;
        else {
            if (target < pivotElement) right = pivotIdx - 1;
            else left = pivotIdx + 1;
        }
    }
    return false;
};
```
