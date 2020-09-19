# [解数独](https://leetcode-cn.com/problems/sudoku-solver/)

## Description

编写一个程序，通过填充空格来解决数独问题。

一个数独的解法需遵循如下规则：

* 数字 1-9 在每一行只能出现一次。
* 数字 1-9 在每一列只能出现一次。
* 数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

空白格用 '.' 表示。

<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" width=300>

一个数独。

<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png" width=300>

答案被标成红色。

### Note:

* 给定的数独序列只包含数字 1-9 和字符 '.' 。
* 你可以假设给定的数独只有唯一解。
* 给定数独永远是 9x9 形式的。

## 思路

回溯，枚举

## 代码
```` Go
var Flag bool

func solveSudoku(board [][]byte)  {
    Flag = false
    solve(0, 0, board)
}

func solve(row int, column int, board [][]byte){
    if row == 9 {
        Flag = true
        fmt.Println(board)
        return
    }
    if board[row][column] != '.' {
        if column < 8 {
            solve(row, column+1, board)
        } else {
            solve(row+1, 0, board)
        }
        return
    }
    str := []byte("123456789")
    for _,val := range str {
        if isOk(row, column, val, board){
            board[row][column] = val
            if column < 8 {
                solve(row, column+1, board)
            } else {
                solve(row+1, 0, board)
            }
            if Flag {
                return
            }
            board[row][column] = '.'
        }
    }
    // board[row][column] = '.'
}

func isOk(row int, column int, val byte, board [][]byte) bool{
    for c:=0; c<9; c++ {
        if board[row][c] == val {
            return false
        }
    }

    for r:=0; r<9; r++ {
        if board[r][column] == val {
            return false
        }
    }
    pr := row / 3
    pc := column / 3
	for i:=0; i<3; i++ {
		for j:=0; j<3;j++ {
            if board[pr*3+i][pc*3+j] == val{
                return false
            }
		}
	}
    return true
}
````

