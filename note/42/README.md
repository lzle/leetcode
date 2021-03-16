# [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

## Description

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

### Example 1:

![img.png](img.png)

````
输入：height = [0,1,0,2,1,0,1,3,2,1,2,1]
输出：6
解释：上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 
````

### Example 2:

````
输入：height = [4,2,0,3,2,5]
输出：9
````

### Example 3:

````
Input: [7,8,9,11,12]
Output: 1
````

## Note:

* n == height.length
* 0 <= n <= 3 * 104
* 0 <= height[i] <= 105
## 思路

双指针

## 代码
```` Go
func trap(height []int) int {
    if len(height) <= 2 {
        return 0
    }
    left,right := 0,len(height)-1
    water := 0
    for left < right {
        if height[left] < height[right] {
            n := left+1
            for n <= right && height[n] < height[left] {
                water += height[left] - height[n]
                n++
            }
            left = n
        } else {
            n := right-1
            for n >= left && height[n] < height[right] {
                water += height[right] - height[n]
                n--
            }
            right = n
        }
    }
    return water
}
````

