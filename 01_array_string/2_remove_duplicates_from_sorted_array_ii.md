## Remove Duplicates from Sorted Array II

### Problem Description
Given a sorted array `nums`, remove the duplicates in place such that duplicates appeared at most twice and return the new length. Do not allocate extra space for another array; you must do this by modifying the input array in place with O(1) extra memory.

### Example
```
Input: nums = [0,0,1,1,1,1,2,3,3]
Output: 7, nums = [0,0,1,1,2,3,3,_]
Explanation: Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3, 3 respectively. It doesn't matter what you leave beyond the returned length.
```

### Solution Approach
To solve this problem, we can use the two-pointer technique. We maintain two pointers: one for iterating through the array (`i`), and one for the position of the next element to be placed in the result (`j`). Additionally, we keep a counter to track the occurrences of the current element.

Here are the detailed steps:

1. **Initialization**:
   - If the array is empty, return 0.
   - Initialize `j` to 1 (since the first element is always valid).
   - Initialize a counter to track the occurrences of the current element, starting with 1.

2. **Iteration**:
   - Iterate through the array with the `i` pointer starting from the second element.
   - For each element, compare it with the previous element (`nums[i]` with `nums[i-1]`).
   - If they are the same, increment the counter.
   - If they are different, reset the counter to 1.
   - If the counter is less than or equal to 2, assign the current element to `nums[j]` and increment `j`.

3. **Completion**:
   - After the iteration, `j` will be the length of the array with the allowed duplicates.

### Python Code
```python
def remove_duplicates(nums):
    if len(nums) <= 2:
        return len(nums)
    
    j = 1
    count = 1
    
    for i in range(1, len(nums)):
        if nums[i] == nums[i - 1]:
            count += 1
        else:
            count = 1
        
        if count <= 2:
            j += 1
            nums[j] = nums[i]
    
    return j
```

### Java Code
```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 2) {
            return nums.length;
        }
        
        int j = 1;
        int count = 1;
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) {
                count++;
            } else {
                count = 1;
            }
            
            if (count <= 2) {
                j++;
                nums[j] = nums[i];
            }
        }
        
        return j;
    }
}
```

### Explanation

1. **Edge Case Handling**:
   - If the array length is less than or equal to 2, the function immediately returns the length of the array since all elements can remain.

2. **Iteration**:
   - We start iterating from the second element (`i = 1`).
   - For each element, we compare it with the previous element (`nums[i-1]`).
   - If they are the same, we increment the counter.
   - If they are different, we reset the counter to 1.
   - If the counter is less than or equal to 2, we place the current element at position `j` and increment `j`.

3. **Returning the Result**:
   - `j` represents the index for the next element to be placed. Therefore, the length of the array with the allowed duplicates is `j + 1`.

This approach ensures that we traverse the array only once, making it an O(n) solution, and we use only O(1) extra space for the pointers and the counter.