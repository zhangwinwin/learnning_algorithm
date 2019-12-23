## 买卖股票的最佳时机

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。  

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。  

注意你不能在买入股票前卖出股票。  

示例 1:  

输入: [7,1,5,3,6,4]  
输出: 5  
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。  
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。  
示例 2:  

输入: [7,6,4,3,1]  
输出: 0  
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。  

### 思路
解法一、这是一个最大连续子数组和的问题，可以用动态规划来解决。  
dp[i]表示以i结尾的最大连续子数组和  
递推公式： dp[i] = Math.max(0, dp[i-1])  
```
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let len = prices.length
    if (len <= 1) return 0;
    let diff = Array(len - 1)
    for (let i=0; i<len-1; ++i) {
        diff[i] = prices[i+1] - prices[i];
    }
    let dp = Array(len-1);
    dp[0] = Math.max(0, diff[0]);
    let profit = dp[0];
    for (let i=1; i<len-1; ++i) {
        dp[i] = Math.max(0, dp[i-1] + diff[i]);
        profit = Math.max(profit, dp[i])
    }
    return profit;
};
```

解法二、去掉dp  
执行用时 :72 ms, 在所有 javascript 提交中击败了74.06%的用户  
内存消耗 :35.3 MB, 在所有 javascript 提交中击败了51.39%的用户  
```
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let len = prices.length
    if (len <= 1) return 0;
    let diff = Array(len - 1)
    for (let i=0; i<len-1; ++i) {
        diff[i] = prices[i+1] - prices[i];
    }
    let last = 0;
    let profit = last;
    for (let i=0; i<len-1; ++i) {
        last = Math.max(0, last + diff[i]);
        profit = Math.max(profit, last)
    }
    return profit;
};
```
