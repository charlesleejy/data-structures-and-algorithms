## Contains Duplicate II

### Problem Description
Given an integer array `nums` and an integer `k`, return `true` if there are two distinct indices `i` and `j` in the array such that `nums[i] == nums[j]` and `abs(i - j) <= k`.

### Example
```
Input: nums = [1,2,3,1], k = 3
Output: true
```
```
Input: nums = [1,0,1,1], k = 1
Output: true
```
```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

### Solution Approach
To solve this problem efficiently, we can use a hashmap (or dictionary) to keep track of the most recent index of each element. This allows us to check if there is a previous occurrence of the current element within the distance `k`.

### Steps in Detail

1. **Initialize Hashmap**:
   - Use a hashmap to store the most recent index of each element in the array.

2. **Iterate Through the Array**:
   - For each element in the array, check if it exists in the hashmap.
   - If it exists, check if the difference between the current index and the stored index is less than or equal to `k`.
   - If the condition is met, return `true`.
   - If the element does not exist in the hashmap, or the condition is not met, update the hashmap with the current index of the element.

3. **Return the Result**:
   - If no such pair of indices is found, return `false`.

### Python Code
```python
def contains_nearby_duplicate(nums, k):
    num_to_index = {}
    
    for i, num in enumerate(nums):
        if num in num_to_index and i - num_to_index[num] <= k:
            return True
        num_to_index[num] = i
    
    return False
```

### Java Code
```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> numToIndex = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            if (numToIndex.containsKey(nums[i]) && i - numToIndex.get(nums[i]) <= k) {
                return true;
            }
            numToIndex.put(nums[i], i);
        }
        
        return false;
    }
}
```

### Explanation

1. **Initialize Hashmap**:
   - In both Python and Java, we use a hashmap to store the most recent index of each element in the array. In Python, we use a dictionary (`num_to_index = {}`) and in Java, we use a `HashMap` (`Map<Integer, Integer> numToIndex = new HashMap<>();`).

2. **Iterate Through the Array**:
   - We iterate through each element in the array using a for loop.
   - In Python, we use `enumerate(nums)` to get both the index and the value of each element. In Java, we use a standard for loop with an index variable (`i`).
   - For each element, we check if it exists in the hashmap (`if num in num_to_index:` in Python and `if (numToIndex.containsKey(nums[i])):` in Java).
   - If it exists, we check if the difference between the current index and the stored index is less than or equal to `k` (`if i - num_to_index[num] <= k:` in Python and `if (i - numToIndex.get(nums[i]) <= k):` in Java).
   - If the condition is met, we return `true`.
   - If the element does not exist in the hashmap, or the condition is not met, we update the hashmap with the current index of the element (`num_to_index[num] = i` in Python and `numToIndex.put(nums[i], i);` in Java).

3. **Return the Result**:
   - If no such pair of indices is found, we return `false`.

This approach ensures that we efficiently check if there are two distinct indices in the array such that the elements are equal and the indices are within the given distance `k` using a hashmap to track the indices, making it an O(n) solution where n is the length of the array. This guarantees an efficient and straightforward solution to the problem.