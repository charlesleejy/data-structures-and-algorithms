## Valid Sudoku

### Problem Description
Determine if a `9x9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.

The Sudoku board could be partially filled, where empty cells are represented by the character `'.'`.

### Example
```
Input: 
board = 
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```
```
Input: 
board = 
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same number "8" in the top left and top middle 3x3 sub-boxes.
```

### Solution Approach
To solve this problem efficiently, we need to check each row, column, and `3x3` sub-box to ensure they contain no duplicate numbers.

### Steps in Detail

1. **Initialize Data Structures**:
   - Use three sets of sets (or arrays of sets) to track the numbers seen in each row, column, and `3x3` sub-box.

2. **Iterate Through the Board**:
   - For each cell in the board, if the cell is not empty (i.e., it contains a number):
     - Calculate the index of the `3x3` sub-box the cell belongs to.
     - Check if the number is already present in the corresponding row, column, or sub-box.
     - If the number is present, return `false`.
     - If not, add the number to the corresponding row, column, and sub-box sets.

3. **Return the Result**:
   - If no duplicates are found after checking all cells, return `true`.

### Python Code
```python
def is_valid_sudoku(board):
    rows = [set() for _ in range(9)]
    columns = [set() for _ in range(9)]
    boxes = [set() for _ in range(9)]
    
    for r in range(9):
        for c in range(9):
            if board[r][c] == '.':
                continue
            num = board[r][c]
            box_index = (r // 3) * 3 + (c // 3)
            
            if num in rows[r] or num in columns[c] or num in boxes[box_index]:
                return False
            
            rows[r].add(num)
            columns[c].add(num)
            boxes[box_index].add(num)
    
    return True
```

### Java Code
```java
import java.util.HashSet;
import java.util.Set;

public class Solution {
    public boolean isValidSudoku(char[][] board) {
        Set<Character>[] rows = new HashSet[9];
        Set<Character>[] columns = new HashSet[9];
        Set<Character>[] boxes = new HashSet[9];
        
        for (int i = 0; i < 9; i++) {
            rows[i] = new HashSet<>();
            columns[i] = new HashSet<>();
            boxes[i] = new HashSet<>();
        }
        
        for (int r = 0; r < 9; r++) {
            for (int c = 0; c < 9; c++) {
                if (board[r][c] == '.') {
                    continue;
                }
                char num = board[r][c];
                int boxIndex = (r / 3) * 3 + (c / 3);
                
                if (rows[r].contains(num) || columns[c].contains(num) || boxes[boxIndex].contains(num)) {
                    return false;
                }
                
                rows[r].add(num);
                columns[c].add(num);
                boxes[boxIndex].add(num);
            }
        }
        
        return true;
    }
}
```

### Explanation

1. **Initialize Data Structures**:
   - In Python, we use lists of sets to track the numbers seen in each row, column, and `3x3` sub-box.
   - In Java, we use arrays of `HashSet<Character>` to achieve the same purpose.

2. **Iterate Through the Board**:
   - We use nested loops to iterate through each cell in the board.
   - If the cell is not empty (contains a number), we calculate the index of the `3x3` sub-box the cell belongs to.
   - We check if the number is already present in the corresponding row, column, or sub-box set.
   - If it is present, we return `false`.
   - If not, we add the number to the corresponding row, column, and sub-box sets.

3. **Return the Result**:
   - After checking all cells, if no duplicates are found, we return `true`.

This approach ensures that we efficiently check the validity of the Sudoku board by using sets to track the numbers seen in each row, column, and `3x3` sub-box, making it an O(1) solution with respect to time complexity since the board size is fixed (9x9). This guarantees an efficient and straightforward solution to the problem.