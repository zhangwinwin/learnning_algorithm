## 最大矩形

### 思路
对于每个点我们会通过以下步骤计算一个矩形：  
* 不断向上方遍历，直到遇到“0”，以此找到矩形的最大高度。
* 向左右两边扩展，直到无法容纳矩形最大高度。 

```
/**
 * @param {character[][]} matrix
 * @return {number}
 */
var maximalRectangle = function(matrix) {
    if(matrix.length === 0) return 0;
    let m = matrix.length, n = matrix[0].length;
    let left = Array(n);
    let right = Array(n);
    let height = Array(n);

    left.fill(0);
    height.fill(0);
    right.fill(n);
    let maxarea = 0;

    for (let i=0; i<m; i++) {
        let cur_left = 0, cur_right = n;
        for (let j=0; j<n; j++) {
            if (matrix[i][j] === '1') height[j]++;
            else height[j] = 0;
        }
        for (let j=0; j<n; j++) {
            if (matrix[i][j] === '1') left[j] = Math.max(left[j], cur_left);
            else {
                left[j] = 0;
                cur_left = j+1;
            }
        }
        for (let j=n-1; j>=0; j--) {
            if (matrix[i][j] === '1') right[i] = Math.min(right[j], cur_right);
            else {
                right[j] = n;
                cur_right = j;
            }
        }
        for (let j=0; j<n; j++) {
            maxarea = Math.max(maxarea, (right[j] - left[j]) * height[j]);
        }
    }
    return maxarea;
};
```