# [全排列](https://leetcode-cn.com/problems/permutations/)

## Description

给定一个 没有重复 数字的序列，返回其所有可能的全排列。

### Example 1:

````
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
````

## 思路

回溯、先画递归树。

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

