###  删除链表的倒数第N个节点
** 解法 ** ：一次遍历算法
  使用两个指针。第一个指针从列表头开始向前移动n+1步，而第二个指针将从列表的开头出发。现在，这两个指针被n个节点间隔，直到第一个指针到达最后一个节点。此时第二个指针将指向从最后一个节点数起的第n个节点。重新链接第二个指针引用的节点的next指针指向该节点的下一个节点。
---

** 复杂度分析 ** 
时间复杂度：O(L) 该算法对含L个节点的列表进行了一次遍历
空间复杂度：O(1) 只使用常量级空间
---


执行用时 :72 ms, 在所有 javascript 提交中击败了80.70%的用户
内存消耗 :33.8 MB, 在所有 javascript 提交中击败了61.28%的用户
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
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function(head, n) {
    let newNode = new ListNode(0);
    newNode.next = head;
    
    let first = newNode;
    let second = newNode;
    
    for (let i=1; i<=n+1; i++) {
        first = first.next;
    }
    
    while (first) {
        first = first.next;
    }
    
    second.next = second.next.next;
    
    return newNode.next
};
```
