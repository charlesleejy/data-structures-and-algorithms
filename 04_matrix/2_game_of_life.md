## Game of Life

### Problem Description
According to the Wikipedia article "Conway's Game of Life," the game is a cellular automaton devised by the British mathematician John Horton Conway in 1970.

The board is made up of an `m x n` grid of cells, where each cell has an initial state: live (represented by a `1`) or dead (represented by a `0`). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following rules (based on the initial state):

1. Any live cell with fewer than two live neighbors dies as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population.
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously. Given the current state of the `m x n` grid `board`, return the next state.

### Example
```
Input: board = [
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
Output: [
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```
```
Input: board = [
  [1,1],
  [1,0]
]
Output: [
  [1,1],
  [1,1]
]
```

### Solution Approach
To solve this problem, we can update the board in place by encoding the changes. Specifically, we use intermediate states to avoid interference between updates:
- `0 -> 1` (a dead cell becomes alive) can be represented by `2`.
- `1 -> 0` (a live cell becomes dead) can be represented by `-1`.

After applying the rules, we decode the intermediate states to obtain the final board.

### Steps in Detail

1. **Initialize Directions**:
   - Define the 8 possible directions (neighbors) around a cell.

2. **Count Live Neighbors**:
   - For each cell, count the number of live neighbors using the defined directions.

3. **Apply Rules**:
   - Apply the rules of the game to determine the next state of each cell and use intermediate states (`2` and `-1`) to mark the changes.

4. **Update the Board**:
   - Traverse the board again and convert the intermediate states to their final values.

### Python Code
```python
def game_of_life(board):
    m, n = len(board), len(board[0])
    directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]
    
    for i in range(m):
        for j in range(n):
            live_neighbors = 0
            for direction in directions:
                r, c = i + direction[0], j + direction[1]
                if 0 <= r < m and 0 <= c < n and abs(board[r][c]) == 1:
                    live_neighbors += 1
            
            if board[i][j] == 1 and (live_neighbors < 2 or live_neighbors > 3):
                board[i][j] = -1
            if board[i][j] == 0 and live_neighbors == 3:
                board[i][j] = 2
    
    for i in range(m):
        for j in range(n):
            if board[i][j] == 2:
                board[i][j] = 1
            elif board[i][j] == -1:
                board[i][j] = 0
```

### Java Code
```java
public class Solution {
    public void gameOfLife(int[][] board) {
        int m = board.length, n = board[0].length;
        int[][] directions = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int liveNeighbors = 0;
                for (int[] direction : directions) {
                    int r = i + direction[0], c = j + direction[1];
                    if (r >= 0 && r < m && c >= 0 && c < n && Math.abs(board[r][c]) == 1) {
                        liveNeighbors += 1;
                    }
                }
                
                if (board[i][j] == 1 && (liveNeighbors < 2 || liveNeighbors > 3)) {
                    board[i][j] = -1;
                }
                if (board[i][j] == 0 && liveNeighbors == 3) {
                    board[i][j] = 2;
                }
            }
        }
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 2) {
                    board[i][j] = 1;
                } else if (board[i][j] == -1) {
                    board[i][j] = 0;
                }
            }
        }
    }
}
```

### Explanation

1. **Initialize Directions**:
   - In both Python and Java, we define the 8 possible directions (neighbors) around a cell using a list or array of tuples/arrays.

2. **Count Live Neighbors**:
   - For each cell, we count the number of live neighbors using the defined directions. We use `abs(board[r][c]) == 1` to count live neighbors, considering the intermediate state `-1` as a live cell.

3. **Apply Rules**:
   - We apply the rules of the game to determine the next state of each cell:
     - If a live cell has fewer than two or more than three live neighbors, it becomes dead (`-1`).
     - If a dead cell has exactly three live neighbors, it becomes alive (`2`).

4. **Update the Board**:
   - We traverse the board again and convert the intermediate states (`2` and `-1`) to their final values (`1` and `0` respectively).

This approach ensures that we efficiently update the board in place by using intermediate states to avoid interference, making it an O(m * n) solution where m and n are the dimensions of the board. This guarantees an efficient and straightforward solution to the problem.