## 旋转链表

### 思路
链表中的点已经相连，一次旋转意味着：
先将链表闭合成环
找到相应的位置断开，并确定新的链头和链尾<br>

找到旧的尾部并将其与链表头相连 old_tail.next = head，整个链表闭合成环，同时计算出链表的长度 n。
找到新的尾部，第 (n - k % n - 1) 个节点 ，新的链表头是第 (n - k % n) 个节点。
断开环 new_tail.next = None，并返回新的链表头 new_head。<br>

执行用时 :72 ms, 在所有 javascript 提交中击败了90.00%的用户<br>
内存消耗 :35.4 MB, 在所有 javascript 提交中击败了52.38%的用户

```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var rotateRight = function(head, k) {
    if (head === null) return null;
    if (head.next === null) return head;

    // 闭环
    let old_tail = head;
    let n
    for (n=1; old_tail.next !== null; n++){
        old_tail = old_tail.next;
    }
    old_tail.next = head;

    // 找到新的链头链尾
    let new_tail = head;
    for (let i=0; i<n - k % n - 1; i++) {
        new_tail = new_tail.next
    }
    let new_head = new_tail.next

    // 打开环
    new_tail.next = null;
    return new_head
};
```