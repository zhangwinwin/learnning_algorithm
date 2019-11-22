## 插入区间
给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

示例 1:

输入: intervals = [[1,3],[6,9]], newInterval = [2,5]
输出: [[1,5],[6,9]]
示例 2:

输入: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出: [[1,2],[3,10],[12,16]]
解释: 这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。

<br>
执行用时 :80 ms, 在所有 javascript 提交中击败了81.69%的用户<br>
内存消耗 :37.5 MB, 在所有 javascript 提交中击败了42.42%的用户

```
/**
 * @param {number[][]} intervals
 * @param {number[]} newInterval
 * @return {number[][]}
 */
var insert = function(intervals, newInterval) {
    intervals.push(newInterval);
    intervals.sort((a, b) => a[0]-b[0]);
    let res = [];
    let len = intervals.length;
    let i=0, left=0, right=0;
    while (i<len) {
        left = intervals[i][0];
        right = intervals[i][1];
        while (i<len-1 && intervals[i+1][0] <= right) {
            i++;
            right = Math.max(intervals[i][1], right);
        }
        res.push([left, right])
        i++
    }
    return res
};
```