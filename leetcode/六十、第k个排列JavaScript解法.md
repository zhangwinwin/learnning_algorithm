给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：

"123"
"132"
"213"
"231"
"312"
"321"
给定 n 和 k，返回第 k 个排列。

说明：

给定 n 的范围是 [1, 9]。
给定 k 的范围是[1,  n!]。
示例 1:

输入: n = 3, k = 3
输出: "213"
示例 2:

输入: n = 4, k = 9
输出: "2314"

### 思路
假设n=5， k=35
n为5的全排列就是首位为1-5，每个各有24的排列，组成12345全排列<br>
由于k=35<48，也就是说第35个肯定在首位为2的全排列里边，所以第一个取2.<br>
接下来就是考虑剩下1345这四个数的全排列里边取第k=35-24=11个，<br>
1345每个各有6个排列，组成1345的全排列<br>
由于k=11<12，也就是说第11个肯定在首位为3的全排列里边，所以第二哥数取3<br>
接下来就是考虑剩下145这三个数的全排列里边取k=11-6=5个<br>
145每个各有2个排列，<br>
由于k=5<6，也就是说第5个肯定在首位为5的全排列里边，所以第三个数取5<br>
如下推理<br>
结果就是23514

执行用时 :64 ms, 在所有 javascript 提交中击败了91.47%的用户<br>
内存消耗 :33.8 MB, 在所有 javascript 提交中击败了70.42%的用户

```
/**
 * @param {number} n
 * @param {number} k
 * @return {string}
 */
var getPermutation = function(n, k) {
    let nums = [];
    let factor = [1,1,2,6,24,120,720,5040,40320,362880];
    for (let i=1; i<=n; i++) {
        nums.push(i)
    }
    let answer = '';
    let interval, loop_times = n;
    for (let i=0; i<loop_times; i++) {
        --n;
        interval = ((k-1) / factor[n]) >>> 0;
        answer += nums[interval];
        nums.splice(interval, 1);
        k = k - interval * factor[n];
    }
    return answer;
};
```