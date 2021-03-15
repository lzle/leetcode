# [编辑距离](https://leetcode-cn.com/problems/edit-distance/)

## Description

给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

* 插入一个字符
* 删除一个字符
* 替换一个字符

### Example 1:

````
输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
````

### Example 2:

````
输入：word1 = "intention", word2 = "execution"
输出：5
解释：
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
````

## Constraints:

```
0 <= word1.length, word2.length <= 500
word1 和 word2 由小写英文字母组成
```

## 思路

动态规划，dp[i][j] 表示 world1 的前 i 个字符与 world2 的前 j 个字符最少操作数。

## 代码

```` Go
func minDistance(word1 string, word2 string) int {
    m,n := len(word1),len(word2)
    dp := make([][]int,m+1)
    for i := range dp {
        dp[i] = make([]int,n+1)
        dp[i][0] = i
    }
    for j:=0; j<n+1; j++ {
        dp[0][j] = j
    }
    for i:=1; i<=m; i++ {
        for j:=1; j<=n; j++ {
            if word1[i-1] == word2[j-1] {
                dp[i][j] = dp[i-1][j-1]
                continue
            }
            a := dp[i-1][j]+1
            b := dp[i][j-1]+1
            c := dp[i-1][j-1]+1
            dp[i][j] = min(a,min(b,c))
        }
    }
    return dp[m][n]
}

func min(x,y int) int {
    if x < y {
        return x
    }
    return y
}
````
