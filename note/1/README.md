# [ Two Sum ](https://leetcode-cn.com/problems/two-sum/)

## Description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

### Example:

````
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
````

## 思路

关键：缓存。

循环数组，从缓存map中尝试查询相加等于target的值。如果查询到则结束，查询不到把当前值添加到map中。

## 代码
``` Go
func twoSum(nums []int, target int) []int {
    mp := make(map[int]int)
    for i,num := range nums {
    	if v,ok := mp[target - num];ok {
    		return []int{v,i}
    	}
    	mp[num] = i
    }
    return nil
}
```

