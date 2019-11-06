## 有效的数独

```
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function(board) {
    let rows=[], columns=[], boxes=[];
    for (let i=0; i<9; i++) {
        rows[i] = new Map();
        columns[i] = new Map();
        boxes[i] = new Map();
    }
    
    for (let i=0; i<9; i++) {
        for (let j=0; j<9; j++){
            let num = board[i][j];
            if (num !== '.') {
                let n = parseInt(num);
                let box_index = Math.floor(i / 3) * 3 + Math.floor(j / 3);
                
                rows[i].has(n) ? rows[i].set(rows[i].get(n) + 1) : rows[i].set(1)
                columns[j].has(n) ? columns[j].set(columns[j].get(n) + 1) : columns[j].set(1)
                boxes[box_index].has(n) ? boxes[box_index].set(boxes[box_index].get(n) + 1) : boxes[box_index].set(1)
                
                if (rows[i].get(n) > 1 || columns[j].get(n) > 1 || boxes[box_index].get(n) > 1) {
                    return false;
                }

            }
        }
    }
    return true
};
```