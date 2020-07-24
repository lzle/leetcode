# [Evaluate Reverse Polish Notation](https://leetcode-cn.com/problems/linked-list-cycle/)

## Description

Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, /. Each operand may be an integer or another expression.

## Note

* Division between two integers should truncate toward zero.
* The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.

### Example 1:

````
Input: ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
````

### Example 2:

````
Input: ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
````

### Example 3:

````
Input: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
````

## 思路

a入栈（0位置），b入栈（1位置），遇到运算符“+”，将a和b出栈。

## 代码
```` Go
func evalRPN(tokens []string) int {
	stack := []int{}

	for i := 0 ; i < len(tokens); i++ {
		length := len(stack)
		if tokens[i] == "+" {
			stack[length-2] = stack[length-2] + stack[length-1]
			stack = stack[:length-1]
		} else if tokens[i] == "-" {
			stack[length-2] = stack[length-2] - stack[length-1]
			stack = stack[:length-1]
		} else if tokens[i] == "*" {
			stack[length-2] = stack[length-2] * stack[length-1]
			stack = stack[:length-1]
		} else if tokens[i] == "/" {
			stack[length-2] = stack[length-2] / stack[length-1]
			stack = stack[:length-1]
		} else {
			v,_ := strconv.Atoi(tokens[i])
			stack = append(stack,v)
		}
	}
	return stack[0]
}
````

