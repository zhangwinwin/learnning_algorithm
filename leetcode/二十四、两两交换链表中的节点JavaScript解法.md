## 两两交换链表中的节点

### 解法
**递归**
递归算法要观察本级递归的解决过程，形成抽象模型。因为递归本质就是不断重复相同的事件，而不是思考完整的调用栈。<br>
主要思考：<br>
1、返回值<br>
2、调用单元做了什么<br>
3、终止条件<br>
在本题中：<br>
1、返回值-交换完成的链表<br>
2、调用单元-设需要交换的两个点为head和next，head连接后面交换完成的子链表，next连接head完成交换。<br>
3、终止条件-head为空或者next为空<br>

执行用时 :68 ms, 在所有 javascript 提交中击败了76.02%的用户<br>
内存消耗 :33.6 MB, 在所有 javascript 提交中击败了48.05%的用户

```
var swapPairs = function(head) {
    if (head == null || head.next == null) {
        return head;
    }
    let next = head.next;
    head.next = swapPairs(next.next);
    next.next = head;
    return next;
};
```