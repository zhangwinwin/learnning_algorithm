## 螺旋矩阵
给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

示例 1:

输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
输出: [1,2,3,6,9,8,7,4,5]
示例 2:

输入:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
输出: [1,2,3,4,8,12,11,10,9,5,6,7]

### 步骤
1、首先定义上下左右边界<br>
2、其次向右移动到最右，此时第一行使用过了，可以将其删除，就是重新定义上边界<br>
3、判断上下边界是否交错，如果交错，则表明遍历结算。<br>
4、若不交错，接着向下，向左，向上移动，重复第一第二步骤<br>
5、直到上下边界交错

```
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
    let ans = [];
    let len = matrix.length
    if (len === 0) return [];
    let u = 0, d = len - 1, l = 0, r = matrix[0].length - 1;
    while (true) {
        for (let i = l; i <= r; ++i) {
            ans.push(matrix[u][i]) // 向右移动直到最右
        }
        if (++u > d) break; // 重新设定上边界，若上边界大于下边界，则遍历完成
        for (let i = u; i <= d; ++i) {
            ans.push(matrix[i][r])
        }
        if (--r < l) break;
        for (let i = r; i >= l; --i) {
            ans.push(matrix[d][i])
        }
        if (--d < u) break
        for (let i = d; i>= u; --i) {
            ans.push(matrix[i][l])
        }
        if (++l > r) break
    }
    return ans;
};
```