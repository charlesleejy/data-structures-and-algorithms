## Trapping Rain Water

### Problem Description
Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

### Example
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The elevation map (in array form) looks like this:
[0,1,0,2,1,0,1,3,2,1,2,1]
The total amount of water trapped is 6 units.
```
```
Input: height = [4,2,0,3,2,5]
Output: 9
```

### Solution Approach
To solve this problem, we can use a two-pointer approach which traverses the height array from both ends towards the center. This approach efficiently calculates the amount of trapped water by maintaining left and right pointers along with their respective maximum heights encountered so far.

### Steps in Detail

1. **Initialization**:
   - Initialize two pointers, `left` and `right`, starting from the leftmost and rightmost indices of the height array, respectively.
   - Initialize two variables, `left_max` and `right_max`, to keep track of the maximum height encountered from the left and right sides, respectively.
   - Initialize `water_trapped` to 0 to accumulate the total amount of trapped water.

2. **Two-Pointer Traversal**:
   - Traverse the height array using a while loop until `left` is less than or equal to `right`.
   - Compare the heights at the `left` and `right` pointers:
     - If `height[left]` is less than or equal to `height[right]`, update `left_max` and calculate the trapped water at the `left` pointer, then move the `left` pointer to the right.
     - Otherwise, update `right_max` and calculate the trapped water at the `right` pointer, then move the `right` pointer to the left.

3. **Calculate Trapped Water**:
   - For each position, if the current height is less than the respective maximum height (`left_max` or `right_max`), the difference between the maximum height and the current height is the amount of water trapped at that position.

4. **Summarize**:
   - Continue the traversal until the `left` and `right` pointers meet. The total trapped water is stored in `water_trapped`.

### Python Code
```python
def trap(height):
    if not height:
        return 0
    
    left, right = 0, len(height) - 1
    left_max, right_max = 0, 0
    water_trapped = 0
    
    while left <= right:
        if height[left] <= height[right]:
            if height[left] >= left_max:
                left_max = height[left]
            else:
                water_trapped += left_max - height[left]
            left += 1
        else:
            if height[right] >= right_max:
                right_max = height[right]
            else:
                water_trapped += right_max - height[right]
            right -= 1
    
    return water_trapped
```

### Java Code
```java
public class Solution {
    public int trap(int[] height) {
        if (height == null || height.length == 0) {
            return 0;
        }
        
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int waterTrapped = 0;
        
        while (left <= right) {
            if (height[left] <= height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    waterTrapped += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    waterTrapped += rightMax - height[right];
                }
                right--;
            }
        }
        
        return waterTrapped;
    }
}
```

### Explanation

1. **Initialization**:
   - In both Python and Java, we initialize `left` to 0 and `right` to the last index of the height array.
   - `left_max` and `right_max` are initialized to 0 to track the highest bars encountered from the left and right, respectively.
   - `water_trapped` is initialized to 0 to accumulate the total trapped water.

2. **Two-Pointer Traversal**:
   - We use a while loop to traverse the array from both ends until `left` is less than or equal to `right`.
   - Inside the loop, we compare `height[left]` and `height[right]` to decide which pointer to move:
     - If `height[left]` is less than or equal to `height[right]`, we update `left_max` if necessary, calculate the water trapped at the `left` pointer, and then move `left` to the right.
     - If `height[right]` is less than `height[left]`, we update `right_max` if necessary, calculate the water trapped at the `right` pointer, and then move `right` to the left.

3. **Calculate Trapped Water**:
   - For each position, if the current height is less than the respective maximum height (`left_max` or `right_max`), the difference between the maximum height and the current height is added to `water_trapped`.

4. **Summarize**:
   - The loop continues until the `left` and `right` pointers meet. The total trapped water is returned as the result.

This approach ensures that we traverse the height array only once, making it an O(n) solution, and we use only O(1) extra space for the pointers and maximum height variables. This guarantees an efficient solution to the problem.