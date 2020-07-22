# [First Missing Positive](https://leetcode-cn.com/problems/first-missing-positive/)

## Description

Given an unsorted integer array, find the smallest missing positive integer.

### Example 1:

````
Input: [1,2,0]
Output: 3
````

### Example 2:

````
Input: [3,4,-1,1]
Output: 2
````

### Example 3:

````
Input: [7,8,9,11,12]
Output: 1
````

## Note:

Your algorithm should run in O(n) time and uses constant extra space.

## 思路

数组的值作为数组的下标，进行置换。

## 代码
````
func firstMissingPositive(nums []int) int {
    n := len(nums)
    for i := 0; i < n; i++ {
        for nums[i] > 0 && nums[i] <= n && nums[nums[i]-1] != nums[i] {
            nums[nums[i]-1], nums[i] = nums[i], nums[nums[i]-1]
        }
    }
    for i := 0; i < n; i++ {
        if nums[i] != i + 1 {
            return i + 1
        }
    }
    return n + 1
}
````

