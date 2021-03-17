# [买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

## Description

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

### Example 1:

````
输入：prices = [3,3,5,0,0,3,1,4]
输出：6
解释：在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
````
### Example 2:

````
输入：prices = [1,2,3,4,5]
输出：4
解释：在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
````

提示：

* 1 <= prices.length <= 105 
* 0 <= prices[i] <= 105


## 思路

1、暴力
2、动态规划，建立三维状态


## 代码 

暴力
``` Go
func maxProfit(prices []int) int {
    buy1,buy2,sell1,sell2 := -prices[0],-prices[0],0,0
    for i:=1; i<len(prices); i++{
        buy1 = max(buy1,-prices[i])
        sell1 = max(sell1,buy1+prices[i])
        buy2 = max(buy2,sell1-prices[i])
        sell2 = max(sell2,buy2+prices[i])
    }
    return sell2

}

func max(x,y int)int {
    if x > y {
        return x
    }
    return y
}
```

动态规划
``` Go
func maxProfit(prices []int) int {
    n := len(prices)
    if n < 2 {
        return 0
    }
    dp := make([][3][2]int,n)
    for k := range dp[0] {
        dp[0][k][0],dp[0][k][1] = 0,-prices[0]
    }
    for i:=1; i<n; i++ {
        for k:=0; k<3; k++ {
            if k != 0 {
                dp[i][k][0] = max(dp[i-1][k-1][1]+prices[i],dp[i-1][k][0])
            } else {
                dp[i][k][0] = dp[i-1][k][0]
            }
            dp[i][k][1] = max(dp[i-1][k][0]-prices[i],dp[i-1][k][1])
        }
    }
    return dp[n-1][2][0]
}

func max(x,y int)int {
    if x > y {
        return x
    }
    return y
}
```