## 全排列

给定一个没有重复数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

### 解法：回溯搜索
深度优先遍历+状态重制+剪枝
只要按照顺序选取数字保证上-层选过的数字不在下一层出现就能够得到不重不漏的所有排列。得到使用一个数组长度这么长的额外空间，只要上层选了一个元素，就得到标记一下表示占位。

状态：在递归树里辅助数组used记录的情况和当前已经选出数组成为一个排列，统称状态
状态重置：在程序执行到上面这棵树的叶子节点的时候，此时递归到底，当前根节点到子叶节点，走过的路径就构成一个全排列，把它加载结果集，
1、结算递归返回释放最后一个数占用
2、将最后一个数从当前选取的排序中弹出。

执行用时 :64 ms, 在所有 javascript 提交中击败了99.89%的用户
内存消耗 :36.7 MB, 在所有 javascript 提交中击败了57.14%的用户


```
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
    let len = nums.length
    if (len === 0) return [];
    let used = [];
    used.length = len;
    used.fill(false);
    let res = [];
    dfs(nums, 0, [], used, res);
    return res;
    
    function dfs(nums, index, pre, used, res) {
        if (index === len) {
           res.push(pre.slice())
           return
        }
        for (let i=0; i<len; i++) {
            if (!used[i]) {
                used[i] = true
                pre.push(nums[i])
                dfs(nums, index+1, pre, used, res)
                used[i] = false
                pre.pop()
            }
        }
    
    }
};
```