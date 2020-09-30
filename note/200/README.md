# [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

## Description

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

### Example 1:

````
输入:
[
['1','1','1','1','0'],
['1','1','0','1','0'],
['1','1','0','0','0'],
['0','0','0','0','0']
]
输出:1
````

### Example 2:

````
输入:
[
['1','1','0','0','0'],
['1','1','0','0','0'],
['0','0','1','0','0'],
['0','0','0','1','1']
]
输出: 3
解释: 每座岛屿只能由水平和/或竖直方向上相邻的陆地连接而成。
````

## 代码
```` Go
func numIslands(grid [][]byte) int {
    slice := make([][]bool,len(grid))
    for i:=0; i<len(grid); i++ {
        slice[i] = make([]bool,len(grid[i]))
    }
    count := 0
    var dfs func(i int,j int)
    dfs = func(i int,j int) {
        if slice[i][j] {
            return
        }
        slice[i][j] = true
        if grid[i][j] == '0' {
            return
        }
        if i > 0 {
            dfs(i-1,j)
        }
        if i < len(grid)-1 {
            dfs(i+1,j)
        }
        if j > 0 {
            dfs(i,j-1)
        }
        if j < len(grid[i])-1 {
            dfs(i,j+1)
        }
    }
    for i:=0; i<len(grid); i++ {
        for j:=0; j<len(grid[i]);j++ {
           if grid[i][j] == '1' && !slice[i][j]{
               dfs(i,j)
               count +=1
           }
        }
    }
    return count
}
````
