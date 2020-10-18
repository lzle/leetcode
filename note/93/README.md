# [复原IP地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

## Description

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

有效的 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效的 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效的 IP 地址。

 
### Example 1:

````
输入：s = "25525511135"
输出：["255.255.11.135","255.255.111.35"]
````

### Example 2:

````
输入：s = "0000"
输出：["0.0.0.0"]
````

### Example 3:

````
输入：s = "1111"
输出：["1.1.1.1"]
````

### Example 4:

````
输入：s = "010010"
输出：["0.10.0.10","0.100.1.0"]
````

## 思路 :whale:

回溯

## 代码
```` Go
func restoreIpAddresses(s string) []string {
    res := []string{}
    if len(s) < 4 || len(s) > 12 {
        return res
    }
    index := 0
    curr := []string{}
    backtrack(s, index, curr, &res)
    return res
}

func backtrack(s string, index int, curr []string, res *[]string) {
    if len(curr) == 4 {
        if index == len(s) {
            *res = append(*res, strings.Join(curr,"."))
            fmt.Println(*res)
        }
        return
    }
    // fmt.Println(curr)
    for i:=1; i<4; i++ {
        if index+i > len(s){
            break
        }
        temp := s[index:index+i]
        if isValidIp(temp) {
            curr = append(curr,temp)
            backtrack(s, index+i, curr, res)
            curr = curr[:len(curr)-1]
        }
    }
}

func isValidIp(temp string) bool {
    if len(temp) == 0 {
        return false
    }
    if temp[0] == '0' && len(temp) >1 {
        return false
    }
    value,err := strconv.Atoi(temp)
    if err != nil {
        return false
    }
    if value > 255 {
        return false
    }
    return true
}
````


