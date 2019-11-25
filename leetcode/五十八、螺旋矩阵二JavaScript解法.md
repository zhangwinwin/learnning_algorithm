## 螺旋矩阵二

给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

示例:

输入: 3
输出:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]

思路：
生成一个n*n空矩阵mat，随后模拟整个向内环绕的填入过程：
1、定义当前的上下左右边界，初始值为num = 1, 迭代值tar=n*n；
2、当num<=tar时，始终按照从左到右，从上到下，从右到左，从下到上填入顺序循环，每次填入后：
21、执行num+=1:得到下一个需要填入的数字；
22、更新边界：例如从左到右填完后，上边界t+=1，相当于上边界向内缩1
3、使用num<=tar而不是l<r || t<b作为迭代条件，是为了解决当n为奇数时，矩阵中心数字无法在迭代过程中被填充的问题。
4、最终返回mat即可.<br>

执行用时 :64 ms, 在所有 javascript 提交中击败了75.83%的用户<br>
内存消耗 :33.7 MB, 在所有 javascript 提交中击败了47.30%的用户

```
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    let l=0, r=n-1, t=0, b=n-1;
    let mat = new Array(n);
    for (let i=0; i<n; i++) {
        mat[i] = new Array(n);
    }
    let num = 1, tar = n * n;
    while(num <= tar) {
        for(let i = l; i <= r; i++) mat[t][i] = num++; // left to right.
        t++;
        for(let i = t; i <= b; i++) mat[i][r] = num++; // top to bottom.
        r--;
        for(let i = r; i >= l; i--) mat[b][i] = num++; // right to left.
        b--;
        for(let i = b; i >= t; i--) mat[i][l] = num++; // bottom to top.
        l++;
    }
    return mat;
};
```