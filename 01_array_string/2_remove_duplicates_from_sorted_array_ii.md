## Remove Duplicates from Sorted Array II

### Problem Description
Given a sorted array `nums`, remove the duplicates in place such that duplicates appeared at most twice and return the new length. Do not allocate extra space for another array; you must do this by modifying the input array in place with O(1) extra memory.

### Example
```
Input: nums = [0,0,1,1,1,1,2,3,3]
Output: 7, nums = [0,0,1,1,2,3,3,_]
Explanation: Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3, 3 respectively. It doesn't matter what you leave beyond the returned length.
```

### Approach:

1. **Two-Pointer Technique**: We'll use two pointers to track the position in the array:
   - **Pointer `i`**: Tracks the position where the next unique or valid duplicate element (appearing at most twice) should be placed.
   - **Pointer `j`**: Iterates through the array and evaluates each element.

2. **Condition for Duplicates**: Since the array is sorted, duplicates will be consecutive. To ensure that each element appears at most twice, we can compare the current element `nums[j]` with the element at `nums[i-2]`:
   - If `nums[j] == nums[i-2]`, skip `nums[j]` because it would create more than two occurrences.
   - Otherwise, copy `nums[j]` to `nums[i]` and increment `i`.

3. **Return the Length (`k`)**: After processing, the first `k` elements of the array (where `k = i`) will be the final result. The elements beyond `k` don’t matter, as they will be ignored.

### Solution in Python:

```python
def removeDuplicates(nums):
    if len(nums) <= 2:
        return len(nums)
    
    i = 2  # Start from the third element because the first two can always stay
    for j in range(2, len(nums)):
        # If current number is not equal to the number two steps back, place it in the result
        if nums[j] != nums[i - 2]:
            nums[i] = nums[j]
            i += 1
    
    return i
```

### Explanation of the Code:

- **Initial Check**: If the array has fewer than or equal to 2 elements, we return the length as no duplicates need to be removed.
- **Two Pointers**: We initialize `i = 2` to start from the third position because the first two elements are guaranteed to remain.
- **For Loop**: We iterate through the array starting from the third element (`j = 2`), checking if `nums[j] != nums[i-2]`:
   - If true, we move `nums[j]` to `nums[i]` and increment `i` to track the new position for unique/valid elements.
- **Return**: At the end of the loop, `i` will represent the length `k` of the modified array, where each unique element appears at most twice.

### Example Walkthrough:

#### Example 1:
**Input**: `nums = [1, 1, 1, 2, 2, 3]`

- Initial array: `[1, 1, 1, 2, 2, 3]`
- First two elements are kept as is.
- At `j = 2`, `nums[2] == nums[0]`, so we skip this duplicate.
- At `j = 3`, `nums[3] != nums[1]`, so we move `nums[3]` to `nums[2]`, resulting in `[1, 1, 2, 2, 2, 3]`.
- At `j = 4`, `nums[4] != nums[2]`, so we move `nums[4]` to `nums[3]`, resulting in `[1, 1, 2, 2, 3, 3]`.
- At `j = 5`, `nums[5] != nums[3]`, so we move `nums[5]` to `nums[4]`.

**Output**: `k = 5`, and `nums = [1, 1, 2, 2, 3]` for the first `k` elements.

#### Example 2:
**Input**: `nums = [0, 0, 1, 1, 1, 1, 2, 3, 3]`

- Initial array: `[0, 0, 1, 1, 1, 1, 2, 3, 3]`
- First two elements are kept as is.
- At `j = 2`, `nums[2] != nums[0]`, so we move `nums[2]` to `nums[2]`.
- At `j = 3`, `nums[3] != nums[1]`, so we move `nums[3]` to `nums[3]`.
- At `j = 4`, `nums[4] == nums[2]`, so we skip this duplicate.
- At `j = 5`, `nums[5] == nums[3]`, so we skip this duplicate.
- At `j = 6`, `nums[6] != nums[4]`, so we move `nums[6]` to `nums[4]`, resulting in `[0, 0, 1, 1, 2, 1, 2, 3, 3]`.
- At `j = 7`, `nums[7] != nums[5]`, so we move `nums[7]` to `nums[5]`.
- At `j = 8`, `nums[8] != nums[6]`, so we move `nums[8]` to `nums[6]`.

**Output**: `k = 7`, and `nums = [0, 0, 1, 1, 2, 3, 3]` for the first `k` elements.

### Complexity Analysis:

- **Time Complexity**: `O(n)`, where `n` is the length of the array. We only iterate through the array once.
- **Space Complexity**: `O(1)`, since we are modifying the array in-place without using extra space. 

This solution efficiently solves the problem by ensuring each unique element appears at most twice, while maintaining the relative order of the elements and modifying the array in-place.