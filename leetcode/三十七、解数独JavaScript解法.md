## 解数独

```
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solveSudoku = function(board) {
    let rowUsed = [], colUsed = [], boxUsed = [];
    for (let row = 0; row < board.length; row++) {
        rowUsed[row] = []
        boxUsed[Math.floor(row/3)] = []
        for (let col = 0; col < board[0].length; col++) {
            colUsed[col]=[]
            boxUsed[Math.floor(row/3)][Math.floor(col/3)] = []
            let num = board[row][col];
            if (1 <= num && num <= 9) {
                rowUsed[row][num] = true;
                colUsed[col][num] = true;
                boxUsed[Math.floor(row/3)][Math.floor(col/3)][num] = true
            }
        }
    }
    // 递归尝试填充数组 
    recusiveSolveSudoku(board, rowUsed, colUsed, boxUsed, 0, 0);
};
function recusiveSolveSudoku (board, rowUsed, colUsed, boxUsed, row, col) {
    if (col === board[0].length) {
        col = 0;
        row++;
        if (row === board.length) return true;
    }
    if (board[row][col] === '.') {
        for (let num = 1; num <= 9; num++) {
            let canUsed = !(rowUsed[row][num] || colUsed[col][num] || boxUsed[Math.floor(row/3)][Math.floor(col/3)][num]);
            if (canUsed) {
                rowUsed[row][num] = true;
                colUsed[col][num] = true;
                boxUsed[Math.floor(row/3)][Math.floor(col/3)][num] = true;
                board[row][col] = `${num}`;
                if (recusiveSolveSudoku(board, rowUsed, colUsed, boxUsed, row, col + 1)) {
                    return true;
                }
                board[row][col] = '.';
                rowUsed[row][num] = false;
                colUsed[col][num] = false;
                boxUsed[Math.floor(row/3)][Math.floor(col/3)][num] = false;
            }
        }
    } else {
        return recusiveSolveSudoku(board, rowUsed, colUsed, boxUsed, row, col + 1);
    }
    return false
}
```