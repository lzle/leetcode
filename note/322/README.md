# [零钱兑换](https://leetcode-cn.com/problems/coin-change/)

## 描述

给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

你可以认为每种硬币的数量是无限的。

### 示例 1

````
输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
````

### 示例 2

````
输入：coins = [2], amount = 3
输出：-1
````

### 示例 3

````
输入：coins = [1], amount = 0
输出：0
````

提示：
````
* 1 <= coins.length <= 12
* 1 <= coins[i] <= 231 - 1
* 0 <= amount <= 104
````

## 思路

动态规划，斐波那契数列


## 代码

```` GO
func coinChange(coins []int, amount int) int {
    dp := make([]int,amount+1)
    for i := range dp {
        dp[i] = amount+1
    }
    dp[0] = 0
    for i:=1; i<=amount; i++ {
        for j := range coins {
            if i-coins[j] >=0 {
                dp[i] = min(dp[i],dp[i-coins[j]]+1)
            }
        }
    }
    if dp[amount] > amount {
        return -1
    }
    return dp[amount]
}

func min(x,y int)int{
    if x < y {
        return x
    }
    return y
}
````