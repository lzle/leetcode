# [Longest Valid Parentheses](https://leetcode-cn.com/problems/first-missing-positive/)

## Description

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

### Example 1:

````
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
````

### Example 2:

````
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"
````

## 思路

用left表示'('数量，right表示')'数量，当left=right时，刚好是一个闭合，left+right=maxLength。

## 代码
```` Go
func longestValidParentheses(s string) int {
    left, right, maxLength := 0, 0, 0
    for i := 0; i < len(s); i++ {
        if s[i] == '(' {
            left++
        } else {
            right++
        }
        if left == right {
            maxLength = max(maxLength, 2 * right)
        } else if right > left {
            left, right = 0, 0
        }
    }
    left, right = 0, 0
    for i := len(s) - 1; i >= 0; i-- {
        if s[i] == '(' {
            left++
        } else {
            right++
        }
        if left == right {
            maxLength = max(maxLength, 2 * left)
        } else if left > right {
            left, right = 0, 0
        }
    }
    return maxLength
}

func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}
````

