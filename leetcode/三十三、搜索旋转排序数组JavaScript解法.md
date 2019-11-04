## 搜索旋转排序数组

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

示例 1:

输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
示例 2:

输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1

### 步骤
以二分法搜索为基本思路<br>
*nums[0] <= nums[mid] (0-min不包含旋转) 且nums[0] <= target <= nums[mid]时hight向前规约<br>
*nums[mid] <= nums[0](0-mid包含旋转)且target <= nums[mid] < nums[0]时向前规约（target在旋转位置到mid之间）<br>
*nums[mid] < nums[0]， nums[mid] < nums[0] <= target时向前规约（target在0到旋转位置之间）<br>
*其他情况向后规约<br>
也就是nums[mid] < nums[0], nums[0] > target, target > nums[mid]三项为真或者一项为真向后规约<br>

注意到原数组为有限制的有序数组<br>
*if nums[0] <= nums[i] 那么nums[0]到nums[i]之间为有序数组，那么当nums[0] <= target <= nums[i]应该在0-i范围内查找<br>
*if nums[i] < nums[0]那么在0-i区间的某个点处发生了下降，那么i+1到最后一个数字的区间为有序数组并且所有数字都是小于nums[0]且大于nums[i]当target不属于nums[0]到nums[i]时<br>
target <= nums[i] < nums[0] or nums[i] < nums[0] < target, 在0-i内查找<br>

执行用时 :48 ms, 在所有 javascript 提交中击败了99.88%的用户<br>
内存消耗 :33.6 MB, 在所有 javascript 提交中击败了62.03%的用户

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    let low = 0, hight = nums.length - 1;
    while (low < hight) {
        let middle = Math.floor((low + hight) / 2);
        if ((nums[0] > target) ^ (nums[0] > nums[middle]) ^ (target > nums[middle])) {
            low = middle + 1
        } else {
            hight = middle;
        }
    }
    return low === hight && nums[low] === target ? low : -1;
};
```