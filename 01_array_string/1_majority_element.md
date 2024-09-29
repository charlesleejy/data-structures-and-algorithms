## Majority Element

### Problem Description
Given an array `nums` of size `n`, return the majority element. The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

### Example
```
Input: nums = [3,2,3]
Output: 3
```
```
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```

### Solution Approach
There are multiple ways to solve this problem. One efficient approach is to use the Boyer-Moore Voting Algorithm. This algorithm works in two passes and uses O(1) extra space.

#### Boyer-Moore Voting Algorithm
1. **Initialization**:
   - Initialize a candidate element and a count.

2. **First Pass (Finding a Candidate)**:
   - Iterate through the array, adjusting the count based on whether the current element matches the candidate. If the count drops to zero, change the candidate to the current element and reset the count.

3. **Second Pass (Verification)**:
   - Verify that the candidate is indeed the majority element by counting its occurrences.

### Python Code
```python
def majority_element(nums):
    # First pass: find the candidate
    candidate = None
    count = 0
    for num in nums:
        if count == 0:
            candidate = num
        count += (1 if num == candidate else -1)
    
    # Second pass: verify the candidate
    count = sum(1 for num in nums if num == candidate)
    if count > len(nums) // 2:
        return candidate
    else:
        raise Exception("No majority element found")
```

### Java Code
```java
public class Solution {
    public int majorityElement(int[] nums) {
        // First pass: find the candidate
        Integer candidate = null;
        int count = 0;
        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }
        
        // Second pass: verify the candidate
        count = 0;
        for (int num : nums) {
            if (num == candidate) {
                count++;
            }
        }
        
        if (count > nums.length / 2) {
            return candidate;
        } else {
            throw new IllegalArgumentException("No majority element found");
        }
    }
}
```

### Explanation

1. **First Pass (Finding a Candidate)**:
   - We initialize `candidate` to `None` and `count` to 0.
   - We iterate through each element in the array. If `count` is 0, we set the `candidate` to the current element and reset `count` to 1.
   - If the current element matches the `candidate`, we increment `count`. Otherwise, we decrement `count`.

2. **Second Pass (Verification)**:
   - After identifying a candidate, we verify its majority status by counting its occurrences in the array.
   - If the count of the candidate is more than half the size of the array, we return the candidate as the majority element.
   - If the candidate does not have more than half the occurrences, we raise an exception (this case should not occur given the problem's constraints).

This approach ensures that we traverse the array only twice, making it an O(n) solution, and we use only O(1) extra space for the candidate and count variables.