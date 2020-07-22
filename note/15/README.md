# [ 3Sum ](https://leetcode-cn.com/problems/3sum/)

## Description

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

### Note

The solution set must not contain duplicate triplets.

### Example:

````
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
````

## 思路 :frog:

关键：排序、俩数之和。

对数组排序，循环数组，作为第一个值，从剩余对象中找寻另外两个值，转为问题为俩数之和。

排序数组，俩数之和，一头一尾，向中间靠拢。

## 代码
```` Go
func threeSum(nums []int) [][]int {
    var ret [][]int
    sort.Ints(nums)

    for first:=0;first<len(nums)-2;first++ {
    	if first>0 && nums[first]==nums[first-1]{
    		continue
    	}
    	second := first + 1
    	third := len(nums)-1
    	target := 0 - nums[first]
    	for second < third{
    		if second > first+1 && nums[second] == nums[second-1]{
    			second++
    			continue
    		}
    		if third < len(nums)-1 && nums[third] == nums[third+1]{
    			third--
    			continue
    		}
    		if nums[second] + nums[third] > target {
    			third--
    		} else if nums[second] + nums[third] < target {
    			second++
    		}else{
    			ret = append(ret,[]int{nums[first],nums[second],nums[third]})
    			second++
    			third--
    		}
    	}
    }
    return ret
}
````

