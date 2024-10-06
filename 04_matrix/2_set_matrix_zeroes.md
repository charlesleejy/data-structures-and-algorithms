## Set Matrix Zeroes

### Problem Description
Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`. You must do it in place.

### Example
```
Input: matrix = [
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
Output: [
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```
```
Input: matrix = [
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
Output: [
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
```

### Solution Approach
To solve this problem efficiently and in place, we can use the first row and first column of the matrix itself to keep track of rows and columns that need to be set to zero. 

### Steps in Detail

1. **Initialize Variables**:
   - Use two flags, `first_row_zero` and `first_col_zero`, to keep track of whether the first row and first column need to be set to zero.

2. **Mark Rows and Columns**:
   - Iterate through the matrix. If an element `matrix[i][j]` is zero, set the first element of the corresponding row and column to zero.

3. **Set Matrix Zeroes**:
   - Iterate through the matrix again (excluding the first row and first column), and if the first element of the row or column is zero, set the entire row or column to zero.

4. **Set First Row and Column Zeroes**:
   - Finally, use the flags to set the first row and first column to zero if needed.

### Python Code
```python
def set_zeroes(matrix):
    m, n = len(matrix), len(matrix[0])
    first_row_zero = any(matrix[0][j] == 0 for j in range(n))
    first_col_zero = any(matrix[i][0] == 0 for i in range(m))
    
    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][j] == 0:
                matrix[i][0] = 0
                matrix[0][j] = 0
    
    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][0] == 0 or matrix[0][j] == 0:
                matrix[i][j] = 0
    
    if first_row_zero:
        for j in range(n):
            matrix[0][j] = 0
    
    if first_col_zero:
        for i in range(m):
            matrix[0][0] = 0
```

### Java Code
```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        boolean firstRowZero = false;
        boolean firstColZero = false;
        
        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }
        
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }
        
        if (firstRowZero) {
            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }
        
        if (firstColZero) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we check if the first row or first column contains any zeros and set `first_row_zero` and `first_col_zero` flags accordingly.

2. **Mark Rows and Columns**:
   - We iterate through the matrix starting from `1, 1` (excluding the first row and first column). If an element `matrix[i][j]` is zero, we set the first element of the corresponding row and column to zero (`matrix[i][0]` and `matrix[0][j]`).

3. **Set Matrix Zeroes**:
   - We iterate through the matrix again, starting from `1, 1`. If the first element of the row (`matrix[i][0]`) or the first element of the column (`matrix[0][j]`) is zero, we set the element `matrix[i][j]` to zero.

4. **Set First Row and Column Zeroes**:
   - Finally, we use the `first_row_zero` and `first_col_zero` flags to set the first row and first column to zero if needed.

This approach ensures that we efficiently set the required rows and columns to zero using O(1) extra space (apart from the space needed to store the input matrix), making it an in-place solution with a time complexity of O(m * n), where m and n are the dimensions of the matrix. This guarantees an efficient and straightforward solution to the problem.