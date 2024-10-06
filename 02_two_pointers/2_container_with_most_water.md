## Container With Most Water

### Problem Description
Given `n` non-negative integers `height` where each represents a point at coordinate `(i, height[i])`, `n` vertical lines are drawn such that the two endpoints of the line `i` are at `(i, 0)` and `(i, height[i])`. Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

### Example
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The vertical lines are drawn at positions 0, 1, 2, 3, 4, 5, 6, 7, and 8.
The two lines at indices 1 and 8 together with the x-axis form a container that can hold 49 units of water.
```
```
Input: height = [1,1]
Output: 1
```

### Solution Approach
To solve this problem efficiently, we can use a two-pointer technique. The idea is to start with the widest container and move the pointers inward to find potentially larger containers.

### Steps in Detail

1. **Initialize Two Pointers**:
   - Initialize a pointer `left` at the beginning of the array (`0` index).
   - Initialize a pointer `right` at the end of the array (`len(height) - 1`).

2. **Calculate the Area**:
   - While `left` pointer is less than `right` pointer:
     - Calculate the width of the container as `right - left`.
     - Calculate the height of the container as the minimum of the heights at the `left` and `right` pointers (`min(height[left], height[right])`).
     - Calculate the area of the container as `width * height`.
     - Update the maximum area if the current area is greater.
     - Move the pointer pointing to the shorter line inward (to try and find a taller line that might hold more water).

3. **Return the Result**:
   - After traversing all possible containers, return the maximum area found.

### Python Code
```python
def max_area(height):
    left, right = 0, len(height) - 1
    max_area = 0
    
    while left < right:
        width = right - left
        current_height = min(height[left], height[right])
        current_area = width * current_height
        max_area = max(max_area, current_area)
        
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    
    return max_area
```

### Java Code
```java
public class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length - 1;
        int maxArea = 0;
        
        while (left < right) {
            int width = right - left;
            int currentHeight = Math.min(height[left], height[right]);
            int currentArea = width * currentHeight;
            maxArea = Math.max(maxArea, currentArea);
            
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        
        return maxArea;
    }
}
```

### Explanation

1. **Initialize Two Pointers**:
   - In both Python and Java, we initialize `left` to `0` and `right` to `len(height) - 1`.

2. **Calculate the Area**:
   - We use a while loop to move the pointers towards each other.
   - At each step, we calculate the width of the container as `right - left`.
   - We calculate the height of the container as the minimum of the heights at the `left` and `right` pointers.
   - We calculate the area of the container as `width * height` and update `max_area` if the current area is greater.
   - We then move the pointer pointing to the shorter line inward to try and find a taller line that might hold more water.

3. **Return the Result**:
   - The loop continues until the `left` pointer is no longer less than the `right` pointer.
   - We return `max_area` as the maximum amount of water that can be stored.

This approach ensures that we efficiently find the maximum water container using the two-pointer technique, making it an O(n) solution where n is the length of the array. This guarantees an efficient and straightforward solution to the problem.