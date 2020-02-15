## 合并K个排序链表

### 解法
**分而治之**
1、将k个链表配对并将同一对中的链表合并<br>
2、第一轮结束后，k个链表被合并成k/2个链表，平均长度为2N/k，然后是k/4、k/8等等<br>
3、重复这一个过程，直到得到答案<br>
在每一次配对合并的过程中都会遍历几乎全部N个节点，并重复这一过程log2N次

### 复杂度分析
**时间复杂度**O(Nlogk) k: lists.length
**空间复杂度**O(1)

执行用时 :88 ms, 在所有 javascript 提交中击败了99.11%的用户<br>
内存消耗 :38 MB, 在所有 javascript 提交中击败了90.23%的用户
```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function(lists) {
    let amount = lists.length;
    if (amount === 0) return null;
    let interval = 1;
    while (interval < amount) {
        for (let i=0; i<amount-interval; i += interval * 2) {
            lists[i] = merge2Lists(lists[i], lists[i+interval]);
        }
        interval *= 2;
    }
    return lists[0];
};
function merge2Lists (l1, l2) {
    let point = new ListNode(0);
    let head = point;

    while (l1 && l2) {
        if (l1.val <= l2.val) {
            point.next = l1;
            l1 = l1.next;
        } else {
            point.next = l2;
            l2 = l2.next;
        }
        point = point.next
    }
    point.next = l1 == null ? l2 : l1;
    return head.next;
}
```

```
// 自上而下递归
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function(lists) {
    let mergeTwo = (l1, l2) => {
        if (!l1) return l2;
        if (!l2) return l1;

        if (l1.val > l2.val) {
            l2.next = mergeTwo(l1, l2.next);
            return l2;
        } else {
            l1.next = mergeTwo(l2, l1.next);
            return l1;
        }
    }
    let mergeLists = (lists, start, end) => {
        if (end - start < 0) return null;
        if (end - start === 0) return lists[end];

        let mid = ((start + end) / 2) >>> 0;
        return mergeTwo(mergeLists(lists, start, mid), mergeLists(lists, mid+1, end))
    }
    return mergeLists(lists, 0, lists.length-1)
}
```