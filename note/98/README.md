# [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)

## Description

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。

### Example 1:

````
输入:
    2
   / \
  1   3
输出: true
````

### Example 2:

```
输入:
    5
   / \
  1   4
    / \
   3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
    根节点的值为 5 ，但是其右子节点值为 4 。
```

## 思路:

````
中序遍历
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

func isValidBST(root *TreeNode) bool {

    max := ^int(^uint(0) >> 1)
    flag := true
    var dfs func(root *TreeNode)
    dfs = func(root *TreeNode){
        if root != nil && flag {
            dfs(root.Left)
            if root.Val <= max {
                flag = false
                return
            }
            max = root.Val
            dfs(root.Right)
        }
    }
    dfs(root)
    return flag
}
```

