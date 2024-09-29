## Rotate Array

### Problem Description
Given an array, rotate the array to the right by `k` steps, where `k` is non-negative.

### Example
```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

### Solution Approach
There are multiple ways to solve this problem. One efficient approach is to use the reversal algorithm. This approach works in three steps:

1. **Reverse the Entire Array**:
   - Reverse the whole array.

2. **Reverse the First `k` Elements**:
   - Reverse the first `k` elements of the array.

3. **Reverse the Remaining Elements**:
   - Reverse the rest of the array from index `k` to the end.

### Steps in Detail
1. **Reverse the Entire Array**:
   - If `nums = [1, 2, 3, 4, 5, 6, 7]`, after reversing, it becomes `[7, 6, 5, 4, 3, 2, 1]`.

2. **Reverse the First `k` Elements**:
   - If `k = 3`, reverse the first 3 elements: `[7, 6, 5]` becomes `[5, 6, 7]`.

3. **Reverse the Remaining Elements**:
   - Reverse the remaining elements `[4, 3, 2, 1]` to become `[1, 2, 3, 4]`.

Combining the results, we get `[5, 6, 7, 1, 2, 3, 4]`.

### Python Code
```python
def rotate(nums, k):
    n = len(nums)
    k = k % n  # In case k is greater than the length of the array

    def reverse(start, end):
        while start < end:
            nums[start], nums[end] = nums[end], nums[start]
            start += 1
            end -= 1

    reverse(0, n - 1)  # Reverse the entire array
    reverse(0, k - 1)  # Reverse the first k elements
    reverse(k, n - 1)  # Reverse the remaining elements
```

### Java Code
```java
public class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;  // In case k is greater than the length of the array

        reverse(nums, 0, n - 1);  // Reverse the entire array
        reverse(nums, 0, k - 1);  // Reverse the first k elements
        reverse(nums, k, n - 1);  // Reverse the remaining elements
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

### Explanation

1. **Handling `k` Greater Than Array Length**:
   - We use `k = k % n` to handle cases where `k` is greater than the length of the array. This reduces unnecessary full rotations.

2. **Reversal Function**:
   - A helper function `reverse` is used to reverse a portion of the array in place. It swaps elements from the start and end towards the center.

3. **Three-Step Reversal**:
   - First, we reverse the entire array to change the order of all elements.
   - Next, we reverse the first `k` elements to place the part that needs to be at the end in the correct order.
   - Finally, we reverse the rest of the array to restore the correct order for the remaining elements.

This approach ensures that we perform the rotations in O(n) time with O(1) extra space for the reversal function.