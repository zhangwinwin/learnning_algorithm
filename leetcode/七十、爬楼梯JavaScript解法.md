##  爬楼梯

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：

输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
示例 2：

输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶

### 思路：
1. 动态规划
这个问题可以被分解为一些包含最优子结构的子问题，即它的最优解可以从其子问题的最优解来有效地构建，可以使用动态规划来解决这一问题。
第i阶可以由以下两种方法得到：
1、在第（i-1）阶后向上爬一阶
2、在第（i-2）阶后向上爬2阶
所以到达第i阶的方法总数就是到第（i-1）阶和第（i-2）阶的方法数之和
令dp[i]表示能到达第i阶的方法总数：
dp[i]=dp[i-1]+dp[i-2]

```
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
    if (n === 1) return 1;
    let dp = Array(n + 1);
    dp.fill(0);
    dp[1] = 1;
    dp[2] = 2;
    for (let i=3; i<=n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
};
```

2、斐波那契数列
在上述方法中，使用了dp数组，其中dp[i]=dp[i-1]+dp[i-2]。很容易通过分析得出dp[i]七十就是第i和斐波那契数。
fib(n) = fib(n-1) + fib(n-2)

```
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
    if (n === 1) return 1;
    let first = 1;
    let second = 2;
    for (let i=3; i<=n; i++) {
        let third = first + second;
        first = second;
        second = third;
    }
    return second;
};
```
