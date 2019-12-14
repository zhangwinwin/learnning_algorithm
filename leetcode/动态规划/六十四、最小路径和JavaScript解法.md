## 最小路径和

### 解题思路：动态规划
状态定义：设dp为大小m * n矩阵，其中dp[i][j]的值代表直到走到(i,j)的最小路径和。
转移方程：走到当前单元格(i, j)的最小路径和="从左方单元格(i-1, j)与上方单元格(i, j-1）走来的两个最小路径和中较小的" + 当前单元格值grid[i][j]。具体分为4中情况：
1、当左边和上边都不是矩阵边界时：即当i != 0, j!=0时，dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
2、当只有左边是矩阵边界时：只能从上面来，即当i=0,j!=0时，dp[i][j] = dp[i][j-1] + grid[i][j];
3、当只有上边是矩阵边界时：只能从左面来，即当i!=0, j=0时，dp[i][j] = do[i-1][j] + gridp[i][j];
4、当左边和上边都是矩阵边界时：即当i=0, j=0时，其实就是起点,dp[i][j] = grid[i][j]

执行用时 :64 ms, 在所有 javascript 提交中击败了93.32%的用户<br>
内存消耗 :35.6 MB, 在所有 javascript 提交中击败了80.30%的用户

```
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
    for (let i=0; i<grid.length; i++) {
        for (let j=0; j<grid[0].length; j++) {
            if (i === 0 && j === 0) continue;
            else if (i === 0) grid[i][j] = grid[i][j-1] + grid[i][j];
            else if (j === 0) grid[i][j] = grid[i-1][j] + grid[i][j];
            else grid[i][j] = Math.min(grid[i-1][j], grid[i][j-1]) + grid[i][j]
        }
    }
    return grid[grid.length - 1][grid[0].length - 1]
};
```