## Jump Game

### Problem Description
You are given an array of non-negative integers `nums` where each element represents your maximum jump length at that position. Your goal is to determine if you can reach the last index starting from the first index.

### Example
```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
```
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

### Solution Approach
To determine if you can reach the last index, you can use a greedy approach. The idea is to keep track of the farthest index you can reach and update it as you iterate through the array.

### Steps in Detail

1. **Initialization**:
   - Initialize a variable `max_reachable` to 0, which will keep track of the farthest index that can be reached.

2. **Iteration**:
   - Iterate through the array using a for loop.
   - For each index `i`:
     - If `i` is greater than `max_reachable`, it means you can't reach this index, so return `false`.
     - Update `max_reachable` to be the maximum of its current value and `i + nums[i]`.

3. **Completion**:
   - After the loop, if you have successfully updated `max_reachable` to be at least the last index, return `true`. Otherwise, return `false`.

### Python Code
```python
def can_jump(nums):
    max_reachable = 0
    
    for i in range(len(nums)):
        if i > max_reachable:
            return False
        max_reachable = max(max_reachable, i + nums[i])
    
    return max_reachable >= len(nums) - 1
```

### Java Code
```java
public class Solution {
    public boolean canJump(int[] nums) {
        int maxReachable = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (i > maxReachable) {
                return false;
            }
            maxReachable = Math.max(maxReachable, i + nums[i]);
        }
        
        return maxReachable >= nums.length - 1;
    }
}
```

### Explanation

1. **Initialization**:
   - We start by setting `max_reachable` to 0 because initially, we can only reach the first index.

2. **Iteration**:
   - We iterate through the array using a for loop.
   - For each index `i`, we check if `i` is greater than `max_reachable`. If it is, it means we can't reach this index, so we return `false`.
   - If `i` is within the reachable range, we update `max_reachable` to be the maximum of its current value and `i + nums[i]`. This update ensures that we are always tracking the farthest index we can reach as we move forward.

3. **Completion**:
   - After iterating through the array, we check if `max_reachable` is at least the last index (`len(nums) - 1`). If it is, we return `true`, indicating that we can reach the last index. Otherwise, we return `false`.

This approach ensures that we traverse the array only once, making it an O(n) solution, and we use only O(1) extra space for the `max_reachable` variable.