## 组合总和

解题思路：
做搜索、回溯问题的套路是画图
*根据题目中的用例，画图，因为是搜索，因此呈现的是一个树形结构图，体现出递归结构
*根据题目中的用例，比对所画的图与结果的差异，如一样，说明正确

示例一：输入[2,3,6,7] target = 7， 求[7],[2,2,3]以7为根节点，每一个分支做减法。减到0或者负数剪枝，其中，减到0的时候，结算。结算表示添加结果集。
```
var combinationSum = function(candidates, target) {
    let len = candidates.length;
    if (len === 0) return [];
    
    // 排序
    candidates.sort((a, b) => {
        return a-b;
    });
    let res = [];
    function findCombinationSum (i, stack, tmp) {
        if (stack > target || i === len) {
            return 
        }
        if (stack === target) {
            res.push(tmp)
            return
        }
        findCombinationSum(i, stack + candidates[i], tmp.concat([candidates[i]]))
        findCombinationSum(i+1, stack, tmp)
    }
    findCombinationSum(0, 0, [])
    return res
};
```

```
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */

var combinationSum = function (candidates, target) {
  candidates.sort((a, b) => b - a);

  let res = [], path = [];
  let len = candidates.length, minNum = candidates[len - 1];

  get_combin(candidates, target, 0, path);

  function get_combin(candidates, target, start, path) {
    if (target == 0) {
      return res.push(path.slice());
    }
    if (target < minNum) return;

    for (let i = start; i < len; i++) {
      path.push(candidates[i]);
      get_combin(candidates, target - candidates[i], i, path);
      path.pop();
    }
  }
  return res
}
```