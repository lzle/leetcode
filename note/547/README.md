# [省份数量](https://leetcode-cn.com/problems/number-of-provinces/)

## Description

有 n 个城市，其中一些彼此相连，另一些没有相连。如果城市 a 与城市 b 直接相连，且城市 b 与城市 c 直接相连，那么城市 a 与城市 c 间接相连。

省份 是一组直接或间接相连的城市，组内不含其他没有相连的城市。

给你一个 n x n 的矩阵 isConnected ，其中 isConnected[i][j] = 1 表示第 i 个城市和第 j 个城市直接相连，而 isConnected[i][j] = 0 表示二者不直接相连。

返回矩阵中 省份 的数量。

### Example 1:
![img.png](graph1.jpg)
````
输入：isConnected = [[1,1,0],[1,1,0],[0,0,1]]
输出：2
````

### Example 2:
![img.png](graph2.jpg)
````
输入：isConnected = [[1,0,0],[0,1,0],[0,0,1]]
输出：3
````

## 思路 :whale:

深度搜索 + 标记。

## 代码
```` Go
func findCircleNum(isConnected [][]int) int {
    n := len(isConnected)
    visited := make([]bool,n)
    res := 0
    var dfs func(i int)
    dfs = func(i int) {
        visited[i] = true
        for j:=0; j<n;j++ {
            if !visited[j] && isConnected[i][j]==1{
                dfs(j)
            }
        }
    }
    for i := range visited {
        if !visited[i] {
            res+=1
            dfs(i)
        }
    }
    return res
}
````

