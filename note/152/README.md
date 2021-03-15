# [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

## Description

给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

### Example 1:

````
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
````

### Example 2:

````
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
````

## 思路

动态规划，保留当前最大值与负数最大值。

三种情况
* 正数，正数
* 正数，负数
* 负数，负数

## 代码
```` Go
func maxProduct(nums []int) int {
	curMax,curMin,res := nums[0],nums[0],nums[0]
	for i:=1; i<len(nums); i++ {
		cm,cn := curMax,curMin
		curMax = max(cm*nums[i],max(nums[i],cn*nums[i]))
		curMin = min(cn*nums[i],min(nums[i],cm*nums[i]))
		res = max(curMax,res)
	}
	return res
}

func max(m,n int) int {
	if m > n {
		return m
	}
	return n
}

func min(m,n int) int {
	if m < n {
		return m
	}
	return n
}
````

