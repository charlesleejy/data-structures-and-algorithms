## Merge Sorted Array

#### Problem Statement
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums2` into `nums1` as one sorted array.

**Note:** The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to 0 and should be ignored.

#### Example
```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6], n = 3

Output:
nums1 = [1,2,2,3,5,6]
```

### Solution

#### Python Solution

In Python, we can solve this problem by iterating from the end of the arrays. This allows us to avoid overwriting elements in `nums1` that have not yet been merged.

```python
def merge(nums1, m, nums2, n):
    # Start from the end of nums1 and nums2
    i = m - 1
    j = n - 1
    k = m + n - 1
    
    # While there are elements to be compared in both arrays
    while i >= 0 and j >= 0:
        if nums1[i] > nums2[j]:
            nums1[k] = nums1[i]
            i -= 1
        else:
            nums1[k] = nums2[j]
            j -= 1
        k -= 1
    
    # If there are remaining elements in nums2
    while j >= 0:
        nums1[k] = nums2[j]
        j -= 1
        k -= 1

# Example usage
nums1 = [1, 2, 3, 0, 0, 0]
m = 3
nums2 = [2, 5, 6]
n = 3
merge(nums1, m, nums2, n)
print(nums1)  # Output: [1, 2, 2, 3, 5, 6]
```

#### Java Solution

In Java, the logic is similar, using pointers to compare elements from the end of the arrays to merge them in place.

```java
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // Start from the end of nums1 and nums2
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        // While there are elements to be compared in both arrays
        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];
                i--;
            } else {
                nums1[k] = nums2[j];
                j--;
            }
            k--;
        }

        // If there are remaining elements in nums2
        while (j >= 0) {
            nums1[k] = nums2[j];
            j--;
            k--;
        }
    }

    // Example usage
    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums1 = {1, 2, 3, 0, 0, 0};
        int m = 3;
        int[] nums2 = {2, 5, 6};
        int n = 3;
        solution.merge(nums1, m, nums2, n);
        System.out.println(Arrays.toString(nums1));  // Output: [1, 2, 2, 3, 5, 6]
    }
}
```

### Explanation

1. **Initialization**: We initialize three pointers: `i` for the end of the first `m` elements of `nums1`, `j` for the end of `nums2`, and `k` for the end of the entire `nums1` array.
2. **Comparison and Merging**:
   - Compare elements at `nums1[i]` and `nums2[j]`.
   - Place the larger element at the end of `nums1[k]`.
   - Move the respective pointer (`i` or `j`) and `k` one step backward.
3. **Remaining Elements**: After the main loop, if there are any remaining elements in `nums2`, we copy them to the beginning of `nums1`.

This approach ensures that we fill `nums1` from the back to the front, avoiding the need to shift elements and maintaining an efficient `O(m + n)` time complexity.
