给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

示例 1:

nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
示例 2:

nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5

思路：
两个数组A(长度为m)和B(长度为n)
首先用任意位置的i将A划分为两个部分
leftA = [A[0], A[1], ... , A[i-1]]
rightA = [A[i], A[i+1], ... , A[m]]
由于A的长度为m，所以有m+1中划法, i = [0, m]
同样划分B
leftB = [B[0], B[1, ... ,B[j-1]]]
rightB = [B[j], B[j+1], ... , B[n]]

将leftA和leftB放在一起形成left_path
将rihgtA和rightB放在一起形成rihgt_path
如果我们可以确认
len(left_path) = len(right_path)
max(left_path) <= min(right_path)
那么：
mediam = (max(left_path) + min(right_path)) / 2

要确保这两个条件，只需
1、i + j = m - i + n - j
2、B|j - 1| <= A[i] 且 A[i - 1] <= B[j]

/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
执行用时 :124 ms, 在所有 JavaScript 提交中击败了98.07%的用户
内存消耗 :38.6 MB, 在所有 JavaScript 提交中击败了96.90%的用户
var findMedianSortedArrays = function(nums1, nums2) {
    let m = nums1.length, n = nums2.length;
    if (m > n) {
        let temp = nums1;
        nums1 = nums2;
        nums2 = temp;
        let a = m;
        m = n;
        n = a;
    }
    let iMin = 0, iMax = m, halfLen = Math.floor((m + n + 1) / 2);
    while (iMin <= iMax) {
        let i = Math.floor((iMin + iMax) / 2);
        let j = halfLen - i;
        if (i < iMax && nums1[i] < nums2[j-1]) {
            iMin = i + 1;
        } else if (i > iMin && nums2[j] < nums1[i-1]) {
            iMax = i - 1;
        } else {
            let leftMax = 0;
            if (i === 0) {
                leftMax = nums2[j-1];
            } else if (j === 0) {
                leftMax = nums1[i-1];
            } else {
                leftMax = Math.max(nums1[i-1], nums2[j-1]);
            }
            if ((n + m) % 2 === 1) {
                return leftMax;
            }
            
            let rightMin = 0;
            if (i === m) {
                rightMin = nums2[j];
            } else if (j === n) {
                rightMin = nums1[i];
            } else {
                rightMin = Math.min(nums1[i], nums2[j]);
            }
            return (leftMax + rightMin) / 2.0;
        }
    }
    return 0.0;
};
