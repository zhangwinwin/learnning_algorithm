## 反转链表 II区间反转
反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。
说明:  
1 ≤ m ≤ n ≤ 链表长度。  

示例:  
输入: 1->2->3->4->5->NULL, m = 2, n = 4  
输出: 1->4->3->2->5->NULL  

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
 * @param {number} m
 * @param {number} n
 * @return {ListNode}
 */
var reverseBetween = function(head, m, n) {
    let count = n - m;
    let p = dummyHead = new ListNode(null);
    p.next = head;
    for (let i=0; i<m-1; i++) {
        p = p.next;
    };

    let first = p;
    let tail = pre = p.next;
    let cur = pre.next;

    for (let i=0; i<count; i++) {
        let next = cur.next;
        cur.next = pre;
        pre = cur;
        cur = next;
    }
    first.next = pre;
    tail.next = cur;
    return dummyHead.next;
};
```