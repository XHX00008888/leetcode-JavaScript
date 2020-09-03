#### [37. 解数独](https://leetcode-cn.com/problems/sudoku-solver/)

难度困难496

编写一个程序，通过已填充的空格来解决数独问题。

一个数独的解法需**遵循如下规则**：

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。

空白格用 `'.'` 表示。

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

一个数独。

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

答案被标成红色。

**Note:**

- 给定的数独序列只包含数字 `1-9` 和字符 `'.'` 。
- 你可以假设给定的数独只有唯一解。
- 给定数独永远是 `9x9` 形式的。

```js
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solveSudoku = function (board) {
    let num = 0
    const row = Array.from({ length: 9 }, () => new Array(9).fill(false))
    const col = Array.from({ length: 9 }, () => new Array(9).fill(false))
    const box = Array.from({ length: 3 }, () => Array.from({ length: 3 }, () => new Array(9).fill(false)))
    const codeAtOne = '1'.charCodeAt(0)
    let at
    for (let i = 0; i < 9; i++) {
        for (let j = 0; j < 9; j++) {
            if (board[i][j] !== '.') {
                at = board[i][j].charCodeAt(0) - codeAtOne
                row[i][at] = true
                col[j][at] = true
                box[Math.floor(i / 3)][Math.floor(j / 3)][at] = true
            }
        }
    }
    const flashBack = (level, level2) => {// level为行，level2为列
        console.log(num++)
        if (level === 9) return true// level为行数
        let tLevel = level
        let tLevel2 = level2 + 1
        if (level2 === 9) {
            tLevel = level + 1
            tLevel2 === 0
        }
        if (board[level][level2] === '.') {
            for (let j = 1; j <= 9; j++) {// 1-9
                let temp = j - 1
                if (!row[level][temp] && !col[level2][temp] && !box[Math.floor(level / 3)][Math.floor(level2 / 3)][temp]) {
                    board[level][level2] = j
                    row[level][temp] = true
                    col[level2][temp] = true
                    box[Math.floor(level / 3)][Math.floor(level2 / 3)][temp] = true
                    if (flashBack(tLevel, tLevel2)) return true
                    row[level][temp] = false
                    col[level2][temp] = false
                    box[Math.floor(level / 3)][Math.floor(level2 / 3)][temp] = false
                    board[level][level2] = '.'
                }
            }
        }
        else flashBack(tLevel, tLevel2)
        return false
    }
    flashBack(0, 0)
    return board
};
```

