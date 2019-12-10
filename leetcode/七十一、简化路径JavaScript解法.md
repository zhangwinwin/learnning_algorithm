## 简化路径
以 Unix 风格给出一个文件的绝对路径，你需要简化它。或者换句话说，将其转换为规范路径。

在 Unix 风格的文件系统中，一个点（.）表示当前目录本身；此外，两个点 （..） 表示将目录切换到上一级（指向父目录）；两者都可以是复杂相对路径的组成部分。更多信息请参阅：Linux / Unix中的绝对路径 vs 相对路径

请注意，返回的规范路径必须始终以斜杠 / 开头，并且两个目录名之间必须只有一个斜杠 /。最后一个目录名（如果存在）不能以 / 结尾。此外，规范路径必须是表示绝对路径的最短字符串。

 

示例 1：

输入："/home/"
输出："/home"
解释：注意，最后一个目录名后面没有斜杠。

### 思路
定义一个辅助栈
先把字符串以'/'为分割符分割成数组，此时数据有路径、''、'.'、'..'这四种情况
遍历数组，当元素为'..'并且栈不空时pop，当元素不等于''且不等于'.'且不等于'..'就把元素入栈
栈空，返回/，栈非空，返回字符串即可.

```
/**
 * @param {string} path
 * @return {string}
 */
var simplifyPath = function(path) {
    const arr = path.split('/');
    const ans = [];
    for (let i=0; i < arr.length; i++) {
        if (!!ans && arr[i] === '..') {
            ans.pop()
        } else if (arr[i] !== '' && arr[i] !== '.' && arr[i] !== '..') {
            ans.push(arr[i])
        }
    }
    if (ans.length === 0) return '/'
    let res = '';
    for (let i=0; i<ans.length; i++) {
        res = res + '/' + ans[i]
    }
    return res
};
```