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

## 思路

利用指针pre，遍历链表，修改当前节点Next指向prev。当前节点下移，prev赋值为当前节点，如此循环。

## 代码
````
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

