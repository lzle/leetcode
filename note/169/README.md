# [ Majority Element ](https://leetcode-cn.com/problems/majority-element/)

## Description

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

### Example 1:

````
Input: [3,2,3]
Output: 3
````

### Example 2:

````
Input: [2,2,1,1,1,2,2]
Output: 2
````


## 思路 1 :frog:

第一种方式，排序完，数组中间位置的值。

## 代码
````
func majorityElement(nums []int) int {
    sort.Ints(nums)
    return nums[len(nums)/2]
}
````

## 思路 2 :whale:

直接看代码

## 代码
````
func majorityElement(nums []int) int {
    count := 0
    candidate := 0

    for i := 0; i < len(nums); i++ {
        if count == 0 {
            candidate = nums[i]
        }
        if candidate == nums[i] {
            count++
        } else {
            count--
        }
    }
    return candidate
}
````


