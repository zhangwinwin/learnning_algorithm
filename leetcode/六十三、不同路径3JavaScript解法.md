## 六十三、不同路径2

跟六十二题解法一样，只不过加了一些判断<br>

执行用时 :64 ms, 在所有 javascript 提交中击败了91.21%的用户<br>
内存消耗 :34.4 MB, 在所有 javascript 提交中击败了100.00%的用户

```
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    const left = obstacleGrid.length
    const right = obstacleGrid[0].length;
    let ans = new Array(right)
    ans.fill(0);
    ans[0] = 1;
    for (let i=0; i<left; i++) {
        for (let j=0; j<right; j++) {
            if (obstacleGrid[i][j] === 1) {
                ans[j] = 0;
            } else if (j > 0) {
                ans[j] += ans[j-1];
            }
        }
    }
    return ans[right - 1];
};
```