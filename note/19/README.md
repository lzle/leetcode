# [ Remove Nth Node From End of List](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

## Description

Given a linked list, remove the n-th node from the end of list and return its head.

### Example:

````
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
````

## Note

Given n will always be valid.

### Follow up:

Could you do this in one pass?

## 思路

把链表对称来看，倒数第n节点就是正数(length-n+1)个结点。

## 代码
````
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    dummy := new(ListNode)
    dummy.Next = head

    first := head
    prev := dummy

    for n > 0 {
        first = first.Next
        n--
    }

    for first != nil {
           first = first.Next
           prev = prev.Next    
    }
    prev.Next = prev.Next.Next
    return dummy.Next
}
````

