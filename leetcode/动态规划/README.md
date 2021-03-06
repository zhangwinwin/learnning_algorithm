## 动态规划

**动态规划**是一种分阶段求解策略问题的数学思想。  
动态规划三大概念：  
* 最优子结构
* 边界
* 状态转移公式  

举例：有一座高度是10级台阶的楼梯，从下往上走，每跨一步只能向上1级或者2级台阶。要求用程序来求出一共有多少种走法。  
比如，每次走1级台阶，一共走10步，这是其中一种走法。我们可以简写成 1,1,1,1,1,1,1,1,1,1。  

**步骤**  
1、假设只剩最后一步就走到了第10阶，这时会出现2种情况。  
* 第一种：从第9阶走到第10阶  
* 第二种：从第8阶走到第10阶

2、假设已知从第0阶走到第9阶有X种方法，从第0阶走到第8阶有Y种方法。那么可以得出从第0阶走到第10阶的方法等于X+Y。  
用f(10) = f(9) + f(8)   
3、所以可以得出f(9) = f(8) + f(7), f(8) = f(7) + f(6)...  
4、可以得出规律  
* f(1) = 1  
* f(2) = 2
* f(n) = f(n-1) + (n-2): n >= 3

5、动态规划的三大概念：  
* 最优子结构(f(9)和f(8)是f(10)的最优子结构)
* f(1) = 1, f(2) = 2是边界
* f(n) = f(n-1) + (n-2): n >= 3 是状态转移方程。

**求解**  
1、递归求解  
```
function getClimbingWay(n) {
  if (n<1) return 0;
  if (n === 1) return 1;
  if (n === 2) return 2;
  return getClimbingWay(n-1) + getClimbingWay(n-2)
}
// 时间复杂度为：O(2**N)
```
2、备忘录算法  
可以看出递归算法中有很多数都是已经算的，不需要再重复算。可以用哈希表缓存  
```
function getClimbingWay(n, map) {
  if (n<1) return 0;
  if (n === 1) return 1;
  if (n === 2) return 2;
  if (map.has(n)) {
    return map.get(n);
  } else {
    const res = getClimbingWay(n-1) + getClimbingWay(n-2);
    map.set(n, res);
    return res
  }
}
// 时间和空间复杂度都为O(N)
```
3、动态规划  
因为从公式可以得出f(3) = f(2) + f(1), f(4) = f(3) + f(2).所以在每次迭代中只要保留之前的两个状态即可，就可以推导最新的状态。  
台阶数：| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |  
走法数：| 1 | 2 | 3 | 5 | 8 |   |   |   |   |    |  
```
function getClimbingWay(n, map) {
  if (n<1) return 0;
  if (n === 1) return 1;
  if (n === 2) return 2;
  let pre = 1, pre2 = 2, res = 0
  for (let i=3; i<=n; i++) {
    res = pre + pre2;
    pre = pre2;
    pre2 = temp;
  } 
  return temp
}
// 程序从i=3开始迭代，一直到i=n结束。每一次迭代，都会计算出多一级台阶的走法数量。迭代过程中只需保留两个临时变量a和b，分别代表了上一次和上上次迭代的结果。
```

### (买卖股票的通用方案)[https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/solution/yi-ge-tong-yong-fang-fa-tuan-mie-6-dao-gu-piao-wen/]