# [Single Number](https://leetcode-cn.com/problems/single-number/)

## Description

Given a non-empty array of integers, every element appears twice except for one. Find that single one.

### Example 1:

````
Input: [2,2,1]
Output: 1
````

### Example 2:

````
Input: [4,1,2,1,2]
Output: 4
````

## Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## 思路

亦或。

## 代码
````
func singleNumber(nums []int) int {
    a := 0
    for i:=0;i<len(nums);i++ {
        a = a ^ nums[i]
    }
    return a
}
````

