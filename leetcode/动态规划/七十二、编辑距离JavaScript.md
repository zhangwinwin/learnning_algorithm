## 七十二、编辑距离
给定两个单词 word1 和 word2，计算出将 word1 转换成 word2 所使用的最少操作数 。  
你可以对一个单词进行如下三种操作：  
插入一个字符  
删除一个字符  
替换一个字符  
示例 1:  
输入: word1 = "horse", word2 = "ros"  
输出: 3  
解释:   
horse -> rorse (将 'h' 替换为 'r')  
rorse -> rose (删除 'r')  
rose -> ros (删除 'e')  
### 思路
1、定义数组元素含义  
dp[i][j]:当字符串word1的长度为i，字符串word2的长度为j，则最少操作数为dp[i][j]  
2、数组间的关系式  
如果word1[i]和word2[j]相等，则dp[i][j] = dp[i-1][j-1]  
如果word1[i]不等于word2[j],可以对word1进行三种操作：插入、删除、替换  
* 替换： dp[i][j] = dp[i-1][j-1] + 1  
* 删除： dp[i][j] = dp[i-1][j] + 1  
* 插入： dp[i][j] = dp[i][j-1] + 1  
3、找出初始值  
当i=0，j=0时运用以上公式都不能得出正确数值，所以都得是必须知道的初始值。  

执行用时 :88 ms, 在所有 javascript 提交中击败了95.41%的用户  
内存消耗 :41.2 MB, 在所有 javascript 提交中击败了55.17%的用户

```
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function(word1, word2) {
    let n = word1.length, m = word2.length;
    let dp = Array(n+1);
    for (let i=0; i<=n; i++) {
        dp[i] = Array(m);
        for (let j=0; j<=m; j++) {
            dp[i][j] = 0
        }
    };
    for (let i=1; i<=n; i++) {
        dp[i][0] = dp[i-1][0] + 1;
    }
    for (let j=1; j<=m; j++) {
        dp[0][j] = dp[0][j-1] + 1;
    }
    for (let i=1; i<=n; i++) {
        for (let j=1; j<=m; j++) {
            if (word1[i-1] === word2[j-1]) {
                dp[i][j] = dp[i-1][j-1];
            } else {
                dp[i][j] = Math.min((dp[i-1][j-1]+1), (dp[i-1][j]+1), (dp[i][j-1]+1))
            }
        }
    }
    return dp[n][m]
};
```

### 优化
当计算第i行的值时，只需要第i-1行的数值，不需要依赖第i-2行的值。所以能用一维数组来解决。  
所以推导公式从dp[i][j] = Math.min((dp[i-1][j-1]+1), (dp[i-1][j]+1), (dp[i][j-1]+1))变成dp[i] = Math.min(dp[i-1], pre, dp[i])  

执行用时 :88 ms, 在所有 javascript 提交中击败了95.41%的用户  
内存消耗 :36.4 MB, 在所有 javascript 提交中击败了100.00%的用户

```
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function(word1, word2) {
    let n = word1.length, m = word2.length;
    let dp = Array(m+1);
    for (let j=0; j<=m; j++) {
        dp[j] = j
    }
    for (let i=1; i<=n; i++) {
        let temp = dp[0]
        dp[0] = i;
        for (let j=1; j<=m; j++) {
            let pre = temp;
            temp = dp[j]
            if (word1[i-1] === word2[j-1]) {
                dp[j] = pre
            } else {
                dp[j] = Math.min(dp[j], pre, dp[j-1]) + 1;
            }
        }
    }
    return dp[m]
};
```