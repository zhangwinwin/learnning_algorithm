## 单词拆分
给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。  

说明：  

拆分时可以重复使用字典中的单词。  
你可以假设字典中没有重复的单词。  
示例 1：  

输入: s = "leetcode", wordDict = ["leet", "code"]  
输出: true  
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。  
示例 2：  

输入: s = "applepenapple", wordDict = ["apple", "pen"]  
输出: true  
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。  
     注意你可以重复使用字典中的单词。  

### 解法：动态规划
对于给定的字符串s可以被拆分为子问题s1和s2.如果子问题都可以独立地拆分符号要求，那么s也符合要求。  
使用i，j。其中i表示当前字符串从头开始的子字符串s的长度，j是当前子字符串s的拆分位置。拆分为s(0, j)和s(j+1, i)  

初始化dp[0]为true，因为空字符串总是字典的一部分。  

对每一个子字符串，通过下标j将它拆分为s1和s2.依此检查每个dp[j]是否为true。如果满足就接着检查s2。如果两个字符串都满足要求，dp[i] = true. 

```
/*
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function(s, wordDict) {
    let len = s.length;
    let dp = Array(len+1).fill(false);
    dp[0] = true;
    for (let i=1; i<=len; i++) {
        for (let j=0; j<i; j++) {
            if (dp[j] && wordDict.includes(s.substring(j, i))) {
                dp[i] = true;
                break;
            }
        }
    }
    return dp[len];
};
```