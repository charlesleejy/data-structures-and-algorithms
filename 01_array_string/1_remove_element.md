## Remove Element

#### Problem Statement
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The relative order of the elements may be changed.

Since it's impossible to change the length of the array in some languages, you must instead have the result placed in the first part of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It doesn't matter what you leave beyond the first `k` elements.

Return `k` after placing the final result in the first `k` slots of `nums`.

**Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.**

#### Example
```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
```

### Solution

To solve this problem, we use the two-pointer technique. One pointer iterates over the array, and the other keeps track of the position where the next non-val element should go.

#### Python Solution

```python
def removeElement(nums, val):
    k = 0  # This is the index where we will place the next non-val element.
    for i in range(len(nums)):
        if nums[i] != val:
            nums[k] = nums[i]
            k += 1
    return k

# Example usage
nums = [3, 2, 2, 3]
val = 3
k = removeElement(nums, val)
print(k)       # Output: 2
print(nums[:k])  # Output: [2, 2]
```

### Explanation
1. **Initialization**: Initialize a pointer `k` at 0. This will track the position where the next non-val element will be placed.
2. **Iteration**: Loop through each element in `nums` with an index `i`.
3. **Condition Check**: If `nums[i]` is not equal to `val`, place `nums[i]` at `nums[k]` and increment `k`.
4. **Return Value**: After the loop, `k` will be the count of elements that are not `val`.

#### Java Solution

```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        int k = 0;  // This is the index where we will place the next non-val element.
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }

    // Example usage
    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums = {3, 2, 2, 3};
        int val = 3;
        int k = solution.removeElement(nums, val);
        System.out.println(k);  // Output: 2
        for (int i = 0; i < k; i++) {
            System.out.print(nums[i] + " ");  // Output: 2 2
        }
    }
}
```

### Explanation
1. **Initialization**: Initialize a pointer `k` at 0. This will track the position where the next non-val element will be placed.
2. **Iteration**: Loop through each element in `nums` using a for-loop.
3. **Condition Check**: If `nums[i]` is not equal to `val`, place `nums[i]` at `nums[k]` and increment `k`.
4. **Return Value**: After the loop, `k` will be the count of elements that are not `val`.

### Summary
- **In-place Modification**: Both solutions modify the `nums` array in-place and use a single additional pointer, ensuring O(1) extra space complexity.
- **Time Complexity**: The time complexity is O(n), where n is the length of the `nums` array, as we only pass through the array once.