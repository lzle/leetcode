# [Merge k Sorted Lists](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

## Description

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

### Example:

````
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
````

## 思路 1

最简单的方式，循环 lists，每次取最小的。

## 代码
```` Go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func mergeKLists(lists []*ListNode) *ListNode {
    head := new(ListNode)
    node := head
    for len(lists) > 0 {
        min := 0
        for i := 1; i < len(lists); i++ {
            if lists[min] == nil {
                min = i
                continue
            } 
            if lists[i] == nil {
                continue
            }
            if lists[i].Val < lists[min].Val {
                min = i
            }
        }
        if lists[min] == nil{
            break
        }
        node.Next = lists[min]
        node = node.Next
        lists[min] = lists[min].Next

    }
    return head.Next
}
````

## 思路 2

归并排序思想，两两排序

## 代码
```` Go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func merge2Lists(listA, listB *ListNode) *ListNode {
    if listA == nil {
        return listB
    }
    if listB == nil {
        return listA
    }

    var head *ListNode
    if listA.Val < listB.Val {
        head = listA
        listA = listA.Next
    } else {
        head = listB
        listB = listB.Next
    }
    tail := head 
    for listA != nil && listB != nil {
        if listA.Val < listB.Val {
            tail.Next = listA
            tail = tail.Next
            listA = listA.Next
        } else {
            tail.Next = listB
            tail = tail.Next
            listB = listB.Next
        }
    }
    if listA == nil {
        tail.Next = listB
    }
    if listB == nil {
        tail.Next = listA
    }
    return head
}

func mergeKLists(lists []*ListNode) *ListNode {
    if len(lists) == 0 {
        return nil
    }
    if len(lists) == 1 {
        return lists[0]
    }
    return merge(lists, 0, len(lists)-1)
}

func merge(lists []*ListNode, left int, right int) *ListNode {
    if left == right {
        return lists[left]
    } 
    if left > right {
        return nil
    }
    mid := (left + right) / 2
    lNode := merge(lists, left, mid)
    rNode := merge(lists, mid+1, right)
    return merge2Lists(lNode, rNode)
}
````