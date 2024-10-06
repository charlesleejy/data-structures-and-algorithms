## 3Sum

### Problem Description
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

### Example
```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```
```
Input: nums = []
Output: []
```
```
Input: nums = [0]
Output: []
```

### Solution Approach
To solve this problem efficiently, we can use a combination of sorting and the two-pointer technique. The idea is to fix one element and use the two-pointer technique to find pairs that sum to the negative of the fixed element.

### Steps in Detail

1. **Sort the Array**:
   - Sorting the array helps to avoid duplicates easily and use the two-pointer technique efficiently.

2. **Iterate Through the Array**:
   - Iterate through the array with an index `i` from 0 to `len(nums) - 3`.
   - For each element `nums[i]`, use the two-pointer technique to find pairs `nums[j]` and `nums[k]` such that `nums[i] + nums[j] + nums[k] == 0`.

3. **Two-Pointer Technique**:
   - Initialize two pointers, `left` to `i + 1` and `right` to `len(nums) - 1`.
   - Move the pointers towards each other:
     - Calculate the sum of `nums[i]`, `nums[left]`, and `nums[right]`.
     - If the sum is zero, add the triplet to the result and move both pointers inward while skipping duplicates.
     - If the sum is less than zero, move the `left` pointer to the right.
     - If the sum is greater than zero, move the `right` pointer to the left.

4. **Avoid Duplicates**:
   - Skip duplicate elements to avoid adding duplicate triplets to the result.

5. **Return the Result**:
   - Return the list of all unique triplets that sum to zero.

### Python Code
```python
def three_sum(nums):
    nums.sort()
    result = []
    
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        left, right = i + 1, len(nums) - 1
        while left < right:
            current_sum = nums[i] + nums[left] + nums[right]
            if current_sum == 0:
                result.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                left += 1
                right -= 1
            elif current_sum < 0:
                left += 1
            else:
                right -= 1
    
    return result
```

### Java Code
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        
        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1, right = nums.length - 1;
            while (left < right) {
                int currentSum = nums[i] + nums[left] + nums[right];
                if (currentSum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1]) {
                        left++;
                    }
                    while (left < right && nums[right] == nums[right - 1]) {
                        right--;
                    }
                    left++;
                    right--;
                } else if (currentSum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        
        return result;
    }
}
```

### Explanation

1. **Sort the Array**:
   - In both Python and Java, we use the built-in sorting functions (`sort()` in Python and `Arrays.sort()` in Java) to sort the array.

2. **Iterate Through the Array**:
   - In both languages, we iterate through the array with an index `i` from 0 to `len(nums) - 3`.
   - If `nums[i]` is the same as the previous element, we skip it to avoid duplicates.

3. **Two-Pointer Technique**:
   - We initialize two pointers, `left` to `i + 1` and `right` to `len(nums) - 1`.
   - We calculate the sum of `nums[i]`, `nums[left]`, and `nums[right]`.
   - If the sum is zero, we add the triplet to the result and move both pointers inward while skipping duplicates.
   - If the sum is less than zero, we move the `left` pointer to the right.
   - If the sum is greater than zero, we move the `right` pointer to the left.

4. **Avoid Duplicates**:
   - After finding a valid triplet, we skip duplicate elements to avoid adding duplicate triplets to the result.

5. **Return the Result**:
   - We return the list of all unique triplets that sum to zero.

This approach ensures that we efficiently find all unique triplets using sorting and the two-pointer technique, making it an O(n^2) solution where n is the length of the array. This guarantees an efficient and straightforward solution to the problem.


