## 反转链表

反转一个单链表。  

示例:  
输入: 1->2->3->4->5->NULL  
输出: 5->4->3->2->1->NULL

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
 * @return {ListNode}
 */

// 循环解法
var reverseList = function(head) {
    if (!head) return head;
    let pre = null, cur = head;

    while (cur) {
        let next = cur.next;
        cur.next = pre;
        pre = cur;
        cur = next
    }
    return pre
};

// 递归解法
var reverseList = function(head) {
    let reverse = (pre, cur) => {
        if (!cur) return pre;
        let next = cur.next;
        cur.next = pre;
        reverse(cur, next);
    }
    return reverse(null, head)
};
```