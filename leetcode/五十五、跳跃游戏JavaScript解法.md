## 跳跃游戏
给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

示例 1:

输入: [2,3,1,1,4]
输出: true
解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。
示例 2:

输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。


### 解法：贪婪算法
从某个位置出发，只需要找到第一个标记为GOOD的坐标，也就是说找到最左边的那个坐标，用一个变量来记录最左边GOOD位置。
从右向左迭代，对每个节点检查是否存在一步跳跃可以达到GOOD的位置(currP + nums[currP] >= leftMoreGoodIndex)。 如果能达到也标为GOOD。同时将这个位置成为最左边GOOD，一直重复到开头。<br>

执行用时 :52 ms, 在所有 javascript 提交中击败了99.43%的用户<br>
内存消耗 :35.6 MB, 在所有 javascript 提交中击败了47.83%的用户

```
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canJump = function(nums) {
    let lastPos = nums.length - 1;
    for (let i = lastPos; i >= 0; i--) {
        if (i + nums[i] >= lastPos) {
            lastPos = i;
        }
    }
    return lastPos == 0;
};
```