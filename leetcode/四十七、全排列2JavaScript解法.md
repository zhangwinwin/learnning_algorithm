##  全排列2
给定一个可包含重复数字的序列，返回所有不重复的全排列。

示例:

输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

### 解法： 回溯+剪枝
基于46题，做两处修改即可<br>
1、开始回溯之前，对数组进行排序<br>
2、在进入新分支之前，看看这个数是不是和之前的数一样，并且之前的数还没使用过，那接下来如果走这个分支，就会使用到之前那个和当前一样的数，就会发生重复。<br>

执行用时 :84 ms, 在所有 javascript 提交中击败了96.73%的用户<br>
内存消耗 :37.4 MB, 在所有 javascript 提交中击败了77.97%的用户<br>

```
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function(nums) {
    let len = nums.length
    if (len === 0) return [];
    
    // 排序
    nums.sort((a, b) => a - b);
    
    let used = [];
    used.length = len;
    used.fill(false);
    let res = [];
    dfs(nums, 0, [], used, res);
    return res;
    
    function dfs(nums, index, pre, used, res) {
        if (index === len) {
            res.push(pre.slice());
            return
        }
        for (let i=0; i<len; i++) {
            if (!used[i]) {
                // 因为排序以后重复的数一定不会出现，i>0
                if (i>0 && nums[i] === nums[i-1] && !used[i-1]) continue;
                used[i] = true;
                pre.push(nums[i]);
                dfs(nums, index + 1, pre, used, res);
                used[i] = false;
                pre.pop()
            }
        }
    }
};
```