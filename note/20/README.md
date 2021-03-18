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

#### 方法一

```` Go
func isValid(s string) bool {
    mp := map[byte]byte{
        ')':'(',
        '}':'{',
        ']':'[',
    }
    queue := []byte{}
    for i := range s {
        value,ok := mp[s[i]]
        n := len(queue)
        if ok {
            if n == 0 || value != queue[n-1] {
                return false
            }
            queue = queue[:n-1]
        } else {
            queue = append(queue,s[i])
        }
    }
    return len(queue) == 0
}
````

#### 方法二

``` Python3
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        m = {")":"(","]":"[","}":"{"}
        for c in s:
            if c not in m :
                stack.append(c)
            elif not stack or stack.pop() != m[c]:
                return False
        return not stack
```
