## Two Sum II - Input Array Is Sorted

### Problem Description
Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where 1 <= `index1` < `index2` <= numbers.length.

Return the indices of the two numbers, `index1` and `index2`, as an integer array `[index1, index2]` of length 2.

### Example
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2.
```
```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
```
```
Input: numbers = [-1,0], target = -1
Output: [1,2]
```

### Solution Approach
To solve this problem efficiently, we can use the two-pointer technique. Since the array is already sorted, we can place one pointer at the beginning of the array and another at the end. We then move the pointers towards each other until we find the two numbers that add up to the target.

### Steps in Detail

1. **Initialize Two Pointers**:
   - Initialize a pointer `left` to the beginning of the array (`0` index in code, but it will be 1-indexed in the final result).
   - Initialize a pointer `right` to the end of the array (`len(numbers) - 1`).

2. **Traverse the Array**:
   - While `left` pointer is less than `right` pointer:
     - Calculate the sum of the elements at the `left` and `right` pointers.
     - If the sum is equal to the target, return the indices as a 1-indexed array.
     - If the sum is less than the target, move the `left` pointer to the right to increase the sum.
     - If the sum is greater than the target, move the `right` pointer to the left to decrease the sum.

3. **Return the Result**:
   - The loop will eventually find the solution, as guaranteed by the problem statement.

### Python Code
```python
def two_sum(numbers, target):
    left, right = 0, len(numbers) - 1
    
    while left < right:
        current_sum = numbers[left] + numbers[right]
        if current_sum == target:
            return [left + 1, right + 1]  # Convert to 1-indexed
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return []  # In case no solution is found, though guaranteed by problem statement
```

### Java Code
```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0, right = numbers.length - 1;
        
        while (left < right) {
            int currentSum = numbers[left] + numbers[right];
            if (currentSum == target) {
                return new int[] { left + 1, right + 1 };  // Convert to 1-indexed
            } else if (currentSum < target) {
                left++;
            } else {
                right--;
            }
        }
        
        return new int[] {};  // In case no solution is found, though guaranteed by problem statement
    }
}
```

### Explanation

1. **Initialize Two Pointers**:
   - In both Python and Java, we initialize `left` to `0` and `right` to `len(numbers) - 1`.

2. **Traverse the Array**:
   - We use a while loop to move the pointers towards each other.
   - At each step, we calculate the sum of the elements at `left` and `right`.
   - If the sum matches the target, we return the 1-indexed positions of the two elements.
   - If the sum is less than the target, we move the `left` pointer to the right to increase the sum.
   - If the sum is greater than the target, we move the `right` pointer to the left to decrease the sum.

3. **Return the Result**:
   - The loop continues until we find the correct pair of indices.
   - The return statements convert the 0-indexed positions to 1-indexed positions as required by the problem.

This approach ensures that we efficiently find the two numbers that add up to the target using the two-pointer technique, making it an O(n) solution where n is the length of the array. This guarantees an efficient and straightforward solution to the problem.