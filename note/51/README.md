# [N 皇后](https://leetcode-cn.com/problems/n-queens)

## Description

n 皇后问题 研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 n ，返回所有不同的 n 皇后问题 的解决方案。

每一种解法包含一个不同的 n 皇后问题 的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

![img.png](queens.jpg)

### Example 1:

````
输入：n = 4
输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
解释：如上图所示，4 皇后问题存在两个不同的解法。
````

### Example 2:

````
输入：n = 1
输出：[["Q"]]
````


## 思路

回溯，深度优先

## 代码
```` Go
func permute(nums []int) [][]int {
    var ret [][]int
    length := len(nums)
    var used = make([]bool,length)
    var path = make([]int,length)

    var dfs func(depth int, path []int, used []bool)
    dfs = func(depth int, path []int, used []bool){
        if depth == length {
            slice := make([]int,length)
            copy(slice,path)
            ret = append(ret,slice)
	        return
        }
        for i:=0; i<length; i++{
            if !used[i] {
                path[depth] = nums[i]
                used[i] = true
                dfs(depth+1,path,used)
                used[i] = false
            }
        }
    }
    dfs(0,path,used)
    return ret
}
````

