## 下一个排序

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。<br>

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。<br>

必须原地修改，只允许使用额外常数空间。<br>

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。<br>
1,2,3 → 1,3,2<br>
3,2,1 → 1,2,3<br>
1,1,5 → 1,5,1<br>

执行用时 :72 ms, 在所有 javascript 提交中击败了93.61%的用户<br>
内存消耗 :34.7 MB, 在所有 javascript 提交中击败了55.56%的用户
```
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var nextPermutation = function(nums) {
    let i = nums.length - 2;
    while (i>=0 && nums[i+1] <= nums[i]) {
        i--;
    }
    if (i >= 0) {
        let j = nums.length - 1;
        while (j>=0 && nums[j] <= nums[i]) {
            j--;
        }
        swap(nums, i, j);
    }
    reverse(nums, i+1)
};

function swap (nums, i, j) {
    let temp = nums[i]
    nums[i] = nums[j]
    nums[j] = temp
}

function reverse (nums, start) {
    let i = start, j = nums.length - 1;
    while (i < j) {
        swap(nums, i, j);
        i++;
        j--;
    }
}
```