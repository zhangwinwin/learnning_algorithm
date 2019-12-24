## 买卖股票的最佳时机 III

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。<br>

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。<br>

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。<br>

示例 1:<br>

输入: [3,3,5,0,0,3,1,4]<br>
输出: 6<br>
解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。<br>
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。<br>
示例 2:<br>

输入: [1,2,3,4,5]<br>
输出: 4<br>
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   <br>
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   <br>
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。<br>

```
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    const n = prices.length;
    if (n === 0) return 0;
    const K = 2;
    const dp = Array.from(new Array(n), () => new Array(K+1));
    for (let i=0; i<n; i++) {
        for (let k=0; k<=K; k++) {
            dp[i][k] = new Array(2).fill(0);
        }
    }
    for (let i=0; i<n; i++) {
        for (let k=K; k>=1; k--) {
            if (i == 0) {
                dp[i][k][0] = 0;
                dp[i][k][1] = -prices[i];
                continue;
            }
            dp[i][k][0] = Math.max(dp[i-1][k][0], dp[i-1][k][1] + prices[i]);
            dp[i][k][1] = Math.max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i])
        }
    }
    return dp[n-1][K][0]
};
```