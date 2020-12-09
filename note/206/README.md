# [Reverse Linked List](https://leetcode-cn.com/problems/reverse-linked-list/)

## Description

Reverse a singly linked list.

### Example:

````
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
````

### Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

## 思路 :whale:

设置prev与cur节点，利用指针prev，遍历链表，修改当前节点next指向prev。当前节点下移，prev赋值为当前节点，如此循环。

## 代码
```` Go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
    var prev *ListNode

    for head != nil {
        next := head.Next
        head.Next = prev
        prev = head
        head = next
    }
    return prev
}
````

``` python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev,cur =  None,head
        while cur:
           cur.next,prev,cur = prev,cur,cur.next
        return prev
```
