## Rotate Image

### Problem Description
You are given an `n x n` 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. **Do not** allocate another 2D matrix and do the rotation.

### Example
```
Input: matrix = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
]
Output: [
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```
```
Input: matrix = [
  [5,1,9,11],
  [2,4,8,10],
  [13,3,6,7],
  [15,14,12,16]
]
Output: [
  [15,13,2,5],
  [14,3,4,1],
  [12,6,8,9],
  [16,7,10,11]
]
```

### Solution Approach
To rotate the matrix by 90 degrees clockwise, we can follow these steps:
1. Transpose the matrix (swap rows with columns).
2. Reverse each row of the matrix.

### Steps in Detail

1. **Transpose the Matrix**:
   - Swap `matrix[i][j]` with `matrix[j][i]` for all `i` and `j` such that `i < j`.

2. **Reverse Each Row**:
   - Reverse each row in the transposed matrix.

### Python Code
```python
def rotate(matrix):
    n = len(matrix)
    
    # Transpose the matrix
    for i in range(n):
        for j in range(i, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    
    # Reverse each row
    for i in range(n):
        matrix[i].reverse()
```

### Java Code
```java
public class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        
        // Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        
        // Reverse each row
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n / 2; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][n - 1 - j];
                matrix[i][n - 1 - j] = temp;
            }
        }
    }
}
```

### Explanation

1. **Transpose the Matrix**:
   - In both Python and Java, we iterate through the matrix with two nested loops.
   - The outer loop runs from `0` to `n-1` and the inner loop runs from `i` to `n-1`.
   - We swap the elements `matrix[i][j]` and `matrix[j][i]`.

2. **Reverse Each Row**:
   - In Python, we use the built-in `reverse()` method to reverse each row of the matrix.
   - In Java, we manually swap the elements in each row from the beginning to the midpoint of the row.

This approach ensures that we efficiently rotate the matrix by 90 degrees in place using the transpose and reverse technique, making it an O(n^2) solution where n is the dimension of the matrix. This guarantees an efficient and straightforward solution to the problem.