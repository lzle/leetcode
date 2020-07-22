# [Fizz Buzz](https://leetcode-cn.com/problems/fizz-buzz/)

## Description

Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

### Example:

````
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
````

## 思路

循环与3、5、15除余。

## 代码
```` Go
func fizzBuzz(n int) []string {
    var list = make([]string,n,n)

    for i := 1; i <= n; i++ {
        s := strconv.Itoa(i)
        if i % 15 == 0 {
            s = "FizzBuzz"
        } else if i % 3 == 0 {
            s = "Fizz"
        } else if i % 5 == 0 {
            s = "Buzz"
        }
        list[i-1] = s
    }
    return list
}
````

