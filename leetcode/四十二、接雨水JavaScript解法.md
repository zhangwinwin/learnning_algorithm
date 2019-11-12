## 接雨水
给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

示例:

输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6

解法：动态规划+双指针<br>
求每一列的水，只需要关注当前列，以及左边最高列，右边最高列的的高度就够了。可分为三种情况<br>
*较矮墙高度大于当前列的高度 -》 有水<br>
*较矮墙高度小于当前列的高度 -》 没有水<br>
*较矮墙高度等于当前列的高度 -》 没有水<br>
对于每一列， 求它最左边最高墙和右边最高墙，都是重新遍历所有高度。<br>
首先用两个数组，max_left[i]代表i列最高墙的高度，max_right[i]代表i列右边最高墙高度。<br>
对于max_right: max_right[i] = Math.max(max_right[i + 1], height[i+ 1]).<br>
右边墙高度和后边墙高度选一个最大的。<br>

双指针：可以看到，max_left[i]和max_right[i]数组中的元素都是只用一次，所以不用数组，只用一个元素就行。<br>

执行用时 :76 ms, 在所有 javascript 提交中击败了73.68%的用户<br>
内存消耗 :35.1 MB, 在所有 javascript 提交中击败了59.02%的用户

```
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function(height) {
    let sum = 0;
    let max_left = 0;
    let max_right = 0;
    let left = 1;
    let right = height.length - 2; // 加右指针进去
    for (let i = 1; i< height.length - 1; i++) {
        // 从左到右更
        if (height[left - 1] < height[right + 1]) {
            max_left = Math.max(max_left, height[left - 1]);
            let min = max_left;
            if (min > height[left]) {
                sum = sum + (min - height[left])
            }
            left++;
        // 从右到左更
        } else {
            max_right = Math.max(max_right, height[right + 1]);
            let min = max_right;
            if (min > height[right]) {
                sum = sum + (min - height[right]);
            }
            right--
        }
    }
    return sum
};
```
