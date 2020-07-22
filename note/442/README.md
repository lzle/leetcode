# [Find All Duplicates in an Array](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/)

## Description

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?

### Example:

````
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
````

## 思路 :whale:

置换，数值存放到对应下标位置。

## 代码
```` Go
func findDuplicates(nums []int) []int {
    ret := []int{}

    for i := 0; i < len(nums); i++ {
        for nums[i] != nums[nums[i]-1]{
            nums[i],nums[nums[i]-1] = nums[nums[i]-1],nums[i]
        }
    }

    for i,v := range nums {
        if i+1 != v {
            ret = append(ret,v)
        }
    }
    return ret
}
````

