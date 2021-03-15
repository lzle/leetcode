# [最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

## 描述

给你一个整数数组 nums ，找到其中最长严格递增子序列的长度。

子序列是由数组派生而来的序列，删除（或不删除）数组中的元素而不改变其余元素的顺序。例如，[3,6,2,7] 是数组 [0,3,1,6,2,2,7] 的子序列。


### 进阶

* 你可以设计时间复杂度为 O(n2) 的解决方案吗？
* 你能将算法的时间复杂度降低到 O(n log(n)) 吗?

### 示例 1

````
输入：nums = [10,9,2,5,3,7,101,18]
输出：4
解释：最长递增子序列是 [2,3,7,101]，因此长度为 4 。
````

### 示例 2

````
输入：nums = [0,1,0,3,2,3]
输出：4
````

### 示例 3

````
输入：nums = [7,7,7,7,7,7,7]
输出：1
````

提示：
````
* 1 <= nums.length <= 2500
* -104 <= nums[i] <= 104
````

## 思路

方法一：暴力回溯，时间复杂度 O(2^n)。

方法二：动态规划，两层循环，记录状态值，当前 i 最长递增子序列，等于之前小于 i 值中最大的最长递增子序列加 1。
时间复杂度 O(n^2)。

方法三：二分，O(nlogn)。


## 代码

动态规划
```` GO
func lengthOfLIS(nums []int) int {
    n := len(nums)
    dp := make([]int,n)
    res := 0
    for i:=0; i<n; i++ {
        max := 0
        for j:=0; j<i; j++ {
            if nums[j] < nums[i] && max < dp[j] {
                max = dp[j]
            }
        }
        dp[i] = max+1
        if max+1 > res {
            res = max+1
        }
    }
    return res
}
````

二分
```` GO
func lengthOfLIS(nums []int) int {
	slice := []int{}
	slice = append(slice,nums[0])
	for i:=1; i<len(nums); i++ {
		if nums[i] > slice[len(slice)-1] {
			slice = append(slice,nums[i])
		} else {
			left,right := 0,len(slice)-1
			for left < right {
				if slice[left] >= nums[i] {
					break
				}
				mid := left+(right-left)/2
				if slice[mid] < nums[i] {
					left = mid+1
				} else {
					right = mid
				}
			}
			slice[left] = nums[i]
		}
	}
	return len(slice)
}

````