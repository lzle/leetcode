# [Linked List Cycle](https://leetcode-cn.com/problems/linked-list-cycle/)

## Description

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.


### Example 1:

````
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
````

### Example 2:

````
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
````


### Follow up:

Can you solve it using O(1) (i.e. constant) memory?

## 思路

快、慢指针

## 代码
```` Go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func hasCycle(head *ListNode) bool {
    fast := head
    slow := head
    for fast != nil && fast.Next != nil {
        fast = fast.Next.Next
        slow = slow.Next
        if slow == fast {
            return true
        }
    }
    return false
}
````

