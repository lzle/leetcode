# [每个元音包含偶数次的最长子字符串](https://leetcode-cn.com/problems/find-the-longest-substring-containing-vowels-in-even-counts/)

## Description

给你一个字符串 s ，请你返回满足以下条件的最长子字符串的长度：每个元音字母，即 'a'，'e'，'i'，'o'，'u' ，在子字符串中都恰好出现了偶数次。

### Example 1:

````
输入：s = "eleetminicoworoep"
输出：13
解释：最长子字符串是 "leetminicowor" ，它包含 e，i，o 各 2 个，以及 0 个 a，u 。
````

### Example 2:

````
输入：s = "leetcodeisgreat"
输出：5
解释：最长子字符串是 "leetc" ，其中包含 2 个 e 。
````

### Example 3:

```
输入：s = "bcbcbc"
输出：6
解释：这个示例中，字符串 "bcbcbc" 本身就是最长的，因为所有的元音 a，e，i，o，u 都出现了 0 次。
```

### Note:

> 1 <= s.length <= 5 x 10^5

>s 只包含小写英文字母。

## 思路 :

前缀和 + 状态压缩

## 代码
```` Go
func findTheLongestSubstring(s string) int {
    ans,status := 0,0
    pos := make([]int,1<<5)
    for i:=0; i<len(pos); i++ {
        pos[i] = -1
    }
    
    pos[0] = 0

    for i:=0; i<len(s); i++ {
        switch s[i] {
        case 'a' :
            status ^= 1 << 0
        case 'e':
            status ^= 1 << 1
        case 'i':
            status ^= 1 << 2
        case 'o':
            status ^= 1 << 3
        case 'u':
            status ^= 1 << 4
        }
        if pos[status] >= 0 {
            ans = max(ans, i+1-pos[status])
        } else {
            pos[status] = i + 1
        }
    }
    return ans
}

func max(a int ,b int) int {
    if a >= b {
        return a
    } 
    return b
}
````

