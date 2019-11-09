## 组合和解

解法：回溯，不复杂，都是套路<br>

执行用时 :80 ms, 在所有 javascript 提交中击败了92.28%的用户<br>
内存消耗 :37.2 MB, 在所有 javascript 提交中击败了51.28%的用户

```
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function (candidates, target) {
  candidates.sort((a, b) => a - b)
  let result = []
  let len = candidates.length

  function backtrack(start, sum, list) {
    if (sum === target) {
      result.push(list)
    }
    for (let i = start; i < len; i++) {
      if (candidates[i] + sum > target) break;
      if (candidates[i] === candidates[i - 1] && i > start) continue;
      backtrack(i + 1, sum + candidates[i], [...list, candidates[i]])
    }
  }

  backtrack(0, 0, [])

  return result
}
```