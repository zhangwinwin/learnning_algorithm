## x的平方根

实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

示例 1:

输入: 4
输出: 2
示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。<br>

思路：
使用二分法搜索。首先明确条件：一个数的平方根肯定不会超过自己，而且一个数的平方根最多不会超过它的一般。例如8的平方根，8的一般是4，4*4=16>8。
所以得出(a/2)*(a/2) >= a
如果一个数的一半的平方大于它自己，那么这个数的取值范围。a>=4或者a<=0.<br>

执行用时 :68 ms, 在所有 javascript 提交中击败了98.99%的用户<br>
内存消耗 :35.4 MB, 在所有 javascript 提交中击败了71.15%的用户

```
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
    if (x === 0) return 0;
    let left = 1;
    let right = x / 2 >>> 0;
    while (left < right) {
        let mid = (left + right + 1) >>> 1;
        let square = mid * mid;
        if (square > x) {
            right = mid - 1;
        } else {
            left = mid;
        }
    }
    return left >>> 0;
};
```


