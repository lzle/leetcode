# [环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

## Description

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意，pos 仅仅是用于标识环的情况，并不会作为参数传递到函数中。

说明：不允许修改给定的链表。

进阶：

* 你是否可以使用 O(1) 空间解决此题？

### Example 1:

````
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
````

### Example 2:

````
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
````

### Example 3:

````
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
````


## 思路

1、循环链表，使用集合
2、快、慢指针，相遇时慢指针继续走，头指针走，两者相遇点为环初始点

## 代码

集合存储
```` Go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
    visited := make(map[*ListNode]bool)
    node := head
    for node != nil {
       if  _,ok := visited[node]; ok {
           return node
       }
       visited[node] = true
       node = node.Next
    }
    return nil
}
````

快慢指针
```Go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
    slow,fast := head,head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
        if slow == fast {
            for slow != head {
                slow,head = slow.Next,head.Next
            }
            return slow
        }
    }
    return nil
}
```
