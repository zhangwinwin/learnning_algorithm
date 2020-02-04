## 交错字符串
给定三个字符串 s1, s2, s3, 验证 s3 是否是由 s1 和 s2 交错组成的。  

示例 1:  

输入: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"  
输出: true  
示例 2:  
 
输入: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"  
输出: false  

```
/**
 * @param {string} s1
 * @param {string} s2
 * @param {string} s3
 * @return {boolean}
 */
var isInterleave = function(s1, s2, s3) {
    let len1 = s1.length, len2 = s2.length, len3 = s3.length;
    if (len1 + len2 !== len3) return false;
    let dp = Array(len2 + 1).fill(false);
    dp[0] = true;
    for (let i=0; i<=len1; ++i) {
        for (let j=0; j<=len2; ++j) {
            if (i>0 && s1[i-1] != s3[i+j-1]) {
                dp[j] = false;
            }
            if (j > 0 && s2[j-1] == s3[i+j-1]) {
                dp[j] = dp[j] || dp[j-1];
            }
        }
    }
    return dp[len2]
};
```