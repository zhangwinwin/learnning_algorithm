## 缺失的第一个整数
给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

示例 1:

输入: [1,2,0]
输出: 3
示例 2:

输入: [3,4,-1,1]
输出: 2
示例 3:

输入: [7,8,9,11,12]
输出: 1
说明:

你的算法的时间复杂度应为O(n)，并且只能使用常数级别的空间<br>

解题思路：<br>
算法：桶排序+基于异或运算交换两个变量的值<br>
思路分析：以[3,4,-1,1]为例<br>
3,4,-1,1<br>
0,1, 2,3<br>
*在索引0上的数字是3，它英国放索引2上，因此将索引0与索引2交换<br>
*循环<br>
*现在需要从头到尾看一遍，找出第一个做不和谐的元素，将其索引值+1返回<br>

1、把数组进行一次排序：如果这个数字i落在区间范围里，就应该放在索引为i-1的位置上。<br>
2、i就应该放在索引为i-1的位置上，或者说索引为i的位置上应该存放的数字为i+1。<br>
3、交换两个整数，基于异或运算是因为利用了异或是不进位的二进制加法，如下性质：<br>
如果a ^ b = c那么a ^ c = b与b ^ c = a同时成立<br>
a = a ^ b     a = a + b<br>
b = a ^ b     b = a - b<br>
a = a ^ b     a = a - b<br>

### 运行结果
执行用时 :60 ms, 在所有 javascript 提交中击败了96.70%的用户<br>
内存消耗 :34.2 MB, 在所有 javascript 提交中击败了60.29%的用户

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var firstMissingPositive = function(nums) {
    function swap (nums, index1, index2) {
        if (index1 === index2) return;
        nums[index1] = nums[index1] ^ nums[index2];
        nums[index2] = nums[index1] ^ nums[index2];
        nums[index1] = nums[index1] ^ nums[index2];
    }
    let len = nums.length;
    for (let i=0; i<len; i++) {
        while (1 <= nums[i] && nums[i] < len && nums[i] !== nums[nums[i] - 1]) {
            swap(nums, i, nums[i] - 1);
        }
    }
    for (let i=0; i<len; i++) {
        if (i+1 !== nums[i]) {
            return i+1;
        }
    }
    return len + 1;
};
```

