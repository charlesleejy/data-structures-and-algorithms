## Jump Game II

### Problem Description
Given an array of non-negative integers `nums`, where each element represents your maximum jump length at that position, your goal is to reach the last index in the minimum number of jumps. You can assume that you can always reach the last index.

### Example
```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
```
Input: nums = [2,3,0,1,4]
Output: 2
```

### Solution Approach
To solve this problem, we can use a greedy approach to track the farthest point we can reach with the current number of jumps, and then decide when to make another jump.

### Steps in Detail

1. **Initialization**:
   - Initialize `jumps` to 0, which will count the number of jumps needed.
   - Initialize `current_end` to 0, which represents the end of the range that can be reached with the current number of jumps.
   - Initialize `farthest` to 0, which represents the farthest point that can be reached with the next jump.

2. **Iteration**:
   - Iterate through the array up to the second-to-last element (since we don't need to jump from the last element).
   - For each index `i`:
     - Update `farthest` to be the maximum of its current value and `i + nums[i]`.
     - If `i` is equal to `current_end`, it means we have reached the end of the current jump range:
       - Increment `jumps`.
       - Update `current_end` to `farthest`.

3. **Completion**:
   - After iterating through the array, `jumps` will contain the minimum number of jumps required to reach the last index.

### Python Code
```python
def jump(nums):
    if len(nums) <= 1:
        return 0
    
    jumps = 0
    current_end = 0
    farthest = 0
    
    for i in range(len(nums) - 1):
        farthest = max(farthest, i + nums[i])
        
        if i == current_end:
            jumps += 1
            current_end = farthest
            
            if current_end >= len(nums) - 1:
                break
    
    return jumps
```

### Java Code
```java
public class Solution {
    public int jump(int[] nums) {
        if (nums.length <= 1) {
            return 0;
        }
        
        int jumps = 0;
        int currentEnd = 0;
        int farthest = 0;
        
        for (int i = 0; i < nums.length - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);
            
            if (i == currentEnd) {
                jumps++;
                currentEnd = farthest;
                
                if (currentEnd >= nums.length - 1) {
                    break;
                }
            }
        }
        
        return jumps;
    }
}
```

### Explanation

1. **Initialization**:
   - We initialize `jumps` to 0 to count the number of jumps needed.
   - `current_end` is initialized to 0 to keep track of the range that can be reached with the current number of jumps.
   - `farthest` is initialized to 0 to keep track of the farthest point that can be reached with the next jump.

2. **Iteration**:
   - We iterate through the array up to the second-to-last element.
   - For each index `i`, we update `farthest` to be the maximum of its current value and `i + nums[i]`. This represents the farthest point that can be reached from the current position.
   - If `i` reaches `current_end`, it means we need to make another jump:
     - Increment `jumps`.
     - Update `current_end` to `farthest`.
     - If `current_end` is already at or beyond the last index, we break out of the loop early.

3. **Completion**:
   - After the loop, `jumps` will contain the minimum number of jumps needed to reach the last index.

This approach ensures that we traverse the array only once, making it an O(n) solution, and we use only O(1) extra space for the variables `jumps`, `current_end`, and `farthest`.