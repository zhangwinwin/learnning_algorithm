## 152、乘积最大子序列
给定一个整数数组 nums ，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）。  

示例 1:  

输入: [2,3,-2,4]  
输出: 6  
解释: 子数组 [2,3] 有最大乘积 6。  
示例 2:  

输入: [-2,0,-1]  
输出: 0  
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。  

### 解法：动态规划  

先定义一个数组dpmax，用dpmax[i]表示以第i的元素结尾的子数组中乘积最大的值，也就是这个数组必须包含第i个元素。  
那么dpmax[i]的取值：  
* 当nums[i] >= 0并且dpmax[i-1] > 0, dpmax[i] = dpmax[i-1] * nums[i]  
* 当nums[i] >= 0并且dpmax[i-1] < 0, dpmax[i] = nums[i]  
* 当nums[i] < 0 此时如果前边累积乘的结果是一个很大的负数，和当前负数累乘的话就变成一个更大的数。所以还需要一个数组dpmin来记录以第i个元素结尾的子数组，乘积最小的值。  当dpmin[i-1] < 0, dpmin[i] = dpmin[i-1] * nums[i]. 当dpmax[i-1] >= 0, dpmax[i] = nums[i].  

dpmax[i] = max(dpmax[i-1] * nums[i], dpmin[i-1] * nums[i], nums[i])  
求dpmin[i]同理  
dpmin[i] = min(dpmax[i-1] * nums[i], dpmin[i-1] * nums[i], nums[i])  
更新过程中，还用一个变量max去保存当前得到的最大值。  

注意到更新 dp[i] 的时候，我们只用到 dp[i-1] 的信息，再之前的信息就用不到了。所以我们完全不需要一个数组，只需要一个变量去重复覆盖更新即可。


```
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function(nums) {
    if (nums.length === 0) return 0;
    let dpmax = nums[0], dpmin = nums[0], max = nums[0];
    for (let i=1; i<nums.length; i++) {
        let preMax = dpmax;
        dpmax = Math.max(dpmin * nums[i], Math.max(dpmax * nums[i], nums[i]));
        dpmin = Math.min(dpmin * nums[i], Math.min(preMax * nums[i], nums[i]));
        max = Math.max(max, dpmax)
    }
    return max;
};
```
