# [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

## Description

给定一个二叉树，返回它的中序 遍历。

### Example 1:

````
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
````

## 进阶:

````
递归算法很简单，你可以通过迭代算法完成吗？
````

## 代码 1
``` Go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func inorderTraversal(root *TreeNode) []int {
    if root == nil {
		return nil
	}
	return append(append(inorderTraversal(root.Left),root.Val,),inorderTraversal(root.Right)...)
}
```


## 代码 2
```` Go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func inorderTraversal(root *TreeNode) []int {
    var ret []int
    var slice []*TreeNode
    if root != nil {
        slice = append(slice,root)
    }
    for len(slice) > 0 {
        node := slice[0]
        if node.Left == nil {
            ret = append(ret,node.Val)
            if node.Right != nil {
                slice[0] = node.Right
            } else {
                slice = slice[1:]
            }
        } else {
            left := node.Left
            node.Left = nil
            slice = append([]*TreeNode{left},slice...) 
        }
    }
    return ret
}
````


