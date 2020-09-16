# [翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

## Description

翻转一棵二叉树。

### Example 1:

输入：
````
     4
   /   \
  2     7
 / \   / \
1   3 6   9
````

输出：
````
     4
   /   \
  7     2
 / \   / \
9   6 3   1
````

## Note:

谷歌：我们90％的工程师使用您编写的软件(Homebrew)，但是您却无法在面试时在白板上写出翻转二叉树这道题，这太糟糕了。
## 思路

递归

## 代码
```` Go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
    if root == nil {
        return root
    }
    root.Left,root.Right = root.Right,root.Left
    invertTree(root.Left)
    invertTree(root.Right)
    return root
}
````

