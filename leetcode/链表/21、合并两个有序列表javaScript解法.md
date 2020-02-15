## 合并两个有序列表
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。   

示例：  
输入：1->2->4, 1->3->4  

```
// 递归解法
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    let merge = (l1, l2) => {
        if (!l1) return l2;
        if (!l2) return l1;

        if (l1.val > l2.val) {
            l2.next = merge(l1, l2.next);
            return l2;
        } else {
            l1.next = merge(l2, l1.next);
            return l1
        }
    }
    return merge(l1, l2);
};
```

```
// 循环解法
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    if (!l1) return l2;
    if (!l2) return l1;

    let p = dummyHead = new ListNode(null);
    let p1 = l1, p2 = l2;

    while(p1 && p2) {
        if (p1.val > p2.val) {
            p.next = p2;
            p = p.next
            p2 = p2.next;
        } else {
            p.next = p1;
            p = p.next
            p1 = p1.next;
        }
    }
    if (p1) p.next = p1;
    else p.next = p2;
    return dummyHead.next;
};
```
