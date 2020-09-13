# [验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

## Description

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

## Note

本题中，我们将空字符串定义为有效的回文串。

### Example 1:

````
输入: "A man, a plan, a canal: Panama"
输出: true
````

### Example 2:

````
输入: "race a car"
输出: false
````

## 思路

左右指针，大小写转换，判断字符、数字

## 代码
```` Go
func isPalindrome(s string) bool {
    s = strings.ToLower(s)
    left, right := 0, len(s) - 1
    for left < right {
        for left < right && !isalnum(s[left]) {
            left++
        }
        for left < right && !isalnum(s[right]) {
            right--
        }
        if left < right {
            if s[left] != s[right] {
                return false
            }
            left++
            right--
        }
    }
    return true
}

func isalnum(ch byte) bool {
    return (ch >= 'A' && ch <= 'Z') || (ch >= 'a' && ch <= 'z') || (ch >= '0' && ch <= '9')
}
````


