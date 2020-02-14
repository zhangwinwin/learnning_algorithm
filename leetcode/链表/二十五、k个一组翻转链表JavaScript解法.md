## k个一组翻转链表
### 解法步骤
1、链表分为已翻、待翻、未翻三个部分<br>
2、每次翻转前，通过k次循环来确定范围<br>
3、记录链表的前一个节点pre和后一个节点end<br>
4、经过k次循环，end到达了末尾，记录next = end.next<br>
5、翻转链表，然后将三部分链表连接起来，然后重置pre和end指针，然后进入下一次循环<br>
6、当翻转部分长度不足k时，定位end完成后end == null，已经到达末尾，说明已完成，直接返回

### 复杂度分析
**时间复杂度** O(N * K)<br>
**空间复杂度** O(1)

执行用时 :92 ms, 在所有 javascript 提交中击败了83.04%的用户<br>
内存消耗 :37.6 MB, 在所有 javascript 提交中击败了32.14%的用户

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
var reverseKGroup = function(head, k) {
    let dummy = new ListNode(0);
    dummy.next = head;
    
    let pre = dummy;
    let end = dummy;
    
    while (end.next) {
        for (let i=0; i<k && end; i++) {
            end = end.next;
        }
        if (!end) break;
        let start = pre.next;
        let next = end.next;
        end.next = null;
        pre.next = reverse(start);
        start.next = next;
        pre = start;
        end = pre;
    }
    return dummy.next;
};

function reverse (start) {
    let pre = null;
    let curr = start;
    while (curr != null) {
        let next = curr.next;
        curr.next = pre;
        pre = curr;
        curr = next;
    }
    return pre;
}
```