## Two Sum

### Problem Description
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

### Solution Approach
To solve this problem efficiently, we can use a hashmap (or dictionary) to keep track of the numbers we have seen so far and their corresponding indices. This allows us to check if the complement of the current number (i.e., `target - current number`) exists in the hashmap in constant time.

### Steps in Detail

1. **Initialize Hashmap**:
   - Use a hashmap to store the numbers we have seen so far and their corresponding indices.

2. **Iterate Through the Array**:
   - For each number in the array, calculate its complement (i.e., `target - current number`).
   - Check if the complement exists in the hashmap.
   - If it does, return the indices of the complement and the current number.
   - If it does not, add the current number and its index to the hashmap.

3. **Return the Result**:
   - Since the problem guarantees that there is exactly one solution, we do not need to handle the case where no solution is found.

### Python Code
```python
def two_sum(nums, target):
    num_to_index = {}
    
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_to_index:
            return [num_to_index[complement], i]
        num_to_index[num] = i
    
    return []
```

### Java Code
```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> numToIndex = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (numToIndex.containsKey(complement)) {
                return new int[] { numToIndex.get(complement), i };
            }
            numToIndex.put(nums[i], i);
        }
        
        return new int[] {};  // As per problem statement, this line should never be reached.
    }
}
```

### Explanation

1. **Initialize Hashmap**:
   - In both Python and Java, we use a hashmap to store the numbers we have seen so far and their corresponding indices. In Python, we use a dictionary (`num_to_index = {}`) and in Java, we use a `HashMap` (`Map<Integer, Integer> numToIndex = new HashMap<>();`).

2. **Iterate Through the Array**:
   - We iterate through each number in the array using a for loop.
   - In Python, we use `enumerate(nums)` to get both the index and the value of each element. In Java, we use a standard for loop with an index variable (`i`).
   - For each number, we calculate its complement (`complement = target - num` in Python and `int complement = target - nums[i];` in Java).
   - We check if the complement exists in the hashmap (`if complement in num_to_index:` in Python and `if (numToIndex.containsKey(complement)):` in Java).
   - If it does, we return the indices of the complement and the current number (`return [num_to_index[complement], i]` in Python and `return new int[] { numToIndex.get(complement), i };` in Java).
   - If it does not, we add the current number and its index to the hashmap (`num_to_index[num] = i` in Python and `numToIndex.put(nums[i], i);` in Java).

3. **Return the Result**:
   - Since the problem guarantees that there is exactly one solution, we do not need to handle the case where no solution is found. However, we include a return statement at the end to satisfy the function signature (`return []` in Python and `return new int[] {};` in Java).

This approach ensures that we efficiently find the indices of the two numbers that add up to the target by using a hashmap to track the numbers we have seen so far, making it an O(n) solution where n is the length of the array. This guarantees an efficient and straightforward solution to the problem.