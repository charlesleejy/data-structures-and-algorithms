## Remove Duplicates from Sorted Array

### Problem Description
You are given a sorted array. Your task is to remove duplicates in place such that each element appears only once and returns the new length. Do not allocate extra space for another array; you must do this by modifying the input array in place with O(1) extra memory.

### Example
```
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the returned length.
```

### Solution Approach
To solve this problem, we can use the two-pointer technique. We maintain two pointers: one for iterating through the array (`i`), and one for the position of the next unique element (`j`). 

Here are the detailed steps:

1. **Initialization**:
   - If the array is empty, return 0.
   - Initialize `j` to 0 (or 1 if starting from the second element).

2. **Iteration**:
   - Iterate through the array with the `i` pointer starting from the second element.
   - For each element, compare it with the last unique element found (`nums[j]`).
   - If it is different, increment `j` and update `nums[j]` with the current element.

3. **Completion**:
   - After the iteration, `j + 1` will be the length of the array with unique elements.

### Python Code
```python
def remove_duplicates(nums):
    if not nums:
        return 0
    
    j = 0
    for i in range(1, len(nums)):
        if nums[i] != nums[j]:
            j += 1
            nums[j] = nums[i]
    
    return j + 1
```

### Java Code
```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        
        int j = 0;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[j]) {
                j++;
                nums[j] = nums[i];
            }
        }
        
        return j + 1;
    }
}
```

### Explanation

1. **Edge Case Handling**:
   - If the array is empty, the function immediately returns 0 since there are no elements to process.

2. **Iteration**:
   - We start iterating from the second element (`i = 1`).
   - For each element, we compare it with the element at position `j`.
   - If they are different, it means we found a new unique element.
   - Increment `j` and assign the current element to `nums[j]`.

3. **Returning the Result**:
   - `j` represents the index of the last unique element, so `j + 1` is the number of unique elements in the array.
   - The array `nums` is modified in place up to the `j`th index to hold the unique elements.

This approach ensures that we traverse the array only once, making it an O(n) solution, and we use only O(1) extra space for the pointers.