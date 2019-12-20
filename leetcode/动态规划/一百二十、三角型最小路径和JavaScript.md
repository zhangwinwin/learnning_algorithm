## 三角形最小路径和

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。  

例如，给定三角形：  
```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。  

执行用时 :64 ms, 在所有 javascript 提交中击败了83.71%的用户  
内存消耗 :35.3 MB, 在所有 javascript 提交中击败了16.05%的用户

```
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
    for(let i=triangle.length-2; i>=0; i--) {
        for (let j=0; j<triangle[i].length; j++) {
            triangle[i][j] = Math.min(triangle[i+1][j], triangle[i+1][j+1]) + triangle[i][j];
        }
    }
    return triangle[0][0]
};
```