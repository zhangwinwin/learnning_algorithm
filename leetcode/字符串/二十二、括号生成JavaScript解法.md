## 括号生成

### 解法
**动态规划**
在求N个括号的排列组合时，把第N种情况（也就是第N个括号的排列组合）视为单独拿一个括号E出来，剩下的N-1个括号分为两部分p个排列组合和q个排列组合。而且p+q=N-1， q和p均为自然数.然后这两部分分别处于E的内部和右边。

### 运行结果
执行用时 :68 ms, 在所有 javascript 提交中击败了86.18%的用户<br>
内存消耗 :34.7 MB, 在所有 javascript 提交中击败了76.14%的用户
```
/**
 * @param {number} n
 * @return {string[]}
 */
var generateParenthesis = function(n) {
    if (n === 0) {
        return [];
    }
    // 0组括号视为0,一组括号视为()
    let result = [['0'], ['()']];
    
    // 计算i组的情况
    for (let i=2; i<=n; i++) {
        let arr = []
        // 计算p和q， p+q=i-1
        for (let j=0; j<i; j++) {
            // p = j的情况
            let plist = result[j]
            // q = i-1-j的情况
            let qlist = result[i-1-j]
            for (let a of plist) {
                for (let b of qlist) {
                    if (b === '0') {
                        b = ''
                    }
                    if (a === '0') {
                        a = ''
                    }
                   arr.push('(' + b + ')' + a) 
                }
            }
        }
        result.push(arr)
    }
    return result[n]
};
```