# [Reverse Words in a String](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

## Description

给定一个字符串，逐个翻转字符串中的每个单词。

### Example 1:

````
输入: "the sky is blue"
输出: "blue is sky the"
````

### Example 2:

````
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
````

### Example 3:

````
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
````

## 思路

切割为数组，去除空格，反向拼接。

## 代码
```` Go
func reverseWords(s string) string {
    slice := strings.Split(s," ")
    left := 0
    right := len(slice)-1
    for left <= right {
        if slice[left] == "" {
            slice = append(slice[:left],slice[left+1:]...)
            right--
            continue
        } 
        if slice[right] == "" {
            slice = append(slice[:right],slice[right+1:]...)
            right--
            continue
        }
        slice[right],slice[left] = slice[left],slice[right]
        left++
        right--
    }
    n := strings.Join(slice," ")
    return n
}
````

