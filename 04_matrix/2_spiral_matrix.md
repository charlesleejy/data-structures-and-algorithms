## Spiral Matrix

### Problem Description
Given an `m x n` matrix, return all elements of the matrix in spiral order.

### Example
```
Input: matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
Output: [1, 2, 3, 6, 9, 8, 7, 4, 5]
```
```
Input: matrix = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 10, 11, 12]
]
Output: [1, 2, 3, 4, 8, 12, 11, 10, 9, 5, 6, 7]
```

### Solution Approach
To solve this problem, we can simulate the process of moving in a spiral pattern. This involves traversing the matrix in the following order: right, down, left, and up. We use boundaries to keep track of where we should stop in each direction.

### Steps in Detail

1. **Initialize Variables**:
   - Initialize an empty list `result` to store the elements in spiral order.
   - Initialize variables to keep track of the boundaries: `top`, `bottom`, `left`, `right`.

2. **Traverse the Matrix**:
   - Use a while loop that continues as long as `top` is less than or equal to `bottom` and `left` is less than or equal to `right`.
   - Traverse from left to right across the top boundary and increment the `top` boundary.
   - Traverse from top to bottom along the right boundary and decrement the `right` boundary.
   - Traverse from right to left along the bottom boundary if `top` is still less than or equal to `bottom`, then decrement the `bottom` boundary.
   - Traverse from bottom to top along the left boundary if `left` is still less than or equal to `right`, then increment the `left` boundary.

3. **Return the Result**:
   - After the loop, return the `result` list containing all elements in spiral order.

### Python Code
```python
def spiral_order(matrix):
    if not matrix:
        return []
    
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    
    while top <= bottom and left <= right:
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1
        
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1
        
        if top <= bottom:
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1
        
        if left <= right:
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1
    
    return result
```

### Java Code
```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        if (matrix == null || matrix.length == 0) {
            return result;
        }
        
        int top = 0, bottom = matrix.length - 1;
        int left = 0, right = matrix[0].length - 1;
        
        while (top <= bottom && left <= right) {
            for (int col = left; col <= right; col++) {
                result.add(matrix[top][col]);
            }
            top++;
            
            for (int row = top; row <= bottom; row++) {
                result.add(matrix[row][right]);
            }
            right--;
            
            if (top <= bottom) {
                for (int col = right; col >= left; col--) {
                    result.add(matrix[bottom][col]);
                }
                bottom--;
            }
            
            if (left <= right) {
                for (int row = bottom; row >= top; row--) {
                    result.add(matrix[row][left]);
                }
                left++;
            }
        }
        
        return result;
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we initialize an empty list `result` to store the elements in spiral order.
   - We use variables `top`, `bottom`, `left`, and `right` to keep track of the current boundaries of the matrix.

2. **Traverse the Matrix**:
   - We use a while loop that continues as long as `top <= bottom` and `left <= right`.
   - For each direction, we traverse the elements and add them to the `result` list:
     - Traverse from left to right across the `top` boundary and increment the `top` boundary.
     - Traverse from top to bottom along the `right` boundary and decrement the `right` boundary.
     - Traverse from right to left along the `bottom` boundary if `top <= bottom`, then decrement the `bottom` boundary.
     - Traverse from bottom to top along the `left` boundary if `left <= right`, then increment the `left` boundary.

3. **Return the Result**:
   - After the loop, we return the `result` list containing all elements in spiral order.

This approach ensures that we efficiently traverse the matrix in a spiral pattern using the sliding window technique, making it an O(m * n) solution where m and n are the dimensions of the matrix. This guarantees an efficient and straightforward solution to the problem.