# [K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

## Description

给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

进阶：

* 你可以设计一个只使用常数额外空间的算法来解决此问题吗？
* 你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。


### Example 1:
![reverse_ex1.jpg](reverse_ex1.jpg)
````
输入：head = [1,2,3,4,5], k = 2
输出：[2,1,4,3,5]
````

### Example 2:
![reverse_ex2.jpg](reverse_ex2.jpg)
````
输入：head = [1,2,3,4,5], k = 3
输出：[3,2,1,4,5]
````

### Example 3:

````
输入：head = [1,2,3,4,5], k = 1
输出：[1,2,3,4,5]
````

## 思路 1

模拟

## 代码
```` Go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseKGroup(head *ListNode, k int) *ListNode {
    hair := new(ListNode)
    hair.Next = head
    prev,tail := hair,hair
    for head != nil {
        for i := 0; i < k; i++ {
            tail = tail.Next
            if tail == nil {
                return hair.Next
            }
        }
        next := tail.Next
        head,tail = reverse(head,tail)
        prev.Next = head
        tail.Next = next
        prev = tail
        head = tail.Next
    }
    return hair.Next
}

func reverse(head,tail *ListNode) (*ListNode,*ListNode) {
    prev := tail.Next
    p := head
    for prev != tail {
        nex := p.Next
        p.Next = prev
        prev = p
        p = nex
    }
    return tail, head
}
````
