# [Valid Parentheses](https://leetcode-cn.com/problems/valid-parentheses/)

## Description

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

    Open brackets must be closed by the same type of brackets.
    Open brackets must be closed in the correct order.
    
Note that an empty string is also considered valid.


### Example 1:

````
Input: "()"
Output: true
````

### Example 2:

````
Input: "()[]{}"
Output: true
````

### Example 3:

````
Input: "(]"
Output: false
````

### Example 4:

````
Input: "([)]"
Output: false
````

### Example 5:

````
Input: "{[]}"
Output: true
````

## 思路

栈。

## 代码
```` Go
func isValid(s string) bool {
	var temp []string
	var left = map[string]string{"(":"", "[":"", "{":""}
	var right = map[string]string{")":"(", "]":"[", "}":"{"}

	for _,v := range s {
		n := string(v)
		_,ok := left[n]
		if ok{
			temp = append(temp,n)
		} else {
			r,_ := right[n]
			length := len(temp)
			if length > 0 && temp[length-1] == r{
				temp = temp[:length-1]
			} else {
				return false
			}
		}
	}
    
	if len(temp) >0 {
		return false
	}
	return true
}
````

