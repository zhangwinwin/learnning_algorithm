## 通配符匹配
给定一个字符串 (s) 和一个字符模式 (p) ，实现一个支持 '?' 和 '*' 的通配符匹配。

'?' 可以匹配任何单个字符。
'*' 可以匹配任意字符串（包括空字符串）。
两个字符串完全匹配才算匹配成功。

说明:

s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母，以及字符 ? 和 *。
示例 1:

输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。

```
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function(s, p) {
    let m = s.length, n = p.length;
    let f = [];
    f.length = m+1;
    f.fill(false)
    for (let i=0; i<m+1; i++) {
        f[i] = [];
        f[i].length = n+1;
        f[i].fill(false)
    }
    f[0][0] = true;
    
    for (let i=1; i<=n; i++) {
        f[0][i] = f[0][i-1] && p[i-1] === '*';
    } 
    for (let i=1; i<= m; i++) {
        for (let j=1; j<=n; j++) {
            if (s[i-1] === p[j-1] || p[j-1] === '?') {
                f[i][j] = f[i-1][j-1];
            }
            if (p[j-1] === '*') {
                f[i][j] = f[i][j-1] || f[i-1][j];
            }
        }
    }
    
    return f[m][n];
};
```