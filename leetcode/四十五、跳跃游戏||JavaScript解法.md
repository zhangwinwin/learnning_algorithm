## 跳跃游戏||

给定一个非负整数数组，你最初位于数组的第一个位置。<br>

数组中的每个元素代表你在该位置可以跳跃的最大长度。<br>

你的目标是使用最少的跳跃次数到达数组的最后一个位置。<br>

示例:

输入: [2,3,1,1,4]<br>
输出: 2<br>
解释: 跳到最后一个位置的最小跳跃数是 2。<br>
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。<br>
说明:

假设你总是可以到达数组的最后一个位置。<br>

### 贪婪算法
每次在可跳范围内选择可以使得跳的更远的位置<br>
举例[2,3,1,1,4]<br>
开始的位置为2， 可跳的范围是3，1，因为3可以跳的更远，所以跳到3的位置<br>
然后位置是3，因为4可以跳的更远，所以跳到4的位置<br>

执行用时 :68 ms, 在所有 javascript 提交中击败了88.79%的用户<br>
内存消耗 :35.5 MB, 在所有 javascript 提交中击败了49.02%的用户

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function(nums) {
    let end = 0;
    let maxPosition = 0;
    let steps = 0;
    for (let i = 0; i< nums.length -1; i++) {
        maxPosition = Math.max(maxPosition, nums[i] + i);
        if (i === end) {
            end = maxPosition;
            steps++;
        }
    }
    return steps
};
```