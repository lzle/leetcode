# [两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

## Description

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。


### Example 1:

````
输入：head = [1,2,3,4]
输出：[2,1,4,3]
````

### Example 2:

````
输入：head = []
输出：[]
````

### Example 3:

````
输入：head = [1]
输出：[1]
````

## 思路 1

定义前驱prev节点，画图。

## 代码
```` Python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        pHead = ListNode()
        prev,prev.next = pHead,head
        while prev.next and prev.next.next:
            a = prev.next
            b = a.next
            a.next,b.next,prev.next = b.next,a,b
            prev = a
        return pHead.next
````
