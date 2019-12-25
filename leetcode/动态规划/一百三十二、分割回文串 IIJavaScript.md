## 分割回文串 II
给定一个字符串 s，将 s 分割成一些子串，使每个子串都是回文串。  

返回符合要求的最少分割次数。  

示例:  

输入: "aab"  
输出: 1  
解释: 进行一次分割就可将 s 分割成 ["aa","b"] 这样两个回文子串。  

```
/**
 * @param {string} s
 * @return {number}
 */
var minCut = function(s) {
    let len = s.length;
    let dp = Array.from(new Array(len), () => new Array(len));
    let min = Array(len);
    min[0] = 0;
    for (let i=1; i<len; i++) {
        let temp = Number.MAX_VALUE;
        for (let j=0; j<=i; j++) {
            if (s[j] === s[i] && (j+1>i-1 || dp[j+1][i-1])) {
                dp[j][i] = true;
                if (j === 0) {
                    temp = 0;
                } else {
                    temp = Math.min(temp, min[j-1] + 1);
                }
            }
        }
        min[i] = temp;
    }
    return min[len - 1];
};
```