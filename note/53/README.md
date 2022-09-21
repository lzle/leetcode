# [最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

## Description

给你一个整数数组 nums ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

子数组 是数组中的一个连续部分。

### Example 1:

````
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
````

### Example 2:

````
输入：nums = [1]
输出：1
````

### Example 3:

````
输入：nums = [5,4,-1,7,8]
输出：23
````

### 提示：

```shell
1 <= nums.length <= 105
-104 <= nums[i] <= 104
```


## 思路

三个指针 l(左)、r(右)、p(移动), 如果区间和小于等于 0 则重置 l 下标。

## 代码
```` Python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        max = nums[0]
        sum = nums[0]

        for p in range(1, len(nums)):
            curr = nums[p]

            if max <= 0:
                if curr > max:
                    max = curr
                    sum = curr
                continue

            sum += curr
            if sum <= 0:
                sum = 0
                continue

            if sum > max:
                max = sum

        return max
````

