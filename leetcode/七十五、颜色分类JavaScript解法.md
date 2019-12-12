## 颜色分类

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

示例:

输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]

### 思路：
沿着数组curr指针，若nums[curr] = 0, 则将其与nums[p0]互换;若nums[curr] = 2,则与nums[p2]互换

```
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let p0 = 0, curr = 0;
    let p2 = nums.length - 1;
    let tmp;
    while (curr <= p2) {
        if (nums[curr] === 0) {
            tmp = nums[p0];
            nums[p0++] = nums[curr];
            nums[curr++] = tmp;
        } else if (nums[curr] === 2) {
            tmp = nums[curr];
            nums[curr] = nums[p2];
            nums[p2--] = tmp;
        } else {
            curr++;
        }
    }
};
```