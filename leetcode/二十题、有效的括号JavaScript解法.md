## 有效的括号
**解法**
维护一个栈和散列表。散列表里增加[')', '(']、['}','{']、[']', '[']。循环字符串中的每个值。如果是左括号则push进栈中，如果是右括号则将栈中的首元素pop出来对比，如果相同则继续，否则return false。

**复杂度分析**
时间复杂度：O(n)O(n)，因为我们一次只遍历给定的字符串中的一个字符并在栈上进行 O(1)O(1) 的推入和弹出操作。
空间复杂度：O(n)O(n)，当我们将所有的开括号都推到栈上时以及在最糟糕的情况下，我们最终要把所有括号推到栈上。

**执行结果**
执行用时 :52 ms, 在所有 javascript 提交中击败了99.85%的用户
内存消耗 :33.6 MB, 在所有 javascript 提交中击败了86.47%的用户
```
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    const containMap = new Map([[')', '('], ['}', '{'], [']', '[']]);
    let stackArr = [];
    let topElement = ''
    for (let i=0; i<s.length; i++) {
        let str = s[i];
        if (containMap.has(str)) {
            topElement = stackArr.length == 0 ? '#' : stackArr.pop();
            if (topElement != containMap.get(str)) {
                return false
            }
        } else {
            stackArr.push(str)
        }
    }
    return stackArr.length === 0;
};
```
